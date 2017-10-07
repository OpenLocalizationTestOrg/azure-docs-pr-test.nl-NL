---
title: aaaConnect tooon-premises-bestandssystemen vanuit Azure Logic Apps | Microsoft Docs
description: Verbinding maken met lokale tooon bestandssystemen van uw werkstroom logic app via Hallo lokale gegevensgateway en File System-connector
keywords: Bestandssystemen
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Verbinding maken met lokale tooon bestandssystemen vanuit logic apps met Hallo File System-connector

Hybride cloud-verbindingen is centrale toologic apps, gegevens in dat geval toomanage en veilig toegang tot on-premises resources, uw logische apps Hallo lokale gegevensgateway kunnen gebruiken. In dit artikel wordt gedemonstreerd hoe tooconnect tooan on-premises bestandssysteem met een eenvoudige scenario: Kopieer een bestand dat geüploade tooDropbox tooa bestandsshare en vervolgens een e-mailbericht verzenden.

## <a name="prerequisites"></a>Vereisten

- Installeer en configureer Hallo nieuwste [lokale gegevensgateway](https://www.microsoft.com/download/details.aspx?id=53127).
- Hallo nieuwste lokale gegevensgateway installeren, versie 1.15.6150.1 of hoger. [Verbinding maken met toohello lokale gegevensgateway](http://aka.ms/logicapps-gateway) lijsten Hallo stappen. Hallo-gateway moet worden geïnstalleerd op een on-premises machine voordat u kunt doorgaan met de rest Hallo van Hallo stappen.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Trigger en acties voor het verbinden van bestandssysteem tooyour toevoegen

1. Een logische app maken en deze Dropbox-trigger toevoegen: **wanneer een bestand wordt gemaakt** 
2. Kies onder Hallo-trigger **doornemen** > **een actie toevoegen**. 
3. Voer in het zoekvak Hallo `file system` zodat u alle ondersteunde acties voor Hallo File System-connector kunt bekijken.

   ![Zoeken naar bestand connector](media/logic-apps-using-file-connector/search-file-connector.png)

2. Kies Hallo **Create file** actie, en maak een verbinding tooyour-bestandssysteem.

   Als u een bestaande verbinding geen hebt, bent u na vragen aan gebruiker toocreate een.

   1. Kies **verbinden via lokale gegevensgateway**. Meer eigenschappen worden weergegeven.
   2. Selecteer de hoofdmap naar het bestandssysteem.
      
       > [!NOTE]
       > Er is een fout opgetreden in de hoofdmap Hallo Hallo belangrijkste bovenliggende map, die wordt gebruikt voor het relatieve paden voor alle bestand-gerelateerde acties. U kunt een lokale map op de machine Hallo waarbij Hallo lokale data gateway is geïnstalleerd of Hallo map kan zich een netwerkshare die Hallo machine toegang heeft tot opgeven.

   3. Hallo-gebruikersnaam en wachtwoord invoeren voor Hallo-gateway.
   4. Selecteer Hallo-gateway die u eerder hebt geïnstalleerd.

       ![Configureer de verbinding](media/logic-apps-using-file-connector/create-file.png)

3. Nadat u alle Hallo gegevens verstrekken, kiest u **maken**. 

   Logic Apps configureert en test uw verbinding, om ervoor te zorgen dat connection Hallo goed werkt. 
   Als het Hallo-verbinding juist is ingesteld, ziet u opties voor het Hallo-actie die u eerder hebt geselecteerd. 
   Hallo file system-connector is nu klaar voor gebruik.

4. Opgeven dat u toocopy bestanden vanuit Dropbox toohello-hoofdmap voor uw lokale bestandsshare.

   ![Bestandsactie maken](media/logic-apps-using-file-connector/create-file-filled.png)

5. Na uw logische app kopieën Hallo-bestand toevoegen een Outlook-actie die een e-mailbericht verzendt, zodat relevante gebruikers over nieuwe Hallo-bestand weten. Hallo ontvangers, titel en hoofdtekst Hallo e-mailadres invoeren. 

   In dynamische inhoud selector hello, kunt u uitvoer van de gegevens van Hallo bestand-connector zodat u meer details toohello e kunt toevoegen.

   ![Verzenden van e-actie](media/logic-apps-using-file-connector/send-email.png)

6. Sla uw logische app. Uw app testen door een tooDropbox bestand uploaden. Hallo-bestand krijgt de gekopieerde toohello lokale bestandsshare en u ontvangt een e-mailbericht over Hallo-bewerking.

   > [!TIP] 
   > Meer informatie over hoe te[uw logische apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Gefeliciteerd, u hebt nu een werkende logische app die verbinding van tooyour on-premises bestandssysteem maken kan. Probeer een andere functionaliteiten die connector biedt, bijvoorbeeld Hallo verkennen:

- Bestand maken
- Bestanden in de map weergeven
- Bestand toevoegen
- Bestand verwijderen
- Bestandsinhoud ophalen
- Bestandsinhoud ophalen via het pad
- Ophalen van metagegevens van bestand
- De metagegevens van het bestand ophalen via het pad
- Bestanden in de hoofdmap weergeven
- Bestand bijwerken

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/fileconnector/). 

## <a name="get-help"></a>Help opvragen

tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

- [Verbinding maken met tooon-premises gegevens](../logic-apps/logic-apps-gateway-connection.md) vanuit logic apps
- Meer informatie over [integratie in de onderneming](../logic-apps/logic-apps-enterprise-integration-overview.md)
