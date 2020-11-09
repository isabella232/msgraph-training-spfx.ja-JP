---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823346"
---
<!-- markdownlint-disable MD002 MD041 -->

このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する [SharePoint のクライアント側 web パーツ](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) を作成する方法について説明します。

> [!TIP]
> 完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-spfx)をダウンロードするか、クローンを作成できます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを開始する前に、開発用コンピューターに次のツールをインストールしておく必要があります。

- [Node.js](https://nodejs.org/en/download/releases/)
- [Yeoman](https://yeoman.io/)
- [Gulp](https://gulpjs.com/)
- [Yeoman の SharePoint ジェネレーター](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

Sharepoint Framework 開発の要件の詳細については [、「sharepoint framework 開発環境を](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment)セットアップする」を参照してください。

> [!IMPORTANT]
> SharePoint Framework には Node.js バージョン 10 .x が必要です。 必ず正しいバージョンをインストールしてください。

また、同じ組織内のグローバル管理者アカウントにアクセスできる、Microsoft の職場または学校アカウントを持っている必要があります。 Microsoft アカウントを持っていない場合は、 [office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program) して、無料の office 365 サブスクリプションを取得することができます。

このチュートリアルを開始する前に、アプリカタログとテストサイトを作成して、Microsoft 365 テナント [を SharePoint Framework 開発用にセットアップ](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)する必要があります。

> [!NOTE]
> このチュートリアルは、上記のツールの次のバージョンで記述されています。 このガイドの手順は、他のバージョンでは動作しますが、テストされていません。
>
> - Node.js 10.22.0
> - ごみ箱オマーン3.1.1
> - Gulp 4.0.2
> - (オマーン) SharePoint ジェネレーター1.11.0

## <a name="feedback"></a>フィードバック

このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-spfx)に記入してください。
