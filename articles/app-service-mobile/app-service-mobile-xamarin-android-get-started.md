---
title: Aan de slag met Azure Mobile Apps voor Xamarin.Android-apps
description: Volg deze zelfstudie om aan de slag te gaan met Azure Mobile Apps voor Xamarin.Android-ontwikkeling
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
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="edb2c-103">Een Xamarin.Android-app maken</span><span class="sxs-lookup"><span data-stu-id="edb2c-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="edb2c-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="edb2c-104">Overview</span></span>
<span data-ttu-id="edb2c-105">Deze zelfstudie laat zien hoe u een back-endservice toevoegt aan een Xamarin.Android-app in de cloud.</span><span class="sxs-lookup"><span data-stu-id="edb2c-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="edb2c-106">Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="edb2c-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="edb2c-107">Hieronder ziet u een schermafbeelding van de voltooide app:</span><span class="sxs-lookup"><span data-stu-id="edb2c-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="edb2c-108">Het voltooien van deze zelfstudie is een vereiste voor alle andere Mobile Apps-zelfstudies voor Xamarin.Android-apps.</span><span class="sxs-lookup"><span data-stu-id="edb2c-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edb2c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edb2c-109">Prerequisites</span></span>
<span data-ttu-id="edb2c-110">Voor het voltooien van deze zelfstudie moet aan de volgende vereisten worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="edb2c-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="edb2c-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="edb2c-111">An active Azure account.</span></span> <span data-ttu-id="edb2c-112">Als u geen account hebt, meld u zich aan voor een proefversie van Azure en ontvangt u maximaal 10 gratis mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="edb2c-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="edb2c-113">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="edb2c-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="edb2c-114">Visual Studio met Xamarin.</span><span class="sxs-lookup"><span data-stu-id="edb2c-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="edb2c-115">Zie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Installeren en instellen voor Visual Studio en Xamarin) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="edb2c-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="edb2c-116">Een back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="edb2c-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="edb2c-117">Volg deze stappen voor het maken van een back-end voor mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="edb2c-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="edb2c-118">U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="edb2c-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="edb2c-119">Download vervolgens een serverproject voor een eenvoudige back-end voor takenlijsten en publiceer deze naar Azure.</span><span class="sxs-lookup"><span data-stu-id="edb2c-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="edb2c-120">Het serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="edb2c-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="edb2c-121">De Xamarin.Android-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="edb2c-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="edb2c-122">Klik onder **Het Xamarin.Android-project downloaden en uitvoeren** op de knop **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="edb2c-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="edb2c-123">Sla het gecomprimeerde projectbestand op uw lokale computer op en noteer de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="edb2c-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="edb2c-124">Druk op de toets **F5** om het project te bouwen en de app te starten.</span><span class="sxs-lookup"><span data-stu-id="edb2c-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="edb2c-125">Typ zinvolle tekst in de app, zoals *Voltooi de zelfstudie*, en klik vervolgens op de knop **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="edb2c-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="edb2c-126">Gegevens van de aanvraag worden opgenomen in de takentabel.</span><span class="sxs-lookup"><span data-stu-id="edb2c-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="edb2c-127">Items die zijn opgeslagen in de tabel, worden geretourneerd door de back-end voor mobiele apps en de gegevens verschijnen in de lijst.</span><span class="sxs-lookup"><span data-stu-id="edb2c-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="edb2c-128">U kunt de code die toegang heeft tot de back-end van uw mobiele app bekijken om gegevens op te vragen en in te voegen. Deze code vindt u in het C#-bestand ToDoActivity.cs.</span><span class="sxs-lookup"><span data-stu-id="edb2c-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="edb2c-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edb2c-129">Next steps</span></span>
* [<span data-ttu-id="edb2c-130">Offlinesynchronisatie toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="edb2c-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="edb2c-131">Verificatie toevoegen aan uw app </span><span class="sxs-lookup"><span data-stu-id="edb2c-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="edb2c-132">Pushmeldingen toevoegen aan uw Xamarin.Android-app</span><span class="sxs-lookup"><span data-stu-id="edb2c-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="edb2c-133">De beheerde client gebruiken voor Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="edb2c-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
