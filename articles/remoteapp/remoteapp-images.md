---
title: "Wat bevatten de sjablooninstallatiekopieën van Azure RemoteApp? | Microsoft Docs"
description: "Meer informatie over de inhoud van de sjablooninstallatiekopieën die worden geleverd bij Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="a2680-104">Wat bevatten de sjablooninstallatiekopieën van Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="a2680-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a2680-105">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="a2680-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a2680-106">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a2680-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a2680-107">Uw abonnement op Azure RemoteApp omvat drie sjablooninstallatiekopieën:</span><span class="sxs-lookup"><span data-stu-id="a2680-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="a2680-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a2680-108">Windows Server 2012</span></span>
* <span data-ttu-id="a2680-109">Microsoft Office 365 ProPlus (abonnement op Office 365 vereist)</span><span class="sxs-lookup"><span data-stu-id="a2680-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="a2680-110">Microsoft Office 2013 Professional Plus (alleen proefversie)</span><span class="sxs-lookup"><span data-stu-id="a2680-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2680-111">Uw Azure RemoteApp-abonnement biedt u toegang tot de software in de installatiekopieën, met uitzondering van Office 365 ProPlus, waarvoor een afzonderlijk abonnement is vereist, en Office 2013, dat niet kan worden gebruikt in productie.</span><span class="sxs-lookup"><span data-stu-id="a2680-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="a2680-112">Dit betekent dat u de programma's of toepassingen op de sjablooninstallatiekopieën met uw gebruikers kunt delen.</span><span class="sxs-lookup"><span data-stu-id="a2680-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="a2680-113">Als u bijvoorbeeld een verzameling maakt waarin de installatiekopie voor Windows Server 2012 R2 wordt gebruikt, kunt u System Center Endpoint Protection voor gebruikers publiceren zodat gebruikers hiertoe toegang hebben via RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a2680-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="a2680-114">Bekijk de [Informatie over RemoteApp-licenties](remoteapp-licensing.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a2680-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="a2680-115">En in [Office gebruiken met Azure RemoteApp](remoteapp-o365.md) kunt u informatie vinden over Office-licenties.</span><span class="sxs-lookup"><span data-stu-id="a2680-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="a2680-116">Lees verder voor meer informatie over de inhoud van elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a2680-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="a2680-117">Windows Server 2012 R2 ('de vanilla-installatiekopie')</span><span class="sxs-lookup"><span data-stu-id="a2680-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="a2680-118">Deze installatiekopie is gebaseerd op het besturingssysteem Microsoft Windows Server 2012 R2 Datacenter en bevat de volgende rollen en functies om te voldoen aan de vereisten voor Azure RemoteApp-sjablooninstallatiekopieën:</span><span class="sxs-lookup"><span data-stu-id="a2680-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="a2680-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="a2680-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="a2680-120">Bureaubladbelevenis</span><span class="sxs-lookup"><span data-stu-id="a2680-120">Desktop Experience</span></span>
* <span data-ttu-id="a2680-121">Inkt- en handschriftservices</span><span class="sxs-lookup"><span data-stu-id="a2680-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="a2680-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="a2680-122">Media Foundation</span></span>
* <span data-ttu-id="a2680-123">Extern bureaublad-sessiehost</span><span class="sxs-lookup"><span data-stu-id="a2680-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="a2680-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="a2680-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="a2680-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="a2680-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="a2680-126">WoW64-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="a2680-126">WoW64 Support</span></span>

<span data-ttu-id="a2680-127">In deze installatiekopie zijn ook de volgende toepassingen geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="a2680-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="a2680-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="a2680-128">Adobe Flash Player</span></span>
* <span data-ttu-id="a2680-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="a2680-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="a2680-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="a2680-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="a2680-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="a2680-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="a2680-132">Microsoft Office 365 ProPlus (abonnement vereist)</span><span class="sxs-lookup"><span data-stu-id="a2680-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="a2680-133">Office 365 is de meest aangevraagde toepassing en om deze reden hebben we een 'aangepaste' installatiekopie voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a2680-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="a2680-134">Deze installatiekopie is een uitbreiding op de vanilla-installatiekopie en bevat de volgende onderdelen van Microsoft Office 365 ProPlus, naast de onderdelen die worden beschreven in de installatiekopie van Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="a2680-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="a2680-135">Toegang</span><span class="sxs-lookup"><span data-stu-id="a2680-135">Access</span></span>
* <span data-ttu-id="a2680-136">Excel</span><span class="sxs-lookup"><span data-stu-id="a2680-136">Excel</span></span>
* <span data-ttu-id="a2680-137">Lync</span><span class="sxs-lookup"><span data-stu-id="a2680-137">Lync</span></span>
* <span data-ttu-id="a2680-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="a2680-138">OneNote</span></span>
* <span data-ttu-id="a2680-139">OneDrive voor Bedrijven (de synchronisatie-agent wordt niet ondersteund voor gebruik met Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="a2680-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="a2680-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="a2680-140">Outlook</span></span>
* <span data-ttu-id="a2680-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="a2680-141">PowerPoint</span></span>
* <span data-ttu-id="a2680-142">Word</span><span class="sxs-lookup"><span data-stu-id="a2680-142">Word</span></span>
* <span data-ttu-id="a2680-143">Microsoft Office-taalprogramma's</span><span class="sxs-lookup"><span data-stu-id="a2680-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="a2680-144">De installatiekopie bevat ook Visio Pro en Project Pro.</span><span class="sxs-lookup"><span data-stu-id="a2680-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="a2680-145">Plus de volgende toepassingen:</span><span class="sxs-lookup"><span data-stu-id="a2680-145">And the following applications, as well:</span></span>

* <span data-ttu-id="a2680-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="a2680-146">SQL Native client</span></span>
* <span data-ttu-id="a2680-147">ODBC-stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="a2680-147">ODBC Driver</span></span>
* <span data-ttu-id="a2680-148">SQL Server Data Mining Client</span><span class="sxs-lookup"><span data-stu-id="a2680-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="a2680-149">MasterDataServices Client</span><span class="sxs-lookup"><span data-stu-id="a2680-149">MasterDataServices client</span></span>
* <span data-ttu-id="a2680-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="a2680-150">Microsoft Publisher</span></span>
* <span data-ttu-id="a2680-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="a2680-151">PowerQuery</span></span>
* <span data-ttu-id="a2680-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="a2680-152">PowerMap</span></span>

<span data-ttu-id="a2680-153">Volledige functionaliteit van Office 365 ProPlus-apps is alleen beschikbaar voor gebruikers met een Office 365 ProPlus-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2680-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="a2680-154">Zie [Service-abonnementen voor Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx) voor meer informatie over Office 365-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a2680-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="a2680-155">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="a2680-155">Still have questions?</span></span> <span data-ttu-id="a2680-156">Bekijk de [Office 365 + RemoteApp](remoteapp-o365.md)-informatie.</span><span class="sxs-lookup"><span data-stu-id="a2680-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="a2680-157">Lees ook het nieuwe artikel [Uw Office 365-abonnement gebruiken met Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="a2680-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="a2680-158">Houd er rekening mee dat u een aparte licentie nodig hebt voor Office 365 ProPlus Visio Pro en Project Pro (deze hebben elk een eigen licentie).</span><span class="sxs-lookup"><span data-stu-id="a2680-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="a2680-159">Microsoft Office 2013 Professional Plus (alleen proefversie)</span><span class="sxs-lookup"><span data-stu-id="a2680-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="a2680-160">U kunt de service met de installatiekopie van het Office 2013 testen gedurende de gratis proefperiode.</span><span class="sxs-lookup"><span data-stu-id="a2680-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="a2680-161">Deze installatiekopie is een uitbreiding op de vanilla-installatiekopie en bevat de volgende onderdelen van Microsoft Office 2013 Professional Plus, naast de onderdelen die worden beschreven in de installatiekopie van Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="a2680-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="a2680-162">Access</span><span class="sxs-lookup"><span data-stu-id="a2680-162">Access</span></span>
* <span data-ttu-id="a2680-163">Excel</span><span class="sxs-lookup"><span data-stu-id="a2680-163">Excel</span></span>
* <span data-ttu-id="a2680-164">Lync</span><span class="sxs-lookup"><span data-stu-id="a2680-164">Lync</span></span>
* <span data-ttu-id="a2680-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="a2680-165">OneNote</span></span>
* <span data-ttu-id="a2680-166">OneDrive voor Bedrijven (de synchronisatie-agent wordt niet ondersteund voor gebruik met Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="a2680-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="a2680-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="a2680-167">Outlook</span></span>
* <span data-ttu-id="a2680-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="a2680-168">PowerPoint</span></span>
* <span data-ttu-id="a2680-169">Project</span><span class="sxs-lookup"><span data-stu-id="a2680-169">Project</span></span>
* <span data-ttu-id="a2680-170">Visio</span><span class="sxs-lookup"><span data-stu-id="a2680-170">Visio</span></span>
* <span data-ttu-id="a2680-171">Word</span><span class="sxs-lookup"><span data-stu-id="a2680-171">Word</span></span>
* <span data-ttu-id="a2680-172">Microsoft Office-taalprogramma's</span><span class="sxs-lookup"><span data-stu-id="a2680-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2680-173">**Juridische informatie:** Deze installatiekopie bevat geen licentie voor Microsoft Office en *kan niet worden gebruikt voor productie*.</span><span class="sxs-lookup"><span data-stu-id="a2680-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="a2680-174">De Office 2013 Professional Plus-installatiekopie is alleen bedoeld als proefversie.</span><span class="sxs-lookup"><span data-stu-id="a2680-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="a2680-175">Als u Office-apps in Azure RemoteApp wilt gebruiken voor productie, maak dan gebruik van de Office 365 ProPlus-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a2680-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="a2680-176">Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie over licentieverlening voor Office.</span><span class="sxs-lookup"><span data-stu-id="a2680-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

