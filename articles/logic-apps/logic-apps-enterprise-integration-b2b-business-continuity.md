---
title: aaaDisaster herstel voor B2B-integratie account - Azure Logic Apps | Microsoft Docs
description: Logic Apps B2B-noodherstel
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Logic Apps B2B regio-overschrijdende noodherstel

B2B-werkbelastingen hebben betrekking op geld transacties zoals orders en facturen. Tijdens een gebeurtenis na noodgevallen is het essentieel voor een zakelijke tooquickly herstellen toomeet Hallo die zakelijke serviceovereenkomsten met hun partners overeengekomen. In dit artikel laat zien hoe een zakelijke continuïteit toobuild plannen voor B2B-werkbelastingen. 

* Gereedheid voor herstel na noodgevallen 
* Toosecondary regio failover tijdens een gebeurtenis na noodgevallen 
* Tooprimary regio terugvallen na een gebeurtenis na noodgevallen

## <a name="disaster-recovery-readiness"></a>Gereedheid voor herstel na noodgevallen  

1. Een secundaire regio identificeert en maakt u een [integratie account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in Hallo secundaire regio.

2. Partners, schema's en overeenkomsten voor Hallo vereist bericht stromen waarin Hallo uitvoeringsstatus toobe gerepliceerd toosecondary regio integratie account moet toevoegen.

   > [!TIP]
   > Zorg ervoor dat er consistentie in de naamgevingsconventie Hallo integratie account artefact van tussen regio's. 

3. toopull hello status uitvoeren vanaf de primaire regio hello, een logische app maken in de secundaire regio Hallo. 

   Deze logische app moet een *trigger* en een *actie*. 
   Hallo trigger moet verbinding maken tooprimary regio integratie account moet, en Hallo actie toosecondary regio integratie-account. 
   Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio uitvoeren statustabel worden opgevraagd en haalt nieuwe records hello, indien van toepassing. Hallo actie werkt ze toosecondary regio integratie-account. 
   Dit helpt tooget incrementele runtimestatus van de primaire regio toosecondary regio.

4. Zakelijke continuïteit in Logic Apps integratie-account is ontworpen op basis van B2B-protocollen - X12, AS2 en EDIFACT toosupport. toofind gedetailleerde stappen, selecteer Hallo respectieve koppelingen.

5. Hallo aanbeveling is toodeploy alle primaire regio resources in een secundaire regio te. 

   Primaire regio resources omvatten Azure SQL Database of Azure Cosmos DB, Azure Service Bus en Azure Event Hubs gebruikt voor messaging Azure API Management en hello Azure Logic Apps-functie in Azure App Service.   

6. Stel een verbinding van een primaire regio tooa secundaire regio. toopull hello status uitvoeren vanaf een primaire regio een logische app maken in een secundaire regio. 

   Hallo logische app moet een trigger en een actie hebben. 
   Hallo trigger moet tooa primaire regio integratie-account koppelen. 
   Hallo-actie moet tooa secundaire regio integratie-account koppelen. 
   Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio uitvoeren statustabel worden opgevraagd en haalt nieuwe records hello, indien van toepassing. 
   Hallo actie werkt ze tooa secundaire regio integratie-account. 
   Dit proces helpt tooget incrementele runtimestatus van Hallo primaire regio toohello secundaire regio.

Zakelijke continuïteit in Logic Apps integratie-account biedt ondersteuning op basis van Hallo B2B-protocollen X12 en AS2, EDIFACT. Zie voor gedetailleerde stappen voor het gebruik van X12 en AS2 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) en [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in dit artikel.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>De secundaire regio tooa failover tijdens een gebeurtenis na noodgevallen

Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar voor bedrijfscontinuïteit, direct verkeer toohello secundaire regio. Een secundaire regio helpt een toorecover zakelijke functies snel toomeet hello RPO/RTO overeengekomen door partners. Ook minimaliseert uit één regio tooanother regio inspanningen toofail via. 

Er is een verwachte latentie tijdens het kopiëren van besturingselement cijfers van een primaire regio tooa secundaire regio. dubbele gegenereerde besturingselement verzenden tooavoid getallen toopartners tijdens een gebeurtenis na noodgevallen, Hallo aanbeveling tooincrement Hallo besturingselement cijfers in Hallo secundaire regio overeenkomsten met behulp van [PowerShell-cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Terugvallen tooa primaire regio na noodgevallen gebeurtenis

toofall back tooa primaire regio wanneer deze beschikbaar is, is als volgt te werk:

1. Stop de berichten van partners in Hallo secundaire regio worden geaccepteerd.  

2. Hallo gegenereerd besturingselement cijfers voor alle Hallo primaire regio overeenkomsten verhogen met behulp van [PowerShell-cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Directe verkeer van Hallo secundaire regio toohello primaire regio.

4. Controleer dat Hallo logische app gemaakt in de secundaire regio Hallo voor het ophalen van de status van uitvoeren vanaf de primaire regio Hallo is ingeschakeld.

## <a name="x12"></a>X12 

Zakelijke continuïteit voor EDI X 12 documenten is gebaseerd op het besturingselement getallen:

> [!TIP]
> U kunt ook Hallo [X12 snel starten sjabloon](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps. Maken primaire en secundaire integratieaccounts zijn vereisten toouse Hallo sjabloon. Hallo helpt sjabloon toocreate twee logic apps, één voor ontvangen besturingselement getallen en één voor de gegenereerde besturingselement cijfers. Respectieve triggers en acties worden in Hallo logic apps, Hallo trigger toohello primaire integratie account en toohello Hallo-secundaire integratie actieaccount verbinding gemaakt.

**Vereisten**

tooenable noodherstel voor inkomende berichten Selecteer Hallo dubbele controle-instellingen in instellingen voor het ontvangen van Hallo X12-overeenkomst.

![Instellingen voor controle op dubbele items selecteren](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in een secundaire regio.    

2. Zoeken op **X12**, en selecteer **X12-als een getal van het besturingselement wordt gewijzigd**.   

   ![Zoeken naar X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   Hallo trigger vraagt u een account voor verbinding tooan integratie tooestablish. 
   Hallo trigger moet worden verbonden tooa primaire regio integratie-account.

3. Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.   

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Hallo **DateTime toostart besturingselement nummer sync** instelling is optioneel. Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.   

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Selecteer **nieuwe stap** > **een actie toevoegen**.

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Zoeken op **X12**, en selecteer **X12-toevoegen of bijwerken van besturingselement cijfers**.   

   ![Toevoegen of bijwerken van besturingselement cijfers](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect tooa secundaire regio integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts. Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**. 

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.

   ![Dynamische inhoud velden](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio ontvangen besturingselement nummer tabel worden opgevraagd en haalt Hallo nieuwe records. 
   Hallo actie werkt Hallo records in Hallo secundaire regio integratie-account. 
   Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.   

   ![Besturingselement number tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Op basis van het tijdsinterval hello, Hallo incrementele runtimestatus van een primaire regio tooa secundaire regio worden gerepliceerd. Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit. 

## <a name="edifact"></a>EDIFACT 

Zakelijke continuïteit voor EDI EDIFACT documenten is gebaseerd op het besturingselement cijfers.

**Vereisten**

noodherstel tooenable voor inkomende berichten Hallo dubbele controle-instellingen te selecteren in instellingen voor het ontvangen van uw EDIFACT-overeenkomst.

![Instellingen voor controle op dubbele items selecteren](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in een secundaire regio.    

2. Zoeken op **EDIFACT**, en selecteer **EDIFACT - als een getal van het besturingselement wordt gewijzigd**.

   ![Zoeken naar EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   Hallo trigger vraagt u een account voor verbinding tooan integratie tooestablish. 
   Hallo trigger moet worden verbonden tooa primaire regio integratie-account. 

3. Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.    

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Hallo **DateTime toostart besturingselement nummer sync** instelling is optioneel. Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.    

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Selecteer **nieuwe stap** > **een actie toevoegen**.    

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Zoeken op **EDIFACT**, en selecteer **EDIFACT - toevoegen of bijwerken van besturingselement cijfers**.   

   ![Toevoegen of bijwerken van besturingselement cijfers](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect tooa secundaire regio integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts. Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**.

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.   

   ![Dynamische inhoud velden](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio ontvangen besturingselement nummer tabel worden opgevraagd en haalt Hallo nieuwe records.
   Hallo actie bijgewerkt Hallo records toohello secundaire regio integratie-account. 
   Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.

   ![Besturingselement number tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Op basis van het tijdsinterval hello, Hallo incrementele runtimestatus van een primaire regio tooa secundaire regio worden gerepliceerd. Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit. 

## <a name="as2"></a>AS2 

Zakelijke continuïteit voor documenten die gebruikmaken van Hallo AS2-protocol is gebaseerd op het Hallo-bericht-ID en Hallo MIC waarde.

> [!TIP]
> U kunt ook Hallo [AS2 snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps. Maken primaire en secundaire integratieaccounts zijn vereisten toouse Hallo sjabloon. Hallo-sjabloon kunt een logische app met een trigger en een actie maken. Hallo logische app maakt een verbinding van een trigger tooa primaire integratie-account en een actie tooa secundaire integratie-account.

1. Maak een [logische app](../logic-apps/logic-apps-create-a-logic-app.md) in Hallo secundaire regio.  

2. Zoeken op **AS2**, en selecteer **AS2 - waarde als een MIC is gemaakt**.   

   ![Zoeken naar AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Een trigger wordt u gevraagd een verbindingsaccount voor de integratie van tooan tooestablish. 
   Hallo trigger moet worden verbonden tooa primaire regio integratie-account. 
   
3. Geef de verbindingsnaam van een, selecteer uw *primaire regio integratie account* van Hallo lijst en kies **maken**.

   ![Primaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Hallo **DateTime toostart MIC waarde sync** instelling is optioneel. Hallo **frequentie** te kunnen worden ingesteld**dag**, **uur**, **minuut**, of **tweede** met een interval.   

   ![Datum/tijd- en frequentie](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Selecteer **nieuwe stap** > **een actie toevoegen**.  

   ![Nieuwe stap, een actie toevoegen](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Zoeken op **AS2**, en selecteer **AS2 - toevoegen of bijwerken van de inhoud van de MIC**.  

   ![MIC toevoegen of bijwerken](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect tooa secundaire integratie actieaccount, selecteer **verbinding wijzigen** > **nieuwe verbinding toevoegen** voor een lijst met beschikbare Hallo-integratieaccounts. Geef de verbindingsnaam van een, selecteer uw *secundaire regio integratie account* van Hallo lijst en kies **maken**.

   ![Secundaire regio integratie-accountnaam](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Tooraw invoer switch door te klikken op Hallo-pictogram in de rechterbovenhoek.

   ![Switch tooraw invoer](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Selecteer hoofdtekst van dynamische inhoud objectkiezer Hallo en Hallo logic app wordt opgeslagen.   

   ![Dynamische inhoud](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Op basis van het tijdsinterval hello, Hallo trigger Hallo primaire regio tabel worden opgevraagd en haalt Hallo nieuwe records. Hallo actie werkt ze toohello secundaire regio integratie-account. 
   Als er geen updates zijn, Hallo trigger status weergegeven als **overgeslagen**.  

   ![Primaire regio tabel](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Op basis van het tijdsinterval hello, repliceert Hallo incrementele runtimestatus van Hallo primaire regio toohello secundaire regio. Tijdens een gebeurtenis na noodgevallen wanneer Hallo primaire regio niet beschikbaar, directe verkeer toohello secundaire regio voor bedrijfscontinuïteit. 

## <a name="next-steps"></a>Volgende stappen

[B2B-berichten bewaken](logic-apps-monitor-b2b-message.md)

