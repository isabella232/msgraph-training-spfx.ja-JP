---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823336"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="23434-101">このチュートリアルでは、Microsoft Graph を使用して現在の週のユーザーの予定表を取得し、ユーザーが予定表にイベントを追加できるようにする [SharePoint クライアント側の web パーツ](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) を作成します。</span><span class="sxs-lookup"><span data-stu-id="23434-101">In this tutorial, you'll create a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that will use Microsoft Graph to get the user's calendar for the current week and allow the user to add an event to their calendar.</span></span>

## <a name="create-a-web-part-project"></a><span data-ttu-id="23434-102">Web パーツプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="23434-102">Create a web part project</span></span>

1. <span data-ttu-id="23434-103">プロジェクトを作成する空のディレクトリで、コマンドラインインターフェイス (CLI) を開きます。</span><span class="sxs-lookup"><span data-stu-id="23434-103">Open your command-line interface (CLI) in an empty directory where you want to create the project.</span></span> <span data-ttu-id="23434-104">次のコマンドを実行して、[ごみ箱] SharePoint ジェネレーターを起動します。</span><span class="sxs-lookup"><span data-stu-id="23434-104">Run the following command to start the Yeoman SharePoint generator.</span></span>

    ```Shell
    yo @microsoft/sharepoint
    ```

1. <span data-ttu-id="23434-105">プロンプトに次のように応答します。</span><span class="sxs-lookup"><span data-stu-id="23434-105">Respond to the prompts as follows.</span></span>

    - <span data-ttu-id="23434-106">**ソリューション名は何ですか。**</span><span class="sxs-lookup"><span data-stu-id="23434-106">**What is your solution name?**</span></span> `graph-tutorial`
    - <span data-ttu-id="23434-107">**どのベースライン パッケージをコンポーネントのターゲットにしたいですか?**</span><span class="sxs-lookup"><span data-stu-id="23434-107">**Which baseline packages do you want to target for your component(s)?**</span></span> `SharePoint Online only (latest)`
    - <span data-ttu-id="23434-108">**ファイルをどこに保存しますか?**</span><span class="sxs-lookup"><span data-stu-id="23434-108">**Where do you want to place the files?**</span></span> `Use the current folder`
    - <span data-ttu-id="23434-109">**テナント管理者が、サイトで機能を展開したり、アプリを追加したりせず、すぐにすべてのサイトでソリューションを展開できるようにしたいですか?**</span><span class="sxs-lookup"><span data-stu-id="23434-109">**Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**</span></span> `Yes`
    - <span data-ttu-id="23434-110">**ソリューション内のコンポーネントには、一意であり、10人の他のコンポーネントと共有していない web Api にアクセスするためのアクセス許可が必要ですか。**</span><span class="sxs-lookup"><span data-stu-id="23434-110">**Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the ten ant?**</span></span> `No`
    - <span data-ttu-id="23434-111">**どの種類のクライアント側コンポーネントを作成しますか?**</span><span class="sxs-lookup"><span data-stu-id="23434-111">**Which type of client-side component to create?**</span></span> `WebPart`
    - <span data-ttu-id="23434-112">**Web パーツ名は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="23434-112">**What is your Web part name?**</span></span> `GraphTutorial`
    - <span data-ttu-id="23434-113">**Web パーツで何を行いますか?**</span><span class="sxs-lookup"><span data-stu-id="23434-113">**What is your Web part description?**</span></span> `GraphTutorial description`
    - <span data-ttu-id="23434-114">**どのフレームワークを使用しますか?**</span><span class="sxs-lookup"><span data-stu-id="23434-114">**Which framework would you like to use?**</span></span> `No JavaScript framework`

1. <span data-ttu-id="23434-115">次のコマンドを実行して、プロジェクトの TypeScript バージョンを3.7 に更新します。</span><span class="sxs-lookup"><span data-stu-id="23434-115">Run the following command to update the TypeScript version in the project to 3.7.</span></span>

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. <span data-ttu-id="23434-116">tsconfig.jsを開き、を **に** 置き換え `rush-stack-compiler-3.3` `rush-stack-compiler-3.7` ます。</span><span class="sxs-lookup"><span data-stu-id="23434-116">Open **./tsconfig.json** and replace `rush-stack-compiler-3.3` with `rush-stack-compiler-3.7`.</span></span>

1. <span data-ttu-id="23434-117">**/tslint.jsを** 開き、行を削除します。 `"no-use-before-declare": true,`</span><span class="sxs-lookup"><span data-stu-id="23434-117">Open **./tslint.json** and remove the `"no-use-before-declare": true,` line.</span></span> <span data-ttu-id="23434-118">`no-use-before-declare`ルールは推奨されなくなり、ビルドプロセス中にエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="23434-118">The `no-use-before-declare` rule is deprecated and will cause an error during the build process.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="23434-119">依存関係のインストール</span><span class="sxs-lookup"><span data-stu-id="23434-119">Install dependencies</span></span>

<span data-ttu-id="23434-120">に進む前に、後で使用する追加の NPM パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="23434-120">Before moving on, install some additional NPM packages that you will use later.</span></span>

- <span data-ttu-id="23434-121">Microsoft graph の[TypeScript 定義](https://github.com/microsoftgraph/msgraph-typescript-typings)を使用して、microsoft graph オブジェクトの Intellisense を提供します。</span><span class="sxs-lookup"><span data-stu-id="23434-121">[Microsoft Graph TypeScript definitions](https://github.com/microsoftgraph/msgraph-typescript-typings) to provide Intellisense for Microsoft Graph objects.</span></span>
- <span data-ttu-id="23434-122">Web パーツの UI コンポーネントを提供する[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) 。</span><span class="sxs-lookup"><span data-stu-id="23434-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to provide UI components for the web part.</span></span>
- <span data-ttu-id="23434-123">[日付-fns 日付](https://date-fns.org/) を操作するための便利な機能。</span><span class="sxs-lookup"><span data-stu-id="23434-123">[date-fns](https://date-fns.org/) for helpful functions for working with dates.</span></span>

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
