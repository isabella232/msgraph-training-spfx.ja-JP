---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831349"
---
# <a name="how-to-run-the-completed-project"></a>完了したプロジェクトを実行する方法

## <a name="prerequisites"></a>前提条件

このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。

- バージョン 10 .x [Node.js](https://nodejs.org/en/download/releases/)
- [Gulp](https://gulpjs.com/)
- 同じ組織内のグローバル管理者アカウントへのアクセス権を持つ Microsoft の職場または学校のアカウント。 Microsoft アカウントを持っていない場合は、 [office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program) して、無料の office 365 サブスクリプションを取得することができます。
- このチュートリアルを開始する前に、アプリカタログとテストサイトを作成して、Microsoft 365 テナント [を SharePoint Framework 開発用にセットアップ](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)する必要があります。

### <a name="deploy-the-web-part"></a>Web パーツを展開する

1. Web パーツをビルドしてパッケージ化するには、CLI で次の2つのコマンドを実行します。

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. ブラウザーを開き、テナントの SharePoint アプリカタログに移動します。 左側の [ **SharePoint 用アプリ** ] メニュー項目を選択します。

1. **/Sharepoint/solution/graph-tutorial.sppkg** ファイルをアップロードします。

1. [ **信頼する..** .] プロンプトに、[ファイルの **package-solution.js** に設定した4つの Microsoft Graph アクセス許可が一覧表示されていることを確認します。 [ **組織内のすべてのサイトでこのソリューションを使用できるようにする** ] を選択し、[ **展開** ] を選択します。

1. テナント管理者を使用して [SharePoint 管理センター](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) に移動します。

1. 左側のメニューで、[ **詳細** ]、[ **API アクセス** ] の順に選択します。

1. **グラフ-チュートリアル-クライアント側ソリューション** パッケージから保留中の各要求を選択し、[ **承認** ] を選択します。

    ![SharePoint 管理センターの API アクセスページのスクリーンショット](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a>Web パーツをテストする

1. Web パーツをテストする SharePoint サイトに移動します。 Web パーツをテストする新しいページを作成します。

1. Web パーツピッカーを使用して、 **Graphtutorial** web パーツを検索し、それをページに追加します。

    ![Web パーツピッカーの GraphTutorial web パーツのスクリーンショット](../tutorial/images/add-web-part.png)
