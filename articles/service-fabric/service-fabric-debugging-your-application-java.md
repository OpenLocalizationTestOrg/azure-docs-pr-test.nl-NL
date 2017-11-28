---
title: aaaDebug uw Azure Service Fabric-toepassing in Eclipse | Microsoft Docs
description: Hallo-betrouwbaarheid en prestaties van uw services verbeteren door de ontwikkeling en foutopsporing ze in Eclipse op een lokaal ontwikkelcluster.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="2f790-103">Fouten opsporen in uw Eclipse met Java Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="2f790-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f790-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="2f790-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="2f790-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="2f790-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="2f790-106">Een lokaal ontwikkelcluster starten door de stappen te volgen Hallo in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2f790-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="2f790-107">Bijwerken van entryPoint.sh van Hallo service desgewenst toodebug, zodat deze Hallo java proces met de parameters voor foutopsporing op afstand begint.</span><span class="sxs-lookup"><span data-stu-id="2f790-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="2f790-108">Dit bestand kan worden gevonden op Hallo volgende locatie: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="2f790-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="2f790-109">Poort 8001 is voor foutopsporing in dit voorbeeld ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2f790-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="2f790-110">Hallo Application Manifest bijwerken door in te stellen Hallo-exemplaren of hello aantal replica's voor Hallo-service die wordt gecontroleerd too1.</span><span class="sxs-lookup"><span data-stu-id="2f790-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="2f790-111">Deze instelling voorkomt Hallo-poort die wordt gebruikt voor het opsporen van conflicten.</span><span class="sxs-lookup"><span data-stu-id="2f790-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="2f790-112">Bijvoorbeeld voor stateless services instellen ``InstanceCount="1"`` en voor stateful services set Hallo doel en min replicaset grootten too1 als volgt: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="2f790-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="2f790-113">Hallo-toepassing implementeren.</span><span class="sxs-lookup"><span data-stu-id="2f790-113">Deploy hello application.</span></span>

5. <span data-ttu-id="2f790-114">Selecteer in Eclipse IDE Hallo, **Run -> fouten opsporen in configuraties -> externe Java-toepassing en voer de verbindingseigenschappen** en Hallo eigenschappen als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="2f790-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="2f790-115">Onderbrekingspunten instellen op de gewenste plaatsen en fouten opsporen in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f790-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="2f790-116">Als het Hallo-toepassing is gecrasht, kunt u ook tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="2f790-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="2f790-117">Uitvoeren van ``ulimit -c`` in een shell en als het resultaat 0, wordt de coredumps zijn niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2f790-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="2f790-118">tooenable onbeperkte coredumps Hallo volgende opdracht uitvoeren: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="2f790-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="2f790-119">U kunt ook met de opdracht Hallo Hallo-status controleren ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="2f790-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="2f790-120">Indien u tooupdate hello coredump generatie pad wenste, uitvoeren ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="2f790-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="2f790-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f790-121">Next steps</span></span>

* <span data-ttu-id="2f790-122">[Verzamelen van logboeken met diagnostische gegevens van Linux Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="2f790-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="2f790-123">[Controle en diagnose van services lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2f790-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
