---
title: PowerShell-voorbeeldscript - toepassing verwijderen uit een cluster aaaAzure | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - verwijderen in een toepassing van een Service Fabric-cluster.
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="0d49d-103">Een toepassing verwijderen van een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="0d49d-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="0d49d-104">Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van de cluster Hallo en Hallo toepassingspakket verwijderd uit de installatiekopieopslag Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0d49d-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="0d49d-105">Verwijderen van het Hallo-toepassingsexemplaar verwijdert tevens alle Hallo service-exemplaren die zijn gekoppeld aan de toepassing uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0d49d-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="0d49d-106">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="0d49d-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="0d49d-107">Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0d49d-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0d49d-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0d49d-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="0d49d-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0d49d-109">Script explanation</span></span>

<span data-ttu-id="0d49d-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="0d49d-110">This script uses hello following commands.</span></span> <span data-ttu-id="0d49d-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0d49d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0d49d-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0d49d-112">Command</span></span> | <span data-ttu-id="0d49d-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0d49d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d49d-114">Verwijder ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="0d49d-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="0d49d-115">Hiermee verwijdert u een actief exemplaar van de Service Fabric-toepassing uit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0d49d-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="0d49d-116">Hef de registratie van ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="0d49d-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="0d49d-117">Heft de registratie van een Service Fabric-toepassingstype en -versie uit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0d49d-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="0d49d-118">Verwijder ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="0d49d-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="0d49d-119">Hiermee verwijdert u een Service Fabric-toepassingspakket uit Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="0d49d-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="0d49d-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0d49d-120">Next steps</span></span>

<span data-ttu-id="0d49d-121">Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="0d49d-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="0d49d-122">Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0d49d-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
