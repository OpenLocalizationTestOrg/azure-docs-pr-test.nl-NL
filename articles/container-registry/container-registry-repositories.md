---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Register-opslagplaatsen voor Azure-container

Azure-container register kunt u toostore container afbeeldingen in de opslagplaatsen. Afbeeldingen in de opslagplaatsen opslaat, kunt u groepen van installatiekopieën (of de versie van afbeeldingen) in een geïsoleerde omgeving hebben. U kunt deze opslagplaatsen opgeven wanneer u push-installatiekopieën tooyour register.


## <a name="prerequisites"></a>Vereisten
* **Azure-containerregister**: maak een containerregister in uw Azure-abonnement. Gebruik bijvoorbeeld Hallo [Azure-portal](container-registry-get-started-portal.md) of Hallo [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, installeren [Docker-Engine](https://docs.docker.com/engine/installation/).
* **Pull-installatiekopie van een** - Pull-een afbeelding uit het register van Hallo openbare Docker-Hub, het labelen en dit tooyour register doorgeven. Voor instructies voor het pushen en installatiekopieën pull, Zie [Push Docker installatiekopie tooAzure persoonlijke register](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Opslagplaatsen in Hallo Portal weergeven

Als u installatiekopieën tooyour container register hebt gedrukt, kunt u een overzicht van Hallo-opslagplaatsen Hallo afbeeldingen in hello Azure-portal te hosten.

Als u de stappen Hallo in Hallo gevolgd [Docker Push installatiekopie tooAzure persoonlijke register](container-registry-get-started-docker-cli.md) artikel, u hebt nu een Nginx-installatiekopie in het register van de container. Als onderdeel van het Hallo-instructies, moet u een naamruimte voor de installatiekopie van het Hallo hebt opgegeven. In onderstaande Hallo voorbeeld pushes Hallo opdracht Hallo NGinx toohello 'voorbeelden' installatiekopieopslagplaats:

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus. Deze functie kunt u toogroup verzamelingen van installatiekopieën gerelateerde tooa specifieke app of een verzameling van apps toospecific ontwikkeling of operationele teams. Zie tooread meer informatie over opslagplaatsen in container-registers [registers voor persoonlijke Docker-container in Azure](container-registry-intro.md).

register-opslagplaatsen voor tooview Hallo container

1. Meld u bij toohello Azure-portal
2. Op Hallo **Azure Container register** blade, selecteer Hallo register gewenst tooinspect
3. Klik op Hallo register blade **opslagplaatsen** toosee een lijst met alle Hallo-opslagplaatsen en hun installatiekopieën
4. (Optioneel) Selecteer een specifieke installatiekopie toosee labels

![Opslagplaatsen in Hallo-portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Volgende stappen
Nu u weet Hallo basisbeginselen, bent u klaar toostart met behulp van het register! Bijvoorbeeld, beginnen met het implementeren van de container installatiekopieën tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.
