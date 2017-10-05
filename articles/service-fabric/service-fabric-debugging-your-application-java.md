---
title: Fouten opsporen in uw Azure Service Fabric-toepassing in Eclipse | Microsoft Docs
description: De betrouwbaarheid en prestaties van uw services verbeteren door de ontwikkeling en foutopsporing ze in Eclipse op een lokaal ontwikkelcluster.
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
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="c1a51-103">Fouten opsporen in uw Eclipse met Java Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="c1a51-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1a51-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="c1a51-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="c1a51-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="c1a51-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="c1a51-106">Een lokaal ontwikkelcluster starten door de stappen in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c1a51-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="c1a51-107">Werk entryPoint.sh van de service die u opsporen in, wilt zodat deze de java-proces met de parameters voor foutopsporing op afstand begint.</span><span class="sxs-lookup"><span data-stu-id="c1a51-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="c1a51-108">Dit bestand kan worden gevonden op de volgende locatie: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="c1a51-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="c1a51-109">Poort 8001 is voor foutopsporing in dit voorbeeld ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c1a51-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="c1a51-110">Werk het Manifest van de toepassing door het instellen van het aantal exemplaren of het aantal replica's voor de service die foutopsporing wordt uitgevoerd op 1.</span><span class="sxs-lookup"><span data-stu-id="c1a51-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="c1a51-111">Deze instelling voorkomt de poort die wordt gebruikt voor het opsporen van conflicten.</span><span class="sxs-lookup"><span data-stu-id="c1a51-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="c1a51-112">Bijvoorbeeld voor stateless services instellen ``InstanceCount="1"`` en voor stateful services het doel heeft en min replica grootten ingesteld op 1 als volgt: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="c1a51-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="c1a51-113">Implementeer de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1a51-113">Deploy the application.</span></span>

5. <span data-ttu-id="c1a51-114">Selecteer in de IDE Eclipse **Run -> fouten opsporen in configuraties -> externe Java-toepassing en voer de verbindingseigenschappen** en stel de eigenschappen als volgt:</span><span class="sxs-lookup"><span data-stu-id="c1a51-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="c1a51-115">Onderbrekingspunten instellen op de gewenste plaatsen en fouten opsporen in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1a51-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="c1a51-116">Als de toepassing is gecrasht, kunt u ook coredumps inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c1a51-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="c1a51-117">Uitvoeren van ``ulimit -c`` in een shell en als het resultaat 0, wordt de coredumps zijn niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c1a51-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="c1a51-118">Voer de volgende opdracht zodat onbeperkte coredumps: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="c1a51-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="c1a51-119">U kunt ook de status van de opdracht controleren ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="c1a51-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="c1a51-120">Als u wilt dat het pad van de generatie coredump bijwerken, uitvoermachtigingen ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="c1a51-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="c1a51-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1a51-121">Next steps</span></span>

* <span data-ttu-id="c1a51-122">[Verzamelen van logboeken met diagnostische gegevens van Linux Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="c1a51-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="c1a51-123">[Controle en diagnose van services lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c1a51-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
