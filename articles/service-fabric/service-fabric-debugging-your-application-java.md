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
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Fouten opsporen in uw Eclipse met Java Service Fabric-toepassing
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Een lokaal ontwikkelcluster starten door de stappen te volgen Hallo in [instellen van uw ontwikkelomgeving Service Fabric](service-fabric-get-started-linux.md).

2. Bijwerken van entryPoint.sh van Hallo service desgewenst toodebug, zodat deze Hallo java proces met de parameters voor foutopsporing op afstand begint. Dit bestand kan worden gevonden op Hallo volgende locatie: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Poort 8001 is voor foutopsporing in dit voorbeeld ingesteld.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Hallo Application Manifest bijwerken door in te stellen Hallo-exemplaren of hello aantal replica's voor Hallo-service die wordt gecontroleerd too1. Deze instelling voorkomt Hallo-poort die wordt gebruikt voor het opsporen van conflicten. Bijvoorbeeld voor stateless services instellen ``InstanceCount="1"`` en voor stateful services set Hallo doel en min replicaset grootten too1 als volgt: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Hallo-toepassing implementeren.

5. Selecteer in Eclipse IDE Hallo, **Run -> fouten opsporen in configuraties -> externe Java-toepassing en voer de verbindingseigenschappen** en Hallo eigenschappen als volgt instellen:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Onderbrekingspunten instellen op de gewenste plaatsen en fouten opsporen in Hallo-toepassing.

Als het Hallo-toepassing is gecrasht, kunt u ook tooenable coredumps. Uitvoeren van ``ulimit -c`` in een shell en als het resultaat 0, wordt de coredumps zijn niet ingeschakeld. tooenable onbeperkte coredumps Hallo volgende opdracht uitvoeren: ``ulimit -c unlimited``. U kunt ook met de opdracht Hallo Hallo-status controleren ``ulimit -a``.  Indien u tooupdate hello coredump generatie pad wenste, uitvoeren ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Volgende stappen

* [Verzamelen van logboeken met diagnostische gegevens van Linux Azure](service-fabric-diagnostics-how-to-setup-lad.md).
* [Controle en diagnose van services lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
