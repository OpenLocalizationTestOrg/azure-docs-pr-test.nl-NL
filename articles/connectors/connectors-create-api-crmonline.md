---
title: aaaConnect tooDynamics 365 (online) vanuit Azure Logic Apps | Microsoft Docs
description: Logic app werkstromen maken die Dynamics 365 (online) entiteiten via Hallo API die door de connector Hallo Dynamics 365 beheren
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Verbinding maken met tooDynamics 365 van logic app-werkstromen

Met Logic Apps kunt u verbinding maken met tooDynamics 365 (online) en nuttig business stromen die records maken, bijwerken items of een lijst met records geretourneerd. U kunt met Hallo Dynamics 365-connector:

* Bouw uw zakelijke flow op basis van Hallo gegevens die u van Dynamics 365 (online).
* Gebruik de acties die reageert en vervolgens Hallo uitvoer beschikbaar voor andere acties. Wanneer een item wordt bijgewerkt in Dynamics 365 (online), kunt u bijvoorbeeld een e-mailbericht met Office 365 verzenden.

Dit onderwerp leest u hoe een logische app toocreate die maakt een taak in Dynamics 365 wanneer een nieuwe lead in Dynamics 365 wordt gemaakt.

## <a name="prerequisites"></a>Vereisten
* Een Azure-account.
* Een account met Dynamics 365 (online).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Een taak wordt gemaakt wanneer een nieuwe lead in Dynamics 365 wordt gemaakt

1.  [Meld u aan tooAzure](https://portal.azure.com).

2.  Typ in hello Azure search `Logic apps`, en druk op ENTER.

      ![Logische Apps zoeken](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  Onder **Logic apps**, klikt u op **toevoegen**.

      ![LogicApp toevoegen](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  toocreate hello logische app, volledige Hallo **naam**, **abonnement**, **resourcegroep**, en **locatie** velden en klik vervolgens op  **Maak**.

5.  Selecteer de nieuwe logische app Hallo. Wanneer u Hallo ontvangt **implementatie is voltooid** melding, klikt u op **vernieuwen**.

6.  Onder **ontwikkelingsprogramma's**, klikt u op **Logic App-ontwerper**. Klik in de lijst met sjablonen hello, **lege logische App**.

7.  Typ in het zoekvak Hallo `Dynamics 365`. Van Hallo Dynamics 365 lijst activeert, selecteert u **Dynamics 365 – wanneer een record gemaakt**.

8.  Als u na vragen aan gebruiker toosign in tooDynamics 365, moet u dat nu doen.

9.  Voer in Hallo trigger details Hallo volgende informatie:

  * **Naam van de organisatie**. Hallo Dynamics 365 exemplaar gewenste Hallo logic app toolisten te selecteren.

  * **Naam van de entiteit**. Hallo-entiteit die u wilt dat toolisten te selecteren. Deze gebeurtenis fungeert als een trigger toostart Hallo logische app. 
  In dit overzicht **leidt** is geselecteerd.

  * **Hoe vaak wilt u toocheck voor artikelen?** Deze waarden instellen hoe vaak Hallo logische app controleert op updates gerelateerde toohello trigger. de standaardinstelling Hallo is toocheck voor elke drie minuten-updates.

    * **Frequentie**. Selecteer seconden, minuten, uren of dagen.

    * **Interval**. Hallo aantal seconden, minuten, uren of dagen dat u wilt dat toopass voordat u het volgende selectievakje Hallo invoeren.

      ![Details van de logica voor App Trigger](./media/connectors-create-api-crmonline/trigger-details.png)

10. Klik op **nieuwe stap**, en klik vervolgens op **een actie toevoegen**.

11. Typ in het zoekvak Hallo `Dynamics 365`. Selecteer in de lijst Acties Hallo **Dynamics 365: Maak een nieuwe record**.

12. Voer Hallo volgende informatie:

    * **Naam van de organisatie**. Selecteer Hallo Dynamics 365 instantie waar u Hallo stroom toocreate Hallo record. 
    U ziet dat deze instantie geen toobe Hallo dezelfde exemplaar waar Hallo gebeurtenis wordt geactiveerd vanuit.

    * **Naam van de entiteit**. Selecteer Hallo entiteit die u wilt een record toocreate wanneer Hallo gebeurtenis wordt geactiveerd. 
    In dit overzicht **taken** is geselecteerd.

13. Klik in het Hallo **onderwerp** vak dat wordt weergegeven. Uit Hallo dynamische inhoud lijst die wordt weergegeven, kunt u een van deze velden selecteren:

    * **Achternaam**. Als u dit veld voegt Hallo achternaam voor Hallo lead in het veld onderwerp Hallo voor Hallo-taak wanneer Hallo taakrecord wordt gemaakt.
    * **Onderwerp**. Als u dit veld voegt Hallo onderwerpveld voor Hallo lead in het veld onderwerp Hallo voor Hallo taak selecteert, wanneer Hallo taakrecord wordt gemaakt. 
    Klik op **onderwerp** tooadd die toohello **onderwerp** vak.

      ![Logische App maken nieuwe records details](./media/connectors-create-api-crmonline/create-record-details.png)

14. Op de werkbalk Logic App-ontwerper Hallo **opslaan**.

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. toostart hello logische App, klikt u op **uitvoeren**.

    ![Logic App-ontwerper werkbalk opslaan](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Nu een leadrecord maken in Dynamics 365 voor verkoop en uw flow in actie zien!

## <a name="set-advanced-options-for-a-logic-app-step"></a>Geavanceerde opties voor de stap van een logische app instellen

hoe toofilter gegevens in logische app stap, klikt u op toospecify **geavanceerde opties weergeven** in deze stap voegt u een filter of de volgorde door query.

U kunt bijvoorbeeld een filter-query tooget alleen actieve accounts gebruiken en sorteren op het Hallo-accountnaam. tooperform dit taak Hallo OData-filter-query invoeren `statuscode eq 1`, en selecteer **accountnaam** van Hallo lijst van dynamische inhoud. Meer informatie: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) en [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Geavanceerde opties voor logische-app](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Aanbevolen procedures voor het gebruik van geavanceerde opties

Wanneer u een veld waarde tooa toevoegt, moet u Hallo veldtype overeenkomen met of u typt u een waarde of Selecteer een waarde van het Hallo-lijst met dynamische inhoud.

Veldtype  |Hoe toouse  |Waar toofind  |Naam  |Gegevenstype  
---------|---------|---------|---------|---------
Tekstvelden|Tekstvelden vereisen een enkele regel tekst of dynamische inhoud die is een type tekstveld. Voorbeelden zijn Hallo categorie en subcategorie velden.|Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden |category |Enkele regel tekst        
Velden geheel getal | Sommige velden vereist geheel getal of dynamische inhoud die een veld van het type geheel getal is. Voorbeelden zijn percentage voltooid en duur. |Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden |PercentComplete |Geheel getal         
Datumvelden | Sommige velden vereisen een datum is opgegeven in de notatie dd-mm-jjjj of dynamische inhoud die is een veld van het type datum. Voorbeelden zijn gemaakt op, begindatum, werkelijke begindatum laatste op de tijd houdt, Werkelijk einde en vervaldatum. | Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > taak > velden |createdon |Datum en tijd
Typ velden waarvoor zowel een record-ID en lookup |Sommige velden die verwijzen naar een andere entiteitsrecord vereist zowel Hallo record-ID en het Hallo lookup-type. |Instellingen > Aanpassingen > aanpassen Hallo System > entiteiten > Account > velden  | AccountId  | Primaire sleutel

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Typ voor meer voorbeelden van de velden die vereisen een record-ID en de lookup dat
Voortbouwend op de vorige tabel hello, vindt hier u meer voorbeelden van de velden die niet met waarden die in de lijst met dynamische inhoud Hallo geselecteerd werken. Deze velden vereisen in plaats daarvan beide een lookup-ID en het recordtype in Hallo velden in PowerApps ingevoerd.  
* Eigenaar en eigenaarstype. Hallo eigenaarveld moet een geldige gebruiker of het team record-ID. Hallo Type eigenaar moet een **systemusers** of **teams**.
* De klant en het klanttype. Hallo klant veld moet een geldig account of neem contact op met de record-ID. Hallo Type eigenaar moet een **accounts** of **contactpersonen**.
* Met betrekking tot en met betrekking tot Type. Hallo met betrekking tot veld moet een geldige record-ID, zoals een account of neem contact op met de record-ID. Hallo met betrekking tot Type moet Hallo Zoektype voor Hallo-record, zoals **accounts** of **contactpersonen**.

Hallo wordt volgende taak maken actie voorbeeld een record voor een account dat overeenkomt met toohello record-ID toe te voegen toohello met betrekking tot veld van Hallo-taak.

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-account.png)

In dit voorbeeld wijst ook Hallo taak tooa specifieke gebruiker op basis van een van de gebruiker Hallo record-ID.

![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind een record-ID, van het Zie volgende sectie Hallo: *Hallo record-ID vinden*

## <a name="find-hello-record-id"></a>Hallo record-ID vinden

1. Open een record bestaat, zoals een record.

2. Op de werkbalk Acties Hallo **Pop uit** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).
U kunt ook Hallo acties op de werkbalk toocopy Hallo volledige URL in het standaard e-mailprogramma **e-MAILBERICHT een koppeling**.

   Hallo record-ID wordt weergegeven tussen Hallo 7 ter en %7 %d tekens van Hallo URL-codering.

   ![Stroom recordId en het type account](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Problemen oplossen
een mislukte stap in een logische app, weergave Hallo Statusdetails van Hallo gebeurtenis tootroubleshoot.

1. Onder **Logic Apps**, selecteer uw logische app en klik vervolgens op **overzicht**. 

   Hallo samenvattingsgebied wordt weergegeven en bevat Hallo uitvoeren status voor Hallo logische app. 

   ![Logische app uitvoeringsstatus](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview meer informatie over eventuele mislukte wordt uitgevoerd, klikt u op Hallo kan gebeurtenis. een mislukte stap tooexpand klikt u op die stap.

   ![Vouw de mislukte stap](./media/connectors-create-api-crmonline/tshoot2.png)

   Hallo Stapgegevens worden weergegeven en Hallo oorzaak van Hallo probleem kunnen oplossen.

   ![Details van de stap is mislukt](./media/connectors-create-api-crmonline/tshoot3.png)

Zie voor meer informatie over het oplossen van logische apps [logic app fouten opsporen](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/crm/). 

## <a name="next-steps"></a>Volgende stappen
Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).
