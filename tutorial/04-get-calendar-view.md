---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823358"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework には、Microsoft Graph への呼び出しを行うための [Msgraphclient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) が用意されています。 このクラスは、 [Microsoft Graph JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript)をラップして、現在ログオンしているユーザーとの認証を事前に行います。

既存の JavaScript ライブラリをラップしているため、使用法は同じであり、Microsoft Graph TypeScript 定義と完全に互換性があります。

## <a name="get-the-users-calendar"></a>ユーザーの予定表を取得する

1. **/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、次の `import` ステートメントをファイルの先頭に追加します。

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. エラーを表示するには、次の関数を **GraphTutorialWebPart** クラスに追加します。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. ユーザーの予定表にあるイベントを印刷するには、次の関数を追加します。

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. 既存の `render` 関数を、以下の関数で置き換えます。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    このコードで行われていることに注目してください。

    - を使用 `this.context.msGraphClientFactory.getClient` して、認証された **Msgraphclient** オブジェクトを取得します。
    - このメソッドは `/me/calendarView` エンドポイントを呼び出し `startDateTime` 、 `endDateTime` 現在の週の開始と終了に対してとクエリパラメーターを設定します。
    - を使用して、 `select` 返されるフィールドを制限し、アプリが使用するフィールドのみを要求します。
    - `orderby`開始時刻でイベントを並べ替えるために使用します。
    - を使用して `top` 、結果を25個のイベントに制限します。

## <a name="deploy-the-web-part"></a>Web パーツを展開する

1. Web パーツをビルドしてパッケージ化するには、CLI で次の2つのコマンドを実行します。

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. ブラウザーを開き、テナントの SharePoint アプリカタログに移動します。 左側の [ **SharePoint 用アプリ** ] メニュー項目を選択します。

1. **/Sharepoint/solution/graph-tutorial.sppkg** ファイルをアップロードします。

1. [ **信頼する..** .] プロンプトに、[ファイルの **package-solution.js** に設定した4つの Microsoft Graph アクセス許可が一覧表示されていることを確認します。 [ **組織内のすべてのサイトでこのソリューションを使用できるようにする** ] を選択し、[ **展開** ] を選択します。

1. Web パーツの Graph アクセス許可をまだ承認していない場合は、ここで実行してください。

    1. テナント管理者を使用して [SharePoint 管理センター](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) に移動します。

    1. 左側のメニューで、[ **詳細** ]、[ **API アクセス** ] の順に選択します。

    1. **グラフ-チュートリアル-クライアント側ソリューション** パッケージから保留中の各要求を選択し、[ **承認** ] を選択します。

        ![SharePoint 管理センターの API アクセスページのスクリーンショット](images/api-access.png)

## <a name="test-the-web-part"></a>Web パーツをテストする

1. Web パーツをテストする SharePoint サイトに移動します。 Web パーツをテストする新しいページを作成します。

1. Web パーツピッカーを使用して、 **Graphtutorial** web パーツを検索し、それをページに追加します。

    ![Web パーツピッカーの GraphTutorial web パーツのスクリーンショット](images/add-web-part.png)

1. 現在の週のイベントの一覧が web パーツに出力されます。

    ![イベントの一覧を表示する web パーツのスクリーンショット](images/calendar-list.png)
