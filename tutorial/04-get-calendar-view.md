---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823358"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0515d-101">SharePoint Framework には、Microsoft Graph への呼び出しを行うための [Msgraphclient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) が用意されています。</span><span class="sxs-lookup"><span data-stu-id="0515d-101">The SharePoint Framework provides the [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) for making calls to Microsoft Graph.</span></span> <span data-ttu-id="0515d-102">このクラスは、 [Microsoft Graph JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript)をラップして、現在ログオンしているユーザーとの認証を事前に行います。</span><span class="sxs-lookup"><span data-stu-id="0515d-102">This class wraps the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript), pre-authenticating it with the current logged on user.</span></span>

<span data-ttu-id="0515d-103">既存の JavaScript ライブラリをラップしているため、使用法は同じであり、Microsoft Graph TypeScript 定義と完全に互換性があります。</span><span class="sxs-lookup"><span data-stu-id="0515d-103">Because it wraps the existing JavaScript library, its usage is the same, and it's fully compatible with the Microsoft Graph TypeScript definitions.</span></span>

## <a name="get-the-users-calendar"></a><span data-ttu-id="0515d-104">ユーザーの予定表を取得する</span><span class="sxs-lookup"><span data-stu-id="0515d-104">Get the user's calendar</span></span>

1. <span data-ttu-id="0515d-105">**/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、次の `import` ステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="0515d-105">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. <span data-ttu-id="0515d-106">エラーを表示するには、次の関数を **GraphTutorialWebPart** クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="0515d-106">Add the following function to the **GraphTutorialWebPart** class to render an error.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. <span data-ttu-id="0515d-107">ユーザーの予定表にあるイベントを印刷するには、次の関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="0515d-107">Add the following function to print out the events in the user's calendar.</span></span>

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

1. <span data-ttu-id="0515d-108">既存の `render` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0515d-108">Replace the existing `render` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    <span data-ttu-id="0515d-109">このコードで行われていることに注目してください。</span><span class="sxs-lookup"><span data-stu-id="0515d-109">Notice what this code does.</span></span>

    - <span data-ttu-id="0515d-110">を使用 `this.context.msGraphClientFactory.getClient` して、認証された **Msgraphclient** オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="0515d-110">It uses `this.context.msGraphClientFactory.getClient` to get an authenticated **MSGraphClient** object.</span></span>
    - <span data-ttu-id="0515d-111">このメソッドは `/me/calendarView` エンドポイントを呼び出し `startDateTime` 、 `endDateTime` 現在の週の開始と終了に対してとクエリパラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="0515d-111">It calls the `/me/calendarView` endpoint, setting the `startDateTime` and `endDateTime` query parameters to the start and end of the current week.</span></span>
    - <span data-ttu-id="0515d-112">を使用して、 `select` 返されるフィールドを制限し、アプリが使用するフィールドのみを要求します。</span><span class="sxs-lookup"><span data-stu-id="0515d-112">It uses `select` to limit which fields are returned, requesting only the fields the app uses.</span></span>
    - <span data-ttu-id="0515d-113">`orderby`開始時刻でイベントを並べ替えるために使用します。</span><span class="sxs-lookup"><span data-stu-id="0515d-113">It uses `orderby` to sort the events by their start time.</span></span>
    - <span data-ttu-id="0515d-114">を使用して `top` 、結果を25個のイベントに制限します。</span><span class="sxs-lookup"><span data-stu-id="0515d-114">It uses `top` to limit the results to 25 events.</span></span>

## <a name="deploy-the-web-part"></a><span data-ttu-id="0515d-115">Web パーツを展開する</span><span class="sxs-lookup"><span data-stu-id="0515d-115">Deploy the web part</span></span>

1. <span data-ttu-id="0515d-116">Web パーツをビルドしてパッケージ化するには、CLI で次の2つのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="0515d-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="0515d-117">ブラウザーを開き、テナントの SharePoint アプリカタログに移動します。</span><span class="sxs-lookup"><span data-stu-id="0515d-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="0515d-118">左側の [ **SharePoint 用アプリ** ] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="0515d-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="0515d-119">**/Sharepoint/solution/graph-tutorial.sppkg** ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="0515d-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="0515d-120">[ **信頼する..** .] プロンプトに、[ファイルの **package-solution.js** に設定した4つの Microsoft Graph アクセス許可が一覧表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="0515d-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="0515d-121">[ **組織内のすべてのサイトでこのソリューションを使用できるようにする** ] を選択し、[ **展開** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="0515d-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="0515d-122">Web パーツの Graph アクセス許可をまだ承認していない場合は、ここで実行してください。</span><span class="sxs-lookup"><span data-stu-id="0515d-122">If you have not already approved the Graph permissions for your web part, do that now.</span></span>

    1. <span data-ttu-id="0515d-123">テナント管理者を使用して [SharePoint 管理センター](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) に移動します。</span><span class="sxs-lookup"><span data-stu-id="0515d-123">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

    1. <span data-ttu-id="0515d-124">左側のメニューで、[ **詳細** ]、[ **API アクセス** ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="0515d-124">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

    1. <span data-ttu-id="0515d-125">**グラフ-チュートリアル-クライアント側ソリューション** パッケージから保留中の各要求を選択し、[ **承認** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="0515d-125">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

        ![SharePoint 管理センターの API アクセスページのスクリーンショット](images/api-access.png)

## <a name="test-the-web-part"></a><span data-ttu-id="0515d-127">Web パーツをテストする</span><span class="sxs-lookup"><span data-stu-id="0515d-127">Test the web part</span></span>

1. <span data-ttu-id="0515d-128">Web パーツをテストする SharePoint サイトに移動します。</span><span class="sxs-lookup"><span data-stu-id="0515d-128">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="0515d-129">Web パーツをテストする新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="0515d-129">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="0515d-130">Web パーツピッカーを使用して、 **Graphtutorial** web パーツを検索し、それをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="0515d-130">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Web パーツピッカーの GraphTutorial web パーツのスクリーンショット](images/add-web-part.png)

1. <span data-ttu-id="0515d-132">現在の週のイベントの一覧が web パーツに出力されます。</span><span class="sxs-lookup"><span data-stu-id="0515d-132">A list of events for the current week are printed in the web part.</span></span>

    ![イベントの一覧を表示する web パーツのスクリーンショット](images/calendar-list.png)
