---
title: Een app publiceren in Azure RemoteApp | Microsoft Docs
description: Informatie over het publiceren van toepassingen en bronnen in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="eff7b-103">Hoe u een app publiceren in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="eff7b-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eff7b-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="eff7b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="eff7b-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eff7b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="eff7b-106">Nadat u uw RemoteApp-collectie gemaakt, moet u de apps of de resources die u beschikbaar wilt maken voor uw gebruikers publiceren.</span><span class="sxs-lookup"><span data-stu-id="eff7b-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="eff7b-107">De sjablooninstallatiekopieën met uw abonnement opgegeven slechts enkele apps die zijn gepubliceerd - standaard voor het delen van andere apps hebben, moet u ze publiceren.</span><span class="sxs-lookup"><span data-stu-id="eff7b-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="eff7b-108">Moet u een app bijwerken?</span><span class="sxs-lookup"><span data-stu-id="eff7b-108">Do you need to update an app?</span></span> <span data-ttu-id="eff7b-109">U moet [bijwerken van de installatiekopie](remoteapp-update.md) eerste.</span><span class="sxs-lookup"><span data-stu-id="eff7b-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="eff7b-110">Op de **Publishing** in de portal en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="eff7b-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="eff7b-111">Kunt u een app toevoegen van uw sjablooninstallatiekopie **Start** menu of geef het pad naar waar de app is geïnstalleerd op de sjablooninstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="eff7b-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="eff7b-112">Als u wilt toevoegen op basis van de **Start** menu, kies de app te publiceren in de lijst.</span><span class="sxs-lookup"><span data-stu-id="eff7b-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="eff7b-113">Als u ervoor kiest om het pad naar de app, voert u een naam voor de app en het pad naar de app.</span><span class="sxs-lookup"><span data-stu-id="eff7b-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="eff7b-114">Variabelen in het pad - bijvoorbeeld '% systemdrive %' gebruiken in plaats van ' c:\".</span><span class="sxs-lookup"><span data-stu-id="eff7b-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="eff7b-115">Als u wilt toevoegen van uw app uit de **Start** menu, moet u beschikken over *die app toevoegt aan de **Start** menu op uw sjablooninstallatiekopie.*</span><span class="sxs-lookup"><span data-stu-id="eff7b-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="eff7b-116">Anders RemoteApp alleen zien wat *is* op de **Start** menu en u wordt verwarren.</span><span class="sxs-lookup"><span data-stu-id="eff7b-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="eff7b-117">Om te controleren of uw app wordt de **Start** menu, plaatst u het snelkoppelingsbestand - **lnk** - binnen de Menu\Programs %systemdrive%\ProgramData\Microsoft\Windows\Start.</span><span class="sxs-lookup"><span data-stu-id="eff7b-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="eff7b-118">Als u vergeten toe te voegen van de app kan de **Start** menu tijdens het maken van de sjabloon kiest u het pad toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="eff7b-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="eff7b-119">(Of maak deze opnieuw uw sjablooninstallatiekopie, maar dat is erg iets meer werk.)</span><span class="sxs-lookup"><span data-stu-id="eff7b-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

