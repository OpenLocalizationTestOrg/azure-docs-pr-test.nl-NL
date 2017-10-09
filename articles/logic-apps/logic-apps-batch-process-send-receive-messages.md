---
title: verwerken van berichten aaaBatch als een groep of een verzameling - Azure Logic Apps | Microsoft Docs
description: Verzenden en ontvangen van berichten voor batchverwerking in logic apps
keywords: batch, batchproces
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Verzenden, ontvangen en verwerken van berichten in logic apps batch

tooprocess berichten samen in groepen, kunt u gegevens items of berichten, tooa verzenden *batch*, en vervolgens deze items als een batch te verwerken. Deze methode is handig als u wilt ervoor gegevensitems toomake zijn gegroepeerd in een bepaalde manier en samen worden verwerkt. 

U kunt logische apps die items als een batch ontvangen met behulp van Hallo maken **Batch** trigger. Vervolgens kunt u logische apps die items tooa batch verzenden met behulp van Hallo maken **Batch** in te grijpen.

Dit onderwerp wordt beschreven hoe u een batchen oplossing kunt maken met het uitvoeren van deze taken: 

* [Maken van een logische app dat ontvangt en verzamelt items als batch](#batch-receiver). Deze 'batch ontvanger' logische app geeft Hallo batch naam en release criteria toomeet voor Hallo ontvanger logische app vrijgegeven en worden items verwerkt. 

* [Maken van een logische app die u items tooa batch verzendt](#batch-sender). Deze 'batch afzender' logische app geeft aan waar toosend-items een bestaande batch ontvanger logic app moeten. U kunt ook een unieke sleutel, zoals een klantnummer opgeven, te 'partitie' of delen, Hallo doel batch in subsets op basis van die sleutel. Op die manier worden alle items met die sleutel verzameld en verwerkt samen. 

## <a name="requirements"></a>Vereisten

toofollow in dit voorbeeld moet u deze items:

* Een Azure-abonnement. Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/). U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).

* Elementaire kennis over [hoe toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md) 

* Een e-mailaccount met een [e-provider wordt ondersteund door Azure Logic Apps](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Logic apps die berichten te als een batch ontvangen maken

Voordat u berichten tooa batch verzenden kunt, moet u eerst een 'batch ontvanger' logische app maken met de Hallo **Batch** trigger. Op die manier kunt u deze ontvanger logic app bij het maken van Hallo afzender logische app. Voor de ontvanger hello geeft u Hallo batchnaam, versie criteria en andere instellingen. 

Afzender logische apps moeten weten waar toosend items, terwijl de ontvanger logische apps tooknow alles over Hallo afzenders niet nodig.

1. In Hallo [Azure-portal](https://portal.azure.com), een logische app maken met deze naam: 'BatchReceiver' 

2. In Logic Apps Designer toevoegen Hallo **Batch** trigger uw logische app-werkstroom op te starten. Voer in het zoekvak hello, 'batch' als filter. Selecteer deze trigger: **Batch: Batch-berichten**

   ![Batch-trigger toevoegen](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Geef een naam voor de batch Hallo en Geef criteria op voor het vrijgeven van Hallo batch, bijvoorbeeld:

   * **Batch-naam**: Hallo naam die wordt gebruikt tooidentify Hallo batch, namelijk 'TestBatch' in dit voorbeeld.
   * **Aantal berichten**: het aantal berichten toohold Hallo als batch voordat vrijgegeven voor verwerking, namelijk '5' in dit voorbeeld.

   ![Geef details op Batch trigger](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Voeg een andere actie die een e-mailbericht wordt verzonden wanneer Hallo batch trigger wordt geactiveerd. Elke keer Hallo-batch heeft vijf items, Hallo logic app stuurt een e-mailbericht.

   1. Kies onder Hallo batch worden geactiveerd, **+ een nieuwe stap** > **een actie toevoegen**.

   2. Voer in het zoekvak hello, 'e' als filter.
   Op basis van uw e-mailprovider, selecteert u een e-connector.
   
      Als u een account voor werk of school hebt, Selecteer bijvoorbeeld Hallo Outlook van Office 365-connector. 
      Als u een Gmail-account hebt, selecteert u Hallo Gmail connector.

   3. Deze actie voor de connector selecteert:  **{*e-mailprovider*}-sturen een e-mail **

      Bijvoorbeeld:

      ![Selecteer de actie 'E-mailbericht verzenden' voor uw e-mailprovider](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Als u niet eerder verbinding kunt voor uw e-mailprovider maken, moet u uw e-referenties opgeven voor verificatie wanneer u wordt gevraagd. Meer informatie over [verifiëren van de referenties van uw e-mailadres](../logic-apps/logic-apps-create-a-logic-app.md).

6. Hallo eigenschappen instellen voor Hallo-actie die u zojuist hebt toegevoegd.

   * In Hallo **naar** Voer Hallo ontvanger van e-mailadres. 
   U kunt uw eigen e-mailadres gebruiken voor testdoeleinden.

   * In Hallo **onderwerp** vak wanneer hello **dynamische inhoud** lijst wordt weergegeven, selecteert u Hallo **partitienaam** veld.

     ![Selecteer 'Partitienaam' Hallo 'Dynamische inhoud' lijst](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     In een volgende sectie, kunt u opgeven dat delen doel batch Hallo in logische unieke partitiesleutel ingesteld toowhere kunt u berichten verzenden. 
     Elke set heeft een uniek nummer dat wordt gegenereerd door Hallo afzender logische app. 
     Deze mogelijkheid kunt u één batch met meerdere subsets gebruikt, en elke subset met Hallo-naam die u opgeeft.

   * In Hallo **hoofdtekst** vak wanneer hello **dynamische inhoud** lijst wordt weergegeven, selecteert u Hallo **bericht-Id** veld.

     ![Selecteer voor 'Hoofdtekst', 'bericht-Id](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Omdat het Hallo-invoer voor Hallo verzenden e-actie is een matrix, voegt Hallo designer automatisch een **voor elk** lus rond Hallo **e-mailbericht verzenden** in te grijpen. 
     Deze lus voert Hallo binnenste actie op elk item in Hallo batch. 
     Dus met Hallo batch trigger set toofive items krijgt u vijf e-mailberichten die elke keer Hallo trigger wordt geactiveerd.

7.  Nu dat u een batch ontvanger logische app hebt gemaakt, sla uw logische app.

    ![Uw logische app opslaan](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Maken van logische apps die berichten tooa batch verzenden

Maak nu een of meer logische apps die items toohello batch gedefinieerd door Hallo ontvanger logische app verzendt. Voor de afzender hello geeft u Hallo ontvanger logische app en de batchnaam van de, inhoud van het bericht en eventuele andere instellingen. Desgewenst kunt u een unieke partitie sleutel toodivide Hallo batch in subsets toocollect items met die sleutel opgeven.

Afzender logische apps moeten weten waar toosend items, terwijl de ontvanger logische apps tooknow alles over Hallo afzenders niet nodig.

1. Een andere logische app maken met deze naam: 'BatchSender'

   1. Voer in het zoekvak Hallo "recurrence" als filter. 
   Selecteer deze trigger: **schema - terugkeerpatroon**

      ![Hallo "Terugkeerpatroon plannen" trigger toevoegen](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Hallo-frequentie en interval toorun Hallo afzender logische app elke minuut instellen.

      ![Frequentie en het interval voor de trigger terugkeerpatroon ingesteld](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Voeg een nieuwe stap voor het verzenden van berichten tooa batch.

   1. Kies onder Hallo terugkeerpatroon trigger **+ een nieuwe stap** > **een actie toevoegen**.

   2. Voer in het zoekvak hello, 'batch' als filter. 

   3. Deze actie selecteert: **verzenden van berichten toobatch: Kies een werkstroom Logic Apps met batch-trigger**

      ![Selecteer 'Verzenden berichten toobatch'](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Nu uw 'BatchReceiver' logische app die u eerder hebt gemaakt, die nu wordt weergegeven als een actie selecteren.

      !['Batch ontvanger' logische app selecteren](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > Hallo-lijst bevat ook andere logic apps waarvoor de batch-triggers.

3. Hallo Batcheigenschappen instellen.

   * **Batch-naam**: de naam van de batch Hallo gedefinieerd Hallo ontvanger logische app, die 'TestBatch' in dit voorbeeld en wordt gevalideerd tijdens runtime.

     > [!IMPORTANT]
     > Zorg ervoor dat u Hallo batchnaam, die moet overeenkomen met Hallo batchnaam die opgegeven door Hallo ontvanger logische app niet te wijzigen.
     > Naam van de batch veranderende Hallo zorgt ervoor dat Hallo afzender logic app toofail.

   * **Inhoud bericht**: inhoud van het bericht dat u wilt dat toosend Hallo. 
   Voor dit voorbeeld voegen deze expressie Hallo huidige datum en tijd van toevoegingen, in het Hallo-bericht inhoud die u toohello batch verzendt:

     1. Wanneer Hallo **dynamische inhoud** lijst wordt weergegeven, kies **expressie**. 
     2. Voer Hallo expressie **utcnow()**, en kies **OK**. 

        ![Kies in 'Bericht inhoud', 'Expressie'. Voer 'utcnow()'.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Nu ingesteld op een partitie voor Hallo batch. Kies in de actie 'BatchReceiver' hello, **geavanceerde opties weergeven**.

   * **De naam van partitie**: een optionele unieke partitie sleutel toouse voor het verdelen van Hallo doel batch. Voor dit voorbeeld voegt u een expressie die een willekeurig getal tussen een en vijf genereert.
   
     1. Wanneer Hallo **dynamische inhoud** lijst wordt weergegeven, kies **expressie**.
     2. Voer deze expressie: **rand(1,6)**

        ![Instellen van een partitie voor de doel-batch](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Dit **RNG** functie genereert een getal tussen 1 en 5. 
        U zijn zodat deze batch verdelen in vijf genummerde partities, waarmee deze expressie voor het dynamisch wordt ingesteld.

   * **Bericht-Id**: een optionele bericht-id en een gegenereerde GUID wanneer leeg is. 
   In dit voorbeeld laat u dit vak leeg.

5. Sla uw logische app. Uw afzender logische app zoekt nu vergelijkbaar toothis voorbeeld:

   ![Sla uw logische app van afzender](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Uw logische apps testen

tootest uw oplossing, batchverwerking laat uw logische apps uitgevoerd voor een paar minuten. Binnenkort u begint met het ophalen van e-mailberichten in groepen van vijf, Hallo met dezelfde sleutel partitie.

Uw BatchSender logische app uitgevoerd elke minuut, genereert een willekeurig getal tussen 1 en 5 en maakt gebruik van deze gegenereerd nummer als partitiesleutel Hallo voor Hallo doel batch waarin berichten worden verzonden. Telkens wanneer Hallo batch vijf items Hello bevat dezelfde partitiesleutel uw BatchReceiver logische app wordt geactiveerd en e-mail voor elk bericht verzendt.

> [!IMPORTANT]
> Wanneer u klaar bent testen, zorg ervoor dat Hallo BatchSender logic app toostop verzenden van berichten uit te schakelen en te voorkomen dat uw postvak in overbelasting.

## <a name="next-steps"></a>Volgende stappen

* [Maken van logic app-definities met behulp van JSON](../logic-apps/logic-apps-author-definitions.md)
* [Een zonder server-App in Visual Studio met Azure Logic Apps en functies](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Afhandeling van uitzonderingen en foutenregistratie voor logic apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
