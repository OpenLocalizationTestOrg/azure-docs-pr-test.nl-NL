---
title: aaaPrivate Docker-container registers in Azure | Microsoft Docs
description: Inleiding toohello Azure Container Registry-service, cloud-gebaseerde, beheerde, persoonlijke Docker-registers bieden.
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Inleiding tooprivate Docker-container registers


Azure Container register is een beheerde [Docker-register](https://docs.docker.com/registry/) service op basis van Hallo open source Docker register 2.0. Maken en onderhouden van Azure container registers toostore en beheren van uw persoonlijke [Docker-container](https://www.docker.com/what-docker) installatiekopieën. Gebruik registers container in Azure met uw bestaande container ontwikkeling en implementatie pijplijnen en tekenen op Hallo hoofdtekst van de kennis van Docker-community.

Voor achtergrondinformatie over Docker en containers raadpleegt u:

* [Gebruikershandleiding voor Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Gebruiksvoorbeelden
Pull-installatiekopieën van een Azure-container register toovarious implementatie doelen:

* **Schaalbare indelingssystemen** die toepassingen in een container beheren voor verschillende hostclusters, waaronder [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) en [Kubernetes](http://kubernetes.io/docs/).
* **Azure-services** die het bouwen en uitvoeren van toepassingen op schaal ondersteunen, waaronder [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) en andere.

Ontwikkelaars kunnen ook tooa container register als onderdeel van de werkstroom van een container ontwikkeling push. Bijvoorbeeld naar een containerregister vanuit doorlopende integratie- implementatieprogramma's als [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) of [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Belangrijkste concepten
* **Register**: maak een of meerdere containerregisters in uw Azure-abonnement. Elke register wordt ondersteund door een standaard Azure [opslagaccount](../storage/common/storage-introduction.md) in Hallo dezelfde locatie. Profiteren van lokale, netwerk-sluiten opslag van uw afbeeldingen container maken in een register met Hallo dezelfde Azure-locatie als uw implementaties. De registernaam van een volledig gekwalificeerde Hallo formulier heeft `myregistry.azurecr.io`.

  U [toegangsbeheer](container-registry-authentication.md) tooa container register met behulp van een Azure Active Directory-back [service-principal](../active-directory/active-directory-application-objects.md) of een opgegeven beheerdersaccount. Voer Hallo standaard `docker login` opdracht tooauthenticate met een register.

* **Beheerd register**: een laag die meer mogelijkheden voor registers biedt, in drie SKU's: Basic, Standard en Premium. Hallo-afbeeldingen in deze SKU's worden opgeslagen in de Storage-Accounts die door Hallo registers van Azure Container service, die verbetert de betrouwbaarheid en nieuwe functies kan worden beheerd. Voorbeelden van nieuwe mogelijkheden zijn integratie van webhooks, verificatie van opslagplaats met Azure Active Directory en ondersteuning voor verwijderfunctionaliteit. Gebruikers hebben Hallo optie toochoose tussen beheerde registers of toocreate een back-up hun eigen Storage-Accounts bij het maken van registers register.

* **Opslagplaats**: een register bevat een of meer opslagplaatsen. Dit zijn groepen met containerinstallatiekopieën. Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus. Deze functie kunt u toogroup verzamelingen van installatiekopieën gerelateerde tooa specifieke app of een verzameling van apps toospecific ontwikkeling of operationele teams. Bijvoorbeeld:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` staat voor een bedrijfsbrede installatiekopie
  * `myregistry.azurecr.io/warrantydept/dotnet-build`vertegenwoordigt een installatiekopie gebruikt toobuild .NET-toepassingen, gedeeld door Hallo garantie afdeling
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`Hiermee geeft u een web-installatiekopie, gegroepeerd in Hallo klant ingediende app, die eigendom zijn van Hallo garantie afdeling

* **Installatiekopie**: installatiekopieën worden opgeslagen in een opslagplaats. Elke installatiekopie is een alleen-lezenmomentopname van een Docker-container. Azure-containerregisters kunnen zowel Windows- als Linux-installatiekopieën bevatten. U beheert de namen van de installatiekopieën voor al uw containerimplementaties. Gebruik standaard [Docker-opdrachten](https://docs.docker.com/engine/reference/commandline/) toopush afbeeldingen in een bibliotheek of een installatiekopie van een opslagplaats pull.

* **Container**: een container definieert een softwaretoepassing en de afhankelijkheden opgenomen in een compleet bestandssysteem inclusief code, runtime, systeemwerkset en bibliotheken. U kunt Docker-containers uitvoeren op basis van Windows- of Linux-installatiekopieën die u ophaalt uit een containerregister. Containers die worden uitgevoerd op één computer delen Hallo besturingssysteemkernel. Docker-containers zijn volledig mobiel tooall belangrijke Linux-distributies, Mac en Windows.




## <a name="next-steps"></a>Volgende stappen
* [Maken van een container register met hello Azure-portal](container-registry-get-started-portal.md)
* [Maken van een container register hello Azure CLI gebruiken](container-registry-get-started-azure-cli.md)
* [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
* Zie toobuild een continue integratie en werkstroom voor de implementatie met behulp van Visual Studio Team Services, Azure Container Service en Azure Container register, [in deze zelfstudie](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Als u wilt tooset van uw eigen Docker persoonlijke register in Azure (zonder een openbaar eindpunt), Zie [implementeren van uw eigen persoonlijke Docker register op Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
