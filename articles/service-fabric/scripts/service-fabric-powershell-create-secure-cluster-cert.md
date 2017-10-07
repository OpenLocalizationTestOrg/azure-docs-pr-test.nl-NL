---
title: aaaAzure PowerShell-voorbeeldscript - maken van een Service Fabric-cluster | Microsoft Docs
description: Azure PowerShell-Script steekproef - Service Fabric-cluster maken.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="9abb4-103">Een Service Fabric-cluster maken</span><span class="sxs-lookup"><span data-stu-id="9abb4-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="9abb4-104">Dit voorbeeldscript wordt een Service Fabric-cluster een cluster met vijf knooppunten beveiligd met een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="9abb4-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="9abb4-105">Hallo opdracht maakt u een zelfondertekend certificaat en de nieuwe sleutelkluis tooa geüpload.</span><span class="sxs-lookup"><span data-stu-id="9abb4-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="9abb4-106">Er is ook Hallo certificaat gekopieerde tooa lokale map.</span><span class="sxs-lookup"><span data-stu-id="9abb4-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="9abb4-107">Set Hallo *-OS* parameter toochoose Hallo versie van Windows of Linux die wordt uitgevoerd op de clusterknooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="9abb4-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="9abb4-108">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="9abb4-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="9abb4-109">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="9abb4-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9abb4-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9abb4-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9abb4-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9abb4-111">Clean up deployment</span></span> 

<span data-ttu-id="9abb4-112">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, cluster en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="9abb4-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="9abb4-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9abb4-113">Script explanation</span></span>

<span data-ttu-id="9abb4-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="9abb4-114">This script uses hello following commands.</span></span> <span data-ttu-id="9abb4-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9abb4-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9abb4-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9abb4-116">Command</span></span> | <span data-ttu-id="9abb4-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9abb4-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9abb4-118">Nieuwe AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="9abb4-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="9abb4-119">Maakt een nieuwe Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="9abb4-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9abb4-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9abb4-120">Next steps</span></span>

<span data-ttu-id="9abb4-121">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9abb4-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9abb4-122">Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9abb4-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
