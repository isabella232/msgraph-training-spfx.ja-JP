---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823323"
---
<!-- markdownlint-disable MD002 MD041 -->

このセクションでは、web パーツを更新して、ユーザーがチームの週のソーシャル時間の予定表にイベントを追加できるようにします。 このシナリオでは、チームは金曜日の午後4時に1週間のソーシャル時間を持ちます。

1. **/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、既存の `addSocialToCalendar()` メソッドを次のように置き換えます。

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    このコードの内容を検討してください。

    - 今後の次の金曜日を調べ、その日の午後4時に **日付** を作成します。
    - このメソッドは、新しい **Microsoft graph の Event** オブジェクトを作成し、 **日付** の値に開始を設定し、1時間後に終了します。
    - **Msgraphclient** を使用して、エンドポイントに新しいイベントをポストし `/me/events` ます。
    - これにより、新しいイベントによってビューが更新されるように、web パーツが再レンダリングされます。

1. Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。

1. [ **チームソーシャルの追加** ] ボタンをクリックします。 ページが更新されたら、金曜日までスクロールし、新しいイベントを見つけます。

    ![Web パーツに表示される新しく作成されたイベントのスクリーンショット](images/new-event.png)
