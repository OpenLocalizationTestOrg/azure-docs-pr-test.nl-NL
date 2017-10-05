---
title: Azure-container register opslagplaatsen | Microsoft Docs
description: "Het gebruik van Azure Container register-opslagplaatsen voor Docker-installatiekopieën"
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
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a>Register-opslagplaatsen voor Azure-container

Azure container register kunt u installatiekopieën van de container opslaan in de opslagplaatsen. Afbeeldingen in de opslagplaatsen opslaat, kunt u groepen van installatiekopieën (of de versie van afbeeldingen) in een geïsoleerde omgeving hebben. U kunt deze opslagplaatsen opgeven wanneer u push-installatiekopieën toe aan het register.


## <a name="prerequisites"></a>Vereisten
* **Azure-containerregister**: maak een containerregister in uw Azure-abonnement. Gebruik bijvoorbeeld [Azure Portal](container-registry-get-started-portal.md) of de [Azure-CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker-CLI**: installeer de [Docker-engine](https://docs.docker.com/engine/installation/) om uw lokale computer als een Docker-host in te stellen en de Docker-CLI-opdrachten te gebruiken.
* **Pull-installatiekopie van een** - Pull-een afbeelding uit het register met openbare Docker-Hub, het labelen en dit doorgeven aan het register. Voor instructies voor het pushen en installatiekopieën pull, Zie [Push Docker-installatiekopie in Azure persoonlijke register](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-the-portal"></a>Opslagplaatsen weergeven in de Portal

Zodra u installatiekopieën toe aan het register van de container gepusht hebt, kunt u een overzicht van de opslagplaatsen die als host fungeert voor de afbeeldingen in de Azure-portal.

Als u de stappen in de [Push Docker-installatiekopie in Azure persoonlijke register](container-registry-get-started-docker-cli.md) artikel, u hebt nu een Nginx-installatiekopie in het register van de container. Als onderdeel van de instructies, moet u een naamruimte voor de installatiekopie hebt opgegeven. In het onderstaande voorbeeld pushes de opdracht de installatiekopie van het NGinx naar de opslagplaats 'voorbeelden':

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus. Met deze functie kunt u verzamelingen van installatiekopieën maken die gerelateerd zijn aan een specifieke app, of verzamelingen apps die gerelateerd zijn aan specifieke ontwikkelingsteams of operationele teams. Voor meer informatie over opslagplaatsen in container registers Zie [registers voor persoonlijke Docker-container in Azure](container-registry-intro.md).

De container register-opslagplaatsen weergeven:

1. Aanmelden bij Azure Portal
2. Op de **Azure Container register** blade, selecteert u het register die u wilt onderzoeken
3. Klik op de blade register **opslagplaatsen** om een lijst weer van alle opslagplaatsen en hun afbeeldingen
4. (Optioneel) Selecteer een specifieke installatiekopie voor een overzicht van tags

![Opslagplaatsen in de portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Volgende stappen
Nu u de basisprincipes kent, kunt u uw register gaan gebruiken. Begin bijvoorbeeld met het implementeren van containerinstallatiekopieën op een [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/)-cluster.
