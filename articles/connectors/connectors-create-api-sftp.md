---
title: aaaLearn hoe toouse SFTP-connector in uw logische apps Hallo | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met tooSFTP API toosend bestanden en ontvangen. U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Aan de slag met Hallo SFTP-connector
Gebruik Hallo SFTP connector tooaccess een toosend SFTP-account en ontvangen van bestanden. U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.  

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Verbinding maken met tooSFTP
Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service. Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.  

### <a name="create-a-connection-toosftp"></a>Een tooSFTP verbinding maken
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Gebruik een trigger SFTP
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

In dit voorbeeld Hallo **SFTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger gebruikte tooinitiate een logic app-werkstroom is wanneer een bestand wordt toegevoegd aan of gewijzigd op een SFTP-server. U ook toevoegen een voorwaarde die inhoud van de nieuwe of gewijzigde bestand Hallo Hallo gecontroleerd en maakt een beslissing tooextract Hallo-bestand als de inhoud ervan aangeven dat deze moet worden opgehaald voordat u inhoud Hallo. Ten slotte een actie tooextract Hallo inhoud van een bestand toevoegen en Hallo uitgepakt inhoud in een map op Hallo SFTP-server plaatsen. 

In een enterprise-voorbeeld: u kunt deze trigger toomonitor een SFTP-map voor nieuwe bestanden die die klantorders vertegenwoordigt.  U kunt vervolgens een actie van de connector SFTP zoals **bestandsinhoud ophalen**, tooget Hallo inhoud van Hallo order voor verdere verwerking en opslag in een orderdatabase.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Een voorwaarde toevoegen
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Gebruik een SFTP-actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Meer connectors
Ga terug toohello [API's lijst](apis-list.md).
