---
title: Dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp | Microsoft Docs
description: Lees hoe u een Office 365-app deelt met uw gebruikers met behulp van Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="f9441-103">Dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f9441-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f9441-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="f9441-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f9441-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f9441-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f9441-106">In dit artikel wordt uitgelegd hoe u Office 365 implementeert op elk apparaat in uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="f9441-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="f9441-107">Uw gebruikers beschikken op Android, Apple en Windows over dezelfde mogelijkheden en gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="f9441-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="f9441-108">We kunnen dit met Azure RemoteApp bewerkstelligen door Office 365 te hosten op schaalbare virtuele machines in Azure, waarmee gebruikers verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="f9441-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="f9441-109">Deze set van virtuele machines noemen we een 'cloudverzameling'.</span><span class="sxs-lookup"><span data-stu-id="f9441-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="f9441-110">Een cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="f9441-110">Create a cloud collection</span></span>
<span data-ttu-id="f9441-111">Ga nadat u een Azure-account hebt gemaakt eerst naar **RemoteApp** door op de koppeling aan de linkerkant te klikken.</span><span class="sxs-lookup"><span data-stu-id="f9441-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="f9441-112">![Azure RemoteApp in Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="f9441-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="f9441-113">Klik vervolgens onderaan op **Nieuw** en kies voor het 'snel maken' van een verzameling.</span><span class="sxs-lookup"><span data-stu-id="f9441-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="f9441-114">Geef een naam, de regio, het abonnement, het plan en de 'Office Proffesional 2013'-installatiekopie die wij verstrekken op.</span><span class="sxs-lookup"><span data-stu-id="f9441-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="f9441-115">![Dialoogvenster Maken](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="f9441-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="f9441-116">Wanneer u het formulier hebt ingevuld, wordt het proces voor het maken van de verzameling gestart.</span><span class="sxs-lookup"><span data-stu-id="f9441-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="f9441-117">Dit duurt ongeveer een uur.</span><span class="sxs-lookup"><span data-stu-id="f9441-117">This may take up to an hour or so.</span></span>

![Wachten](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="f9441-119">Als dit proces is voltooid, ziet dit er ongeveer als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="f9441-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="f9441-120">Als u op **Publiceren** klikt, ziet u dat de meeste Office-toepassingen al zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="f9441-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="f9441-121">![Verzameling gemaakt](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="f9441-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Gepubliceerde apps](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="f9441-123">Nu kunt u ook op **Gebruikerstoegang** klikken om meer gebruikers toe te voegen die toegang hebben tot deze verzameling.</span><span class="sxs-lookup"><span data-stu-id="f9441-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="f9441-124">![Gebruikerstoegang configureren](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="f9441-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="f9441-125">Nu gaan we proberen verbinding te maken met Office 365.</span><span class="sxs-lookup"><span data-stu-id="f9441-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="f9441-126">Verbinding maken met Office 365</span><span class="sxs-lookup"><span data-stu-id="f9441-126">Connect to Office 365</span></span>
<span data-ttu-id="f9441-127">Ga naar [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), schuif naar beneden en klik op **Clients downloaden** om de Azure RemoteApp-client op uw apparaat te installeren.</span><span class="sxs-lookup"><span data-stu-id="f9441-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="f9441-128">De onderstaande schermafbeeldingen zijn voor Windows.</span><span class="sxs-lookup"><span data-stu-id="f9441-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="f9441-129">Zodra de toepassing wordt gestart, wordt u gevraagd om u aan te melden met uw Microsoft-account (voorheen een 'Live-ID'). Gebruik nu uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f9441-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="f9441-130">Wanneer u bent aangemeld, ziet u een melding over nieuwe uitnodigingen. Klik op de melding, waarna een lijst zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f9441-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="f9441-131">Accepteer de uitnodiging die overeenkomt met het e-mailadres de eigenaar van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f9441-131">Accept the invitation that matches your Azure account owner email.</span></span>

![Nieuwe uitnodiging](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="f9441-133">Zo ziet het eruit wanneer er nieuwe uitnodigingen zijn.</span><span class="sxs-lookup"><span data-stu-id="f9441-133">What it looks like when there are new invitations.</span></span>

![Een toepassing accepteren](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="f9441-135">Wanneer u de uitnodiging hebt geaccepteerd, worden alle Office-apps weergegeven in de Azure RemoteApp-client.</span><span class="sxs-lookup"><span data-stu-id="f9441-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![Lijst met apps](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="f9441-137">Wanneer u op een van deze toepassing klikt, wordt deze gestart op de virtuele machine van Azure en kunt u ermee aan de slag.</span><span class="sxs-lookup"><span data-stu-id="f9441-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="f9441-138">Veel plezier!</span><span class="sxs-lookup"><span data-stu-id="f9441-138">Enjoy!</span></span>

![starten](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

