---
title: aaaAzure infrastructuur naamgevingsregels - Linux | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor de naamgeving in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="8f580-103">Azure-infrastructuur naamgevingsregels voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="8f580-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="8f580-104">Dit artikel is gericht op het inzicht in hoe tooapproach naamconventies voor uw verschillende Azure-resources toobuild een logische en gemakkelijk kan worden geïdentificeerd instellen van resources in uw hele omgeving.</span><span class="sxs-lookup"><span data-stu-id="8f580-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="8f580-105">Implementatie van richtlijnen voor naamgevingsregels</span><span class="sxs-lookup"><span data-stu-id="8f580-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="8f580-106">Beslissingen te nemen:</span><span class="sxs-lookup"><span data-stu-id="8f580-106">Decisions:</span></span>

* <span data-ttu-id="8f580-107">Wat zijn uw naamgevingsregels voor Azure-resources?</span><span class="sxs-lookup"><span data-stu-id="8f580-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="8f580-108">Taken:</span><span class="sxs-lookup"><span data-stu-id="8f580-108">Tasks:</span></span>

* <span data-ttu-id="8f580-109">Hallo-en achtervoegsel toouse tussen de consistentie van uw resources toomaintain definiëren.</span><span class="sxs-lookup"><span data-stu-id="8f580-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="8f580-110">Definieer opslagaccount namen Hallo vereiste voor deze toobe globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="8f580-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="8f580-111">Document Hallo naming convention toobe gebruikt en tooall partijen betrokken tooensure consistentie verdelen over implementaties.</span><span class="sxs-lookup"><span data-stu-id="8f580-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="8f580-112">Naamgevingsregels</span><span class="sxs-lookup"><span data-stu-id="8f580-112">Naming conventions</span></span>
<span data-ttu-id="8f580-113">U moet beschikken over een goede naamgevingsconventie voordat u verder niets te maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f580-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="8f580-114">Een naamgevingsconventie zorgt ervoor dat alle Hallo resources een voorspelbare naam, waarmee de administratieve last van lagere Hallo die zijn gekoppeld aan deze resources beheren.</span><span class="sxs-lookup"><span data-stu-id="8f580-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="8f580-115">U kunt een specifieke set domeinnaamconventies die zijn gedefinieerd voor de hele organisatie of voor een specifieke Azure-abonnement of account toofollow.</span><span class="sxs-lookup"><span data-stu-id="8f580-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="8f580-116">Hoewel het eenvoudig voor personen binnen organisaties tooestablish impliciete regels bij het werken met Azure-resources, moet u kunnen tooscale toobe voor teams die samenwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f580-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="8f580-117">Een reeks vooraf naamconventies overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="8f580-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="8f580-118">Er zijn enkele overwegingen met betrekking tot de naamconventies die meerdere waarmee wordt ingesteld van regels.</span><span class="sxs-lookup"><span data-stu-id="8f580-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="8f580-119">Brengt</span><span class="sxs-lookup"><span data-stu-id="8f580-119">Affixes</span></span>
<span data-ttu-id="8f580-120">Als u een naamgevingsconventie toodefine kijkt, is een beslissing of Hallo voorvoegsel is op:</span><span class="sxs-lookup"><span data-stu-id="8f580-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="8f580-121">Hallo-naam (voorvoegsel) Hallo begint</span><span class="sxs-lookup"><span data-stu-id="8f580-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="8f580-122">Hallo-einde van Hallo-naam (achtervoegsel)</span><span class="sxs-lookup"><span data-stu-id="8f580-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="8f580-123">Hier worden bijvoorbeeld twee verschillende namen voor een resourcegroep met Hallo `rg` brengt:</span><span class="sxs-lookup"><span data-stu-id="8f580-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="8f580-124">Rg-WebApp (voorvoegsel)</span><span class="sxs-lookup"><span data-stu-id="8f580-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="8f580-125">WebApp-Rg (achtervoegsel)</span><span class="sxs-lookup"><span data-stu-id="8f580-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="8f580-126">Achtervoegsel kunnen toodifferent aspecten die bepaalde resources Hallo Beschrijf verwijzen.</span><span class="sxs-lookup"><span data-stu-id="8f580-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="8f580-127">Hallo ziet volgende tabel u enkele voorbeelden doorgaans worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8f580-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="8f580-128">Aspect</span><span class="sxs-lookup"><span data-stu-id="8f580-128">Aspect</span></span> | <span data-ttu-id="8f580-129">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8f580-129">Examples</span></span> | <span data-ttu-id="8f580-130">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8f580-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8f580-131">Omgeving</span><span class="sxs-lookup"><span data-stu-id="8f580-131">Environment</span></span> |<span data-ttu-id="8f580-132">de prod-dev-, stg,</span><span class="sxs-lookup"><span data-stu-id="8f580-132">dev, stg, prod</span></span> |<span data-ttu-id="8f580-133">Afhankelijk van het Hallo-doel en de naam van elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="8f580-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="8f580-134">Locatie</span><span class="sxs-lookup"><span data-stu-id="8f580-134">Location</span></span> |<span data-ttu-id="8f580-135">usw (VS-West), gebruiken (VS-Oost 2)</span><span class="sxs-lookup"><span data-stu-id="8f580-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="8f580-136">Afhankelijk van de regio Hallo Hallo datacenter of Hallo regio van Hallo-organisatie.</span><span class="sxs-lookup"><span data-stu-id="8f580-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="8f580-137">Azure onderdeel, service of product</span><span class="sxs-lookup"><span data-stu-id="8f580-137">Azure component, service, or product</span></span> |<span data-ttu-id="8f580-138">Rg voor de resourcegroep VNet voor het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="8f580-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="8f580-139">Afhankelijk van het Hallo-product voor welke Hallo-bron biedt ondersteuning voor.</span><span class="sxs-lookup"><span data-stu-id="8f580-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="8f580-140">Rol</span><span class="sxs-lookup"><span data-stu-id="8f580-140">Role</span></span> |<span data-ttu-id="8f580-141">DB, app, web</span><span class="sxs-lookup"><span data-stu-id="8f580-141">db, app, web</span></span> |<span data-ttu-id="8f580-142">Afhankelijk van de rol Hallo van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8f580-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="8f580-143">Exemplaar</span><span class="sxs-lookup"><span data-stu-id="8f580-143">Instance</span></span> |<span data-ttu-id="8f580-144">01, 02, 03, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8f580-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="8f580-145">Voor bronnen die u meer dan één exemplaar hebt.</span><span class="sxs-lookup"><span data-stu-id="8f580-145">For resources that have more than one instance.</span></span> <span data-ttu-id="8f580-146">Bijvoorbeeld, taakverdeling webservers in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="8f580-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="8f580-147">Bij het maken van uw naamconventies, zorg ervoor dat ze duidelijk vermeld die brengt toouse voor elk type resource en in welke volgorde (voorvoegsel tegenover achtervoegsel).</span><span class="sxs-lookup"><span data-stu-id="8f580-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="8f580-148">datums</span><span class="sxs-lookup"><span data-stu-id="8f580-148">Dates</span></span>
<span data-ttu-id="8f580-149">Vaak is het belangrijk toodetermine Hallo datum van het maken van Hallo-naam van een bron.</span><span class="sxs-lookup"><span data-stu-id="8f580-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="8f580-150">Het wordt aangeraden de Hallo JJJJMMDD datumnotatie.</span><span class="sxs-lookup"><span data-stu-id="8f580-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="8f580-151">Het voordeel hiervan is niet alleen Hallo volledige datum geregistreerd, maar ook twee resources waarvan de namen verschillen op Hallo datum alfabetisch en in chronologische volgorde worden gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="8f580-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="8f580-152">Naamgeving van resources</span><span class="sxs-lookup"><span data-stu-id="8f580-152">Naming resources</span></span>
<span data-ttu-id="8f580-153">Elk type resource definiëren in Hallo naamgevingsconventie die moet hebben regels die bepalen hoe tooassign tooeach resource namen die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f580-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="8f580-154">Deze regels gelden tooall typen resources, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8f580-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="8f580-155">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="8f580-155">Subscriptions</span></span>
* <span data-ttu-id="8f580-156">Accounts</span><span class="sxs-lookup"><span data-stu-id="8f580-156">Accounts</span></span>
* <span data-ttu-id="8f580-157">Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="8f580-157">Storage accounts</span></span>
* <span data-ttu-id="8f580-158">Virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="8f580-158">Virtual networks</span></span>
* <span data-ttu-id="8f580-159">Subnetten</span><span class="sxs-lookup"><span data-stu-id="8f580-159">Subnets</span></span>
* <span data-ttu-id="8f580-160">Beschikbaarheidssets</span><span class="sxs-lookup"><span data-stu-id="8f580-160">Availability sets</span></span>
* <span data-ttu-id="8f580-161">Resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="8f580-161">Resource groups</span></span>
* <span data-ttu-id="8f580-162">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="8f580-162">Virtual machines</span></span>
* <span data-ttu-id="8f580-163">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="8f580-163">Endpoints</span></span>
* <span data-ttu-id="8f580-164">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="8f580-164">Network security groups</span></span>
* <span data-ttu-id="8f580-165">Rollen</span><span class="sxs-lookup"><span data-stu-id="8f580-165">Roles</span></span>

<span data-ttu-id="8f580-166">tooensure die naam Hallo biedt voldoende informatie toodetermine toowhich resource verwijst, moet u beschrijvende namen.</span><span class="sxs-lookup"><span data-stu-id="8f580-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="8f580-167">Computernamen</span><span class="sxs-lookup"><span data-stu-id="8f580-167">Computer names</span></span>
<span data-ttu-id="8f580-168">Wanneer u een virtuele machine (VM) maakt, wordt in Azure een VM-naam van up too64 tekens dat wordt gebruikt voor de resourcenaam Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="8f580-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="8f580-169">Maakt gebruik van Azure Hallo dezelfde naam voor het Hallo-besturingssysteem is geïnstalleerd in Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8f580-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="8f580-170">Echter, deze namen mogelijk niet altijd worden Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="8f580-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="8f580-171">Als een virtuele machine wordt gemaakt van een VHD-afbeeldingsbestand dat al een besturingssysteem bevat, Hallo de naam van de virtuele machine in Azure, kan afwijken van Hallo computernaam van de virtuele machine-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8f580-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="8f580-172">Deze situatie kan een zekere mate van moeite tooVM management, dus u niet kunt beter kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8f580-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="8f580-173">Wijs hello Azure VM resource Hallo dezelfde naam als de naam van de computer Hallo toohello besturingssysteem van die virtuele machine toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="8f580-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="8f580-174">U wordt aangeraden deze hello Azure VM-naam is hetzelfde als het onderliggende besturingssysteem computernaam Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f580-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="8f580-175">Namen van opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="8f580-175">Storage account names</span></span>
<span data-ttu-id="8f580-176">Deze sectie geldt niet te[Azure beheerd schijven](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), omdat u geen afzonderlijke storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="8f580-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="8f580-177">Storage-accounts hebben voor niet-beheerde schijven speciale regels die zijn voor hun namen.</span><span class="sxs-lookup"><span data-stu-id="8f580-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="8f580-178">U kunt alleen kleine letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="8f580-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="8f580-179">Zie voor meer informatie [een opslagaccount maken](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8f580-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="8f580-180">Daarnaast moet Hallo opslagaccountnaam, met core.windows.net, een globaal geldig, unieke DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="8f580-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="8f580-181">Bijvoorbeeld, als Hallo storage-account mystorageaccount aangeroepen wordt, moeten hello volgende resulterende DNS-namen uniek zijn:</span><span class="sxs-lookup"><span data-stu-id="8f580-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="8f580-182">mystorageaccount.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="8f580-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="8f580-183">mystorageaccount.Table.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="8f580-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="8f580-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="8f580-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f580-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f580-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

