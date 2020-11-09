---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823346"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c02ed-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する [SharePoint のクライアント側 web パーツ](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) を作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c02ed-101">This tutorial teaches you how to build a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="c02ed-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-spfx)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="c02ed-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c02ed-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="c02ed-103">Prerequisites</span></span>

<span data-ttu-id="c02ed-104">このチュートリアルを開始する前に、開発用コンピューターに次のツールをインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="c02ed-104">Before you start this tutorial, you should have the following tools installed on your development machine.</span></span>

- [<span data-ttu-id="c02ed-105">Node.js</span><span class="sxs-lookup"><span data-stu-id="c02ed-105">Node.js</span></span>](https://nodejs.org/en/download/releases/)
- [<span data-ttu-id="c02ed-106">Yeoman</span><span class="sxs-lookup"><span data-stu-id="c02ed-106">Yeoman</span></span>](https://yeoman.io/)
- [<span data-ttu-id="c02ed-107">Gulp</span><span class="sxs-lookup"><span data-stu-id="c02ed-107">Gulp</span></span>](https://gulpjs.com/)
- [<span data-ttu-id="c02ed-108">Yeoman の SharePoint ジェネレーター</span><span class="sxs-lookup"><span data-stu-id="c02ed-108">Yeoman SharePoint generator</span></span>](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

<span data-ttu-id="c02ed-109">Sharepoint Framework 開発の要件の詳細については [、「sharepoint framework 開発環境を](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment)セットアップする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c02ed-109">You can find more details about requirements for SharePoint Framework development at [Set up your SharePoint Framework development environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c02ed-110">SharePoint Framework には Node.js バージョン 10 .x が必要です。</span><span class="sxs-lookup"><span data-stu-id="c02ed-110">SharePoint Framework requires Node.js version 10.x.</span></span> <span data-ttu-id="c02ed-111">必ず正しいバージョンをインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="c02ed-111">Be sure to install the correct version.</span></span>

<span data-ttu-id="c02ed-112">また、同じ組織内のグローバル管理者アカウントにアクセスできる、Microsoft の職場または学校アカウントを持っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="c02ed-112">You should also have a Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="c02ed-113">Microsoft アカウントを持っていない場合は、 [office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program) して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="c02ed-113">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

<span data-ttu-id="c02ed-114">このチュートリアルを開始する前に、アプリカタログとテストサイトを作成して、Microsoft 365 テナント [を SharePoint Framework 開発用にセットアップ](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c02ed-114">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="c02ed-115">このチュートリアルは、上記のツールの次のバージョンで記述されています。</span><span class="sxs-lookup"><span data-stu-id="c02ed-115">This tutorial was written with the following versions of the above tools.</span></span> <span data-ttu-id="c02ed-116">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="c02ed-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="c02ed-117">Node.js 10.22.0</span><span class="sxs-lookup"><span data-stu-id="c02ed-117">Node.js 10.22.0</span></span>
> - <span data-ttu-id="c02ed-118">ごみ箱オマーン3.1.1</span><span class="sxs-lookup"><span data-stu-id="c02ed-118">Yeoman 3.1.1</span></span>
> - <span data-ttu-id="c02ed-119">Gulp 4.0.2</span><span class="sxs-lookup"><span data-stu-id="c02ed-119">Gulp 4.0.2</span></span>
> - <span data-ttu-id="c02ed-120">(オマーン) SharePoint ジェネレーター1.11.0</span><span class="sxs-lookup"><span data-stu-id="c02ed-120">Yeoman SharePoint generator 1.11.0</span></span>

## <a name="feedback"></a><span data-ttu-id="c02ed-121">フィードバック</span><span class="sxs-lookup"><span data-stu-id="c02ed-121">Feedback</span></span>

<span data-ttu-id="c02ed-122">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-spfx)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="c02ed-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>
