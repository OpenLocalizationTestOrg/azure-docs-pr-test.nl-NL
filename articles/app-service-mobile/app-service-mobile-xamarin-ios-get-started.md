---
title: aaaGet de slag met Azure App Service Mobile Apps voor Xamarin.iOS-apps | Microsoft Docs
description: Volg deze zelfstudie tooget slag kunt met Mobile Apps voor Xamarin.iOS-ontwikkeling.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="0df76-103">Een Xamarin.iOS-app maken</span><span class="sxs-lookup"><span data-stu-id="0df76-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0df76-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0df76-104">Overview</span></span>
<span data-ttu-id="0df76-105">Deze zelfstudie leert u hoe tooadd back-end van een cloud-gebaseerde mobiele tooa Xamarin.iOS-app service met behulp van een back-end voor mobiele Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="0df76-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="0df76-106">U maakt zowel een nieuwe back-end voor mobiele apps als een eenvoudige Xamarin.iOS-app voor *takenlijsten* die app-gegevens opslaat in Azure.</span><span class="sxs-lookup"><span data-stu-id="0df76-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="0df76-107">Voltooien van deze zelfstudie is een vereiste voor alle andere Xamarin.iOS-zelfstudies over het gebruik van de functie Mobile Apps Hallo in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0df76-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0df76-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0df76-108">Prerequisites</span></span>
<span data-ttu-id="0df76-109">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="0df76-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="0df76-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="0df76-110">An active Azure account.</span></span> <span data-ttu-id="0df76-111">Als u geen account hebt, zich aanmelden voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0df76-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="0df76-112">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0df76-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0df76-113">Visual Studio met Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0df76-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="0df76-114">Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="0df76-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="0df76-115">Een Mac met Xcode v7.0 of hoger en waarop Xamarin Studio Community is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0df76-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="0df76-116">Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) en [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Instructies voor installatie, configuratie en verificatie voor Mac-gebruikers) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="0df76-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="0df76-117">Een back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="0df76-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="0df76-118">Volg deze stappen toocreate een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="0df76-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="0df76-119">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="0df76-119">Configure hello server project</span></span>
<span data-ttu-id="0df76-120">U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="0df76-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="0df76-121">Vervolgens een serverproject downloaden voor een eenvoudige 'todo list' back-end en deze tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="0df76-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="0df76-122">Volg stappen tooconfigure Hallo server project toouse na Hallo beide Hallo Node.js- of .NET-back-end.</span><span class="sxs-lookup"><span data-stu-id="0df76-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="0df76-123">Hallo Xamarin.iOS-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0df76-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="0df76-124">Open Hallo [Azure-portal] in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="0df76-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="0df76-125">Klik op de blade met Hallo-instellingen voor uw mobiele App, **aan de slag** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="0df76-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="0df76-126">Klik in stap 3 op **Een nieuwe app maken** als deze optie nog niet is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0df76-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="0df76-127">Klik vervolgens op Hallo **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="0df76-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="0df76-128">Een clienttoepassing die verbinding tooyour mobiele back-end maakt wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="0df76-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="0df76-129">Hallo gecomprimeerde projectbestand op uw lokale computer opslaan en maak een notitie van de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="0df76-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="0df76-130">Pak Hallo-project dat u hebt gedownload en open het in Xamarin Studio (of Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="0df76-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="0df76-131">Druk op Hallo F5 sleutel toobuild Hallo project en Hallo-app te starten in Hallo iPhone-emulator.</span><span class="sxs-lookup"><span data-stu-id="0df76-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="0df76-132">Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en klik vervolgens op Hallo  **+**  knop.</span><span class="sxs-lookup"><span data-stu-id="0df76-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="0df76-133">De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="0df76-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="0df76-134">Items die zijn opgeslagen in de tabel Hallo zijn geretourneerd door de back-end van Hallo mobiele app en de gegevens worden weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="0df76-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="0df76-135">U kunt Hallo-code die toegang heeft tot uw back-end voor mobiele app tooquery bekijken en gegevens invoegen in Hallo QSTodoService.cs C#-bestand.</span><span class="sxs-lookup"><span data-stu-id="0df76-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0df76-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0df76-136">Next steps</span></span>
* [<span data-ttu-id="0df76-137">Offline synchronisatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="0df76-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="0df76-138">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="0df76-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="0df76-139">Push notifications tooyour Xamarin.Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="0df76-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="0df76-140">Hoe toouse Hallo-client voor mobiele Apps van Azure beheerd</span><span class="sxs-lookup"><span data-stu-id="0df76-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure-portal]: https://portal.azure.com/
