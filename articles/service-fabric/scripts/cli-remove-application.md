---
title: Service Fabric CLI verwijderen voorbeeldscript aaaAzure
description: Een toepassing verwijderen van een Azure Service Fabric-cluster met behulp van hello Azure Service Fabric CLI
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="2e2f1-103">Een toepassing verwijderen van een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="2e2f1-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="2e2f1-104">Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="2e2f1-105">Verwijderen van het Hallo-toepassingsexemplaar verwijdert tevens alle Hallo service-exemplaren die zijn gekoppeld aan de toepassing uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="2e2f1-106">Hallo toepassingsbestanden worden vervolgens verwijderd uit de installatiekopieopslag Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e2f1-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="2e2f1-107">Installeer zo nodig Hallo [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="2e2f1-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2e2f1-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="2e2f1-109">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e2f1-109">Next steps</span></span>

<span data-ttu-id="2e2f1-110">Zie voor meer informatie, Hallo [Service Fabric CLI documentatie](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="2e2f1-111">Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in Hallo [Service Fabric CLI voorbeelden](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e2f1-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
