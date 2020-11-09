---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823428"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="cd2f6-101">このセクションでは、 [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) を使用して、イベントの簡単な一覧をリッチ UI に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-101">In this section, you'll use the [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to replace the simple list of events with rich UI.</span></span>

<span data-ttu-id="cd2f6-102">このツールキットには、イベントの一覧を表示するための適切な [議題コンポーネント](https://docs.microsoft.com/graph/toolkit/components/agenda)が用意されています。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-102">The toolkit provides an [Agenda component](https://docs.microsoft.com/graph/toolkit/components/agenda), which is well-suited to render our list of events.</span></span>

## <a name="update-the-web-part"></a><span data-ttu-id="cd2f6-103">Web パーツを更新する</span><span class="sxs-lookup"><span data-stu-id="cd2f6-103">Update the web part</span></span>

1. <span data-ttu-id="cd2f6-104">/Src/webparts/graphTutorial/GraphTutorialWebPart.module.scss を開きます **。**</span><span class="sxs-lookup"><span data-stu-id="cd2f6-104">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss**.</span></span> <span data-ttu-id="cd2f6-105">エントリの属性の値 `background-color` `.row` をに変更し `$ms-color-white` ます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-105">Change the value of the `background-color` attribute in the `.row` entry to `$ms-color-white`.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. <span data-ttu-id="cd2f6-106">エントリの中に次のエントリを追加し `.graphTutorial` ます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-106">Add the following entry inside the `.graphTutorial` entry.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. <span data-ttu-id="cd2f6-107">**/Src/webparts/graphTutorial/GraphTutorialWebPart.ts** を開き、次の `import` ステートメントをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-107">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. <span data-ttu-id="cd2f6-108">**GraphTutorialWebPart** クラスに次の関数を追加して、ツールキットを初期化します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-108">Add the following function to the **GraphTutorialWebPart** class to initialize the toolkit.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. <span data-ttu-id="cd2f6-109">既存の `renderCalendarView` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-109">Replace the existing `renderCalendarView` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    <span data-ttu-id="cd2f6-110">これにより、基本リストは、ツールキットの **議題** コンポーネントに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-110">This replaces the basic list with the **Agenda** component from the toolkit.</span></span>

1. <span data-ttu-id="cd2f6-111">Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-111">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

    ![議題コンポーネントを含む web パーツのスクリーンショット](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a><span data-ttu-id="cd2f6-113">別の方法</span><span class="sxs-lookup"><span data-stu-id="cd2f6-113">An alternate approach</span></span>

<span data-ttu-id="cd2f6-114">この時点で、次のコードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-114">At this point, you have code that:</span></span>

- <span data-ttu-id="cd2f6-115">**Msgraphclient** を使用して、Microsoft Graph から現在の週のユーザーの予定表ビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-115">Uses the **MSGraphClient** to get the user's calendar view for the current week from Microsoft Graph.</span></span>
- <span data-ttu-id="cd2f6-116">これらのイベントを Microsoft Graph Toolkit から **議題** コンポーネントに追加します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-116">Add those events to the **Agenda** component from the Microsoft Graph Toolkit.</span></span>

<span data-ttu-id="cd2f6-117">この方法では、Graph API の呼び出しを完全に制御でき、必要に応じてレンダリングする前にイベントの任意の処理を実行できます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-117">With this approach, you have full control over the Graph API call and can do any processing of the events prior to rendering that you want.</span></span> <span data-ttu-id="cd2f6-118">ただし、必要でない場合は、 **議題** コンポーネントに作業を任せることによって簡単にすることができます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-118">However, if that isn't required, you can simplify by letting the **Agenda** component do the work for you.</span></span>

<span data-ttu-id="cd2f6-119">すべての Microsoft Graph Toolkit コンポーネントは、すべての関連する API 呼び出しを Microsoft Graph に対して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-119">All Microsoft Graph Toolkit components are capable of making all of the relevant API calls to the Microsoft Graph.</span></span> <span data-ttu-id="cd2f6-120">たとえば、 **議題** コンポーネントを web パーツに追加するだけで、プロパティを設定しない場合、web パーツは既定の設定を使用して、現在の日付のイベントを取得します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-120">For example, by just adding the **Agenda** component to the web part, and not setting any properties, the web part would use its default settings to get events for the current day.</span></span> <span data-ttu-id="cd2f6-121">現在の同じ結果 (現在の週のイベント) を実現する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-121">Let's look at how we can achieve the same results we currently have (events for the current week).</span></span>

1. <span data-ttu-id="cd2f6-122">既存の `render` メソッドを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-122">Replace the existing `render` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    <span data-ttu-id="cd2f6-123">これで、API 呼び出しを行う代わりに、 `render` `mgt-agenda` HTML に要素を直接追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-123">Now, instead of making an API call in `render`, you simply add an `mgt-agenda` element directly into the HTML.</span></span> <span data-ttu-id="cd2f6-124">`date`週の開始日と7に設定すると、 `days` コンポーネントは以前のバージョンのと同じ API 呼び出しを作成 `render` します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-124">By setting `date` to the start of the week, and `days` to 7, the component will make the same API call the previous version of `render` was making.</span></span>

1. <span data-ttu-id="cd2f6-125">**GraphTutorialWebPart** クラスに、次の空の関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-125">Add the following empty function to the **GraphTutorialWebPart** class.</span></span>

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > <span data-ttu-id="cd2f6-126">また、web パーツに [ **チームのソーシャルを追加** ] ボタンを追加し、このメソッドを `addSocialToCalendar` イベントリスナーとして追加しました。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-126">We also added an **Add team social** button to the web part, and added the `addSocialToCalendar` method as an event listener.</span></span>  <span data-ttu-id="cd2f6-127">次のセクションで、分離コードを実装します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-127">You'll implement the code behind that in the next section.</span></span> <span data-ttu-id="cd2f6-128">ここでは、コードをコンパイルするだけです。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-128">For now, we just want the code to compile.</span></span>

1. <span data-ttu-id="cd2f6-129">Web パーツをビルド、パッケージ化、再アップロードし、テストするページを更新します。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-129">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span> <span data-ttu-id="cd2f6-130">ビューは、前のテストと同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-130">The view should be the same as your previous test.</span></span>

### <a name="using-the-toolkit-vs-making-api-calls"></a><span data-ttu-id="cd2f6-131">ツールキット vs API 呼び出しの使用</span><span class="sxs-lookup"><span data-stu-id="cd2f6-131">Using the toolkit vs making API calls</span></span>

<span data-ttu-id="cd2f6-132">この時点で、ツールキットが機能しているときに、 **Msgraphclient** を使用する際にトラブルが発生した理由を不思議に思うかもしれません。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-132">At this point you may be wondering why you went through the trouble of using the **MSGraphClient** at all, when the toolkit does the work for you.</span></span> <span data-ttu-id="cd2f6-133">ツールキットは、イベントの一覧など、Microsoft Graph からクエリを実行する結果を表示するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-133">The toolkit is designed for rendering results that you query from Microsoft Graph, such as a list of events.</span></span> <span data-ttu-id="cd2f6-134">ただし、自分で API 呼び出しを行う必要があるシナリオもあります。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-134">However, there are scenarios where making API calls yourself is necessary.</span></span>

- <span data-ttu-id="cd2f6-135">要求ではない API 呼び出し `GET` 。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-135">Any API calls that are not a `GET` request.</span></span> <span data-ttu-id="cd2f6-136">たとえば、予定表に新しいイベントを作成したり、ユーザーの電話番号を更新したりします。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-136">For example, creating a new event on the calendar, or updating a user's phone number.</span></span>
- <span data-ttu-id="cd2f6-137">バックグラウンドでの使用を目的としたデータを取得し、直接レンダリングしないようにするための API 呼び出し。</span><span class="sxs-lookup"><span data-stu-id="cd2f6-137">API calls to get data that's intended to be used "behind the scenes" and not rendered directly.</span></span>
