---
title: Problemen met Azure RBAC | Microsoft Docs
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
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="0acdf-103">Probleemoplossing voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="0acdf-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="0acdf-104">In dit artikel document antwoorden op veelgestelde vragen over de specifieke rechten die zijn verleend aan rollen, zodat u wat u weet kunt verwachten wanneer u de rollen in de Azure-portal en kan toegangsproblemen oplossen.</span><span class="sxs-lookup"><span data-stu-id="0acdf-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="0acdf-105">Deze drie rollen hebben betrekking op alle brontypen:</span><span class="sxs-lookup"><span data-stu-id="0acdf-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="0acdf-106">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="0acdf-106">Owner</span></span>  
* <span data-ttu-id="0acdf-107">Inzender</span><span class="sxs-lookup"><span data-stu-id="0acdf-107">Contributor</span></span>  
* <span data-ttu-id="0acdf-108">Lezer</span><span class="sxs-lookup"><span data-stu-id="0acdf-108">Reader</span></span>  

<span data-ttu-id="0acdf-109">Eigenaars en medewerkers hebt volledige toegang tot de beheerervaring, maar een medewerker kan geen toegang verlenen aan andere gebruikers of groepen.</span><span class="sxs-lookup"><span data-stu-id="0acdf-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="0acdf-110">Dingen ophalen iets interessanter met de lezersrol zodat waar we even uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="0acdf-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="0acdf-111">Zie de [toegangsbeheer op basis van rollen get-started artikel](role-based-access-control-configure.md) voor meer informatie over het om toegang te verlenen.</span><span class="sxs-lookup"><span data-stu-id="0acdf-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="0acdf-112">App service-werkbelastingen</span><span class="sxs-lookup"><span data-stu-id="0acdf-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="0acdf-113">Toegang voor schrijven-mogelijkheden</span><span class="sxs-lookup"><span data-stu-id="0acdf-113">Write access capabilities</span></span>
<span data-ttu-id="0acdf-114">Als u een gebruiker alleen-lezen toegang tot een enkel web-app verlenen, worden sommige functies zijn uitgeschakeld dat u niet verwacht.</span><span class="sxs-lookup"><span data-stu-id="0acdf-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="0acdf-115">De volgende beheermogelijkheden vereisen **schrijven** toegang tot een web-app (Inzender of eigenaar) en niet beschikbaar zijn in een scenario met alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="0acdf-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="0acdf-116">Opdrachten (zoals starten, stoppen, enz.)</span><span class="sxs-lookup"><span data-stu-id="0acdf-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="0acdf-117">Wijzigen van de instellingen, zoals algemene configuratie, schaalinstellingen, back-upinstellingen en controle-instellingen</span><span class="sxs-lookup"><span data-stu-id="0acdf-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="0acdf-118">Toegang tot publishing referenties en andere geheime informatie zoals het app-instellingen en verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="0acdf-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="0acdf-119">Streaminglogboeken</span><span class="sxs-lookup"><span data-stu-id="0acdf-119">Streaming logs</span></span>
* <span data-ttu-id="0acdf-120">Configuratie van diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="0acdf-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="0acdf-121">Console (opdrachtprompt)</span><span class="sxs-lookup"><span data-stu-id="0acdf-121">Console (command prompt)</span></span>
* <span data-ttu-id="0acdf-122">Actieve en recente implementaties (voor lokale git-continue implementatie)</span><span class="sxs-lookup"><span data-stu-id="0acdf-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="0acdf-123">Geschatte besteden</span><span class="sxs-lookup"><span data-stu-id="0acdf-123">Estimated spend</span></span>
* <span data-ttu-id="0acdf-124">Webtests</span><span class="sxs-lookup"><span data-stu-id="0acdf-124">Web tests</span></span>
* <span data-ttu-id="0acdf-125">Virtueel netwerk (alleen zichtbaar voor een lezer als eerder een virtueel netwerk is geconfigureerd door een gebruiker met toegang voor schrijven).</span><span class="sxs-lookup"><span data-stu-id="0acdf-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="0acdf-126">Als u geen toegang deze tegels tot, moet u de systeembeheerder voor Inzender toegang tot de web-app.</span><span class="sxs-lookup"><span data-stu-id="0acdf-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="0acdf-127">Omgaan met verwante bronnen</span><span class="sxs-lookup"><span data-stu-id="0acdf-127">Dealing with related resources</span></span>
<span data-ttu-id="0acdf-128">Web-apps worden door de aanwezigheid van een paar verschillende bronnen die wisselwerking ingewikkeld.</span><span class="sxs-lookup"><span data-stu-id="0acdf-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="0acdf-129">Hier volgt een typisch resourcegroep met een paar websites:</span><span class="sxs-lookup"><span data-stu-id="0acdf-129">Here is a typical resource group with a couple websites:</span></span>

![Web-app-resourcegroep](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="0acdf-131">Als gevolg hiervan, als u iemand toegang tot alleen de web-app veel van de functionaliteit op de websiteblade in de Azure portal is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0acdf-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="0acdf-132">Deze items vereisen **schrijven** toegang tot de **App Service-abonnement** die overeenkomt met uw website:</span><span class="sxs-lookup"><span data-stu-id="0acdf-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="0acdf-133">Weergeven van de web-app de prijscategorie (vrije of standaard)</span><span class="sxs-lookup"><span data-stu-id="0acdf-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="0acdf-134">Configuratie van de schaal (aantal exemplaren, de grootte van virtuele machine, de instellingen voor automatisch schalen)</span><span class="sxs-lookup"><span data-stu-id="0acdf-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="0acdf-135">Quota (opslag, bandbreedte, CPU)</span><span class="sxs-lookup"><span data-stu-id="0acdf-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="0acdf-136">Deze items vereisen **schrijven** toegang tot het gehele **resourcegroep** die uw website bevat:</span><span class="sxs-lookup"><span data-stu-id="0acdf-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="0acdf-137">SSL-certificaten en bindingen (SSL-certificaten kunnen worden gedeeld tussen sites in dezelfde resourcegroep en de geografische locatie)</span><span class="sxs-lookup"><span data-stu-id="0acdf-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="0acdf-138">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="0acdf-138">Alert rules</span></span>  
* <span data-ttu-id="0acdf-139">instellingen voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="0acdf-139">Autoscale settings</span></span>  
* <span data-ttu-id="0acdf-140">Application insights-onderdelen</span><span class="sxs-lookup"><span data-stu-id="0acdf-140">Application insights components</span></span>  
* <span data-ttu-id="0acdf-141">Webtests</span><span class="sxs-lookup"><span data-stu-id="0acdf-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="0acdf-142">Virtual machine-werkbelasting</span><span class="sxs-lookup"><span data-stu-id="0acdf-142">Virtual machine workloads</span></span>
<span data-ttu-id="0acdf-143">Veel zoals met web-apps, sommige functies op de blade van de virtuele machine vereist schrijftoegang op de virtuele machine, of op andere bronnen in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0acdf-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="0acdf-144">Virtuele machines zijn gerelateerd aan het domein namen, virtuele netwerken, opslagaccounts en regels voor waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="0acdf-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="0acdf-145">Deze items vereisen **schrijven** toegang tot de **virtuele machine**:</span><span class="sxs-lookup"><span data-stu-id="0acdf-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="0acdf-146">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="0acdf-146">Endpoints</span></span>  
* <span data-ttu-id="0acdf-147">IP-adressen</span><span class="sxs-lookup"><span data-stu-id="0acdf-147">IP addresses</span></span>  
* <span data-ttu-id="0acdf-148">Disks</span><span class="sxs-lookup"><span data-stu-id="0acdf-148">Disks</span></span>  
* <span data-ttu-id="0acdf-149">Extensies</span><span class="sxs-lookup"><span data-stu-id="0acdf-149">Extensions</span></span>  

<span data-ttu-id="0acdf-150">Hiervoor is vereist **schrijven** toegang tot zowel de **virtuele machine**, en de **resourcegroep** (samen met de domeinnaam) dat deze zich in:</span><span class="sxs-lookup"><span data-stu-id="0acdf-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="0acdf-151">Beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="0acdf-151">Availability set</span></span>  
* <span data-ttu-id="0acdf-152">Laden van de set met gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="0acdf-152">Load balanced set</span></span>  
* <span data-ttu-id="0acdf-153">Regels voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="0acdf-153">Alert rules</span></span>  

<span data-ttu-id="0acdf-154">Als u geen toegang deze tegels tot, vraag uw beheerder voor Inzender toegang tot de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0acdf-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="0acdf-155">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="0acdf-155">See more</span></span>
* <span data-ttu-id="0acdf-156">[Op rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md): aan de slag met RBAC in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0acdf-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="0acdf-157">[Ingebouwde rollen](role-based-access-built-in-roles.md): meer informatie over de functies die standaard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="0acdf-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="0acdf-158">[Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md): informatie over het maken van aangepaste rollen aan uw behoeften toegang.</span><span class="sxs-lookup"><span data-stu-id="0acdf-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="0acdf-159">[Maken van een geschiedenisrapport voor gewijzigde van toegang](role-based-access-control-access-change-history-report.md): bijhouden van wijzigen van roltoewijzingen in RBAC.</span><span class="sxs-lookup"><span data-stu-id="0acdf-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

