---
title: aaaManage Azure Service Fabric-toepassingen met Azure Service Fabric CLI
description: Meer informatie over hoe toepassingen toodeploy en verwijderen van een Azure Service Fabric-cluster met behulp van Azure Service Fabric CLI
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Een Azure Service Fabric-toepassing te beheren met behulp van Azure Service Fabric CLI

Meer informatie over hoe toocreate en delete-toepassingen die worden uitgevoerd in een Azure Service Fabric-cluster.

## <a name="prerequisites"></a>Vereisten

* Service Fabric CLI installeren. Selecteer vervolgens uw Service Fabric-cluster. Zie voor meer informatie [aan de slag met Service Fabric CLI](service-fabric-cli.md).

* Een Service Fabric-toepassing pakket gereed toobe geïmplementeerd hebben. Lees voor meer informatie over het tooauthor en een toepassing, pakket over Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md).

## <a name="overview"></a>Overzicht

een nieuwe toepassing toodeploy deze stappen hebt uitgevoerd:

1. Upload een pakket toohello Service Fabric installatiekopie toepassingsarchief.
2. Een toepassingstype inrichten.
3. Geef op en maak een toepassing.
4. Geef en services maken.

een bestaande toepassing tooremove deze stappen hebt uitgevoerd:

1. Hallo-toepassing verwijderen.
2. Inrichting verwijderen Hallo gekoppelde toepassingstype.
3. Hallo image store inhoud verwijderen.

## <a name="deploy-a-new-application"></a>Een nieuwe toepassing implementeren

toodeploy een nieuwe toepassing voltooid Hallo taken te volgen:

### <a name="upload-a-new-application-package-toohello-image-store"></a>Een nieuwe toepassing toohello installatiekopie pakketopslag uploaden

Voordat u een toepassing maakt, uploadt u Hallo pakket toohello Service Fabric installatiekopie toepassingsarchief.

Bijvoorbeeld, als uw toepassingspakket is in Hallo `app_package_dir` directory, gebruik Hallo opdrachten tooupload Hallo directory te volgen:

```azurecli
sfctl application upload --path ~/app_package_dir
```

Voor grote toepassingpakketten, kunt u Hallo `--show-progress` optie toodisplay Hallo voortgang van Hallo uploaden.

### <a name="provision-hello-application-type"></a>Hallo-toepassingstype inrichten

Wanneer Hallo uploaden is voltooid, inrichten Hallo-toepassing. tooprovision hello toepassing gebruik Hallo volgende opdracht:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

waarde voor Hallo `application-type-build-path` Hallo naam is van Hallo directory waar u uw toepassingspakket geüpload.

### <a name="create-an-application-from-an-application-type"></a>Maak een toepassing van een toepassingstype

Nadat u de toepassing hello inricht, na de opdracht tooname hello gebruiken en uw toepassing maken:

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`wilt u toouse voor toepassingsexemplaar Hallo Hallo-naam is. Aanvullende parameters kunt u krijgen via het eerder ingerichte toepassingsmanifest.

Hallo toepassingsnaam moet beginnen met Hallo voorvoegsel `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Services voor de nieuwe toepassing hello maken

Nadat u een toepassing hebt gemaakt, kunt u services maken van de toepassing hello. In Hallo voorbeeld te volgen, maken we een nieuwe service staatloze van onze toepassing. Hallo-services die u van een toepassing maken kunt worden gedefinieerd in een servicemanifest in Hallo eerder ingerichte toepassingspakket.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Controleer of de implementatie van de toepassing en status

tooverify alles in orde is, gebruikt u Hallo health opdrachten te volgen:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

tooverify Hallo-service is in orde, gebruikt u dezelfde opdrachten tooretrieve Hallo status van zowel Hallo-service en de toepassing:

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

In orde services en toepassingen hebben een `HealthState` waarde van `Ok`.

## <a name="remove-an-existing-application"></a>Een bestaande toepassing verwijderen

tooremove een toepassing, volledige Hallo taken te volgen:

### <a name="delete-hello-application"></a>Hallo-toepassing verwijderen

toodelete hello toepassing gebruik Hallo volgende opdracht:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Type van de toepassing hello inrichting

Nadat u de toepassing hello verwijdert, kunt u het toepassingstype Hallo inrichting als u niet langer. toounprovision toepassingstype hello, gebruik Hallo volgende opdracht:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Hallo type naam en type versie moet overeenkomen met Hallo naam en versie Hallo eerder ingerichte toepassingsmanifest.

### <a name="delete-hello-application-package"></a>Hallo-toepassingspakket wissen

Nadat u hebt het toepassingstype Hallo inrichting, kunt u Hallo toepassingspakket verwijderen uit de installatiekopieopslag Hallo als u deze niet langer nodig hebt. Verwijderen van toepassingspakketten helpt Maak schijfruimte vrij. 

Hallo toepassingspakket toodelete uit de installatiekopieopslag hello, gebruik Hallo volgende opdracht:

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`moet de naam Hallo van Hallo-directory die u tijdens het maken van de toepassing hello geüpload.

## <a name="upgrade-application"></a>Toepassing bijwerken

Na het maken van uw toepassing, kunt u herhalen Hallo dezelfde reeks stappen tooprovision een tweede versie van uw toepassing. Vervolgens kunt u met de upgrade van een Service Fabric-toepassing toorunning Hallo tweede versie van de toepassing hello overstappen. Zie voor meer informatie Hallo-documentatie op [Service Fabric-toepassingsupgrades](service-fabric-application-upgrade.md).

tooperform een upgrade eerste inrichten Hallo volgende versie van het gebruik van de toepassing hello Hallo dezelfde opdrachten als voorheen:

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

U wordt aangeraden en vervolgens een bewaakte Automatische upgrade tooperform Hallo-upgrade starten door het uitvoeren van de volgende opdracht Hallo:

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

Upgrades overschrijven bestaande parameters met welke set is opgegeven. Parameters voor de toepassing moeten worden doorgegeven als argumenten toohello opdracht upgraden, indien nodig. Parameters voor de toepassing moeten worden gecodeerd als een JSON-object.

tooretrieve parameters eerder hebt opgegeven, kunt u Hallo `sfctl application info` opdracht.

Wanneer u een upgrade van de toepassing wordt uitgevoerd, Hallo status kan worden opgehaald met de `sfctl application upgrade-status` opdracht.

Ten slotte, als een upgrade uitgevoerd wordt en toobe geannuleerd moet, kunt u Hallo `sfctl application upgrade-rollback` tooroll terug Hallo upgrade.

## <a name="next-steps"></a>Volgende stappen

* [Basisprincipes van service Fabric CLI](service-fabric-cli.md)
* [Aan de slag met Service Fabric op Linux](service-fabric-get-started-linux.md)
* [Starten van de upgrade van een Service Fabric-toepassing](service-fabric-application-upgrade.md)
