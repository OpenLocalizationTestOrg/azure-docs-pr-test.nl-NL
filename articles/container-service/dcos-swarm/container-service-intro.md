---
title: hosting-aaaDocker container in Azure-cloud | Microsoft Docs
description: Azure Container Service biedt een manier toosimplify Hallo maken, configuratie en beheer van een cluster van virtuele machines die vooraf geconfigureerde toorun beperkte toepassingen zijn.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a>Inleiding tooDocker container-oplossingen met Azure Container Service die als host fungeert 
Azure Container Service maakt het eenvoudiger voor u toocreate, configureren en beheren van een cluster van virtuele machines die vooraf geconfigureerde toorun beperkte toepassingen zijn. De service maakt gebruik van een geoptimaliseerde configuratie van populaire open-source tools voor planning en orchestration. Dit kunt u toouse uw bestaande vaardigheden of tekenen van een grote en groeiende hoofdtekst van de community-expertise, toodeploy en beheren van toepassingen op basis van een container op Microsoft Azure.

![Azure Container Service biedt een manier toomanage beperkte toepassingen op meerdere hosts in Azure.](./media/acs-intro/acs-cluster-new.png)

Azure Container Service maakt gebruik van Hallo Docker-container indeling tooensure dat uw toepassingscontainers volledig mobiel zijn. Het ondersteunt ook uw keuze van Marathon en DC/OS, Docker Swarm of Kubernetes zodat u kunt deze toepassingen toothousands van containers of zelfs tienduizenden te schalen.

Met behulp van Azure Container Service kunt u profiteren van de functies bedrijfsniveau van Azure, zonder dat zij de toepassing draagbaarheid--inclusief draagbaarheid op Hallo orkestratielaag.

## <a name="using-azure-container-service"></a>Azure Container Service gebruiken
Ons doel met Azure Container Service is een container hostomgeving tooprovide met behulp van open-source hulpprogramma's en -technologieën die tegenwoordig populair onder onze klanten. einde toothis, geven we Hallo API-eindpunten voor uw gekozen orchestrator (DC/OS, Docker Swarm of Kubernetes). Met behulp van deze eindpunten, kunt u gebruikmaken van alle software die geschikt is voor toothose eindpunten communiceren. U kunt bijvoorbeeld in geval van Docker Swarm-eindpunt Hallo Hallo toouse hello Docker-opdrachtregelinterface (CLI) selecteren. U kunt voor DC/OS Hallo DCOS CLI. Voor Kubernetes zou u `kubectl` kunnen gebruiken.

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>Een Docker-cluster maken met behulp van Azure Container Service
toobegin met behulp van Azure Container Service implementeren van een Azure Container Service-cluster via Hallo-portal (zoeken Hallo Marketplace voor **Azure Container Service**), met behulp van een Azure Resource Manager-sjabloon ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), of [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), of met Hallo [Azure CLI 2.0](container-service-create-acs-cluster-cli.md). Hallo opgegeven Quick Start-sjablonen kunnen worden gewijzigd tooinclude extra of geavanceerde configuratie van Azure. Zie [Een Azure Container Service-cluster implementeren](container-service-deployment.md) voor meer informatie.

## <a name="deploying-an-application"></a>Een toepassing implementeren
Voor orchestration met Azure Container Service kunt u kiezen uit Docker Swarm, DC/OS of Kubernetes. De implementatie van uw toepassing hangt af van de orchestrator die u kiest.

### <a name="using-dcos"></a>Met DC/OS
DC/OS is een gedistribueerde besturingssysteem op basis van Hallo Apache Mesos gedistribueerde systemen kernel. Apache Mesos is ondergebracht op Hallo Apache Software Foundation en vindt u enkele Hallo [grootste namen in IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) als gebruikers en medewerkers.

![Azure Container Service geconfigureerd voor DC/OS met agents en masters.](media/acs-intro/dcos.png)

DC/OS en Apache Mesos bieden een indrukwekkende functieset:

* In de praktijk beproefde schaalbaarheid
* Fouttolerante gerepliceerde master en slaves op basis van Apache ZooKeeper
* Ondersteuning voor containers met Docker-indeling
* Systeemeigen isolatie tussen taken met Linux-containers
* Multiresource planning (geheugen, CPU, schijf en poorten)
* Java, Python en C++ API's voor het ontwikkelen van nieuwe parallelle toepassingen
* Een web-UI voor weergave van de clusterstatus

DC/OS uitgevoerd op Azure Container Service bevat standaard Hallo Marathon orchestration platform voor het plannen van workloads. Inbegrepen bij Hallo DC/OS-implementatie van ACS is echter Hallo Mesosphere Universe van services die tooyour service kunnen worden toegevoegd. Services in Hallo Universe bevatten Spark, Hadoop, Cassandra en nog veel meer.

![DC/OS Universe in Azure Container Service](media/dcos/universe.png)

#### <a name="using-marathon"></a>Met Marathon
Marathon is een cluster-brede init en controlesysteem voor services in cgroups-- of, in geval van een Azure Container Service Docker ingedeelde containers Hallo. Marathon biedt een web-UI van waaruit u uw toepassingen kunt implementeren. U hebt hiertoe toegang via een URL die er ongeveer als volgt uitziet: `http://DNS_PREFIX.REGION.cloudapp.azure.com`. DNS\_VOORVOEGSEL en REGIO worden gedefinieerd tijdens de implementatie. Indien gewenst, kunt u ook uw eigen DNS-naam opgeven. Zie voor meer informatie over het uitvoeren van een container met Hallo webgebruikersinterface van Marathon [DC/OS-containerbeheer via Hallo webgebruikersinterface van Marathon](container-service-mesos-marathon-ui.md).

![Lijst met Marathon-toepassingen](media/dcos/marathon-applications-list.png)

U kunt ook Hallo REST-API's gebruiken voor communicatie met Marathon. Er zijn een aantal clientbibliotheken beschikbaar voor elke tool. Ze hebben betrekking op diverse talen-- en natuurlijk kunt u Hallo HTTP-protocol in een andere taal. Daarnaast bieden veel populaire DevOps-tools ondersteuning voor Marathon. Zo beschikt u over maximale flexibiliteit voor uw bedrijfsteam wanneer u met een Azure Container Service-cluster werkt. Zie voor meer informatie over het uitvoeren van een container via Marathon REST API Hallo [DC/OS-containerbeheer via Marathon REST API Hallo](container-service-mesos-marathon-rest.md).

### <a name="using-docker-swarm"></a>Met Docker Swarm
Docker Swarm biedt systeemeigen clustering voor Docker. Omdat de Docker Swarm fungeert Hallo standard Docker API, een hulpmiddel dat al met een daemon Docker communiceert Swarm tootransparently scale toomultiple hosts op Azure Container Service kunt gebruiken.

![Azure Container Service geconfigureerd toouse Swarm.](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Ondersteunde hulpprogramma's voor het beheer van containers in een Swarm-cluster bevatten, maar zijn niet beperkt tot Hallo volgende:

* Dokku
* Docker CLI en Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>Kubernetes gebruiken
Kubernetes is een populaire open-source orchestrator van productieklasse voor containers. Kubernetes automatiseert het implementeren, schalen en beheren van toepassingen in containers. Omdat dit een open source is en wordt aangedreven door Hallo open source-community, naadloos op Azure Container Service wordt uitgevoerd en kan worden gebruikt toodeploy containers op grote schaal op Azure Container Service.

![Azure Container Service geconfigureerd toouse Kubernetes.](media/acs-intro/kubernetes.png)

De applicatie bevat een uitgebreide set functies, zoals:
* Horizontaal schalen
* Servicedetectie en taakverdeling
* Geheimen en configuratiebeheer
* Op API gebaseerde geautomatiseerde implementaties en terugdraaiacties
* Automatisch herstel

## <a name="videos"></a>Video's
Aan de slag met Azure Container Service (101):  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

Gebouw toepassingen gebruik hello Azure Container Service (Build 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>Volgende stappen

Een container service-cluster met behulp van Hallo implementeren [portal](container-service-deployment.md) of [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).
