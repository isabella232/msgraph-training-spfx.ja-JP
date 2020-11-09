---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831349"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="ab949-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="ab949-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab949-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="ab949-102">Prerequisites</span></span>

<span data-ttu-id="ab949-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="ab949-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="ab949-104">バージョン 10 .x [Node.js](https://nodejs.org/en/download/releases/)</span><span class="sxs-lookup"><span data-stu-id="ab949-104">[Node.js](https://nodejs.org/en/download/releases/) version 10.x</span></span>
- [<span data-ttu-id="ab949-105">Gulp</span><span class="sxs-lookup"><span data-stu-id="ab949-105">Gulp</span></span>](https://gulpjs.com/)
- <span data-ttu-id="ab949-106">同じ組織内のグローバル管理者アカウントへのアクセス権を持つ Microsoft の職場または学校のアカウント。</span><span class="sxs-lookup"><span data-stu-id="ab949-106">A Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="ab949-107">Microsoft アカウントを持っていない場合は、 [office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program) して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="ab949-107">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>
- <span data-ttu-id="ab949-108">このチュートリアルを開始する前に、アプリカタログとテストサイトを作成して、Microsoft 365 テナント [を SharePoint Framework 開発用にセットアップ](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab949-108">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

### <a name="deploy-the-web-part"></a><span data-ttu-id="ab949-109">Web パーツを展開する</span><span class="sxs-lookup"><span data-stu-id="ab949-109">Deploy the web part</span></span>

1. <span data-ttu-id="ab949-110">Web パーツをビルドしてパッケージ化するには、CLI で次の2つのコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ab949-110">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="ab949-111">ブラウザーを開き、テナントの SharePoint アプリカタログに移動します。</span><span class="sxs-lookup"><span data-stu-id="ab949-111">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="ab949-112">左側の [ **SharePoint 用アプリ** ] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab949-112">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="ab949-113">**/Sharepoint/solution/graph-tutorial.sppkg** ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="ab949-113">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="ab949-114">[ **信頼する..** .] プロンプトに、[ファイルの **package-solution.js** に設定した4つの Microsoft Graph アクセス許可が一覧表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="ab949-114">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="ab949-115">[ **組織内のすべてのサイトでこのソリューションを使用できるようにする** ] を選択し、[ **展開** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab949-115">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="ab949-116">テナント管理者を使用して [SharePoint 管理センター](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) に移動します。</span><span class="sxs-lookup"><span data-stu-id="ab949-116">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="ab949-117">左側のメニューで、[ **詳細** ]、[ **API アクセス** ] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="ab949-117">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="ab949-118">**グラフ-チュートリアル-クライアント側ソリューション** パッケージから保留中の各要求を選択し、[ **承認** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="ab949-118">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![SharePoint 管理センターの API アクセスページのスクリーンショット](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="ab949-120">Web パーツをテストする</span><span class="sxs-lookup"><span data-stu-id="ab949-120">Test the web part</span></span>

1. <span data-ttu-id="ab949-121">Web パーツをテストする SharePoint サイトに移動します。</span><span class="sxs-lookup"><span data-stu-id="ab949-121">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="ab949-122">Web パーツをテストする新しいページを作成します。</span><span class="sxs-lookup"><span data-stu-id="ab949-122">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="ab949-123">Web パーツピッカーを使用して、 **Graphtutorial** web パーツを検索し、それをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="ab949-123">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Web パーツピッカーの GraphTutorial web パーツのスクリーンショット](../tutorial/images/add-web-part.png)
