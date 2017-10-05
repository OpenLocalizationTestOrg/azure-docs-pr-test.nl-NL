---
title: Een Universal Windows Platform-app (UWP) maken die gebruikmaakt van Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie om aan de slag te gaan met back-ends voor mobiele apps van Azure voor Universal Windows Platform (UWP)-app-ontwikkeling in C#, Visual Basic of JavaScript.
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
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="98bcd-103">Een Windows-app maken</span><span class="sxs-lookup"><span data-stu-id="98bcd-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="98bcd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="98bcd-104">Overview</span></span>
<span data-ttu-id="98bcd-105">Deze zelfstudie laat zien hoe u een back-endservice toevoegt aan een Universal Windows Platform (UWP)-app in de cloud.</span><span class="sxs-lookup"><span data-stu-id="98bcd-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="98bcd-106">Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="98bcd-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="98bcd-107">Hier volgen enkele schermopnamen van een voltooide app:</span><span class="sxs-lookup"><span data-stu-id="98bcd-107">The following are screen captures from the completed app:</span></span>

![Voltooide bureaublad-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="98bcd-109">Uitgevoerd op bureaublad.</span><span class="sxs-lookup"><span data-stu-id="98bcd-109">Running on a desktop.</span></span>

![Voltooide telefoon-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="98bcd-111">Uitgevoerd op telefoon.</span><span class="sxs-lookup"><span data-stu-id="98bcd-111">Running on a phone</span></span>

<span data-ttu-id="98bcd-112">Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor UWP-apps.</span><span class="sxs-lookup"><span data-stu-id="98bcd-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98bcd-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="98bcd-113">Prerequisites</span></span>
<span data-ttu-id="98bcd-114">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="98bcd-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="98bcd-115">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="98bcd-115">An active Azure account.</span></span> <span data-ttu-id="98bcd-116">Als u geen account hebt, kunt u zich aanmelden voor een proefversie van Azure en maximaal tien gratis mobiele apps krijgen die u ook na de proefperiode kunt blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98bcd-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="98bcd-117">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="98bcd-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="98bcd-118">[Visual Studio Community 2015] of een nieuwere versie.</span><span class="sxs-lookup"><span data-stu-id="98bcd-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="98bcd-119">Een nieuwe back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="98bcd-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="98bcd-120">Volg deze stappen voor het maken van een nieuwe back-end voor mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="98bcd-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="98bcd-121">U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="98bcd-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="98bcd-122">Nu gaat u een serverproject downloaden voor een eenvoudige back-end voor takenlijsten en deze publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="98bcd-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="98bcd-123">Het serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="98bcd-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="98bcd-124">Het clientproject downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="98bcd-124">Download and run the client project</span></span>
<span data-ttu-id="98bcd-125">Zodra u de back-end voor mobiele apps hebt geconfigureerd, kunt u een nieuwe client-app maken of een bestaande app wijzigen om verbinding te maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="98bcd-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="98bcd-126">In deze sectie download u een sjabloonproject voor een UWP-app die is aangepast om verbinding te kunnen maken met de back-end voor uw mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="98bcd-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="98bcd-127">Op de blade **Snel starten** voor de back-end voor uw mobile app klikt u op **Een nieuwe app maken** > **Downloaden**. Pak de gecomprimeerde projectbestanden uit op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="98bcd-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Het project Windows-snelstartgids downloaden](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="98bcd-129">Optioneel: Voeg het UWP-appproject toe aan dezelfde oplossing als het serverproject.</span><span class="sxs-lookup"><span data-stu-id="98bcd-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="98bcd-130">Hierdoor kunt u desgewenst zowel de app als de back-end makkelijker debuggen en testen in dezelfde Visual-Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="98bcd-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="98bcd-131">Als u een UWP-app-project aan de oplossing wilt toevoegen, dient u Visual Studio 2015 of een nieuwere versie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98bcd-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="98bcd-132">Met de UWP-app als opstartproject, drukt u op de F5-toets om de app te implementeren en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="98bcd-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="98bcd-133">Typ zinvolle tekst in de app, zoals *Voltooi de zelfstudie*, in het tekstvak **Nieuwe taak invoegen** en klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="98bcd-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows-snelstartgids: bureaublad voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="98bcd-135">Hierdoor wordt een POST-aanvraag verzonden naar de nieuwe back-end voor mobiele apps die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="98bcd-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="98bcd-136">Optioneel: Stop de app en start deze opnieuw op een ander apparaat of mobiele emulator.</span><span class="sxs-lookup"><span data-stu-id="98bcd-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Windows-snelstartgids: telefoon voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="98bcd-138">De gegevens die in de vorige stap zijn opgeslagen, worden vanuit Azure geladen nadat de UWP-app is gestart.</span><span class="sxs-lookup"><span data-stu-id="98bcd-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98bcd-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98bcd-139">Next steps</span></span>
* [<span data-ttu-id="98bcd-140">Verificatie toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="98bcd-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="98bcd-141">Ontdek hoe u gebruikers van uw app verifieert met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="98bcd-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="98bcd-142">Pushmeldingen toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="98bcd-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="98bcd-143">Informatie over het toevoegen van ondersteuning van pushmeldingen aan uw app en het configureren van de backend voor mobiele apps voor gebruik van Azure Notification Hubs voor het verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="98bcd-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="98bcd-144">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="98bcd-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="98bcd-145">Informatie over het toevoegen van offlineondersteuning aan uw app met een back-end voor mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="98bcd-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="98bcd-146">Met offlinesynchronisatie kunnen eindgebruikers interactie aangaan met een mobiele app&mdash;gegevens weergeven, toevoegen of wijzigen&mdash;ook als er geen netwerkverbinding is.</span><span class="sxs-lookup"><span data-stu-id="98bcd-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="98bcd-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="98bcd-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
