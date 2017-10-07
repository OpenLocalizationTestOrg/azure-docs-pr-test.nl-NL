---
title: aaaAzure Containerexemplaren en Container Orchestration
description: Begrijpen hoe Azure Containerexemplaren communiceren met de container orchestrators
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Azure Container-exemplaren en container orchestrators

Vanwege de klein en de afdrukstand van de toepassing zijn containers uitermate geschikt is voor flexibele levering omgevingen en op basis van microservice-architecturen. Hallo-taak van automatiseren en beheren van een groot aantal containers en hun werking wordt ook wel *orchestration*. Populaire container orchestrators zijn Kubernetes DC/OS en Docker Swarm dit allemaal beschikbaar in Hallo zijn [Azure Container Service](https://docs.microsoft.com/azure/container-service/).

Azure Containerexemplaren staan enkele Hallo basic planfuncties orchestration-platforms, maar ze omvatten geen Hallo hogere waarde services dat deze platforms bieden en in feite aanvullende met hen worden kunnen. Dit artikel wordt beschreven Hallo bereik van wat Azure Containerexemplaren verwerkt en hoe vol container orchestrators ermee kunnen communiceren.

## <a name="traditional-orchestration"></a>Traditionele orchestration

Hallo standaarddefinitie van orchestration bevat Hallo taken te volgen:

- **Planning**: een geschikte machine op welke toorun Hallo container gezien een installatiekopie van een container en een resource-aanvraag, vinden.
- **Affiniteit /-affinity**: opgeven dat een set van containers moet worden uitgevoerd in de buurt van elkaar (prestaties) of voldoende ver uit elkaar (voor beschikbaarheid).
- **Statuscontrole**: Bekijk bij fouten van de container en automatisch opnieuw te plannen.
- **Failover**: bijhouden wat wordt uitgevoerd op elke machine en plannen van containers van mislukte machines toohealthy knooppunten.
- **Schalen**: toevoegen of verwijderen van container exemplaren toomatch vraag handmatig of automatisch.
- **Networking**: een overlaynetwerk bieden voor het coördineren van containers toocommunicate over meerdere hostmachines.
- **Servicedetectie**: inschakelen containers toolocate elkaar automatisch zelfs als ze worden verplaatst tussen hostmachines en IP-adressen wijzigen.
- **Coördinatie toepassingsupgrades**: container upgrades tooavoid toepassing uitvaltijd te beheren en terugdraaien als er iets mis gaat.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orchestration met exemplaren van Azure-Container: een gelaagde benadering.

Azure Containerexemplaren Hiermee een tooorchestration beheerslaag bieden alle Hallo planning- en beheermogelijkheden vereist toorun een enkele container en tegelijkertijd orchestrator platforms toomanage container meerdere taken toe.

Omdat alle Hallo onderliggende infrastructuur voor exemplaren van de Container door Azure wordt beheerd, heeft een orchestrator-platform tooconcern zelf bij het zoeken van een geschikte host-machine op welke toorun een enkele container niet nodig. Hallo elasticiteit van Hallo cloud zorgt ervoor dat een altijd beschikbaar is. In plaats daarvan kunt Hallo orchestrator zich richten op Hallo-taken die het Hallo-ontwikkeling van meerdere container architecturen, met inbegrip van schalen en gecoördineerde upgrades vereenvoudigen.



## <a name="potential-scenarios"></a>Mogelijke scenario 's

Orchestrator-integratie met Azure Containerexemplaren is nog steeds opkomende, verwachten we dat er een paar verschillende omgevingen kunnen ontstaan:

### <a name="orchestration-of-container-instances-exclusively"></a>Orchestration van Containerexemplaren uitsluitend

Omdat ze snel starten en door Hallo factureren tweede, een omgeving met uitsluitend op op basis van exemplaren van Azure-Container biedt de snelste manier tooget Hallo gestart en toodeal met maximaal variabele werkbelastingen.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinatie van Containerexemplaren en Containers in virtuele Machines

Voor langdurige wordt stabiele werkbelastingen, organiseren containers in een cluster toegewezen virtuele machines doorgaans goedkoper dan Hallo dezelfde containers uitgevoerd met exemplaren van de Container. Containerexemplaren bieden echter een uitstekende oplossing voor het snel uitbreiden en verdragsluitende uw algehele capaciteit toodeal met onverwachte of tijdelijke pieken in gebruik. In plaats van het aantal virtuele machines in uw cluster Hallo uitbreiden, vervolgens extra containers op die computers implementeert, Hallo orchestrator kunt gewoon Hallo extra containers met instanties van de Container plannen en verwijderen wanneer ze zijn geen meer nodig.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Voorbeeldimplementatie: Azure Container exemplaren-Connector voor Kubernetes

toodemonstrate hoe container orchestration platforms met Azure Containerexemplaren integreren kunnen, hebben we gebouw gestart een [voorbeeld-connector voor Kubernetes][aci-connector-k8s]. 

Hallo connector voor Kubernetes lijkt op Hallo [kubelet] [ kubelet-doc] door te registreren als een knooppunt met onbeperkte capaciteit en tijdens het verzenden van Hallo maken van [gehele product] [ pod-doc] als containergroepen in Azure Containerexemplaren. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Connectors voor andere orchestrators kunnen die op dezelfde manier worden geïntegreerd met platform primitieven toocombine Hallo power van Hallo orchestrator API met Hallo snelheid en eenvoud van het beheer van containers in Azure Containerexemplaren worden gebouwd.

> [!WARNING]
> Hallo ACI connector voor Kubernetes is *experimentele* en mag niet worden gebruikt in productie.

## <a name="next-steps"></a>Volgende stappen

Uw eerste container maken met Azure Container-exemplaren die gebruikmaken van Hallo [snelstartgids](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/