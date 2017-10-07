---
title: aaaManage integratie artefact metagegevens - account Azure Logic Apps | Microsoft Docs
description: Toevoegen of artefact metagegevens ophalen uit integratieaccounts voor Azure Logic Apps
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>De metagegevens van de artefacten in integratieaccounts voor logic apps beheren

U kunt aangepaste metagegevens voor artefacten in integratieaccounts definiëren en ophalen van metagegevens tijdens de runtime voor uw logische app. Bijvoorbeeld, kunt u metagegevens voor artefacten zoals partners, overeenkomsten, schema's en maps - alle sleutelwaarde-paren met metagegevens opslaan. Momenteel artefacten metagegevens via de gebruikersinterface kunnen niet worden gemaakt, maar u kunt met behulp van REST-API's toocreate metagegevens. tooadd metagegevens wanneer u maakt of selecteert u een partner, een overeenkomst of een schema in hello Azure-portal, kies **bewerken als JSON**. tooretrieve artefact metagegevens in logic apps, kunt u Hallo integratie Account artefact Lookup-functie.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Metagegevens tooartifacts in integratieaccounts toevoegen

1. Maak een [integratie account](logic-apps-enterprise-integration-create-integration-account.md).

2. Toevoegen van een artefact tooyour integratie-account, bijvoorbeeld, een [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [overeenkomst](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), of [schema](logic-apps-enterprise-integration-schemas.md).

3.  Hallo artefact selecteert, kiest u **bewerken als JSON**, en voer de details van de metagegevens.

    ![Voer de metagegevens](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Ophalen van metagegevens van artefacten voor logic apps

1. Maak een [logische app](logic-apps-create-a-logic-app.md).

2. Maak een [koppeling van uw logische app tooyour integratie account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. In Logic App-ontwerper, voegt u een trigger zoals *aanvragen* of *HTTP* tooyour logische app.

4.  Kies **doornemen** > **een actie toevoegen**. Zoeken naar *integratie* zodat u kunt zoeken naar en selecteer vervolgens **integratie Account - integratie Account artefact Lookup**.

    ![Selecteer integratie Account artefact Lookup](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Selecteer Hallo **artefact Type**, en geef Hallo **artefact naam**.

    ![Selecteer artefact type en geef de naam van het artefact](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Voorbeeld: Ophalen partner metagegevens

Partner metagegevens bevat deze `routingUrl` details:

![Partner 'routingURL' metagegevens vinden](media/logic-apps-enterprise-integration-metadata/image6.png)

1. Voeg de trigger in uw logische app, een **integratie Account - integratie Account artefact Lookup** actie voor uw partner en een **HTTP**.

    ![Trigger, artefacten opzoeken en 'HTTP' tooyour logische app toevoegen](media/logic-apps-enterprise-integration-metadata/image4.png)

2. tooretrieve hello URI, gaat u tooCode weergeven voor uw logische app. De definitie van de logische app moet eruitzien als in dit voorbeeld:

    ![Zoeken zoeken](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over de overeenkomsten](logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
