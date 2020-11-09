---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823336"
---
<!-- markdownlint-disable MD002 MD041 -->

このチュートリアルでは、Microsoft Graph を使用して現在の週のユーザーの予定表を取得し、ユーザーが予定表にイベントを追加できるようにする [SharePoint クライアント側の web パーツ](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) を作成します。

## <a name="create-a-web-part-project"></a>Web パーツプロジェクトを作成する

1. プロジェクトを作成する空のディレクトリで、コマンドラインインターフェイス (CLI) を開きます。 次のコマンドを実行して、[ごみ箱] SharePoint ジェネレーターを起動します。

    ```Shell
    yo @microsoft/sharepoint
    ```

1. プロンプトに次のように応答します。

    - **ソリューション名は何ですか。** `graph-tutorial`
    - **どのベースライン パッケージをコンポーネントのターゲットにしたいですか?** `SharePoint Online only (latest)`
    - **ファイルをどこに保存しますか?** `Use the current folder`
    - **テナント管理者が、サイトで機能を展開したり、アプリを追加したりせず、すぐにすべてのサイトでソリューションを展開できるようにしたいですか?** `Yes`
    - **ソリューション内のコンポーネントには、一意であり、10人の他のコンポーネントと共有していない web Api にアクセスするためのアクセス許可が必要ですか。** `No`
    - **どの種類のクライアント側コンポーネントを作成しますか?** `WebPart`
    - **Web パーツ名は何ですか?** `GraphTutorial`
    - **Web パーツで何を行いますか?** `GraphTutorial description`
    - **どのフレームワークを使用しますか?** `No JavaScript framework`

1. 次のコマンドを実行して、プロジェクトの TypeScript バージョンを3.7 に更新します。

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. tsconfig.jsを開き、を **に** 置き換え `rush-stack-compiler-3.3` `rush-stack-compiler-3.7` ます。

1. **/tslint.jsを** 開き、行を削除します。 `"no-use-before-declare": true,` `no-use-before-declare`ルールは推奨されなくなり、ビルドプロセス中にエラーが発生します。

## <a name="install-dependencies"></a>依存関係のインストール

に進む前に、後で使用する追加の NPM パッケージをインストールします。

- Microsoft graph の[TypeScript 定義](https://github.com/microsoftgraph/msgraph-typescript-typings)を使用して、microsoft graph オブジェクトの Intellisense を提供します。
- Web パーツの UI コンポーネントを提供する[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) 。
- [日付-fns 日付](https://date-fns.org/) を操作するための便利な機能。

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
