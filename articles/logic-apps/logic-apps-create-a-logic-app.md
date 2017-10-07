---
title: aaaCreate uw eerste werkstroom tussen cloud-apps & cloudservices - Azure Logic Apps | Microsoft Docs
description: Bedrijfsprocessen voor systeemintegratie en EAI-scenario's (Enterprise Application Integration) automatiseren door werkstromen te maken en uit te voeren in Azure Logic Apps
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: werkstroom, cloud-apps, cloudservices, bedrijfsprocessen, systeemintegratie, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Uw eerste logische app tooautomate workflowprocessen tussen cloud-apps en cloudservices maken

Zonder dat u code hoeft te schrijven, kunt u bedrijfsprocessen eenvoudiger en sneller automatiseren door werkstromen te maken en uit te voeren met [Azure Logic Apps](logic-apps-what-are-logic-apps.md). Het eerste voorbeeld ziet hoe toocreate een basic logic app-werkstroom waarmee wordt gecontroleerd of een RSS-feed voor nieuwe inhoud op een website. Wanneer nieuwe items worden weergegeven in de feed Hallo-website, verzendt Hallo logische app e-mail van een account met Outlook of Gmail.

toocreate en voer een logische app, moet u deze items:

* Een Azure-abonnement. Als u geen abonnement hebt, kunt u [beginnen met een gratis Azure-account](https://azure.microsoft.com/free/). U kunt eventueel ook direct kiezen voor [een Betalen per gebruik-abonnement](https://azure.microsoft.com/pricing/purchase-options/).

  Uw Azure-abonnement wordt gebruikt voor facturering van het gebruik van de logische app. Lees hier meer informatie over [meten van gebruik](../logic-apps/logic-apps-pricing.md) en [prijzen](https://azure.microsoft.com/pricing/details/logic-apps) voor Azure Logic Apps.

Verder zijn nog deze items nodig voor het voorbeeld:

* Een account van Outlook.com, Office 365 Outlook of Gmail

    > [!TIP]
    > Als u een persoonlijk [Microsoft-account](https://account.microsoft.com/account) hebt, beschikt u over een Outlook.com-account. Als u een werk- of schoolaccount hebt van Azure, hebt u een **Office 365 Outlook**-account.

* Een koppeling tooa van de website RSS-feed. In dit voorbeeld wordt Hallo [RSS-feed voor bovenste artikelen van Hallo CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Een trigger toevoegen voor het starten van de werkstroom

Een [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een gebeurtenis die uw logische app werkstroom start en eerste Hallo-item die behoeften van uw logische app.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").

2. Kies in het linkermenu Hallo **nieuw** > **Enterprise Integration** > **logische App** als volgt te werk:

     ![Azure Portal, Nieuw, Enterprise Integration, Logische app](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > U kunt ook **nieuw**, typt u vervolgens in het zoekvak Hallo `logic app`, en druk op Enter. Kies vervolgens **Logische app** > **Maken**.

3. Voer een naam in voor de logische app en selecteer uw Azure-abonnement. Maak of selecteer vervolgens een Azure-resourcegroep, zodat u gerelateerde Azure-resources makkelijker kunt organiseren en beheren. Ten slotte Selecteer Hallo datacenter locatie voor het hosten van uw logische app. Als u klaar bent, kiest u **pincode toodashboard** en vervolgens **maken**.

     ![Details van logische app](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Wanneer u selecteert **pincode toodashboard**, uw logische app wordt weergegeven op Hallo Azure-dashboard na de implementatie en wordt automatisch geopend. Als uw logische app niet wordt weergegeven op Hallo-dashboard op Hallo **alle resources** tegel, kiest u **meer**, en selecteer uw logische app. Of Kies op Hallo linkermenu **meer services**. Kies vervolgens **Logische apps** onder **Enterprise Integration** en selecteer dan de logische app.

4. Wanneer u uw logische app voor Hallo eerste keer opent, ziet Hallo Logic App-ontwerper voor sjablonen waarmee u tooget gestart kunt. Kies voor dit voorbeeld **Lege logische app**, zodat u de logische app helemaal zelf kunt ontwerpen.

    Hallo Logic App-ontwerper wordt geopend en ziet u beschikbare services en *triggers* die u in uw logische app kunt gebruiken.

5. Typ in het zoekvak Hallo `RSS`, en selecteert u deze trigger: **RSS - wanneer een item van de feed wordt gepubliceerd** 

    ![RSS-trigger](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Hallo-koppeling voor RSS-feed Hallo-website die u wilt dat tootrack invoeren. 

     U kunt ook andere waarden opgeven voor **Frequentie** en **Interval**. 
     Deze instellingen bepalen hoe vaak de logische app op nieuwe items controleert. Alle gevonden items tijdens die periode worden geretourneerd.

     In dit voorbeeld gaan we Controleer voor elke dag voor bovenste artikelen geboekt toohello CNN website.

     ![Trigger instellen met RSS-feed, frequentie en interval](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Sla uw werk nu op. (Op Hallo designer opdrachtbalk, kiest u **opslaan**.)

   ![Uw logische app opslaan](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Als u opslaan, uw logische app live gaat, maar momenteel uw logische app alleen controleert op nieuwe items in opgegeven Hallo RSS-feed. 
   toomake nuttiger, dat we een actie die uw logische app na de trigger uitvoert toevoegen voorbeeld wordt geactiveerd.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Een actie die tooyour trigger reageert toevoegen

Een [*actie*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is een taak die wordt uitgevoerd tijdens de werkstroom voor de logische app. Nadat u een trigger tooyour logische app hebt toegevoegd, kunt u een actie tooperform bewerkingen kunt toevoegen met gegevens die zijn gegenereerd door deze trigger. In ons voorbeeld toevoegen we nu een actie die e-mailbericht verzendt wanneer nieuwe items worden weergegeven in de RSS-feed Hallo-website.

1. Kies in de ontwerpfunctie voor Hallo onder de trigger **nieuwe stap** > **een actie toevoegen** als volgt te werk:

   ![Een actie toevoegen](media/logic-apps-create-a-logic-app/add-new-action.png)

   Hallo designer toont [beschikbare connectors](../connectors/apis-list.md) zodat u een tooperform actie selecteren kunt als de trigger wordt geactiveerd.

2. Op basis van uw e-mailaccount, stappen Hallo voor Outlook of Gmail.

   * toosend e-mail van uw Outlook-account in het zoekvak hello, voer `outlook`. Kies onder **Services** **Outlook.com** voor persoonlijke Microsoft-accounts of **Office 365 Outlook** voor werk- of schoolaccount van Azure. 
   Selecteer **Een e-mail verzenden** onder **Acties**.

       ![De actie Een e-mail verzenden voor Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * toosend e-mail van uw account Gmail in het zoekvak hello, voer `gmail`. 
   Selecteer **E-mail verzenden** onder **Acties**.

       ![De actie E-mail verzenden voor Gmail](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Wanneer u wordt gevraagd om referenties, moet u aanmelden met Hallo gebruikersnaam en wachtwoord voor uw e-mailaccount. 

4. Hallo-informatie opgeven voor deze actie, zoals Hallo bestemming e-mailadres en Hallo parameters voor Hallo gegevens tooinclude in Hallo e-mailbericht, bijvoorbeeld kiezen:

   ![Selecteer gegevens tooinclude in e-mailbericht](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Als u Outlook hebt gekozen, kan uw logische app eruitzien zoals in dit voorbeeld:

    ![Logische app die klaar is](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Sla uw wijzigingen op. (Op Hallo designer opdrachtbalk, kiest u **opslaan**.)

6. U kunt de logische app nu handmatig uitvoeren om te kijken of alles werkt zoals verwacht. Kies op de ontwerpfunctie opdrachtbalk Hallo, **uitvoeren**. Anders kunt u uw logische app controleren Hallo opgegeven RSS-feed op basis van Hallo planning die u hebt ingesteld.

   Als uw logische app vindt de nieuwe items, verzendt Hallo logische app e-mailbericht met de geselecteerde gegevens. 
   Als er geen nieuwe objecten zijn gevonden, slaat uw logische app Hallo-actie die e-mailbericht verzendt.

7. Kies toomonitor en controleer uw logische app de uitgevoerd en de geschiedenis, op uw logische app-menu activeren **overzicht**.

   ![Uitvoerings- en triggergeschiedenis van de logische app controleren en bekijken](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Als u niet kunt Hallo-gegevens die u verwacht vinden, op de opdrachtbalk hello, kies **vernieuwen**.

   meer over de status van uw logische app toolearn of voer en geschiedenis of toodiagnose uw logische app activeren, Zie [problemen met uw logische app](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > De logische app wordt uitgevoerd totdat u de app uitschakelt. Kies tooturn uit uw app nu op uw logische app-menu **overzicht**. Kies op de opdrachtbalk Hallo **uitschakelen**.

U weet nu hoe u een logische app kunt maken en uitvoeren. Daarnaast hebt u geleerd hoe eenvoudig het is om werkstromen te maken voor het automatiseren van processen en hoe u cloud-apps en cloudservices kunt integreren. Allemaal zonder één regel code te hoeven schrijven.

## <a name="manage-your-logic-app"></a>Uw logische app beheren

toomanage uw app kunt u taken zoals het Hallo-status controleren, bewerken, weergeven, uitschakelen of verwijderen van uw logische app uitvoeren.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").

2. Kies op het linkermenu Hallo, **meer services**. Kies onder **Enterprise Integration** de optie **Logic Apps**. Selecteer uw logische app. 

   U vindt in Hallo logic app-menu deze beheertaken voor logic app:

   |Taak|Stappen| 
   |:---|:---| 
   | De status, uitvoeringsgeschiedenis en algemene informatie voor uw app bekijken| Kies **Overzicht**.| 
   | De app bewerken | Kies **Logic App Designer**. | 
   | De JSON-definitie van de werkstroom van uw app bekijken | Kies **Codeweergave van logische app**. | 
   | Bewerkingen bekijken die zijn uitgevoerd in uw logische app | Kies **Activiteitenlogboek**. | 
   | Eerdere versies voor uw logische app weergeven | Kies **Versies**. | 
   | Uw app tijdelijk uitschakelen | Kies **overzicht**, kiest op de opdrachtbalk Hallo **uitschakelen**. | 
   | De app verwijderen | Kies **overzicht**, kiest op de opdrachtbalk Hallo **verwijderen**. Voer de naam van de logische app in en kies **Verwijderen**. | 

## <a name="get-help"></a>Help opvragen

tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

*  [Voorwaarden toevoegen en werkstromen uitvoeren](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Sjablonen voor logische app](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Logische apps maken van Azure Resource Manager-sjablonen](../logic-apps/logic-apps-arm-provision.md)
