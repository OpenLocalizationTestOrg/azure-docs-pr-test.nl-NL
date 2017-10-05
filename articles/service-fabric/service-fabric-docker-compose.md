---
title: Azure Service Fabric Docker Compose Preview
description: Azure Service Fabric accepteert Docker Compose indeling voor het indelen van bestaande containers met behulp van Service Fabric te vereenvoudigen. Deze ondersteuning is momenteel in preview.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Ondersteuning voor docker Compose toepassingen in Azure Service Fabric (Preview)

Maakt gebruik van docker de [docker-compose.yml](https://docs.docker.com/compose) bestand voor het definiëren van toepassingen met meerdere container. Als u eenvoudig voor klanten bekend zijn met Docker u bestaande containertoepassingen op Azure Service Fabric indeelt, hebben we preview-ondersteuning voor Docker Compose systeemeigen opgenomen in het platform. Service Fabric kan accepteren versie 3 en hoger van `docker-compose.yml` bestanden. 

Omdat deze ondersteuning in preview is, wordt alleen een subset van Compose richtlijnen ondersteund. Bijvoorbeeld: toepassingsupgrades worden niet ondersteund. U kunt echter altijd verwijderen en implementeren van toepassingen in plaats van de upgrade.

Maak het cluster wilt gebruiken deze preview, met versie 5.7 of hoger van de Service Fabric-runtime via de Azure portal samen met de bijbehorende SDK. 

> [!NOTE]
> Deze functie is Preview-versie en wordt niet ondersteund in productie.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Een bestand Docker Compose op Service Fabric implementeren

De volgende opdrachten een Service Fabric-toepassing maken (met de naam `fabric:/TestContainerApp` in het voorgaande voorbeeld), die u kunt bewaken en beheert, zoals een andere Service Fabric-toepassing. U kunt de naam van de opgegeven toepassing voor statusquery's gebruiken.

### <a name="use-powershell"></a>PowerShell gebruiken

Een opstellen voor Service Fabric-toepassing maken van een docker-compose.yml-bestand met de volgende opdracht in PowerShell:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`en `RegistryPassword` verwijzen naar de container register gebruikersnaam en wachtwoord. Nadat u de toepassing hebt voltooid, kunt u de status ervan controleren met behulp van de volgende opdracht:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

Gebruik de volgende opdracht voor het verwijderen van de toepassing opstellen via PowerShell:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Gebruik van Azure Service Fabric CLI (sfctl)

U kunt ook de volgende Service Fabric CLI-opdracht gebruiken:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Als u de toepassing hebt gemaakt, kunt u de status ervan controleren met behulp van de volgende opdracht:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Gebruik de volgende opdracht voor het verwijderen van de toepassing opstellen:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Richtlijnen voor ondersteunde opstellen

Deze preview ondersteunt een subset van de configuratieopties uit de opstellen versie 3-indeling, met inbegrip van de volgende primitieven:

* Services > implementeren > replica's
* Services > implementeren > plaatsing > beperkingen
* Services > implementeren > Resources > limieten
    * cpu-shares
    * -geheugen
    * -geheugen-swap
* Services > opdrachten
* Services > omgeving
* Services > poorten
* Services > afbeelding
* Services > isolatie (alleen voor Windows)
* Services > logboekregistratie > stuurprogramma
* Services > logboekregistratie > stuurprogramma > Opties
* Volume & implementeren > Volume

Instellen van het cluster voor het afdwingen van de resource-limieten, zoals beschreven in [Service Fabric resource governance](service-fabric-resource-governance.md). Alle andere Docker Compose richtlijnen worden niet ondersteund voor deze preview.

## <a name="servicednsname-computation"></a>ServiceDnsName berekening

Als de naam van de service die u in een bestand Compose opgeeft een volledig gekwalificeerde domeinnaam is (dat wil zeggen, bevat een punt [.]), de DNS-naam geregistreerd door het Service Fabric `<ServiceName>` (inclusief de punt). Als dat niet het geval is, moet u elk padsegment in de naam van de toepassing wordt een domeinlabel in de service DNS-naam met het eerste padsegment om het domeinlabel op het hoogste niveau.

Als de naam van de opgegeven toepassing is bijvoorbeeld `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` zou de geregistreerde DNS-naam zijn.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Verschillen tussen opstellen (exemplaar definitie) en Service Fabric-toepassingsmodel (typedefinitie)

Een docker-compose.yml-bestand wordt een implementeerbaar van containers, waaronder de eigenschappen en de configuraties beschreven.
Het bestand kan bijvoorbeeld omgevingsvariabelen en poorten bevatten. U kunt ook implementatieparameters, zoals plaatsingsbeperkingen en limieten voor DNS-namen, in de docker-compose.yml-bestand opgeven.

De [Service Fabric-toepassingsmodel](service-fabric-application-model.md) maakt gebruik van service typen en de toepassingstypen, waarbij u veel exemplaren van een toepassing van hetzelfde type kan hebben. U kunt bijvoorbeeld één exemplaar per klant hebben. Dit model op basis van het type ondersteunt meerdere versies van hetzelfde toepassingstype dat geregistreerd bij de runtime.

Bijvoorbeeld kan een klant een toepassing met het type 1.0 AppTypeA geïnstantieerd, en klant B kan een andere toepassing die zijn gemaakt met hetzelfde type en dezelfde versie hebben. Definieert u de soorten toepassingen in de Toepassingsmanifesten en u de naam en de implementatie van een toepassingsparameters opgeven wanneer u de toepassing maakt.

Dit model biedt flexibiliteit, wel we hebben ook plannen voor de ondersteuning van een eenvoudigere, op basis van het exemplaar implementatiemodel waar typen impliciete van het manifestbestand zijn. In dit model wordt elke toepassing een eigen onafhankelijk manifest. We bekijkt deze inspanningen met ondersteuning voor docker-compose.yml, dit is een implementatie op basis van een exemplaar-indeling.

## <a name="next-steps"></a>Volgende stappen

* Lees informatie over de [toepassingsmodel Service Fabric](service-fabric-application-model.md)
* [Aan de slag met Service Fabric-CLI](service-fabric-cli.md)
