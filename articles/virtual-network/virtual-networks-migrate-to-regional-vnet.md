---
title: een Azure-netwerk (klassiek) van een affiniteitsgroep tooa regio aaaMigrate | Microsoft Docs
description: Meer informatie over hoe een virtueel netwerk (klassiek) uit een affiniteit toomigrate tooa regio groepeert.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="18d15-103">Een virtueel netwerk (klassiek) migreren van een affiniteitsgroep tooa regio</span><span class="sxs-lookup"><span data-stu-id="18d15-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18d15-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18d15-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="18d15-105">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="18d15-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="18d15-106">Microsoft raadt aan dat de meeste nieuwe implementaties Hallo Resource Manager-implementatiemodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18d15-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="18d15-107">Affiniteitsgroepen ervoor dat resources gemaakt binnen Hallo dezelfde affiniteitsgroep fysiek op servers die zich dicht bij elkaar inschakelen van deze resources toocommunicate sneller worden gehost.</span><span class="sxs-lookup"><span data-stu-id="18d15-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="18d15-108">In de Hallo is afgelopen waren affiniteitsgroepen een vereiste voor het maken van virtuele netwerken (klassiek).</span><span class="sxs-lookup"><span data-stu-id="18d15-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="18d15-109">Op dat moment werken Hallo manager netwerkservice die beheerd virtuele netwerken (klassiek) kan alleen binnen een set van fysieke servers of schaaleenheid.</span><span class="sxs-lookup"><span data-stu-id="18d15-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="18d15-110">Architectuur verbeteringen toegenomen Hallo bereik van netwerk management tooa regio.</span><span class="sxs-lookup"><span data-stu-id="18d15-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="18d15-111">Als gevolg van deze architectuur verbeteringen zijn affiniteitsgroepen niet langer aanbevolen of vereist zijn voor virtuele netwerken (klassiek).</span><span class="sxs-lookup"><span data-stu-id="18d15-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="18d15-112">Hallo gebruik van affiniteitsgroepen voor virtuele netwerken (klassiek) wordt vervangen door de regio's.</span><span class="sxs-lookup"><span data-stu-id="18d15-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="18d15-113">Regionale virtuele netwerken, virtuele netwerken (klassiek) die gekoppeld aan de regio's zijn worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="18d15-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="18d15-114">Het is raadzaam dat u in het algemeen affiniteitsgroepen niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18d15-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="18d15-115">Behalve Hallo virtueel netwerk vereiste, affiniteitsgroepen is ook belangrijk toouse tooensure resources, zoals berekeningen (klassiek) en opslag (klassiek), in de buurt van elkaar zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="18d15-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="18d15-116">Met de huidige Azure-netwerkarchitectuur hello zijn niet langer deze vereisten plaatsing vereist.</span><span class="sxs-lookup"><span data-stu-id="18d15-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18d15-117">Hoewel het technisch nog steeds mogelijk toocreate een virtueel netwerk dat is gekoppeld aan een affiniteitsgroep, is er geen dwingende redenen toodo dus.</span><span class="sxs-lookup"><span data-stu-id="18d15-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="18d15-118">Veel functies van virtueel netwerk, zoals netwerkbeveiligingsgroepen, zijn alleen beschikbaar wanneer u een regionaal virtueel netwerk en zijn niet beschikbaar voor virtuele netwerken die gekoppeld aan affiniteitsgroepen zijn.</span><span class="sxs-lookup"><span data-stu-id="18d15-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="18d15-119">Hallo netwerk configuratiebestand bewerken</span><span class="sxs-lookup"><span data-stu-id="18d15-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="18d15-120">Hallo netwerk configuratiebestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="18d15-120">Export hello network configuration file.</span></span> <span data-ttu-id="18d15-121">Zie toolearn hoe tooexport netwerkconfiguratie bestand met PowerShell of Azure-opdrachtregelinterface (CLI) 1.0, Hallo [configureren van een virtueel netwerk met een netwerk-configuratiebestand](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="18d15-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="18d15-122">Hallo netwerkconfiguratiebestand bewerken vervangen **AffinityGroup** met **locatie**.</span><span class="sxs-lookup"><span data-stu-id="18d15-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="18d15-123">Geef van een Azure [regio](https://azure.microsoft.com/regions) voor **locatie**.</span><span class="sxs-lookup"><span data-stu-id="18d15-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18d15-124">Hallo **locatie** Hallo regio die u hebt opgegeven voor affiniteitsgroep Hallo die is gekoppeld aan het virtuele netwerk (klassiek).</span><span class="sxs-lookup"><span data-stu-id="18d15-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="18d15-125">Als het virtuele netwerk (klassiek) is gekoppeld aan een affiniteitsgroep die zich in VS-West, wanneer u migreert, bijvoorbeeld uw **locatie** tooWest VS moet verwijzen.</span><span class="sxs-lookup"><span data-stu-id="18d15-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="18d15-126">Hallo volgende regels in het configuratiebestand van uw netwerk, waarbij Hallo waarden vervangt door uw eigen bewerken:</span><span class="sxs-lookup"><span data-stu-id="18d15-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="18d15-127">**Oude waarde:** \<VirtualNetworkSitename = 'VNetUSWest' AffinityGroup = "VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="18d15-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="18d15-128">**Nieuwe waarde:** \<VirtualNetworkSitename = "VNetUSWest" locatie 'VS-West' =\></span><span class="sxs-lookup"><span data-stu-id="18d15-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="18d15-129">Uw wijzigingen hebt opgeslagen en [importeren](virtual-networks-using-network-configuration-file.md#import) Hallo van network configuration tooAzure.</span><span class="sxs-lookup"><span data-stu-id="18d15-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="18d15-130">Deze migratie veroorzaakt geen downtime tooyour services.</span><span class="sxs-lookup"><span data-stu-id="18d15-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="18d15-131">Welke toodo als u een virtuele machine (klassiek) in een affiniteitsgroep hebt</span><span class="sxs-lookup"><span data-stu-id="18d15-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="18d15-132">VMs (klassiek) die momenteel in een affiniteitsgroep nodig toobe verwijderd uit de affiniteitsgroep Hallo is niet.</span><span class="sxs-lookup"><span data-stu-id="18d15-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="18d15-133">Als een virtuele machine is geïmplementeerd, is het geïmplementeerde tooa één schaaleenheid.</span><span class="sxs-lookup"><span data-stu-id="18d15-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="18d15-134">Affiniteitsgroepen kunt beperken Hallo set beschikbare VM-grootten voor een nieuwe VM-implementatie, maar er is al een bestaande virtuele machine die wordt geïmplementeerd beperkt toohello set van VM-groottes beschikbaar in Hallo schaaleenheid in welke Hallo VM is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="18d15-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="18d15-135">Omdat Hallo die VM al is geïmplementeerd tooa schaaleenheid, heeft een virtuele machine verwijderen uit een affiniteitsgroep geen effect op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="18d15-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
