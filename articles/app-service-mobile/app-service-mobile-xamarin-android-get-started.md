---
title: aaaGet gestart met Azure Mobile Apps voor Xamarin.Android-apps
description: Volg deze zelfstudie tooget de slag met Azure Mobile Apps voor Xamarin.android-ontwikkeling
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="25dbf-103">Een Xamarin.Android-app maken</span><span class="sxs-lookup"><span data-stu-id="25dbf-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="25dbf-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="25dbf-104">Overview</span></span>
<span data-ttu-id="25dbf-105">Deze zelfstudie laat zien hoe een cloud-gebaseerde back-end tooadd tooa Xamarin.Android-app service.</span><span class="sxs-lookup"><span data-stu-id="25dbf-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="25dbf-106">Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25dbf-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="25dbf-107">Een schermafbeelding van de app Hallo voltooid lager is dan:</span><span class="sxs-lookup"><span data-stu-id="25dbf-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="25dbf-108">Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Apps-zelfstudies voor Xamarin.Android-apps.</span><span class="sxs-lookup"><span data-stu-id="25dbf-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25dbf-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="25dbf-109">Prerequisites</span></span>
<span data-ttu-id="25dbf-110">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="25dbf-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="25dbf-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="25dbf-111">An active Azure account.</span></span> <span data-ttu-id="25dbf-112">Als u geen account hebt, zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="25dbf-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="25dbf-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="25dbf-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="25dbf-114">Visual Studio met Xamarin.</span><span class="sxs-lookup"><span data-stu-id="25dbf-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="25dbf-115">Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="25dbf-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="25dbf-116">Een back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="25dbf-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="25dbf-117">Volg deze stappen toocreate een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="25dbf-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="25dbf-118">U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="25dbf-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="25dbf-119">Vervolgens een serverproject downloaden voor een eenvoudige 'todo list' back-end en deze tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="25dbf-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="25dbf-120">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="25dbf-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="25dbf-121">Hallo Xamarin.Android-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="25dbf-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="25dbf-122">Onder **uw Xamarin.Android-project downloaden en uitvoeren**, klikt u op Hallo **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="25dbf-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="25dbf-123">Hallo project gecomprimeerde bestand tooyour lokale computer opslaan en maak een notitie van de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="25dbf-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="25dbf-124">Druk op Hallo **F5** toobuild Hallo project sleutel en het Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="25dbf-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="25dbf-125">Typ in het Hallo-app zinvolle tekst, zoals *voltooid Hallo zelfstudie* en klik vervolgens op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="25dbf-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="25dbf-126">De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="25dbf-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="25dbf-127">Items die zijn opgeslagen in de tabel Hallo zijn geretourneerd door de back-end van Hallo mobiele app en de gegevens worden weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="25dbf-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25dbf-128">U kunt Hallo-code die toegang heeft tot uw back-end voor mobiele app tooquery bekijken en gegevens vindt u in C#-bestand ToDoActivity.cs Hallo invoegen.</span><span class="sxs-lookup"><span data-stu-id="25dbf-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="25dbf-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25dbf-129">Next steps</span></span>
* [<span data-ttu-id="25dbf-130">Offline synchronisatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="25dbf-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="25dbf-131">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="25dbf-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="25dbf-132">Push notifications tooyour Xamarin.Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="25dbf-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="25dbf-133">Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd</span><span class="sxs-lookup"><span data-stu-id="25dbf-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
