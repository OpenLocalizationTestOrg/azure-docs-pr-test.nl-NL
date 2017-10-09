---
title: aaaGet Hallo dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooshare elke Office 365-app met uw gebruikers met behulp van Azure RemoteApp.
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
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="93a4a-103">Get Hallo dezelfde Office 365-ervaring op elk apparaat met Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="93a4a-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93a4a-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="93a4a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="93a4a-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="93a4a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="93a4a-106">Dit artikel wordt uitgelegd hoe toodeploy Office 365 op elk apparaat in uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="93a4a-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="93a4a-107">Uw gebruikers toegang krijgen Hallo dezelfde mogelijkheden en gebruikersinterface ervaring voor Android, Apple en Windows.</span><span class="sxs-lookup"><span data-stu-id="93a4a-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="93a4a-108">We kunnen dit met Azure RemoteApp bewerkstelligen door Office 365 te hosten op schaalbare virtuele machines in Azure, waarmee gebruikers verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="93a4a-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="93a4a-109">Deze set van virtuele machines noemen we een 'cloudverzameling'.</span><span class="sxs-lookup"><span data-stu-id="93a4a-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="93a4a-110">Een cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="93a4a-110">Create a cloud collection</span></span>
<span data-ttu-id="93a4a-111">Eerst nadat u een Azure-account hebt gemaakt, gaat u te**RemoteApp** door te klikken op Hallo-koppeling op Hallo linkerkant.</span><span class="sxs-lookup"><span data-stu-id="93a4a-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="93a4a-112">![Azure RemoteApp wordt weergegeven op Hallo Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="93a4a-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="93a4a-113">Ga verder door te klikken op **nieuwe** op Hallo onder en 'snel maken' een verzameling.</span><span class="sxs-lookup"><span data-stu-id="93a4a-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="93a4a-114">Geef een naam, Hallo regio, Hallo abonnement, Hallo-plan en Hallo installatiekopie 'Office Proffesional 2013' die wij verstrekken.</span><span class="sxs-lookup"><span data-stu-id="93a4a-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="93a4a-115">![Dialoogvenster Maken](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="93a4a-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="93a4a-116">Hallo formulier Hallo verzameling maken van het proces moet worden gestart wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="93a4a-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="93a4a-117">Dit kan tooan uur duren.</span><span class="sxs-lookup"><span data-stu-id="93a4a-117">This may take up tooan hour or so.</span></span>

![Wachten](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="93a4a-119">Zodra het Hallo-proces is voltooid, er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="93a4a-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="93a4a-120">Als u op **Publiceren** klikt, ziet u dat de meeste Office-toepassingen al zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="93a4a-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="93a4a-121">![Verzameling gemaakt](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="93a4a-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Gepubliceerde apps](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="93a4a-123">Op dit moment kunt u ook meer gebruikers die toegang toothis verzameling hebben door te klikken op toevoegen **gebruikerstoegang**.</span><span class="sxs-lookup"><span data-stu-id="93a4a-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="93a4a-124">![Gebruikerstoegang configureren](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="93a4a-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="93a4a-125">Nu gaan we proberen verbinding te maken tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="93a4a-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="93a4a-126">Verbinding maken met tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="93a4a-126">Connect tooOffice 365</span></span>
<span data-ttu-id="93a4a-127">We je head via te[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), schuif naar beneden en klik op **clients downloaden** tooinstall hello Azure RemoteApp-client op Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="93a4a-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="93a4a-128">Hallo onderstaande schermafbeeldingen zijn voor Windows.</span><span class="sxs-lookup"><span data-stu-id="93a4a-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="93a4a-129">Zodra de toepassing hello Start wordt u gevraagd toosign met uw Microsoft-account (voorheen een 'Live-ID'), gebruik Hallo dezelfde die uw Azure-account nu.</span><span class="sxs-lookup"><span data-stu-id="93a4a-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="93a4a-130">Wanneer u bent aangemeld, ziet u een melding over nieuwe uitnodigingen. Klik op de melding, waarna een lijst zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="93a4a-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="93a4a-131">Hallo-uitnodiging die overeenkomt met uw e-mailadres Azure-account eigenaar accepteren.</span><span class="sxs-lookup"><span data-stu-id="93a4a-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Nieuwe uitnodiging](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="93a4a-133">Zo ziet het eruit wanneer er nieuwe uitnodigingen zijn.</span><span class="sxs-lookup"><span data-stu-id="93a4a-133">What it looks like when there are new invitations.</span></span>

![Een toepassing accepteren](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="93a4a-135">U ziet alle Hallo Office-apps in Azure RemoteApp-client Hallo zodra u Hallo uitnodiging accepteren.</span><span class="sxs-lookup"><span data-stu-id="93a4a-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Lijst met apps](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="93a4a-137">Wanneer u klikt op een van deze toepassing hello moeten worden gestart op Hallo virtuele machine van Azure en u moet alle!</span><span class="sxs-lookup"><span data-stu-id="93a4a-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="93a4a-138">Veel plezier!</span><span class="sxs-lookup"><span data-stu-id="93a4a-138">Enjoy!</span></span>

![starten](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

