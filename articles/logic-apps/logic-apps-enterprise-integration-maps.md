---
title: aaaTransform XML met maps XSLT - Azure Logic Apps | Microsoft Docs
description: XSLT tootransform XML-gegevens met Azure Logic Apps en Enterprise Integration Pack Hallo toewijst toevoegen
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Toewijzingen voor transformatie van XML-gegevens toevoegen

Enterprise integration maakt gebruik van maps tootransform XML-gegevens tussen indelingen. Een kaart is een XML-document dat wordt gedefinieerd op Hallo gegevens in een document dat moet worden omgezet in een andere indeling. 

## <a name="why-use-maps"></a>Waarom maps gebruiken?

Stel dat u regelmatig ontvangt B2B orders of facturen van een klant die Hallo YYYMMDD indeling voor datums gebruikt. Echter in uw organisatie slaat u datums Hallo MMDDYYY indeling. U kunt een kaart te gebruiken*transformeren* hello YYYMMDD datumnotatie in Hallo MMDDYYY voordat Hallo order of factuur informatie wordt opgeslagen in de database van de activiteit klant.

## <a name="how-do-i-create-a-map"></a>Hoe maak ik een kaart

U kunt BizTalk Integration projecten maken met de Hallo [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "meer informatie over Hallo enterprise integration pack") voor Visual Studio 2015. Vervolgens kunt u een Integratiekaart-bestand waarmee u artikelen tussen twee XML-schemabestanden visueel toewijzen. Nadat u dit project bouwen, hebt u een XSLT-document.

## <a name="how-do-i-add-a-map"></a>Hoe kan ik een kaart toevoegen

1. Selecteer in de Azure-portal hello, **Bladeren**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Voer in het zoekvak Hallo-filter, **integratie**, selecteer daarna **Integratieaccounts** uit de lijst met resultaten Hallo.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Hallo-integratie account waar u tooadd Hallo kaart wilt selecteren.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Selecteer Hallo **Maps** tegel.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Nadat het Hallo Maps blade wordt geopend, kiest u **toevoegen**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Voer een **naam** voor uw kaart. tooupload hello kaart bestand, kies Hallo mappictogram aan de rechterkant Hallo Hallo **kaart** in het tekstvak. Nadat het uploadproces Hallo is voltooid, kiest u **OK**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Nadat u Azure Hallo kaart tooyour integratie account toevoegt, krijgen het bericht op het scherm waarin u of uw toewijzingsbestand of niet is toegevoegd. Nadat u dit bericht ontvangt, kiest u Hallo **Maps** tegel zodat u kunt nieuwe Hallo bekijken toewijzing toegevoegd.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Hoe kan ik een kaart bewerken?

U moet een nieuwe toewijzingsbestand met Hallo-wijzigingen die u wilt uploaden. Hallo-kaart voor bewerken kunt u eerst downloaden.

tooupload een nieuwe kaart die wordt vervangen door de bestaande toewijzing hello, volg deze stappen.

1. Kies Hallo **Maps** tegel.

2. Nadat het Hallo Maps blade wordt geopend, selecteert u dat u wilt dat tooedit Hallo-kaart.

3. Op Hallo **Maps** blade kiezen **Update**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. Selecteer in de bestandskiezer hello, Hallo toewijzingsbestand dat u wilt dat tooupload en selecteer **Open**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Hoe een kaart toodelete?

1. Kies Hallo **Maps** tegel.

2. Nadat Hallo Maps blade wordt geopend, selecteert u de gewenste toodelete Hallo-kaart.

3. Kies **verwijderen**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. U wilt bevestigen dat toodelete Hallo-kaart.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [Meer informatie over de overeenkomsten](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
* [Meer informatie over transformaties](logic-apps-enterprise-integration-transform.md "meer informatie over enterprise integration-transformaties")  

