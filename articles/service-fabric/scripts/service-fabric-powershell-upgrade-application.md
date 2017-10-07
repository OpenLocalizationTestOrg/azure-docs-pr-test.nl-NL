---
title: aaaAzure PowerShell-voorbeeldscript - upgrade uitvoert van een Service Fabric-toepassing | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Upgrade van een Service Fabric-toepassing.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="a6e64-103">Upgrade van een Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="a6e64-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="a6e64-104">Dit voorbeeldscript wordt een actieve Service Fabric-toepassing exemplaar-tooversion 1.3.0 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a6e64-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="a6e64-105">Hallo script Hallo nieuwe pakket toohello cluster installatiekopie toepassingsarchief kopieert, Hallo toepassingstype registreert, begint de upgrade van een bewaakte en continu Hallo upgradestatus controleert totdat het Hallo-upgrade is voltooid of teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="a6e64-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="a6e64-106">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a6e64-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="a6e64-107">Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6e64-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a6e64-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a6e64-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="a6e64-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a6e64-109">Script explanation</span></span>

<span data-ttu-id="a6e64-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a6e64-110">This script uses hello following commands.</span></span> <span data-ttu-id="a6e64-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a6e64-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a6e64-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a6e64-112">Command</span></span> | <span data-ttu-id="a6e64-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a6e64-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6e64-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="a6e64-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="a6e64-115">Hiermee haalt u alle Hallo toepassingen in Hallo Service Fabric-cluster of een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6e64-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="a6e64-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="a6e64-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="a6e64-117">Status van de upgrade van een Service Fabric-toepassing hello opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a6e64-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="a6e64-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="a6e64-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="a6e64-119">Hiermee haalt u Hallo Service Fabric-toepassingstypen geregistreerd op Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="a6e64-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="a6e64-120">Hef de registratie van ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="a6e64-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="a6e64-121">Heft de registratie van het type van een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6e64-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="a6e64-122">Kopiëren ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="a6e64-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="a6e64-123">Kopieert de installatiekopie van een Service Fabric toepassing pakket toohello opslaan.</span><span class="sxs-lookup"><span data-stu-id="a6e64-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="a6e64-124">Register ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="a6e64-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="a6e64-125">Het type van een Service Fabric-toepassing geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a6e64-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="a6e64-126">Start ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="a6e64-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="a6e64-127">Hiermee wordt een Service Fabric-toepassing toohello opgegeven versie van het toepassingstype bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a6e64-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a6e64-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6e64-128">Next steps</span></span>

<span data-ttu-id="a6e64-129">Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="a6e64-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="a6e64-130">Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a6e64-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
