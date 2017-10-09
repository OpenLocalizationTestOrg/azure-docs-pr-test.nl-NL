---
title: aaaConvert XML-gegevens met transformaties - Azure Logic Apps | Microsoft Docs
description: Maken van transformaties of mapps tooconvert XML-gegevens tussen indelingen in logic apps met behulp van Hallo Enterprise Integration-SDK
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Enterprise-integratie met XML-transformaties
## <a name="overview"></a>Overzicht
Hallo Enterprise integration transformatie connector worden gegevens van de ene indeling tooanother indeling geconverteerd. Bijvoorbeeld wellicht hebt u een binnenkomend bericht Hallo met huidige datum in Hallo YearMonthDay indeling. U kunt een transformatie tooreformat Hallo datum toobe hello MonthDayYear indeling.

## <a name="what-does-a-transform-do"></a>Wat is een transformatie?
Een transformatie die ook wel bekend als een kaart, bestaat uit een bron-XML-schema (hello invoer) en een doel-XML-schema (Hallo uitvoer). Kunt u verschillende ingebouwde functies toohelp manipuleren of onder uw beheer Hallo gegevens, waaronder tekenreeksmanipulatie, voorwaardelijke toewijzingen, aritmetische expressies, datum tijd formatters en zelfs lussen constructies.

## <a name="how-toocreate-a-transform"></a>Hoe een transformatie toocreate?
U kunt een transformatie/map maken met behulp van Visual Studio Hallo [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas). Wanneer u bent klaar te maken en te testen Hallo transformatie, moet u Hallo transformatie toegang tot je account integratie uploaden. 

## <a name="how-toouse-a-transform"></a>Hoe toouse transformatie
Nadat u Hallo transformatie/kaart naar uw integratie-account uploaden, kunt u deze toocreate een logische app. Hallo logische app uitgevoerd uw transformaties wanneer Hallo logische app wordt geactiveerd (en er is invoer inhoud die toobe getransformeerd moet).

**Hier vindt u Hallo stappen toouse transformatie**:

### <a name="prerequisites"></a>Vereisten

* Een integratie-account maken en toevoegen van een kaart tooit  

Nu u hebt gezorgd voor Hallo vereisten, is het tijd toocreate uw logische app:  

1. Een logische app maken en [tooyour integratie account een koppeling](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink een integratie account tooa logische app meer") die Hallo kaart bevat.
2. Voeg een **aanvragen** trigger tooyour logische app  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Hallo toevoegen **XML-transformatie** actie selecteren **een actie toevoegen**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Voer Hallo word *transformeren* in Hallo zoeken vak toofilter alle acties toohello een gewenste toouse Hallo  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Selecteer Hallo **XML-transformatie** actie   
6. Hallo XML toevoegen **inhoud** die u transformeren. U kunt een XML-gegevens die u in Hallo HTTP-aanvraag als Hallo ontvangt **inhoud**. Selecteer in dit voorbeeld Hallo hoofdtekst van Hallo HTTP-aanvraag die Hallo logische app heeft geactiveerd.
7. Selecteer Hallo-naam van Hallo **kaart** die u wilt dat toouse tooperform Hallo transformatie. Hallo-kaart moet al in uw account integratie. In een eerdere stap hebt u al uw logische app access tooyour integratie-account dat de kaart bevat gegeven.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Sla uw werk  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

Op dit moment bent u klaar instellen van de kaart. U kunt in een toepassing concrete toostore Hallo getransformeerd gegevens in een LOB-toepassing zoals SalesForce. U kunt eenvoudig als actie toosend Hallo uitvoer Hallo tooSalesforce transformeren. 

U kunt nu de transformatie testen door het maken van een aanvraag toohello HTTP-eindpunt.  

## <a name="features-and-use-cases"></a>Functies en gebruiksvoorbeelden
* Hallo-transformatie die zijn gemaakt in een kaart kan eenvoudig, zoals het kopiëren van een naam en adres van een document tooanother zijn. Of u complexere transformaties Hallo out-of-the-box-kaart bewerkingen kunt maken.  
* Meerdere bewerkingen van de kaart of functies zijn direct beschikbaar is, met inbegrip van tekenreeksen, Datum tijdfuncties, enzovoort.  
* U kunt een kopie van de gegevens direct tussen Hallo schema's kunt doen. In Hallo die toewijzen in Hallo SDK is opgenomen, is dit net zo eenvoudig als een lijn die Hallo-elementen in Hallo gegevensbronschema regenereren met hun collega's in doelschema Hallo verbindt.  
* Wanneer u een toewijzing maakt, weergave u een grafische van Hallo-kaart, waarin alle Hallo relaties en koppelingen die u maakt.
* Hallo Test kaart functie tooadd een bericht van de XML-voorbeeld gebruiken. U kunt met een enkele klik Hallo kaart hebt gemaakt Zie Hallo gegenereerde uitvoer testen.  
* Bestaande maps uploaden  
* Biedt ondersteuning voor Hallo XML-indeling.

## <a name="learn-more"></a>Meer informatie
* [Meer informatie over Enterprise Integration Pack Hallo](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [Meer informatie over maps](../logic-apps/logic-apps-enterprise-integration-maps.md "meer informatie over enterprise integration maps")  

