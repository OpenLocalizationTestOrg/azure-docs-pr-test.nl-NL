---
title: aaaCreate Azure Service Fabric-clusters in Windows Server- en Linux | Microsoft Docs
description: Service Fabric-clusters worden uitgevoerd in Windows Server- en Linux, wat betekent u dat zult kunnen toodeploy en host-Service Fabric-toepassingen overal kunnen worden uitgevoerd Windows Server of Linux.
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Service Fabric-clusters op Windows Server of Linux maken
Een Azure Service Fabric-cluster is een set netwerk verbonden virtuele of fysieke machines waarin uw microservices worden geïmplementeerd en beheerd. Een machine of virtuele machine die deel uitmaakt van een cluster wordt een clusterknooppunt genoemd. Clusters kunnen schalen toothousands van knooppunten. Als u nieuwe knooppunten toohello cluster toevoegt, rebalances Service Fabric Hallo service partitie replica's en -exemplaren over het aantal knooppunten Hallo verhoogd. De algemene verbetert de prestaties van toepassingen en conflicten over toegang toomemory verkleint. Als het Hallo-knooppunten in cluster Hallo niet efficiënt worden gebruikt, kunt u het aantal knooppunten in cluster Hallo Hallo verminderen. Service Fabric rebalances opnieuw Hallo partitie replica's en exemplaren over Hallo afgenomen aantal knooppunten toomake beter gebruik van Hallo hardware op elk knooppunt.

Service Fabric basisinventarisrapporten Hallo van Service Fabric-clusters op elke virtuele machines of computers waarop Windows Server of Linux wordt uitgevoerd. Dit betekent dat u kunt toodeploy en Service Fabric-toepassingen uitvoeren in een omgeving waar het hebben van een set van Windows Server- of Linux-computers onderling, on-premises, Microsoft Azure worden of met elke cloudprovider.

## <a name="create-service-fabric-clusters-on-azure"></a>Service Fabric-clusters maken in Azure
Maken van een cluster in Azure wordt uitgevoerd, hetzij via een Resourcemodel sjabloon of hello Azure-portal. Lees [Service Fabric-cluster maken met behulp van een Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) of [een Service Fabric-cluster maken van hello Azure-portal](service-fabric-cluster-creation-via-portal.md) voor meer informatie.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Ondersteunde besturingssystemen voor clusters op Azure
U zijn kunt toocreate clusters op virtuele machines met deze besturingssystemen:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (in de openbare preview) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Zelfstandige Service Fabric-clusters lokale maken of bij een cloudprovider
Service Fabric bevat een installatiepakket voor u toocreate zelfstandige Service Fabric-clusters on-premises of op elke cloudprovider

Lees voor meer informatie over het instellen van zelfstandige service fabric-clusters op Windows Server, [Service Fabric-cluster maken voor Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Alle cloudimplementaties tegenover on-premises implementaties
Hallo-proces voor het maken van een Service Fabric-cluster lokale is vergelijkbaar toohello proces voor het maken van een cluster in een cloud van uw keuze met een set van virtuele machines. Hallo eerste stappen tooprovision Hallo virtuele machines worden beheerst door de cloudprovider Hallo of on-premises omgeving die u gebruikt. Zodra u een aantal virtuele machines met hebt netwerkverbinding is tussen deze twee, ingeschakeld vervolgens Hallo stappen tooset Hallo Service Fabric-pakket, Hallo clusterinstellingen bewerken en Hallo cluster maken uitvoeren en scripts voor identiek zijn. Dit zorgt ervoor dat uw kennis en ervaring van het besturingssysteem en Service Fabric-clusters beheren overgedragen wanneer u nieuwe hostingomgevingen tootarget kiest.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Voordelen van zelfstandige Service Fabric-clusters maken
* U staat op het gratis toochoose een cloud provider toohost uw cluster.
* Service Fabric-toepassingen, één keer worden geschreven, kunnen worden uitgevoerd in omgevingen met meerdere hosting met minimale toono wijzigingen.
* Kennis van het bouwen van Service Fabric-toepassingen uitvoert via uit één hosting omgeving tooanother.
* Praktijkervaring van uitvoert en beheert de Service Fabric-clusters uitvoert via van de ene omgeving tooanother.
* Brede klant reach is unbounded door het hosten van de beperkingen van de omgeving.
* Een extra beveiligingslaag betrouwbaarheid en bescherming tegen storingen wijdverbreid bestaat omdat u Hallo services via tooanother implementatieomgeving als een datacenter verplaatsen of cloudprovider een onleesbaar kunt heeft.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Ondersteunde besturingssystemen voor zelfstandige clusters
U zijn kunt toocreate clusters op virtuele machines of computers met deze besturingssystemen:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (binnenkort)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Voordelen van het Service Fabric-clusters op Azure via zelfstandige die service Fabric-clusters lokale gemaakt
Service Fabric-clusters op Azure biedt voordelen ten opzichte van Hallo lokale optie, dus als er geen specifieke behoeften voor waarin u uw clusters wordt uitgevoerd, klikt u vervolgens het is raadzaam dat u deze op Azure uitvoeren. In Azure bieden we een integratie met andere Azure-functies en services, waardoor bewerkingen en het beheer van Hallo cluster eenvoudiger en betrouwbaarder.

* **Azure-portal:** Azure-portal maakt het eenvoudig toocreate en beheren van clusters.
* **Azure Resource Manager:** gebruik van Azure Resource Manager kunt u eenvoudig beheer van alle resources die door hello worden gebruikt als een eenheid en vereenvoudigt u kosten bijhouden en facturering.
* **Service Fabric-Cluster als een Azure-Resource** A Service Fabric-cluster is een ARM-bron, waarmee u kunt het model zoals andere ARM-resources in Azure.
* **Integratie met Azure-infrastructuur** Service Fabric-coördinaten met Hallo onderliggende Azure-infrastructuur voor het besturingssysteem, netwerk, en andere upgrades tooimprove beschikbaarheid en betrouwbaarheid van uw toepassingen.  
* **Diagnostische gegevens:** in Azure, bieden we integratie met Azure diagnoses en Log Analytics.
* **Automatische schaling:** voor clusters op Azure, bieden we ingebouwde automatische schaling functionaliteit vanwege tooVirtual-machineschaalsets. In on-premises en andere cloudomgevingen hebt u toobuild uw eigen automatische schaling functie of schaal handmatig met behulp van Hallo API's die Service Fabric beschikbaar maakt voor het schalen van clusters.

## <a name="next-steps"></a>Volgende stappen

* Een cluster maken op virtuele machines of computers met Windows Server: [Service Fabric-cluster maken voor Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Een cluster maken op virtuele machines of computers waarop Linux wordt uitgevoerd: [Service Fabric op Linux](service-fabric-linux-overview.md)
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

