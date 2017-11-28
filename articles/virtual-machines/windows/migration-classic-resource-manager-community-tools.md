---
title: Community-tools - klassieke resources verplaatsen naar Azure Resource Manager | Microsoft Docs
description: In dit artikel catalogus maken van de hulpprogramma's die zijn opgegeven door de community om te migreren van IaaS-middelen van klassiek naar de Azure Resource Manager-implementatiemodel.
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
ms.openlocfilehash: d3fc0246088eddeb345bea0ffbd2c5247b218006
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="b1161-103">Community-programma’s voor de migratie van IaaS-resources van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="b1161-104">In dit artikel catalogus maken van de hulpprogramma's die zijn opgegeven door de community om te helpen bij de migratie van IaaS-middelen van klassiek naar de Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b1161-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="b1161-105">Deze hulpprogramma's zijn niet officieel ondersteund door Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="b1161-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="b1161-106">Daarom zijn open source op GitHub en we willen graag PRs accepteren voor oplossingen of aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="b1161-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="b1161-107">Om een probleem melden, gebruikt u de functie van de problemen met GitHub.</span><span class="sxs-lookup"><span data-stu-id="b1161-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="b1161-108">Met deze hulpprogramma's voor migratie, zullen uitvaltijd voor uw klassieke virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="b1161-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="b1161-109">Als u de migratie ondersteund platform zoekt, gaat u naar</span><span class="sxs-lookup"><span data-stu-id="b1161-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="b1161-110">Migratie van IaaS-middelen van klassiek naar Azure Resource Manager-stack ondersteund platform</span><span class="sxs-lookup"><span data-stu-id="b1161-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="b1161-111">Technische Deep Dive op Platform ondersteund migratie van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="b1161-112">Migreren van IaaS-middelen van klassiek naar Azure Resource Manager met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1161-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="b1161-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="b1161-113">AsmMetadataParser</span></span>
<span data-ttu-id="b1161-114">Dit is een verzameling hulpprogramma's die zijn gemaakt als onderdeel van enterprise-migraties van Azure Service Management in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b1161-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="b1161-115">Dit hulpprogramma kunt u uw infrastructuur repliceren naar een ander abonnement die kan worden gebruikt voor het testen van migratie en ijzer uit eventuele problemen voordat u de migratie op uw productie-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1161-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="b1161-116">Koppeling naar de documentatie van het hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="b1161-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="b1161-117">migAz</span><span class="sxs-lookup"><span data-stu-id="b1161-117">migAz</span></span>
<span data-ttu-id="b1161-118">migAz is een extra optie voor een volledige reeks klassieke IaaS-bronnen migreren naar Azure Resource Manager IaaS-middelen.</span><span class="sxs-lookup"><span data-stu-id="b1161-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="b1161-119">De migratie kan zich voordoen binnen hetzelfde abonnement of tussen verschillende abonnementen en typen abonnementen (ex: CSP-abonnementen).</span><span class="sxs-lookup"><span data-stu-id="b1161-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="b1161-120">Koppeling naar de documentatie van het hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="b1161-120">Link to the tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="b1161-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1161-121">Next Steps</span></span>

* [<span data-ttu-id="b1161-122">Overzicht van de migratie van IaaS resources van klassieke in Azure Resource Manager-platform ondersteund</span><span class="sxs-lookup"><span data-stu-id="b1161-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-123">Technische deep dive op platform ondersteund migratie van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-124">Planning voor de migratie van IaaS-resources van het klassieke implementatiemodel naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-125">PowerShell gebruiken voor het migreren van IaaS-middelen van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-126">CLI gebruiken voor het migreren van IaaS-middelen van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-127">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="b1161-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b1161-128">Lees de veelgestelde vragen over IaaS Resourcemigratie van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1161-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

