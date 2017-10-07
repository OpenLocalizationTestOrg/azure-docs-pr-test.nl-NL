---
title: aaaTroubleshoot Azure RBAC | Microsoft Docs
description: Hulp bij problemen of vragen hebt over op rollen gebaseerd toegangsbeheer resources.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="2aef9-103">Probleemoplossing voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="2aef9-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="2aef9-104">In dit artikel document antwoorden op veelgestelde vragen over Hallo specifieke toegangsrechten die zijn verleend aan rollen, zodat u welke tooexpect weet wanneer met behulp van rollen in Azure-portal Hallo Hallo en toegangsproblemen kunnen oplossen.</span><span class="sxs-lookup"><span data-stu-id="2aef9-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="2aef9-105">Deze drie rollen hebben betrekking op alle brontypen:</span><span class="sxs-lookup"><span data-stu-id="2aef9-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="2aef9-106">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="2aef9-106">Owner</span></span>  
* <span data-ttu-id="2aef9-107">Inzender</span><span class="sxs-lookup"><span data-stu-id="2aef9-107">Contributor</span></span>  
* <span data-ttu-id="2aef9-108">Lezer</span><span class="sxs-lookup"><span data-stu-id="2aef9-108">Reader</span></span>  

<span data-ttu-id="2aef9-109">Eigenaars en medewerkers hebt volledige toegang toohello management ervaring, maar een medewerker kan niet geven toegang tooother gebruikers of groepen.</span><span class="sxs-lookup"><span data-stu-id="2aef9-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="2aef9-110">Dingen krijgt u iets interessanter met de rol Lezer hello, zodat die waar we je besteed voldoende tijd is.</span><span class="sxs-lookup"><span data-stu-id="2aef9-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="2aef9-111">Zie Hallo [toegangsbeheer op basis van rollen get-started artikel](role-based-access-control-configure.md) voor meer informatie over hoe toogrant toegang tot.</span><span class="sxs-lookup"><span data-stu-id="2aef9-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="2aef9-112">App service-werkbelastingen</span><span class="sxs-lookup"><span data-stu-id="2aef9-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="2aef9-113">Toegang voor schrijven-mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="2aef9-113">Write access capabilities</span></span>
<span data-ttu-id="2aef9-114">Als u een gebruiker alleen-lezentoegang tooa één web-app toewijst, worden sommige functies zijn uitgeschakeld dat u niet verwacht.</span><span class="sxs-lookup"><span data-stu-id="2aef9-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="2aef9-115">Hallo na beheermogelijkheden vereisen **schrijven** toegang tot tooa web-app (Inzender of eigenaar) en niet beschikbaar in een scenario met alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="2aef9-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="2aef9-116">Opdrachten (zoals starten, stoppen, enz.)</span><span class="sxs-lookup"><span data-stu-id="2aef9-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="2aef9-117">Wijzigen van de instellingen, zoals algemene configuratie, schaalinstellingen, back-upinstellingen en controle-instellingen</span><span class="sxs-lookup"><span data-stu-id="2aef9-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="2aef9-118">Toegang tot publishing referenties en andere geheime informatie zoals het app-instellingen en verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="2aef9-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="2aef9-119">Streaminglogboeken</span><span class="sxs-lookup"><span data-stu-id="2aef9-119">Streaming logs</span></span>
* <span data-ttu-id="2aef9-120">Configuratie van diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="2aef9-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="2aef9-121">Console (opdrachtprompt)</span><span class="sxs-lookup"><span data-stu-id="2aef9-121">Console (command prompt)</span></span>
* <span data-ttu-id="2aef9-122">Actieve en recente implementaties (voor lokale git-continue implementatie)</span><span class="sxs-lookup"><span data-stu-id="2aef9-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="2aef9-123">Geschatte besteden</span><span class="sxs-lookup"><span data-stu-id="2aef9-123">Estimated spend</span></span>
* <span data-ttu-id="2aef9-124">Webtests</span><span class="sxs-lookup"><span data-stu-id="2aef9-124">Web tests</span></span>
* <span data-ttu-id="2aef9-125">Virtueel netwerk (alleen zichtbaar tooa lezer als eerder een virtueel netwerk is geconfigureerd door een gebruiker met toegang voor schrijven).</span><span class="sxs-lookup"><span data-stu-id="2aef9-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="2aef9-126">Als u geen toegang deze tegels tot, moet u op tooask uw beheerder voor Inzender toegang toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="2aef9-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="2aef9-127">Omgaan met verwante bronnen</span><span class="sxs-lookup"><span data-stu-id="2aef9-127">Dealing with related resources</span></span>
<span data-ttu-id="2aef9-128">Web-apps zijn door Hallo aanwezigheid van een paar verschillende bronnen die wisselwerking ingewikkeld.</span><span class="sxs-lookup"><span data-stu-id="2aef9-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="2aef9-129">Hier volgt een typisch resourcegroep met een paar websites:</span><span class="sxs-lookup"><span data-stu-id="2aef9-129">Here is a typical resource group with a couple websites:</span></span>

![Web-app-resourcegroep](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="2aef9-131">Als gevolg hiervan, als u iemand toegang toojust Hallo web-app verleent, dat veel Hallo-functionaliteit op de websiteblade Hallo in hello Azure-portal is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2aef9-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="2aef9-132">Deze items vereisen **schrijven** toegang tot toohello **App Service-abonnement** die overeenkomt met tooyour website:</span><span class="sxs-lookup"><span data-stu-id="2aef9-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="2aef9-133">Weergave Hallo web-app de prijscategorie (vrije of standaard)</span><span class="sxs-lookup"><span data-stu-id="2aef9-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="2aef9-134">Configuratie van de schaal (aantal exemplaren, de grootte van virtuele machine, de instellingen voor automatisch schalen)</span><span class="sxs-lookup"><span data-stu-id="2aef9-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="2aef9-135">Quota (opslag, bandbreedte, CPU)</span><span class="sxs-lookup"><span data-stu-id="2aef9-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="2aef9-136">Deze items vereisen **schrijven** toegang toohello hele **resourcegroep** die uw website bevat:</span><span class="sxs-lookup"><span data-stu-id="2aef9-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="2aef9-137">SSL-certificaten en bindingen (SSL-certificaten kunnen worden gedeeld tussen sites in Hallo dezelfde resourcegroep en de geografische locatie)</span><span class="sxs-lookup"><span data-stu-id="2aef9-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="2aef9-138">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="2aef9-138">Alert rules</span></span>  
* <span data-ttu-id="2aef9-139">instellingen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="2aef9-139">Autoscale settings</span></span>  
* <span data-ttu-id="2aef9-140">Application insights-onderdelen</span><span class="sxs-lookup"><span data-stu-id="2aef9-140">Application insights components</span></span>  
* <span data-ttu-id="2aef9-141">Webtests</span><span class="sxs-lookup"><span data-stu-id="2aef9-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="2aef9-142">Virtual machine-werkbelasting</span><span class="sxs-lookup"><span data-stu-id="2aef9-142">Virtual machine workloads</span></span>
<span data-ttu-id="2aef9-143">Veel zoals met web-apps, sommige functies op Hallo virtuele machineblade vereisen schrijftoegang toohello virtuele machine of tooother resources in Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2aef9-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="2aef9-144">Virtuele machines zijn verwante tooDomain namen, virtuele netwerken, opslagaccounts en regels voor waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="2aef9-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="2aef9-145">Deze items vereisen **schrijven** toegang tot toohello **virtuele machine**:</span><span class="sxs-lookup"><span data-stu-id="2aef9-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="2aef9-146">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="2aef9-146">Endpoints</span></span>  
* <span data-ttu-id="2aef9-147">IP-adressen</span><span class="sxs-lookup"><span data-stu-id="2aef9-147">IP addresses</span></span>  
* <span data-ttu-id="2aef9-148">Disks</span><span class="sxs-lookup"><span data-stu-id="2aef9-148">Disks</span></span>  
* <span data-ttu-id="2aef9-149">Extensies</span><span class="sxs-lookup"><span data-stu-id="2aef9-149">Extensions</span></span>  

<span data-ttu-id="2aef9-150">Hiervoor is vereist **schrijven** toegang tooboth hello **virtuele machine**, en Hallo **resourcegroep** (samen met de domeinnaam Hallo) dat deze zich in:</span><span class="sxs-lookup"><span data-stu-id="2aef9-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="2aef9-151">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="2aef9-151">Availability set</span></span>  
* <span data-ttu-id="2aef9-152">Laden van de set met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="2aef9-152">Load balanced set</span></span>  
* <span data-ttu-id="2aef9-153">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="2aef9-153">Alert rules</span></span>  

<span data-ttu-id="2aef9-154">Als u geen toegang deze tegels tot, vraag uw beheerder voor Inzender toegang toohello resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2aef9-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="2aef9-155">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="2aef9-155">See more</span></span>
* <span data-ttu-id="2aef9-156">[Op rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2aef9-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="2aef9-157">[Ingebouwde rollen](role-based-access-built-in-roles.md): meer informatie over het Hallo-functies die standaard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="2aef9-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="2aef9-158">[Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md): meer informatie over hoe toocreate aangepaste rollen toofit uw toegang moet.</span><span class="sxs-lookup"><span data-stu-id="2aef9-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="2aef9-159">[Maken van een geschiedenisrapport voor gewijzigde van toegang](role-based-access-control-access-change-history-report.md): bijhouden van wijzigen van roltoewijzingen in RBAC.</span><span class="sxs-lookup"><span data-stu-id="2aef9-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

