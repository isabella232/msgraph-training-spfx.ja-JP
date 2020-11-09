---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823428"
---
<!-- markdownlint-disable MD002 MD041 -->

このセクションでは、 [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) を使用して、イベントの簡単な一覧をリッチ UI に置き換えます。

このツールキットには、イベントの一覧を表示するための適切な [議題コンポーネント](https://docs.microsoft.com/graph/toolkit/components/agenda)が用意されています。

## <a name="update-the-web-part"></a>Web パーツを更新する

1. /Src/webparts/graphTutorial/GraphTutorialWebPart.module.scss を開きます **。** エントリの属性の値 `background-color` `.row` をに変更し `$ms-color-white` ます。

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. エントリの中に次のエントリを追加し `.graphTutorial` ます。

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. **/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、次の `import` ステートメントをファイルの先頭に追加します。

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. **GraphTutorialWebPart** クラスに次の関数を追加して、ツールキットを初期化します。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. 既存の `renderCalendarView` 関数を、以下の関数で置き換えます。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    これにより、基本リストは、ツールキットの **議題** コンポーネントに置き換えられます。

1. Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。

    ![議題コンポーネントを含む web パーツのスクリーンショット](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a>別の方法

この時点で、次のコードを使用できます。

- **Msgraphclient** を使用して、Microsoft Graph から現在の週のユーザーの予定表ビューを取得します。
- これらのイベントを Microsoft Graph Toolkit から **議題** コンポーネントに追加します。

この方法では、Graph API の呼び出しを完全に制御でき、必要に応じてレンダリングする前にイベントの任意の処理を実行できます。 ただし、必要でない場合は、 **議題** コンポーネントに作業を任せることによって簡単にすることができます。

すべての Microsoft Graph Toolkit コンポーネントは、すべての関連する API 呼び出しを Microsoft Graph に対して行うことができます。 たとえば、 **議題** コンポーネントを web パーツに追加するだけで、プロパティを設定しない場合、web パーツは既定の設定を使用して、現在の日付のイベントを取得します。 現在の同じ結果 (現在の週のイベント) を実現する方法を見てみましょう。

1. 既存の `render` メソッドを次のように置き換えます。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    これで、API 呼び出しを行う代わりに、 `render` `mgt-agenda` HTML に要素を直接追加するだけです。 `date`週の開始日と7に設定すると、 `days` コンポーネントは以前のバージョンのと同じ API 呼び出しを作成 `render` します。

1. **GraphTutorialWebPart** クラスに、次の空の関数を追加します。

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > また、web パーツに [ **チームのソーシャルを追加** ] ボタンを追加し、このメソッドを `addSocialToCalendar` イベントリスナーとして追加しました。  次のセクションで、分離コードを実装します。 ここでは、コードをコンパイルするだけです。

1. Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。 ビューは、前のテストと同じである必要があります。

### <a name="using-the-toolkit-vs-making-api-calls"></a>ツールキット vs API 呼び出しの使用

この時点で、ツールキットが機能しているときに、 **Msgraphclient** を使用する際にトラブルが発生した理由を不思議に思うかもしれません。 ツールキットは、イベントの一覧など、Microsoft Graph からクエリを実行する結果を表示するように設計されています。 ただし、自分で API 呼び出しを行う必要があるシナリオもあります。

- 要求ではない API 呼び出し `GET` 。 たとえば、予定表に新しいイベントを作成したり、ユーザーの電話番号を更新したりします。
- バックグラウンドでの使用を目的としたデータを取得し、直接レンダリングしないようにするための API 呼び出し。
