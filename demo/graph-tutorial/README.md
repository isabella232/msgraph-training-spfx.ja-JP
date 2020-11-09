---
ms.openlocfilehash: 98ecf04b99250ceab37ce46f47f2e9a46714d7ed
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831293"
---
# <a name="graph-tutorial"></a><span data-ttu-id="d10d0-101">グラフ-チュートリアル</span><span class="sxs-lookup"><span data-stu-id="d10d0-101">graph-tutorial</span></span>

## <a name="summary"></a><span data-ttu-id="d10d0-102">要約</span><span class="sxs-lookup"><span data-stu-id="d10d0-102">Summary</span></span>

<span data-ttu-id="d10d0-103">機能と使用されたテクノロジについての簡単な概要。</span><span class="sxs-lookup"><span data-stu-id="d10d0-103">Short summary on functionality and used technologies.</span></span>

<span data-ttu-id="d10d0-104">[動作中のソリューションの画像 (可能な場合)]</span><span class="sxs-lookup"><span data-stu-id="d10d0-104">[picture of the solution in action, if possible]</span></span>

## <a name="used-sharepoint-framework-version"></a><span data-ttu-id="d10d0-105">使用された SharePoint Framework のバージョン</span><span class="sxs-lookup"><span data-stu-id="d10d0-105">Used SharePoint Framework Version</span></span>

![バージョン](https://img.shields.io/badge/version-1.11-green.svg)

## <a name="applies-to"></a><span data-ttu-id="d10d0-107">適用対象</span><span class="sxs-lookup"><span data-stu-id="d10d0-107">Applies to</span></span>

- [<span data-ttu-id="d10d0-108">SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="d10d0-108">SharePoint Framework</span></span>](https://aka.ms/spfx)
- [<span data-ttu-id="d10d0-109">Microsoft 365 テナント</span><span class="sxs-lookup"><span data-stu-id="d10d0-109">Microsoft 365 tenant</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)

> <span data-ttu-id="d10d0-110">[Microsoft 365 開発者プログラム](http://aka.ms/o365devprogram)に加入して、独自の無料開発テナントを取得する</span><span class="sxs-lookup"><span data-stu-id="d10d0-110">Get your own free development tenant by subscribing to [Microsoft 365 developer program](http://aka.ms/o365devprogram)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d10d0-111">前提条件</span><span class="sxs-lookup"><span data-stu-id="d10d0-111">Prerequisites</span></span>

> <span data-ttu-id="d10d0-112">特別な前提条件はありますか?</span><span class="sxs-lookup"><span data-stu-id="d10d0-112">Any special pre-requisites?</span></span>

## <a name="solution"></a><span data-ttu-id="d10d0-113">ソリューション</span><span class="sxs-lookup"><span data-stu-id="d10d0-113">Solution</span></span>

<span data-ttu-id="d10d0-114">ソリューション</span><span class="sxs-lookup"><span data-stu-id="d10d0-114">Solution</span></span>|<span data-ttu-id="d10d0-115">作成者 (s)</span><span class="sxs-lookup"><span data-stu-id="d10d0-115">Author(s)</span></span>
--------|---------
<span data-ttu-id="d10d0-116">フォルダー名</span><span class="sxs-lookup"><span data-stu-id="d10d0-116">folder name</span></span> | <span data-ttu-id="d10d0-117">作成者の詳細情報 ([名前]、[会社]、[twitter エイリアス (リンク付き)])</span><span class="sxs-lookup"><span data-stu-id="d10d0-117">Author details (name, company, twitter alias with link)</span></span>

## <a name="version-history"></a><span data-ttu-id="d10d0-118">バージョン履歴</span><span class="sxs-lookup"><span data-stu-id="d10d0-118">Version history</span></span>

<span data-ttu-id="d10d0-119">バージョン</span><span class="sxs-lookup"><span data-stu-id="d10d0-119">Version</span></span>|<span data-ttu-id="d10d0-120">日付</span><span class="sxs-lookup"><span data-stu-id="d10d0-120">Date</span></span>|<span data-ttu-id="d10d0-121">コメント</span><span class="sxs-lookup"><span data-stu-id="d10d0-121">Comments</span></span>
-------|----|--------
<span data-ttu-id="d10d0-122">1.1</span><span class="sxs-lookup"><span data-stu-id="d10d0-122">1.1</span></span>|<span data-ttu-id="d10d0-123">2021年3月10日</span><span class="sxs-lookup"><span data-stu-id="d10d0-123">March 10, 2021</span></span>|<span data-ttu-id="d10d0-124">コメントの更新</span><span class="sxs-lookup"><span data-stu-id="d10d0-124">Update comment</span></span>
<span data-ttu-id="d10d0-125">1.0</span><span class="sxs-lookup"><span data-stu-id="d10d0-125">1.0</span></span>|<span data-ttu-id="d10d0-126">2021年1月29日</span><span class="sxs-lookup"><span data-stu-id="d10d0-126">January 29, 2021</span></span>|<span data-ttu-id="d10d0-127">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="d10d0-127">Initial release</span></span>

## <a name="disclaimer"></a><span data-ttu-id="d10d0-128">免責事項</span><span class="sxs-lookup"><span data-stu-id="d10d0-128">Disclaimer</span></span>

<span data-ttu-id="d10d0-129">**このコードは、特定の目的、市販性、または非侵害に対する暗黙の保証を含め、明示的または黙示的ないかなる種類の保証なし *に提供されます* 。**</span><span class="sxs-lookup"><span data-stu-id="d10d0-129">**THIS CODE IS PROVIDED *AS IS* WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**</span></span>

---

## <a name="minimal-path-to-awesome"></a><span data-ttu-id="d10d0-130">Awesome への最小限のパス</span><span class="sxs-lookup"><span data-stu-id="d10d0-130">Minimal Path to Awesome</span></span>

- <span data-ttu-id="d10d0-131">このリポジトリの複製を作成する</span><span class="sxs-lookup"><span data-stu-id="d10d0-131">Clone this repository</span></span>
- <span data-ttu-id="d10d0-132">ソリューションフォルダーにあることを確認する</span><span class="sxs-lookup"><span data-stu-id="d10d0-132">Ensure that you are at the solution folder</span></span>
- <span data-ttu-id="d10d0-133">コマンドラインで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="d10d0-133">in the command-line run:</span></span>
  - <span data-ttu-id="d10d0-134">**npm インストール**</span><span class="sxs-lookup"><span data-stu-id="d10d0-134">**npm install**</span></span>
  - <span data-ttu-id="d10d0-135">**gulp サービス**</span><span class="sxs-lookup"><span data-stu-id="d10d0-135">**gulp serve**</span></span>

> <span data-ttu-id="d10d0-136">必要に応じて追加の手順を含めます。</span><span class="sxs-lookup"><span data-stu-id="d10d0-136">Include any additional steps as needed.</span></span>

## <a name="features"></a><span data-ttu-id="d10d0-137">機能</span><span class="sxs-lookup"><span data-stu-id="d10d0-137">Features</span></span>

<span data-ttu-id="d10d0-138">上位レベルの概要に基づいて展開される拡張機能の説明。</span><span class="sxs-lookup"><span data-stu-id="d10d0-138">Description of the extension that expands upon high-level summary above.</span></span>

<span data-ttu-id="d10d0-139">この拡張機能は、次の概念を示しています。</span><span class="sxs-lookup"><span data-stu-id="d10d0-139">This extension illustrates the following concepts:</span></span>

- <span data-ttu-id="d10d0-140">トピック1</span><span class="sxs-lookup"><span data-stu-id="d10d0-140">topic 1</span></span>
- <span data-ttu-id="d10d0-141">トピック2</span><span class="sxs-lookup"><span data-stu-id="d10d0-141">topic 2</span></span>
- <span data-ttu-id="d10d0-142">トピック3</span><span class="sxs-lookup"><span data-stu-id="d10d0-142">topic 3</span></span>

> <span data-ttu-id="d10d0-143">図とドキュメントがより良いことは、サンプルの使用法と、他のユーザーに提供される価値に大きくなることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d10d0-143">Notice that better pictures and documentation will increase the sample usage and the value you are providing for others.</span></span> <span data-ttu-id="d10d0-144">提出の前に感謝します。</span><span class="sxs-lookup"><span data-stu-id="d10d0-144">Thanks for your submissions advance.</span></span>

> <span data-ttu-id="d10d0-145">Microsoft 365 のパターンとプラクティスのプログラムを使用して、web パーツを他のユーザーと共有し、表示と露出を実現します。</span><span class="sxs-lookup"><span data-stu-id="d10d0-145">Share your web part with others through Microsoft 365 Patterns and Practices program to get visibility and exposure.</span></span> <span data-ttu-id="d10d0-146">コミュニティ、オープンソースプロジェクト、およびからのその他のアクティビティについての詳細 http://aka.ms/m365pnp 。</span><span class="sxs-lookup"><span data-stu-id="d10d0-146">More details on the community, open-source projects and other activities from http://aka.ms/m365pnp.</span></span>

## <a name="references"></a><span data-ttu-id="d10d0-147">関連情報</span><span class="sxs-lookup"><span data-stu-id="d10d0-147">References</span></span>

- [<span data-ttu-id="d10d0-148">SharePoint Framework の概要</span><span class="sxs-lookup"><span data-stu-id="d10d0-148">Getting started with SharePoint Framework</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)
- [<span data-ttu-id="d10d0-149">Microsoft teams の構築</span><span class="sxs-lookup"><span data-stu-id="d10d0-149">Building for Microsoft teams</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/build-for-teams-overview)
- [<span data-ttu-id="d10d0-150">ソリューションで Microsoft Graph を使用する</span><span class="sxs-lookup"><span data-stu-id="d10d0-150">Use Microsoft Graph in your solution</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/using-microsoft-graph-apis)
- [<span data-ttu-id="d10d0-151">SharePoint Framework アプリケーションを Marketplace に発行する</span><span class="sxs-lookup"><span data-stu-id="d10d0-151">Publish SharePoint Framework applications to the Marketplace</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/publish-to-marketplace-overview)
- <span data-ttu-id="d10d0-152">Microsoft [365 のパターンとプラクティス](https://aka.ms/m365pnp)-microsoft 365 開発用のガイダンス、ツーリング、サンプル、およびオープンソースのコントロール</span><span class="sxs-lookup"><span data-stu-id="d10d0-152">[Microsoft 365 Patterns and Practices](https://aka.ms/m365pnp) - Guidance, tooling, samples and open-source controls for your Microsoft 365 development</span></span>
