---
title: Azure Service Fabric CLI-voorbeeldscript verwijderen
description: Een toepassing verwijderen van een Azure Service Fabric-cluster met de Azure Service Fabric-CLI
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="9b447-103">Een toepassing verwijderen van een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="9b447-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="9b447-104">Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b447-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="9b447-105">Het toepassingsexemplaar ook verwijdert alle uitgevoerd service-exemplaren die zijn gekoppeld aan die toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b447-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="9b447-106">De toepassingsbestanden worden vervolgens verwijderd uit de image store.</span><span class="sxs-lookup"><span data-stu-id="9b447-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="9b447-107">Installeer zo nodig de [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9b447-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="9b447-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9b447-108">Sample script</span></span>

<span data-ttu-id="9b447-109">[!code-sh[belangrijkste](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "een toepassing verwijderen uit een cluster")]</span><span class="sxs-lookup"><span data-stu-id="9b447-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b447-110">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b447-110">Next steps</span></span>

<span data-ttu-id="9b447-111">Zie voor meer informatie de [Service Fabric CLI documentatie](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9b447-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="9b447-112">Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in de [Service Fabric CLI voorbeelden](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9b447-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
