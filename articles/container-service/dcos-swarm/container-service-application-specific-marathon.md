---
title: aaaApplication of gebruikersspecifieke Marathon-service | Microsoft Docs
description: Een toepassings- of gebruikersspecifieke Marathon-service maken
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, Marathon, Micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Een toepassings- of gebruikersspecifieke Marathon-service maken
Azure Container Service voorziet in een set masterservers waarop we Apache Mesos en Marathon vooraf configureren. Deze kunnen zich gebruikte tooorchestrate uw toepassingen op Hallo-cluster, maar het beste niet toouse Hallo masterservers voor dit doel. Bijvoorbeeld Hallo configuratie van Marathon aanpassingen vereist aan te melden bij Hallo masterservers zelf en het aanbrengen van wijzigingen--dit gebruikers aangemoedigd unieke masterservers die enigszins verschillen van hello standard- en nodig toobe verzorgd beheerde en onafhankelijk van elkaar. Hallo configuratie uit te voeren door een team mogelijk ook geen Hallo optimale configuratie voor een ander team.

In dit artikel wordt uitgelegd hoe tooadd een toepassing of gebruikersspecifieke Marathon-service.

Aangezien deze service tooa één gebruiker of het team behoren wordt, worden ze gratis tooconfigure deze op een manier die ze willen. Ook zorgt Azure Container Service ervoor dat de service Hallo toorun blijft. Als het Hallo-service is mislukt, opnieuw Azure Container Service het voor u. Meestal zijn Hallo u won't zelfs niets merken van eventuele uitval.

## <a name="prerequisites"></a>Vereisten
[Implementeer een exemplaar van Azure Container Service](container-service-deployment.md) met orchestrator typen DC/OS en [Zorg dat de client verbinding maken met cluster tooyour](../container-service-connect.md). Bovendien Hallo volgende stappen.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Een toepassings- of gebruikersspecifieke Marathon-service maken
Beginnen met het maken van een JSON-configuratiebestand die Hallo-naam van de toepassingsservice Hallo dat u wilt dat toocreate definieert. Hier gebruiken we `marathon-alice` als Hallo framework naam. Hallo-bestand opslaan als ongeveer `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Gebruik vervolgens Hallo DC/OS CLI tooinstall Hallo Marathon-exemplaar met Hallo-opties die in uw configuratiebestand zijn ingesteld:

```bash
dcos package install --options=marathon-alice.json marathon
```

U ziet nu uw `marathon-alice` -service wordt uitgevoerd op het tabblad voor Hallo-Services van uw DC/OS-gebruikersinterface. Hallo gebruikersinterface worden `http://<hostname>/service/marathon-alice/` als u wilt dat tooaccess dit rechtstreeks.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Hallo DC/OS CLI tooaccess Hallo service instellen
U kunt eventueel configureren uw DC/OS CLI tooaccess deze nieuwe service met instelling Hallo `marathon.url` eigenschap toopoint toohello `marathon-alice` exemplaar als volgt:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

U kunt controleren welk exemplaar van Marathon die uw CLI met Hallo werkt `dcos config show` opdracht. U kunt terugkeren toousing uw Marathon-masterservice met de opdracht Hallo `dcos config unset marathon.url`.

