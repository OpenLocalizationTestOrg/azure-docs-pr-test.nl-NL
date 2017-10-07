---
title: aaaIntroduction tooAzure Containerservice voor Kubernetes | Microsoft Docs
description: Azure Container Service voor Kubernetes maakt het eenvoudig toodeploy en beheren van toepassingen op basis van een container in Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, containers, microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Inleiding tooAzure Containerservice voor Kubernetes
Azure Container Service voor Kubernetes maakt het eenvoudig toocreate, configureren en beheren van een cluster van virtuele machines die vooraf geconfigureerde toorun beperkte toepassingen zijn. Dit kunt u toouse uw bestaande vaardigheden of tekenen van een grote en groeiende hoofdtekst van de community-expertise, toodeploy en beheren van toepassingen op basis van een container op Microsoft Azure.

U kunt profiteren van Hallo bedrijfsniveau functies van Azure, zonder dat zij de toepassing draagbaarheid via Kubernetes en Docker-afbeeldingsindeling Hallo met behulp van Azure Container Service.

## <a name="using-azure-container-service-for-kubernetes"></a>Azure Container Service voor Kubernetes gebruiken
Ons doel met Azure Container Service is een container hostomgeving tooprovide met behulp van open-source hulpprogramma's en -technologieën die tegenwoordig populair onder onze klanten. einde toothis, geven we Hallo standaard Kubernetes API-eindpunten. Met behulp van deze standaard eindpunten, kunt u gebruikmaken van alle software die geschikt is voor het praten tooa Kubernetes cluster. U kunt bijvoorbeeld [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) of [draft](https://github.com/Azure/draft) gebruiken.

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Een Kubernetes-cluster maken met Azure Container Service
toobegin Azure Containerservice met een Azure Container Service-cluster met Hallo implementeren [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) of via de portal hello (zoeken Hallo Marketplace voor **Azure Container Service**). Als u een geavanceerde gebruiker die meer controle over hello Azure Resource Manager-sjablonen moet, kunt u open-source Hallo [acs-engine](https://github.com/Azure/acs-engine) project toobuild uw eigen aangepaste Kubernetes cluster en deze implementeren via Hallo `az` CLI.

### <a name="using-kubernetes"></a>Kubernetes gebruiken
Kubernetes automatiseert het implementeren, schalen en beheren van toepassingen in containers. De applicatie bevat een uitgebreide set functies, zoals:
* Automatische binpacking
* Automatisch herstel
* Horizontaal schalen
* Servicedetectie en taakverdeling
* Geautomatiseerde implementaties en terugdraaiacties
* Geheimen- en configuratiebeheer
* Opslagindeling
* Batchuitvoering

Architectuurdiagram van Kubernetes geïmplementeerd via Azure Container Service:

![Azure Container Service geconfigureerd toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Video's

Ondersteuning voor Kubernetes in Azure Container Service (Azure Friday, januari 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Hulpprogramma's voor het ontwikkelen en implementeren van toepassingen in Kubernetes (Azure OpenDev, juni 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Volgende stappen

Hallo verkennen [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin vandaag nog met het verkennen van Azure Container Service.
