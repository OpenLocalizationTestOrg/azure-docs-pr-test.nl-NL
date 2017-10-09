---
title: aaaAzure Service Fabric Docker Compose Preview
description: Azure Service Fabric-indeling toomake Docker Compose accepteert deze eenvoudiger tooorchestrate bestaande containers met behulp van Service Fabric. Deze ondersteuning is momenteel in preview.
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
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Ondersteuning voor docker Compose toepassingen in Azure Service Fabric (Preview)

Hallo maakt gebruik van docker [docker-compose.yml](https://docs.docker.com/compose) bestand voor het definiëren van toepassingen met meerdere container. toomake het eenvoudig voor klanten die bekend zijn met Docker tooorchestrate bestaande container-toepassingen op Azure Service Fabric, zijn opgenomen preview-ondersteuning voor Docker Compose systeemeigen op Hallo-platform. Service Fabric kan accepteren versie 3 en hoger van `docker-compose.yml` bestanden. 

Omdat deze ondersteuning in preview is, wordt alleen een subset van Compose richtlijnen ondersteund. Bijvoorbeeld: toepassingsupgrades worden niet ondersteund. U kunt echter altijd verwijderen en implementeren van toepassingen in plaats van de upgrade.

toouse dit voorbeeld, uw cluster hebt gemaakt met versie 5.7 of hoger van Service Fabric-runtime Hallo via hello Azure-portal samen met de Hallo SDK overeenkomt. 

> [!NOTE]
> Deze functie is Preview-versie en wordt niet ondersteund in productie.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Een bestand Docker Compose op Service Fabric implementeren

Hallo volgende opdrachten een Service Fabric-toepassing maken (met de naam `fabric:/TestContainerApp` in het voorgaande voorbeeld Hallo), die u kunt bewaken en beheert, zoals een andere Service Fabric-toepassing. U kunt de opgegeven toepassingsnaam Hallo voor statusquery's gebruiken.

### <a name="use-powershell"></a>PowerShell gebruiken

Een Service Fabric opstellen-toepassing van een docker-compose.yml-bestand maken door het uitvoeren van de volgende opdracht in PowerShell Hallo:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`en `RegistryPassword` verwijzen toohello container register gebruikersnaam en wachtwoord. Nadat u de toepassing hello hebt voltooid, kunt u de status ervan controleren met behulp van de volgende opdracht Hallo:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete Hallo opstellen toepassing via PowerShell, Hallo volgende opdracht gebruiken:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Gebruik van Azure Service Fabric CLI (sfctl)

U kunt ook Hallo na Service Fabric CLI-opdracht gebruiken:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Als u de toepassing hello hebt gemaakt, kunt u de status ervan controleren met behulp van de volgende opdracht Hallo:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

toodelete Hallo opstellen-toepassing hello volgende opdracht gebruiken:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Richtlijnen voor ondersteunde opstellen

Deze preview ondersteunt een subset van de configuratieopties Hallo van Hallo opstellen versie 3-indeling, inclusief Hallo primitieven te volgen:

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

Hallo-cluster voor het afdwingen van de resource-limieten ingesteld zoals beschreven in [Service Fabric resource governance](service-fabric-resource-governance.md). Alle andere Docker Compose richtlijnen worden niet ondersteund voor deze preview.

## <a name="servicednsname-computation"></a>ServiceDnsName berekening

Als het Hallo-servicenaam die u in een bestand Compose opgeeft is een volledig gekwalificeerde domeinnaam (dat wil zeggen, bevat een punt [.]), Hallo DNS-naam is geregistreerd door het Service Fabric is `<ServiceName>` (inclusief Hallo punt). Als dat niet het geval is, wordt elke padsegment in de naam van de toepassing hello verandert in een domeinlabel in Hallo service DNS-naam met Hallo eerste padsegment steeds Hallo topleveldomein label.

Bijvoorbeeld, als Hallo toepassingsnaam opgegeven is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` zou worden Hallo geregistreerde DNS-naam.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Verschillen tussen opstellen (exemplaar definitie) en Service Fabric-toepassingsmodel (typedefinitie)

Een docker-compose.yml-bestand wordt een implementeerbaar van containers, waaronder de eigenschappen en de configuraties beschreven.
Hallo-bestand kan bijvoorbeeld bevatten omgevingsvariabelen en poorten. U kunt ook implementatieparameters, zoals plaatsingsbeperkingen en limieten voor DNS-namen in Hallo docker-compose.yml-bestand opgeven.

Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md) servicetypen gebruikt en de toepassingstypen, waarbij u veel exemplaren van een toepassing van kan hebben Hallo hetzelfde type. U kunt bijvoorbeeld één exemplaar per klant hebben. Dit model op basis van het type ondersteunt meerdere versies van Hallo hetzelfde toepassingstype dat geregistreerd bij Hallo-runtime.

Bijvoorbeeld een klant kan een toepassing met het type 1.0 AppTypeA geïnstantieerd hebben en klant B kan een andere toepassing Hello geïnstantieerd hebben hetzelfde type en met versie. Definieert u Hallo toepassingstypen in Toepassingsmanifesten hello en u naam- en implementatie-parameters van toepassing hello opgeven wanneer u de toepassing hello maakt.

Hoewel dit model flexibiliteit biedt, zijn we ook toosupport een eenvoudigere, op basis van het exemplaar implementatiemodel waar typen impliciete van het manifestbestand Hallo zijn planning. In dit model wordt elke toepassing een eigen onafhankelijk manifest. We bekijkt deze inspanningen met ondersteuning voor docker-compose.yml, dit is een implementatie op basis van een exemplaar-indeling.

## <a name="next-steps"></a>Volgende stappen

* Lees informatie over Hallo [toepassingsmodel Service Fabric](service-fabric-application-model.md)
* [Aan de slag met Service Fabric-CLI](service-fabric-cli.md)
