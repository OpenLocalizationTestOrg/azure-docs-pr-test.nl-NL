---
title: aaaConnect tooan on-premises SAP systeem in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooan on-premises SAP-systeem van uw werkstroom logic app via Hallo lokale gegevensgateway
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Verbinding maken met on-premises SAP-systeem tooan vanuit logic apps met Hallo SAP-connector 

Hallo lokale gegevensgateway kunt u gegevens toomanage en veilige toegang tot resources die zich on-premises. Dit onderwerp wordt beschreven hoe u verbinding kunt maken van logic apps tooan on-premises SAP-systeem. In dit voorbeeld wordt met uw logische app een IDOC via HTTP-aanvragen en stuurt Hallo antwoord terug.    

> [!NOTE]
> Huidige beperkingen: 
> - Uw logische app een time-out optreedt als u alle stappen die nodig zijn voor antwoord Hallo niet voltooid binnen de Hallo [aanvraag time-outlimiet](./logic-apps-limits-and-config.md). In dit scenario mogelijk aanvragen worden geblokkeerd. 
> - Hallo-bestandskiezer worden niet weergegeven voor alle Hallo beschikbare velden. In dit scenario kunt u paden handmatig toevoegen.

## <a name="prerequisites"></a>Vereisten

- Installeer en configureer Hallo nieuwste [lokale gegevensgateway](https://www.microsoft.com/download/details.aspx?id=53127) versie 1.15.6150.1 of hoger. [Hoe tooconnect toohello lokale gegevensgateway in een logische app](http://aka.ms/logicapps-gateway) lijsten Hallo stappen. Hallo-gateway moet worden geïnstalleerd op een on-premises machine voordat u verder kunt gaan.

- Download en installeer Hallo nieuwste SAP-clientbibliotheek op Hallo van de computer dezelfde waar u de gegevensgateway Hallo hebt geïnstalleerd. Een van volgende SAP-versies hello gebruiken: 
    - SAP-Server
        - Een SAP-Server die ondersteuning Hallo .NET-Connector (NCo) 3.0
 
    - SAP-Client
        - SAP .NET-Connector (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Triggers en acties voor het verbinden van tooyour SAP-systeem toevoegen

Hallo SAP-connector heeft acties, maar geen triggers. Dus hebben we toouse een andere trigger op Hallo Hallo workflow is gestart. 

1. Hallo aanvraag/antwoord-trigger toevoegen en selecteer vervolgens **nieuwe stap**.

2. Selecteer **een actie toevoegen**, en selecteer vervolgens Hallo SAP-connector door te typen `SAP` in Hallo zoekveld:    

     ![SAP-toepassingsserver of SAP berichtenserver selecteren](media/logic-apps-using-sap-connector/sap-action.png)

3. Selecteer [ **SAP-toepassingsserver** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) of [ **SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), op basis van uw SAP-instellingen. Als u een bestaande verbinding geen hebt, bent u na vragen aan gebruiker toocreate een.

   1. Selecteer **verbinden via lokale gegevensgateway**, en geef Hallo-gegevens voor uw SAP-systeem:   

       ![Verbinding tekenreeks tooSAP toevoegen](media/logic-apps-using-sap-connector/picture2.png)  

   2. Onder **Gateway**, selecteer een bestaande gateway of een nieuwe gateway tooinstall, selecteert u **Gateway installeren**.

        ![Een nieuwe gateway installeren](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Nadat u alle Hallo gegevens invoeren, selecteert u **maken**. 
   Logic Apps configureert en test de verbinding hello, om ervoor te zorgen dat connection Hallo goed werkt.

4. Voer een naam voor uw SAP-verbinding.

5. Hallo verschillende SAP-opties zijn nu beschikbaar. toofind uw IDOC categorie, selecteert u een van de lijst Hallo. Of typ handmatig Hallo pad, en selecteer Hallo HTTP-antwoord in Hallo **hoofdtekst** veld:

     ![SAP-actie](media/logic-apps-using-sap-connector/picture3.png)

6. Voeg Hallo-actie voor het maken van een **HTTP-antwoord**. Hallo response-bericht moet van Hallo SAP-uitvoer.

7. Sla uw logische app. Testen door een IDOC via HTTP Hallo trigger URL verzenden. Na Hallo die IDOC wordt verzonden, wacht u Hallo reactie van Hallo logische app:   

     > [!TIP]
     > Te zoeken over[uw logische Apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Hallo SAP-connector is tooyour logische app toegevoegd, start u de andere functionaliteiten verkennen:

- BAPI
- RFC

## <a name="get-help"></a>Help opvragen

tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe toovalidate, transformeren en andere functies BizTalk-achtige in Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Verbinding maken met tooon-premises gegevens](../logic-apps/logic-apps-gateway-connection.md) vanuit logic apps
