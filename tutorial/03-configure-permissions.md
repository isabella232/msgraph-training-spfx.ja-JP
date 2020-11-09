---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823370"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ee752-101">SharePoint Framework では、Microsoft Graph にアクセスするためのアクセストークンを取得するために、Azure AD でアプリケーションを登録する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="ee752-101">The SharePoint Framework eliminates the need to register an application in Azure AD for getting access tokens to access Microsoft Graph.</span></span> <span data-ttu-id="ee752-102">SharePoint にログインしているユーザーの認証を処理し、web パーツでユーザートークンを取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="ee752-102">It handles the authentication for the user that is logged into SharePoint, allowing your web part to get user tokens.</span></span> <span data-ttu-id="ee752-103">Web パーツで必要な [グラフアクセス許可のスコープ](https://docs.microsoft.com/graph/permissions-reference) を指定する必要があり、テナント管理者はインストール中にこれらのアクセス許可を承認できます。</span><span class="sxs-lookup"><span data-stu-id="ee752-103">Your web part needs to indicate which [Graph permission scopes](https://docs.microsoft.com/graph/permissions-reference) it requires, and a tenant admin can approve those permissions during installation.</span></span>

## <a name="configure-permissions"></a><span data-ttu-id="ee752-104">アクセス許可を構成する</span><span class="sxs-lookup"><span data-stu-id="ee752-104">Configure permissions</span></span>

1. <span data-ttu-id="ee752-105">/ **Config/package-solution.jsを** 開きます。</span><span class="sxs-lookup"><span data-stu-id="ee752-105">Open **./config/package-solution.json**.</span></span>

1. <span data-ttu-id="ee752-106">次のコードをプロパティに追加し `solution` ます。</span><span class="sxs-lookup"><span data-stu-id="ee752-106">Add the following code to the `solution` property.</span></span>

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

<span data-ttu-id="ee752-107">`Calendars.ReadWrite`アクセス許可によって、web パーツは、ユーザーの予定表を取得したり、Microsoft Graph を使用してイベントを追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="ee752-107">The `Calendars.ReadWrite` permission allows your web part to retrieve the user's calendar and add events using Microsoft Graph.</span></span> <span data-ttu-id="ee752-108">その他のアクセス許可は、イベントの参加者と開催者に関する情報を表示するために、Microsoft Graph Toolkit のコンポーネントによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="ee752-108">The other permissions are used by components in the Microsoft Graph Toolkit to render information about event attendees and organizers.</span></span>

## <a name="optional-test-token-acquisition"></a><span data-ttu-id="ee752-109">オプション: テストトークンの取得</span><span class="sxs-lookup"><span data-stu-id="ee752-109">Optional: Test token acquisition</span></span>

> [!NOTE]
> <span data-ttu-id="ee752-110">このページの残りの手順はオプションです。</span><span class="sxs-lookup"><span data-stu-id="ee752-110">The rest of the steps on this page are optional.</span></span> <span data-ttu-id="ee752-111">Microsoft Graph のコーディングをすぐに開始したい場合は、 [予定表ビューを取得](/graph/tutorials/spfx?tutorial-step=3)することができます。</span><span class="sxs-lookup"><span data-stu-id="ee752-111">If you'd prefer to get to the Microsoft Graph coding right away, you can proceed to [Get a calendar view](/graph/tutorials/spfx?tutorial-step=3).</span></span>

<span data-ttu-id="ee752-112">トークンの取得をテストするために、いくつかの一時コードを web パーツに追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="ee752-112">Let's add some temporary code to the web part to test token acquisition.</span></span>

1. <span data-ttu-id="ee752-113">**/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、次の `import` ステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="ee752-113">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. <span data-ttu-id="ee752-114">既存の `render` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ee752-114">Replace the existing `render` function with the following.</span></span>

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a><span data-ttu-id="ee752-115">Web パーツを展開する</span><span class="sxs-lookup"><span data-stu-id="ee752-115">Deploy the web part</span></span>

1. <span data-ttu-id="ee752-116">Web パーツをビルドしてパッケージ化するには、CLI で次の2つのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ee752-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="ee752-117">ブラウザーを開き、テナントの SharePoint アプリカタログに移動します。</span><span class="sxs-lookup"><span data-stu-id="ee752-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="ee752-118">左側の [ **SharePoint 用アプリ** ] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="ee752-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="ee752-119">**/Sharepoint/solution/graph-tutorial.sppkg** ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="ee752-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="ee752-120">[ **信頼する..** .] プロンプトに、[ファイルの **package-solution.js** に設定した4つの Microsoft Graph アクセス許可が一覧表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ee752-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="ee752-121">[ **組織内のすべてのサイトでこのソリューションを使用できるようにする** ] を選択し、[ **展開** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ee752-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="ee752-122">テナント管理者を使用して [SharePoint 管理センター](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) に移動します。</span><span class="sxs-lookup"><span data-stu-id="ee752-122">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="ee752-123">左側のメニューで、[ **詳細** ]、[ **API アクセス** ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ee752-123">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="ee752-124">**グラフ-チュートリアル-クライアント側ソリューション** パッケージから保留中の各要求を選択し、[ **承認** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ee752-124">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![SharePoint 管理センターの API アクセスページのスクリーンショット](images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="ee752-126">Web パーツをテストする</span><span class="sxs-lookup"><span data-stu-id="ee752-126">Test the web part</span></span>

1. <span data-ttu-id="ee752-127">Web パーツをテストする SharePoint サイトに移動します。</span><span class="sxs-lookup"><span data-stu-id="ee752-127">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="ee752-128">Web パーツをテストする新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="ee752-128">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="ee752-129">Web パーツピッカーを使用して、 **Graphtutorial** web パーツを検索し、それをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="ee752-129">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Web パーツピッカーの GraphTutorial web パーツのスクリーンショット](images/add-web-part.png)

1. <span data-ttu-id="ee752-131">アクセストークンは、「 **SharePoint へようこそ!** 」の下に印刷されます。</span><span class="sxs-lookup"><span data-stu-id="ee752-131">The access token is printed below the **Welcome to SharePoint!**</span></span> <span data-ttu-id="ee752-132">web パーツ内のメッセージ。</span><span class="sxs-lookup"><span data-stu-id="ee752-132">message in the web part.</span></span> <span data-ttu-id="ee752-133">このトークンをコピーして解析することで、 [https://jwt.ms/](https://jwt.ms/) web パーツに必要なアクセス許可のスコープが含まれていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="ee752-133">You can copy this token and parse it at [https://jwt.ms/](https://jwt.ms/) to confirm that it contains the permission scopes required by the web part.</span></span>

    ![アクセストークンを表示する web パーツのスクリーンショット](images/access-token.png)
