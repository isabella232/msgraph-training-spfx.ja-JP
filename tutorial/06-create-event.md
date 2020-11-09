---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823323"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="88ec4-101">このセクションでは、web パーツを更新して、ユーザーがチームの週のソーシャル時間の予定表にイベントを追加できるようにします。</span><span class="sxs-lookup"><span data-stu-id="88ec4-101">In this section you'll update the web part to allow the user to add an event to their calendar for the team's weekly social hour.</span></span> <span data-ttu-id="88ec4-102">このシナリオでは、チームは金曜日の午後4時に1週間のソーシャル時間を持ちます。</span><span class="sxs-lookup"><span data-stu-id="88ec4-102">In this scenario, the team has a weekly social hour at 4 PM on Friday.</span></span>

1. <span data-ttu-id="88ec4-103">**/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、既存の `addSocialToCalendar()` メソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="88ec4-103">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and replace the existing `addSocialToCalendar()` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    <span data-ttu-id="88ec4-104">このコードの内容を検討してください。</span><span class="sxs-lookup"><span data-stu-id="88ec4-104">Consider what this code does.</span></span>

    - <span data-ttu-id="88ec4-105">今後の次の金曜日を調べ、その日の午後4時に **日付** を作成します。</span><span class="sxs-lookup"><span data-stu-id="88ec4-105">It determines the next upcoming Friday and constructs a **Date** for 4 PM on that day.</span></span>
    - <span data-ttu-id="88ec4-106">このメソッドは、新しい **Microsoft graph の Event** オブジェクトを作成し、 **日付** の値に開始を設定し、1時間後に終了します。</span><span class="sxs-lookup"><span data-stu-id="88ec4-106">It constructs a new **MicrosoftGraph.Event** object, setting the start to the value of the **Date** , and the end for one hour later.</span></span>
    - <span data-ttu-id="88ec4-107">**Msgraphclient** を使用して、エンドポイントに新しいイベントをポストし `/me/events` ます。</span><span class="sxs-lookup"><span data-stu-id="88ec4-107">It uses the **MSGraphClient** to POST the new event to the `/me/events` endpoint.</span></span>
    - <span data-ttu-id="88ec4-108">これにより、新しいイベントによってビューが更新されるように、web パーツが再レンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="88ec4-108">It re-renders the web part so the view is updated with the new event.</span></span>

1. <span data-ttu-id="88ec4-109">Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。</span><span class="sxs-lookup"><span data-stu-id="88ec4-109">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

1. <span data-ttu-id="88ec4-110">[ **チームソーシャルの追加** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="88ec4-110">Click the **Add team social** button.</span></span> <span data-ttu-id="88ec4-111">ページが更新されたら、金曜日までスクロールし、新しいイベントを見つけます。</span><span class="sxs-lookup"><span data-stu-id="88ec4-111">Once the page refreshes, scroll down to Friday and find the new event.</span></span>

    ![Web パーツに表示される新しく作成されたイベントのスクリーンショット](images/new-event.png)
