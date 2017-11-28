---
title: aaaCreate een Universal Windows Platform (UWP) die gebruikmaakt van de Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie tooget gestart met behulp van back-ends voor mobiele Apps van Azure voor Universal Windows Platform (UWP)-app-ontwikkeling in C#, Visual Basic of JavaScript.
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="aa4c8-103">Een Windows-app maken</span><span class="sxs-lookup"><span data-stu-id="aa4c8-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="aa4c8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="aa4c8-104">Overview</span></span>
<span data-ttu-id="aa4c8-105">Deze zelfstudie laat zien hoe een cloud-gebaseerde back-end tooadd tooa Universal Windows Platform (UWP)-app service.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="aa4c8-106">Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="aa4c8-107">Hallo hieronder vindt u er schermafbeeldingen worden gemaakt vanuit de app Hallo voltooid:</span><span class="sxs-lookup"><span data-stu-id="aa4c8-107">hello following are screen captures from hello completed app:</span></span>

![Voltooide bureaublad-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="aa4c8-109">Uitgevoerd op bureaublad.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-109">Running on a desktop.</span></span>

![Voltooide telefoon-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="aa4c8-111">Uitgevoerd op telefoon.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-111">Running on a phone</span></span>

<span data-ttu-id="aa4c8-112">Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor UWP-apps.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa4c8-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa4c8-113">Prerequisites</span></span>
<span data-ttu-id="aa4c8-114">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa4c8-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="aa4c8-115">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-115">An active Azure account.</span></span> <span data-ttu-id="aa4c8-116">Als u geen account hebt, kunt u zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="aa4c8-117">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="aa4c8-118">[Visual Studio Community 2015] of een nieuwere versie.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="aa4c8-119">Een nieuwe back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="aa4c8-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="aa4c8-120">Volg deze stappen toocreate een nieuwe back-end voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="aa4c8-121">U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="aa4c8-122">Nu gaat u een serverproject voor een eenvoudige 'todo list' downloaden back-end en deze tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="aa4c8-123">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="aa4c8-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="aa4c8-124">Hallo client-project downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aa4c8-124">Download and run hello client project</span></span>
<span data-ttu-id="aa4c8-125">Als u uw back-end voor de mobiele App hebt geconfigureerd, kunt u een nieuwe clientapp maken of wijzigen van een bestaande app tooconnect tooAzure.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="aa4c8-126">In deze sectie maakt downloaden u een UWP-app-sjabloonproject dat is backend voor mobiele Apps van aangepaste tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="aa4c8-127">Terug in Hallo **snel starten** blade voor uw mobiele App back-end, klikt u op **maakt een nieuwe app** > **downloaden**, pak vervolgens Hallo gecomprimeerde projectbestanden tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Het project Windows-snelstartgids downloaden](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="aa4c8-129">(Optioneel) Hallo UWP-app-project toohello toevoegen dezelfde oplossing als Hallo serverproject.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="aa4c8-130">Hiermee kunt u gemakkelijker toodebug en test beide app en Hallo back-end in Hallo Hallo dezelfde Visual Studio-oplossing als u ervoor toodo doet kiest.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="aa4c8-131">tooadd een UWP-app-project toohello oplossing, moet u Visual Studio 2015 of hoger.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="aa4c8-132">Hallo UWP-app als opstartproject hello, drukt u op Hallo F5 sleutel toodeploy en Voer Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="aa4c8-133">Typ in het Hallo-app zinvolle tekst, zoals *voltooid Hallo zelfstudie*, in Hallo **nieuwe taak invoegen** in het tekstvak en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows-snelstartgids: bureaublad voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="aa4c8-135">Hierdoor wordt een POST-aanvraag toohello nieuwe mobiele app back-end die wordt gehost in Azure verzonden.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="aa4c8-136">(Optioneel) Hallo app Stop en start deze opnieuw op een ander apparaat of mobiele emulator.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Windows-snelstartgids: telefoon voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="aa4c8-138">U ziet die gegevens opgeslagen van de vorige stap Hallo vanuit Azure geladen nadat Hallo UWP-app is gestart.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4c8-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa4c8-139">Next steps</span></span>
* [<span data-ttu-id="aa4c8-140">Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa4c8-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="aa4c8-141">Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="aa4c8-142">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa4c8-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="aa4c8-143">Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="aa4c8-144">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="aa4c8-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="aa4c8-145">Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="aa4c8-146">Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="aa4c8-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
