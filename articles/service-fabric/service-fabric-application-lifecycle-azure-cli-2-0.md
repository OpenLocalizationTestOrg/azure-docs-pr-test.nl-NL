---
title: Beheren van Azure Service Fabric-toepassingen met Azure CLI 2.0
description: Informatie over het implementeren en toepassingen van een Azure Service Fabric-cluster verwijderen met behulp van Azure CLI 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Een Azure Service Fabric-toepassing te beheren met behulp van Azure CLI 2.0

Informatie over het maken en verwijderen van toepassingen die worden uitgevoerd in een Azure Service Fabric-cluster.

## <a name="prerequisites"></a>Vereisten

* Installeer Azure CLI 2.0. Selecteer vervolgens uw Service Fabric-cluster. Zie voor meer informatie [aan de slag met Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* Een Service Fabric-toepassingspakket gereed om te worden geïmplementeerd hebben. Lees voor meer informatie over het maken en een toepassing pakket over de [Service Fabric-toepassingsmodel](service-fabric-application-model.md).

## <a name="overview"></a>Overzicht

Voer deze stappen voor het implementeren van een nieuwe toepassing:

1. Upload een toepassingspakket naar het archief van de Service Fabric-installatiekopie.
2. Een toepassingstype inrichten.
3. Geef op en maak een toepassing.
4. Geef en services maken.

Een bestaande toepassing te verwijderen door deze stappen te voltooien:

1. Verwijder de toepassing.
2. Het type van de bijbehorende inrichting.
3. Verwijder de inhoud van de store.

## <a name="deploy-a-new-application"></a>Een nieuwe toepassing implementeren

Voer de volgende taken voor het implementeren van een nieuwe toepassing.

### <a name="upload-a-new-application-package-to-the-image-store"></a>Een nieuw toepassingspakket uploaden naar de image store

Voordat u een toepassing maakt, moet u het toepassingspakket uploaden naar het archief van de Service Fabric-installatiekopie. 

Bijvoorbeeld, als uw toepassingspakket is in de `app_package_dir` directory, de volgende opdrachten gebruiken voor het uploaden van de map:

```azurecli
az sf application upload --path ~/app_package_dir
```

Voor grote toepassingpakketten, kunt u de `--show-progress` optie om de voortgang van het uploaden van de weer te geven.

### <a name="provision-the-application-type"></a>Het toepassingstype inrichten

Wanneer het uploaden is voltooid, richt u de toepassing. Gebruik de volgende opdracht voor het inrichten van de toepassing:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

De waarde voor `application-type-build-path` is de naam van de map waar u uw toepassingspakket geüpload.

### <a name="create-an-application-from-an-application-type"></a>Maak een toepassing van een toepassingstype

Nadat u de toepassing inricht, moet u de volgende opdracht gebruiken een naam en het maken van uw toepassing:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`de naam die u wilt gebruiken voor het toepassingsexemplaar is. Aanvullende parameters kunt u krijgen via het eerder ingerichte toepassingsmanifest.

De toepassingsnaam moet beginnen met het voorvoegsel `fabric:/`.

### <a name="create-services-for-the-new-application"></a>Services voor de nieuwe toepassing maken

Nadat u een toepassing hebt gemaakt, kunt u services maken van de toepassing. In het volgende voorbeeld maken wordt een nieuwe staatloze service van de toepassing. De services die u van een toepassing maken kunt worden gedefinieerd in een servicemanifest in het eerder ingerichte toepassingspakket.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Controleer of de implementatie van de toepassing en status

Om te bevestigen dat een toepassing en service zijn geïmplementeerd, Controleer of de toepassing en service zijn vermeld:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

Om te controleren of de service in orde is, gelijksoortige opdrachten te gebruiken voor het ophalen van de status van de service en de toepassing:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

In orde services en toepassingen hebben een `HealthState` waarde van `Ok`.

## <a name="remove-an-existing-application"></a>Een bestaande toepassing verwijderen

Voer de volgende taken een toepassing te verwijderen.

### <a name="delete-the-application"></a>De toepassing verwijderen

Gebruik de volgende opdracht voor het verwijderen van de toepassing:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a>Het type van de inrichting

Nadat u de toepassing hebt verwijderd, kunt u het type van de inrichting als u deze niet langer nodig hebt. Als u wilt het toepassingstype inrichting, moet u de volgende opdracht gebruiken:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

De naam en type versie moeten overeenkomen met de naam en versie in de eerder ingerichte toepassingsmanifest.

### <a name="delete-the-application-package"></a>Het toepassingspakket wissen

Nadat u hebt het toepassingstype inrichting, kunt u het toepassingspakket verwijderen uit het installatiekopiearchief als u deze niet langer nodig hebt. Verwijderen van toepassingspakketten helpt Maak schijfruimte vrij. 

De om toepassingspakket te verwijderen uit het installatiekopiearchief, gebruik de volgende opdracht:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`moet de naam van de map die u hebt geüpload wanneer u de toepassing gemaakt.

## <a name="related-articles"></a>Verwante artikelen:

* [Aan de slag met Service Fabric en Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Aan de slag met Service Fabric XPlat CLI](service-fabric-azure-cli.md)
