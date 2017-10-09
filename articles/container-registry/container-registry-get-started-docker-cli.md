---
title: aaaPush Docker installatiekopie tooprivate Azure register | Microsoft Docs
description: "Push als pull Docker installatiekopieën tooa privé-container register in Azure met behulp van Docker CLI Hallo"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Uw eerste afbeelding tooa persoonlijke Docker-container register met Hallo Docker CLI push
Een Azure container-register worden opgeslagen en beheerd persoonlijke [Docker](http://hub.docker.com) container afbeeldingen, vergelijkbare toohello manier [Docker Hub](https://hub.docker.com/) openbare Docker-installatiekopieën worden opgeslagen. Gebruik van Hallo [Docker-opdrachtregelinterface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) voor [aanmelding](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), en andere bewerkingen op de container het register.

Zie voor meer informatie over de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)



## <a name="prerequisites"></a>Vereisten
* **Azure-containerregister**: maak een containerregister in uw Azure-abonnement. Gebruik bijvoorbeeld Hallo [Azure-portal](container-registry-get-started-portal.md) of Hallo [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Docker CLI** -tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, installeren [Docker-Engine](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Meld u bij tooa register
Voer `docker login` toolog in tooyour container register met uw [register referenties](container-registry-authentication.md).

Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md). Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Zorg ervoor dat toospecify Hallo register volledig gekwalificeerde naam (alle kleine letters). In dit voorbeeld is het `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Stappen toopull en een installatiekopie van een push
Hallo volgen downloads Hallo Nginx-installatiekopie uit Hallo openbare Docker Hub register, tags voor uw register persoonlijke Azure-container duwt deze tooyour register vervolgens opnieuw ophaalt.

**1. Pull-hallo Docker officiële installatiekopie voor Nginx**

Eerste pull hallo openbare Nginx-image tooyour lokale computer.

```
docker pull nginx
```
**2. Hallo Nginx-container starten**

Hallo volgende opdracht start Hallo lokale Nginx-container interactief op poort 8080, zodat u toosee uitvoer van Nginx. Verwijdert deze container één keer gestopt met Hallo.

```
docker run -it --rm -p 8080:80 nginx
```

Te bladeren[http://localhost: 8080](http://localhost:8080) tooview Hallo container uitgevoerd. U ziet een scherm vergelijkbare toohello volgt.

![Nginx op lokale computer](./media/container-registry-get-started-docker-cli/nginx.png)

toostop Hallo actieve container, drukt u op [CTRL] + [C].

**3. Een alias van Hallo afbeelding maken in het register**

Hallo volgende opdracht maakt u een alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register. In dit voorbeeld geeft Hallo `samples` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Push Hallo installatiekopie tooyour register**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Pull-hallo-installatiekopie uit het register**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Hallo Nginx-container starten vanuit het register**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Te bladeren[http://localhost: 8080](http://localhost:8080) tooview Hallo container uitgevoerd.

toostop Hallo actieve container, drukt u op [CTRL] + [C].

**7. (Optioneel) Hallo afbeelding verwijderen**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Gelijktijdige limieten
In sommige gevallen kan het gelijktijdig uitvoeren van aanroepen leiden tot fouten. Hallo volgende tabel bevat Hallo limieten van gelijktijdige aanroepen met 'Push' en 'Pull' bewerkingen op Azure-container registersleutel:

| Bewerking  | Limiet                                  |
| ---------- | -------------------------------------- |
| PULL       | Haalt up too10 gelijktijdige per register |
| PUSH       | Up too5 gelijktijdige pushes per register |

## <a name="next-steps"></a>Volgende stappen
Nu u weet Hallo basisbeginselen, bent u klaar toostart met behulp van het register! Bijvoorbeeld, beginnen met het implementeren van de container installatiekopieën tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.
