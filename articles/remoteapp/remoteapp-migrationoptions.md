---
title: aaaOptions voor het migreren van buiten het Azure RemoteApp | Microsoft Docs
description: Meer informatie over het Hallo-opties voor het migreren van buiten het Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="ee0a6-103">Opties voor het migreren van buiten het Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ee0a6-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee0a6-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ee0a6-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="ee0a6-106">Als u met Azure RemoteApp vanwege Hallo hebt gestopt [buiten gebruik stellen aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) of omdat u de evaluatie hebt voltooid, moet u toomigrate afmeldt bij Azure RemoteApp tooanother-app service.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="ee0a6-107">Er zijn twee verschillende manieren voor het migreren van: een zelfbeheerde (vaak infrastructuur als een Service [IaaS] genoemd)-implementatie of een volledig beheerde (vaak genoemd Platform als een Service) of Software als een Service [PaaS/SaaS] aanbieden.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="ee0a6-108">Selfservice IaaS is een doe implementatie die wordt beheerd, beheerd en die eigendom zijn van door u rechtstreeks worden geïmplementeerd op virtuele machines (VM's) of fysieke systemen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="ee0a6-109">Bij andere Hallo beëindigen, een volledig beheerde PaaS/SaaS aanbieding is vergelijkbaar met een Azure RemoteApp - een partner biedt een servicelaag bovenop een oplossing voor externe toegang die verantwoordelijk is voor operationele en onderhoud terwijl u, als klant hello, gaat u sommige installatiekopie en app-beheer.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="ee0a6-110">[Hello Azure RemoteApp webinars bekijken op migratiemogelijkheden](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), of lees verder voor meer informatie (inclusief voorbeelden van andere opties host Hallo).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="ee0a6-111">Zelfbeheerde (IaaS) oplossingen</span><span class="sxs-lookup"><span data-stu-id="ee0a6-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="ee0a6-112">**RDS op IaaS**</span><span class="sxs-lookup"><span data-stu-id="ee0a6-112">**RDS on IaaS**</span></span>
<span data-ttu-id="ee0a6-113">U kunt een eigen sessie implementatie op basis van extern bureaublad-Services (in Windows Server) met RemoteApp of bureaubladen on-premises of in een gehoste omgeving (like op Azure Virtual machines).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="ee0a6-114">RDS op IaaS-implementaties zijn het meest geschikt is voor klanten die bekend zijn met en waarvoor de bestaande technische kennis met RDS-implementaties.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee0a6-115">Moet u Volume Licensing met Software Assurance (SA) voor RDS-client access-licenties toouse deze Implementatieoptie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="ee0a6-116">Implementeren van RDS op Azure Virtual machines is eenvoudiger dan ooit wanneer u implementatie gebruiken en patchen sjablonen (lezen een [overzicht](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) en vervolgens [gaat u ze](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="ee0a6-117">U kunt Hallo dezelfde elastisch schalen mogelijkheden met Azure classic deployment model resources (geen Azure-Resourcemodel bronnen) in Azure RemoteApp ophalen met behulp van Hallo [automatisch schalen script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), hoewel er meer zijn aanpassingen en configuraties.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="ee0a6-118">Wanneer u RDS op Azure Virtual machines implementeert, ondersteuning is beschikbaar via [ondersteuning van Azure](https://azure.microsoft.com/support/plans/), Hallo dezelfde ondersteuningsmedewerkers die u met Azure RemoteApp wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="ee0a6-119">U maakt een schatting op basis van het gebruik van uw bestaande contact opnemen met de ophalen kost [ondersteuning van Azure](https://azure.microsoft.com/support/plans/), of u kunt berekeningen zelf uitvoeren met behulp van een snel toobe kosten Rekenmachine uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="ee0a6-120">Met N-serie VMs (momenteel in een afgeschermd voorbeeld) kunt u ook vGPU - toevoegen meer over het toevoegen van vGPU en het te horen[benutten RDS-verbeteringen in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in onze Ignite-sessie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="ee0a6-121">We hebben stapsgewijze implementatiehandleidingen voor [Windows Server 2012 R2](http://aka.ms/rdsonazure) en [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist met uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="ee0a6-122">Bekijk Hallo [extern bureaublad-blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) voor het laatste nieuws Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="ee0a6-123">**Citrix op IaaS**</span><span class="sxs-lookup"><span data-stu-id="ee0a6-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="ee0a6-124">Een systeemeigen Citrix implementatie van op sessies gebaseerde XenApp of XenDesktop kan worden geïmplementeerd op lokale of binnen een gehoste omgeving (zoals op Azure Virtual machines).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="ee0a6-125">Stapsgewijze implementatie-handleiding Hallo, Bekijk [Citrix XA 7.6 op Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="ee0a6-126">Lees meer over [Citrix op Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), met inbegrip van een rekenmachine prijs.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="ee0a6-127">U vindt ook een [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss uw opties met.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="ee0a6-128">Volledig beheerd (PaaS/SaaS)-aanbiedingen</span><span class="sxs-lookup"><span data-stu-id="ee0a6-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="ee0a6-129">Citrix XenApp Essentials (uitgebracht April 2017)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="ee0a6-130">Nu beschikbaar op Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is Hallo nieuwe application virtualization-service, Hallo power combineren en flexibiliteit van Hallo Citrix cloudplatform met een eenvoudig hello, prescriptieve, en eenvoudig te gebruiken visie van Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="ee0a6-131">Bestaande Azure RemoteApp-klanten kunnen [registreren voor een gratis proefversie](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="ee0a6-132">Opmerking: Alleen Citrix service gebruiksrecht is gratis, Azure kosten voor berekeningen en opslag van toepassing</span><span class="sxs-lookup"><span data-stu-id="ee0a6-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="ee0a6-133">Meer informatie:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-133">Learn More:</span></span>
- [<span data-ttu-id="ee0a6-134">Migreren van Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="ee0a6-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="ee0a6-135">Citrix en Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee0a6-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="ee0a6-136">[Citrix XenApp Essentials presentatie](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="ee0a6-137">Citrix-Cloudservice XenApp en XenDesktop Service</span><span class="sxs-lookup"><span data-stu-id="ee0a6-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="ee0a6-138">[Citrix-Cloudservice XenApp en XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) Hallo beste oplossing voor de levering van Hallo van zowel apps en desktops, plus Geavanceerd beheer en bewakingsmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="ee0a6-139">Conexlink (de naam van het Platform: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="ee0a6-140">[MyCloudIT](https://mycloudit.com) is een automatiseringsplatform voor IT-bedrijven toosimplify, te optimaliseren en Hallo migratie schalen en levering van externe bureaubladen, externe toepassingen en infrastructuur in Microsoft Azure Cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="ee0a6-141">Hallo MyCloudIT platform implementatietijd minder met 95%, Azure kosten per 30%, en de gehele IT-infrastructuur van de client is verplaatst naar de cloud binnen een paar enkele toetsaanslagen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="ee0a6-142">Partners kunnen klanten nu beheren vanuit één globale dashboard, service-eindgebruikers Hallo wereld zoals nooit tevoren en inkomsten te vergroten zonder extra overhead of uitgebreide Azure training toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="ee0a6-143">Primaire locatie: Dallas, TX, VS</span><span class="sxs-lookup"><span data-stu-id="ee0a6-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="ee0a6-144">Bewerkingsregio: overal ter wereld</span><span class="sxs-lookup"><span data-stu-id="ee0a6-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="ee0a6-145">Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="ee0a6-146">Microsoft Cloud-serviceprovider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-147">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-148">Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="ee0a6-149">Brian Garoutte, Onderdirecteur Business Development</span><span class="sxs-lookup"><span data-stu-id="ee0a6-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="ee0a6-150">Telefoon: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="ee0a6-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="ee0a6-151">E-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="ee0a6-152">Frame</span><span class="sxs-lookup"><span data-stu-id="ee0a6-152">Frame</span></span>

<span data-ttu-id="ee0a6-153">IT-organisaties in enterprise en government, beheerde serviceproviders en toonaangevende leveranciers Kies Frame toocreate en hun beveiligde, door software gedefinieerde werkruimten in de cloud Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="ee0a6-154">Van kleine toolarge organisaties, Frame maakt het zeer eenvoudig toolet gebruikers toegang krijgen tot Windows-toepassingen in elke browser vanaf elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="ee0a6-155">Hello Frame platform alles bevat een beheerder moet toodeploy toepassingen vanuit Hallo cloud met inbegrip van hello Azure-infrastructuur en RDS-licenties (uw eigen Azure-account en de licenties te brengen is optioneel).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="ee0a6-156">Meer informatie over [Frame op Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="ee0a6-157">Primaire locatie: San Mateo, CA, VS</span><span class="sxs-lookup"><span data-stu-id="ee0a6-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="ee0a6-158">Bewerkingsregio: overal ter wereld</span><span class="sxs-lookup"><span data-stu-id="ee0a6-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="ee0a6-159">Microsoft-Partner: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-160">Telefoon: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="ee0a6-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="ee0a6-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="ee0a6-161">Awingu</span></span>
<span data-ttu-id="ee0a6-162">Awingu biedt een eenvoudige online werkruimte-oplossing oudere apps, SaaS en documenten worden uitgevoerd vanuit een browser html5.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="ee0a6-163">Als zodanig toepassingen veilig beschikbaar maken op elk type apparaat.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="ee0a6-164">Voor SaaS-services is een breed scala op eenmalige aanmelding opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="ee0a6-165">Diverse (cloud) bestandssystemen kunnen ook nauw geïntegreerd in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="ee0a6-166">Volgende toofull-mobiliteit van Awingu uitgebreide online werkruimte, optimale beveiliging met gedetailleerde besturingselementen (bijvoorbeeld downloaden/uploadt), volledig gebruik van multi-factor Authentication (bijvoorbeeld Azure MFA), het opnemen van de sessie en meer controle krijgt.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="ee0a6-167">Out-of-the-box, Awingu kunnen documenten en delen van applicaties sessie voor geoptimaliseerde en beveiligde samenwerking.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="ee0a6-168">De Awingu oplossing is multitenant, meerdere AD en open API.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="ee0a6-169">Deze wordt gebruikt door zowel grote als kleine bedrijven, Cloudserviceproviders en [ISV's](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="ee0a6-170">Deze klanten waarderen vooral Hallo eenvoudig te gebruiken, eenvoudig te installeren en lage totale Eigendomskosten.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="ee0a6-171">Awingu alles in-één is [beschikbaar zijn in Azure Marketplace Hallo](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) met 2 ingebouwde gelijktijdige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="ee0a6-172">Aanvullende licenties zijn beschikbaar via een [breed scala aan distributeurs en resellers](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="ee0a6-173">Meer informatie over [Awingu op als alternatieve tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="ee0a6-174">Primaire locatie: België</span><span class="sxs-lookup"><span data-stu-id="ee0a6-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="ee0a6-175">Operationele gebieden: EMEA, Noord-Amerika en Brazilië</span><span class="sxs-lookup"><span data-stu-id="ee0a6-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="ee0a6-176">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="ee0a6-177">**Globale**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-177">**Global**:</span></span>
> 
> <span data-ttu-id="ee0a6-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="ee0a6-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="ee0a6-179">E-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="ee0a6-180">Telefoon: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="ee0a6-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="ee0a6-181">**België hoofdkantoor**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="ee0a6-182">B44 808 Ottergemsesteenweg-Zuid</span><span class="sxs-lookup"><span data-stu-id="ee0a6-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="ee0a6-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="ee0a6-183">9000 Gent</span></span>
> 
> <span data-ttu-id="ee0a6-184">E-mail:[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="ee0a6-185">Telefoon: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="ee0a6-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="ee0a6-186">**VERENIGDE STATEN**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-186">**USA**:</span></span>
> 
> <span data-ttu-id="ee0a6-187">7 floor, Ave voor 1177 Hallo Americas,</span><span class="sxs-lookup"><span data-stu-id="ee0a6-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="ee0a6-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="ee0a6-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="ee0a6-189">E-mail:[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="ee0a6-190">Microsoft gehoste serviceprovider</span><span class="sxs-lookup"><span data-stu-id="ee0a6-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="ee0a6-191">Hosting partners bieden doorgaans een volledig beheerde, gehoste Windows-bureaublad en helpdesk Hallo partner met de licentieovereenkomsten met Microsoft application service, waaronder het beheer van hello Azure-resources, besturingssystemen, toepassingen en andere software-providers samen met een licentieovereenkomst voor serviceproviders tooallow directe verkoop van abonnee Access License (SAL) wordt.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="ee0a6-192">Hallo bevat volgende informatie details en informatie over het verkrijgen van een aantal Hallo hosters die zijn gespecialiseerd in het ondersteunen van klanten met hun Azure RemoteApp-migratie.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="ee0a6-193">Bekijk [Hallo huidige lijst met serviceproviders gehost](http://aka.ms/rdsonazurecertified) die Hallo RDS op IaaS learning pad en de evaluatie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="ee0a6-194">Citrix-Service Provider-programma</span><span class="sxs-lookup"><span data-stu-id="ee0a6-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="ee0a6-195">Hallo programma voor Service Provider Citrix eenvoudig serviceproviders toodeliver Hallo eenvoud van virtuele cloud computing tooSMBs, het aanbieden van Hallo-services die ze in een model eenvoudig, betalen naar gebruik willen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="ee0a6-196">Citrix-serviceproviders groeien hun Microsoft SPLA-bedrijven en hun RDS platform investeringen uitbreiden met een apparaat, overal toegang, Hallo breedste ondersteuning voor toepassingen, een rijke ervaring, extra beveiliging en verbeterde schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="ee0a6-197">Op zijn beurt Citrix serviceproviders meer abonnees trekken, de klanttevredenheid verhogen en de operationele kosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="ee0a6-198">[Meer informatie](http://www.citrix.com/products/service-providers.html) of [vinden van een partner](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="ee0a6-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="ee0a6-199">Acuutech</span></span>
<span data-ttu-id="ee0a6-200">[Acuutech](http://www.acuutech.com) gespecialiseerd in het bieden van gehoste bureaublad oplossingen volledig bureaublad en ISV-toepassingen te bezorgen ervaringen gebouwd op Microsoft-technologie tooa globale client base van Azure en hun eigen datacenters.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="ee0a6-201">Primaire locatie: Londen, UK; Singapore; Houston, TX</span><span class="sxs-lookup"><span data-stu-id="ee0a6-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="ee0a6-202">Bewerkingsregio: overal ter wereld</span><span class="sxs-lookup"><span data-stu-id="ee0a6-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="ee0a6-203">Status partner: Gold</span><span class="sxs-lookup"><span data-stu-id="ee0a6-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="ee0a6-204">Microsoft Cloud-serviceprovider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-205">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-206">Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="ee0a6-207">**Verenigd Koninkrijk**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="ee0a6-208">5/6 York House, Langston weg,</span><span class="sxs-lookup"><span data-stu-id="ee0a6-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="ee0a6-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="ee0a6-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="ee0a6-210">Telefoon: + 44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="ee0a6-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="ee0a6-211">**Singapore**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="ee0a6-212">100 Cecil straat, #09-02</span><span class="sxs-lookup"><span data-stu-id="ee0a6-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="ee0a6-213">Hallo wereld, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="ee0a6-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="ee0a6-214">Telefoon: + 65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="ee0a6-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="ee0a6-215">**Noord-Amerika**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-215">**North America**:</span></span>
>   
> <span data-ttu-id="ee0a6-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="ee0a6-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="ee0a6-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="ee0a6-218">Telefoon: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="ee0a6-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="ee0a6-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="ee0a6-219">ASPEX</span></span>
<span data-ttu-id="ee0a6-220">[ASPEX](http://www.aspex.be/en) gespecialiseerd in ISV's in een overgang toohello Cloud en ISV' opzoeken toooptimize hun huidige instellingen van de cloud.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="ee0a6-221">ASPEX biedt een breed scala aan beheerde services, devops en advies.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="ee0a6-222">Primaire locatie: Antwerpen, België</span><span class="sxs-lookup"><span data-stu-id="ee0a6-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="ee0a6-223">Bewerkingsregio: West-Europa</span><span class="sxs-lookup"><span data-stu-id="ee0a6-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="ee0a6-224">Status partner: [zilver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="ee0a6-225">Microsoft Cloud-serviceprovider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-226">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-227">Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="ee0a6-228">Telefoon: +3232202198</span><span class="sxs-lookup"><span data-stu-id="ee0a6-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="ee0a6-229">E-mail:[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="ee0a6-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="ee0a6-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="ee0a6-231">Caase.com</span></span>
<span data-ttu-id="ee0a6-232">[Caase.com](http://www.caase.com/) helpt bedrijven, lokale overheid, niet-overheidsorganisaties en gezondheidszorg instellingen met hun reis naar een betere manier van werk in Hallo Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="ee0a6-233">Een productiever en veiliger op welke plaats, met een apparaat en lage IT-kosten.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="ee0a6-234">Caase.com is een waar gespecialiseerde voor Microsoft Office365, Azure, Enterprise Mobility en Security en Windows.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="ee0a6-235">Maakt een geoptimaliseerde en veilig platform voor samenwerking voor zowel klanten werknemers, partners en leveranciers met onze advies, migratieservices, acceptatie programma's, training, beheer en ondersteuning Caase.com.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="ee0a6-236">Caase.com is Hallo mastermind van Hallo externe Azure-werkruimte (mobiele werkplek) en Hallo digitale werkplek (sociale Intranet).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="ee0a6-237">Beide oplossingen – bewerkstelligd met acceptatie – zijn Hallo foundation die zorgt ervoor dat gebruikers van deze oplossingen Hallo Hallo meest prettig, geslaagd en effectieve ervaring in hun route toohello Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="ee0a6-238">De vertaling van Nederlandse ánd een ondersteunende film hier: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="ee0a6-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="ee0a6-239">Bewerkingsregio: Nederlands gebaseerd, wereldwijde bereik</span><span class="sxs-lookup"><span data-stu-id="ee0a6-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="ee0a6-240">Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="ee0a6-241">Microsoft Cloud-serviceprovider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-242">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-243">Azure RemoteApp-oplossingen voor migratie: Ja, [meer](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="ee0a6-244">Nederland:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-244">Netherlands:</span></span>
> 
> <span data-ttu-id="ee0a6-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="ee0a6-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="ee0a6-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="ee0a6-247">Telefoon: EnterIT + 31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="ee0a6-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="ee0a6-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="ee0a6-248">Nerdio</span></span>
<span data-ttu-id="ee0a6-249">[Nerdio voor Azure](http://getnerdio.com/nfa/) is een automatiseringsplatform IT die heel eenvoudig inrichten, management en optimalisatie van de volledige IT-omgevingen in Hallo Microsoft cloud biedt.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="ee0a6-250">Onafhankelijk van de virtuele bureaubladen, externe apps en -servers in een paar uur.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="ee0a6-251">Hallo-omgeving in drie klikken beheren of minder met Nerdio-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="ee0a6-252">Gebruik intelligent automatisch schalen en 40% voor too60 opslaan in Azure IaaS-middelen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="ee0a6-253">Primaire locatie: Chicago, zh-bewerkingsregio: status wereldwijd Partner: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-254">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-255">Azure RemoteApp-oplossingen voor migratie: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="ee0a6-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="ee0a6-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="ee0a6-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="ee0a6-257">Suite 212</span></span>
> 
> <span data-ttu-id="ee0a6-258">Skokie IL 60077</span><span class="sxs-lookup"><span data-stu-id="ee0a6-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="ee0a6-259">USA</span><span class="sxs-lookup"><span data-stu-id="ee0a6-259">USA</span></span>
> 
> <span data-ttu-id="ee0a6-260">(844) 4NERDIO toest. 6</span><span class="sxs-lookup"><span data-stu-id="ee0a6-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="ee0a6-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="ee0a6-261">**SaaSplaza**</span></span>
<span data-ttu-id="ee0a6-262">[SaaSplaza](http://www.saasplaza.com/) biedt volledig Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) persoonlijke en openbare cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="ee0a6-263">Primaire locatie: Nederland</span><span class="sxs-lookup"><span data-stu-id="ee0a6-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="ee0a6-264">Bewerkingsregio: overal ter wereld</span><span class="sxs-lookup"><span data-stu-id="ee0a6-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="ee0a6-265">Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="ee0a6-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="ee0a6-266">Microsoft Cloud-serviceprovider: Ja</span><span class="sxs-lookup"><span data-stu-id="ee0a6-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="ee0a6-267">RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide</span><span class="sxs-lookup"><span data-stu-id="ee0a6-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="ee0a6-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="ee0a6-269">Prins Mauritslaan 29 35</span><span class="sxs-lookup"><span data-stu-id="ee0a6-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="ee0a6-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="ee0a6-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="ee0a6-271">Hallo Nederland</span><span class="sxs-lookup"><span data-stu-id="ee0a6-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="ee0a6-272">Telefoon: EnterIT + 31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="ee0a6-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="ee0a6-273">**Americas**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-273">**Americas**:</span></span>
> 
> <span data-ttu-id="ee0a6-274">171 Saxony weg, Suite 105</span><span class="sxs-lookup"><span data-stu-id="ee0a6-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="ee0a6-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="ee0a6-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="ee0a6-276">Gouda</span><span class="sxs-lookup"><span data-stu-id="ee0a6-276">San Diego</span></span>
> 
> <span data-ttu-id="ee0a6-277">Verenigde Staten</span><span class="sxs-lookup"><span data-stu-id="ee0a6-277">United States</span></span>
> 
> <span data-ttu-id="ee0a6-278">Telefoon: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="ee0a6-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="ee0a6-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="ee0a6-279">**APAC**:</span></span>
> 
> <span data-ttu-id="ee0a6-280">105 Cecil straat</span><span class="sxs-lookup"><span data-stu-id="ee0a6-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="ee0a6-281">\#11-08 Hallo achthoek</span><span class="sxs-lookup"><span data-stu-id="ee0a6-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="ee0a6-282">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="ee0a6-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="ee0a6-283">Singapore</span><span class="sxs-lookup"><span data-stu-id="ee0a6-283">Singapore</span></span>
>   
> <span data-ttu-id="ee0a6-284">Telefoon - Singapore: + 65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="ee0a6-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="ee0a6-285">Telefoon - Australië: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="ee0a6-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="ee0a6-286">Telefoon - Nieuw-Zeeland: + 64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="ee0a6-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="ee0a6-287">Meer hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="ee0a6-287">Need more help?</span></span>
<span data-ttu-id="ee0a6-288">Nog steeds moeten helpen kiezen of meer vragen hebt?</span><span class="sxs-lookup"><span data-stu-id="ee0a6-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="ee0a6-289">Gebruik een van de volgende methoden tooget help Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="ee0a6-290">Een e-mail sturen naar [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="ee0a6-291">Neem contact op met [ondersteuning van Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="ee0a6-292">Start via een [Azure ondersteuningsaanvraag](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="ee0a6-293">Ons te bellen.</span><span class="sxs-lookup"><span data-stu-id="ee0a6-293">Call us.</span></span> <span data-ttu-id="ee0a6-294">[Zoeken naar een lokaal verkoop nummer](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="ee0a6-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

