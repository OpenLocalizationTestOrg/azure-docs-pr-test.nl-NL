---
title: Azure PowerShell-Script voorbeeld - toepassing verwijderen uit een cluster | Microsoft Docs
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
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="b93ab-103">Een toepassing verwijderen van een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="b93ab-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="b93ab-104">Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het cluster en verwijdert het toepassingspakket uit het archief van de cluster-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b93ab-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster, and deletes the application package from the cluster image store.</span></span>  <span data-ttu-id="b93ab-105">Het toepassingsexemplaar ook verwijdert alle uitgevoerd service-exemplaren die zijn gekoppeld aan die toepassing.</span><span class="sxs-lookup"><span data-stu-id="b93ab-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="b93ab-106">Pas de parameters zo nodig.</span><span class="sxs-lookup"><span data-stu-id="b93ab-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="b93ab-107">Installeer zo nodig de Service Fabric PowerShell-module met de [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b93ab-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b93ab-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b93ab-108">Sample script</span></span>

<span data-ttu-id="b93ab-109">[!code-powershell[belangrijkste](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "een toepassing verwijderen uit een cluster")]</span><span class="sxs-lookup"><span data-stu-id="b93ab-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="b93ab-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b93ab-110">Script explanation</span></span>

<span data-ttu-id="b93ab-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="b93ab-111">This script uses the following commands.</span></span> <span data-ttu-id="b93ab-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="b93ab-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b93ab-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b93ab-113">Command</span></span> | <span data-ttu-id="b93ab-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b93ab-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b93ab-115">Verwijder ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b93ab-115">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="b93ab-116">Hiermee verwijdert u een actief exemplaar van de Service Fabric-toepassing uit het cluster.</span><span class="sxs-lookup"><span data-stu-id="b93ab-116">Removes a running Service Fabric application instance from the cluster.</span></span>  |
| [<span data-ttu-id="b93ab-117">Hef de registratie van ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="b93ab-117">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="b93ab-118">Heft de registratie van een Service Fabric-toepassingstype en -versie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b93ab-118">Unregisters a Service Fabric application type and version from the cluster.</span></span> |
| [<span data-ttu-id="b93ab-119">Verwijder ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="b93ab-119">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="b93ab-120">Hiermee verwijdert u een Service Fabric-toepassingspakket uit de image store.</span><span class="sxs-lookup"><span data-stu-id="b93ab-120">Removes a Service Fabric application package from the image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="b93ab-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b93ab-121">Next steps</span></span>

<span data-ttu-id="b93ab-122">Zie voor meer informatie over de Service Fabric PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b93ab-122">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="b93ab-123">Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in de [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b93ab-123">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
