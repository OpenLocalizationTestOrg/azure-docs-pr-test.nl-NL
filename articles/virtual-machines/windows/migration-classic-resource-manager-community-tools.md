---
title: Extra aaaCommunity - verplaatsen klassieke resources tooAzure Resource Manager | Microsoft Docs
description: Dit artikel catalogussen Hallo hulpprogramma's die zijn getroffen door Hallo community toohelp migreren IaaS resources van klassieke toohello Azure Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="d5f73-103">Community van hulpprogramma's voor toomigrate IaaS resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5f73-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="d5f73-104">Dit artikel catalogussen Hallo-hulpprogramma's die zijn getroffen door Hallo community tooassist bij de migratie van IaaS-resources van klassieke toohello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d5f73-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="d5f73-105">Deze hulpprogramma's zijn niet officieel ondersteund door Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="d5f73-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="d5f73-106">Daarom zijn open source op GitHub en wij zijn blij tooaccept PRs voor oplossingen of aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="d5f73-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="d5f73-107">tooreport een probleem Hallo GitHub problemen functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5f73-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="d5f73-108">Met deze hulpprogramma's voor migratie, zullen uitvaltijd voor uw klassieke virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="d5f73-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="d5f73-109">Als u de migratie ondersteund platform zoekt, gaat u naar</span><span class="sxs-lookup"><span data-stu-id="d5f73-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="d5f73-110">Migratie van IaaS-resources van klassieke tooAzure Resource Manager-stack ondersteund platform</span><span class="sxs-lookup"><span data-stu-id="d5f73-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="d5f73-111">Technische Deep Dive op Platform ondersteund migratie van klassiek tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5f73-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="d5f73-112">IaaS-bronnen worden gemigreerd van klassiek tooAzure Resource Manager met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5f73-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="d5f73-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="d5f73-113">AsmMetadataParser</span></span>
<span data-ttu-id="d5f73-114">Dit is een verzameling hulpprogramma's die zijn gemaakt als onderdeel van enterprise-migraties van Azure Service Management tooAzure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d5f73-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="d5f73-115">Dit hulpprogramma kunt u tooreplicate uw infrastructuur in een ander abonnement die kan worden gebruikt voor het testen van migratie en strijk uit eventuele problemen voordat Hallo migratie wordt uitgevoerd op uw productie-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d5f73-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="d5f73-116">Koppeling toohello hulpprogramma documentatie</span><span class="sxs-lookup"><span data-stu-id="d5f73-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="d5f73-117">migAz</span><span class="sxs-lookup"><span data-stu-id="d5f73-117">migAz</span></span>
<span data-ttu-id="d5f73-118">migAz is een extra optie toomigrate een volledige reeks klassieke IaaS resources tooAzure Resource Manager IaaS-resources.</span><span class="sxs-lookup"><span data-stu-id="d5f73-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="d5f73-119">Hallo migratie kan plaatsvinden in Hallo hetzelfde abonnement of tussen verschillende abonnementen en typen abonnementen (ex: CSP-abonnementen).</span><span class="sxs-lookup"><span data-stu-id="d5f73-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="d5f73-120">Koppeling toohello hulpprogramma documentatie</span><span class="sxs-lookup"><span data-stu-id="d5f73-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="d5f73-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5f73-121">Next Steps</span></span>

* [<span data-ttu-id="d5f73-122">Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund</span><span class="sxs-lookup"><span data-stu-id="d5f73-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-123">Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5f73-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-124">Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen</span><span class="sxs-lookup"><span data-stu-id="d5f73-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-125">PowerShell toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5f73-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-126">CLI toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5f73-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-127">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="d5f73-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d5f73-128">Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5f73-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

