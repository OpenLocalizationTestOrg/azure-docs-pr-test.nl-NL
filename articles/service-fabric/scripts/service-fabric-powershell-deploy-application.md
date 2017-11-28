---
title: aaaAzure PowerShell-voorbeeldscript - toepassing tooa cluster implementeren | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - een toepassing tooa Service Fabric-cluster implementeren.
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="c4b8b-103">Een toepassing tooa Service Fabric-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="c4b8b-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="c4b8b-104">Dit voorbeeldscript gekopieerd van een toepassing pakket tooa cluster image store, registreert Hallo toepassingstype in Hallo cluster en maakt een toepassingsexemplaar van toepassingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="c4b8b-105">Als alle services die standaard zijn gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing hello, worden op dit moment die services gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="c4b8b-106">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="c4b8b-107">Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8b-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c4b8b-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c4b8b-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4b8b-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c4b8b-109">Clean up deployment</span></span> 

<span data-ttu-id="c4b8b-110">Na het uitvoeren van het voorbeeldscript Hallo Hallo script in [een toepassing verwijderen](service-fabric-powershell-remove-application.md) gebruikte tooremove Hallo toepassingsexemplaar worden, registratie van toepassingstype Hallo en Hallo toepassingspakket wissen van Hallo image store.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="c4b8b-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c4b8b-111">Script explanation</span></span>

<span data-ttu-id="c4b8b-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-112">This script uses hello following commands.</span></span> <span data-ttu-id="c4b8b-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4b8b-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c4b8b-114">Command</span></span> | <span data-ttu-id="c4b8b-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c4b8b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4b8b-116">Kopiëren ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="c4b8b-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="c4b8b-117">Kopieer een pakket toohello cluster installatiekopie toepassingsarchief.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="c4b8b-118">Register ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c4b8b-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="c4b8b-119">Registreert een toepassingstype en -versie op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="c4b8b-120">Nieuwe ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="c4b8b-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="c4b8b-121">Maakt een toepassing van een geregistreerde toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="c4b8b-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4b8b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4b8b-122">Next steps</span></span>

<span data-ttu-id="c4b8b-123">Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c4b8b-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="c4b8b-124">Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8b-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
