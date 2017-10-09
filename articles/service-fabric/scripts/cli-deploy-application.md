---
title: Service Fabric CLI implementeren voorbeeldscript aaaAzure
description: Een toepassing tooan Azure Service Fabric-cluster met behulp van Azure Service Fabric CLI Hallo implementeren
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="427c0-103">Een toepassing tooa Service Fabric-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="427c0-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="427c0-104">Dit voorbeeldscript gekopieerd van een toepassing pakket tooa cluster image store, registreert Hallo toepassingstype in Hallo cluster en maakt een toepassingsexemplaar van toepassingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="427c0-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="427c0-105">Alle services die standaard worden ook op dit moment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="427c0-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="427c0-106">Installeer zo nodig Hallo [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="427c0-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="427c0-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="427c0-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="427c0-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="427c0-108">Clean up deployment</span></span>

<span data-ttu-id="427c0-109">Wanneer u klaar bent, Hallo [verwijderen](cli-remove-application.md) script gebruikte tooremove Hallo toepassing kan worden.</span><span class="sxs-lookup"><span data-stu-id="427c0-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="427c0-110">Hallo verwijderen script Hallo toepassingsexemplaar verwijdert, heft de registratie van toepassingstype Hallo en Hallo toepassingspakket verwijdert uit de image store.</span><span class="sxs-lookup"><span data-stu-id="427c0-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="427c0-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="427c0-111">Next steps</span></span>

<span data-ttu-id="427c0-112">Zie voor meer informatie, Hallo [Service Fabric CLI documentatie](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="427c0-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="427c0-113">Extra Service Fabric CLI steekproeven voor de Azure Service Fabric vindt u in Hallo [Service Fabric CLI voorbeelden](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="427c0-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
