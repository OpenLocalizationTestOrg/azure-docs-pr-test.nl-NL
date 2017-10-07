---
title: oplossingen voor aaaCreate B2B - Azure Logic Apps | Microsoft Docs
description: Gegevens in logische apps met behulp van Hallo B2B-functies in Enterprise Integration Pack Hallo ontvangen
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Gegevens in logische apps met Hallo B2B-functies in Enterprise Integration Pack Hallo ontvangen

Nadat u een account voor integratie met partners en overeenkomsten maakt, bent u klaar toocreate een zakelijke toobusiness (B2B)-werkstroom voor uw logische app Hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Vereisten

toouse Hallo AS2 en X12 acties, moet u een Enterprise Integration-Account hebben. Meer informatie over [hoe toocreate een Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Een logische app maken met B2B-connectors

Volg deze stappen toocreate een B2B logische app die gebruikmaakt van Hallo AS2 en X12 acties tooreceive gegevens uit een trading partner:

1. Maak een logische app, klikt u vervolgens [Koppel uw app tooyour integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. Hallo tooadd **decoderen AS2** actie, selecteer **een actie toevoegen**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter alle acties toohello die u wilt, Voer Hallo word **as2** in het zoekvak Hallo.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Selecteer Hallo **AS2 - decoderen AS2-bericht** in te grijpen.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Hallo toevoegen **hoofdtekst** dat u wilt dat toouse als invoer. Selecteer in dit voorbeeld Hallo hoofdtekst van HTTP-aanvraag Hallo dat triggers Hallo logische app. Of typ een expressie die Hallo kopteksten in Hallo-ingangen **HEADERS** veld:

    @triggerOutputs([headers])

7. Hallo vereist toevoegen **Headers** voor AS2, kunt u vinden in de aanvraagheaders Hallo HTTP. In dit voorbeeld Hallo-headers van Hallo HTTP-aanvraag die trigger Hallo logic app selecteren.

8. Nu Hallo decoderen X12 berichtactie toevoegen. Selecteer **een actie toevoegen**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter alle acties toohello die u wilt, Voer Hallo word **x12** in het zoekvak Hallo.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Selecteer Hallo **X12-decoderen X12 bericht** in te grijpen.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. U moet nu Hallo invoer toothis actie opgeven. Deze invoer is Hallo-uitvoer van de vorige AS2-actie Hallo.

    inhoud van het werkelijke bericht Hallo is in een JSON-object en is met base64 gecodeerd, dus u een expressie als invoer Hallo opgeven moet. 
    Voer Hallo expressie in Hallo na **X12 PLATTE bestand bericht tooDECODE** invoerveld:
    
    @base64ToString(body('Decode_AS2_message')? ['AS2Message']? ['Inhoud'])

    Voeg nu stappen toodecode hello X12 gegevens ontvangen van Hallo trading partner en uitvoer van de items in een JSON-object. 
    toonotify hello partner die gegevens Hallo is ontvangen, kunt u sturen weer een antwoord met Hallo AS2 bericht Disposition melding (MDN) in een HTTP-antwoord-actie.

12. Hallo tooadd **antwoord** actie, kies **een actie toevoegen**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter alle acties toohello die u wilt, Voer Hallo word **antwoord** in het zoekvak Hallo.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Selecteer Hallo **antwoord** in te grijpen.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess MDN van uitvoer Hallo HALLO hallo **decoderen X12 bericht** actie, set Hallo antwoord **hoofdtekst** veld met deze expressie:

    @base64ToString(body('Decode_AS2_message')? ['OutgoingMdn']? ['Inhoud'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Sla uw werk op.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

U bent nu klaar uw B2B logische app in te stellen. In werkelijkheid toepassing, kunt u toostore Hallo gedecodeerd X12 gegevens in een line-of-business (LOB)-app of de gegevensopslag. tooconnect uw eigen LOB-apps en het gebruik van deze API's in uw logische app, kunt u verdere acties toevoegen of aangepaste API's schrijft.

## <a name="features-and-use-cases"></a>Functies en gebruiksvoorbeelden

* Hallo AS2 en X12 decoderen en coderen acties kunnen uitwisselen van gegevens tussen handelspartners via standaardprotocollen in logic apps.
* tooexchange gegevens met handelspartners, kunt u AS2 en X12 met of zonder elkaar.
* Hallo B2B acties kunnen u eenvoudig partners en -overeenkomsten maken in uw account integratie en gebruiken in een logische app.
* Wanneer u uw logische app met andere acties uitbreidt, kunt u deze kunt verzenden en ontvangen van gegevens tussen andere apps en services zoals SalesForce.

## <a name="learn-more"></a>Meer informatie
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md)
