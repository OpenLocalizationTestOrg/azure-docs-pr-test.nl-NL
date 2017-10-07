---
title: virtuele machine wijzigingen aaaMonitor - Azure gebeurtenis raster & Logic Apps | Microsoft Docs
description: Controleren op wijzigingen van de configuratie in virtuele machines (VM's) met behulp van Azure Event raster en Logic Apps
keywords: Logic apps, gebeurtenis rasters, virtuele machine, VM
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Wijzigingen van de virtuele machine met Azure Event raster en Logic Apps bewaken

U kunt een geautomatiseerde starten [logic app werkstroom](../logic-apps/logic-apps-what-are-logic-apps.md) wanneer specifieke gebeurtenissen plaatsvinden in Azure-resources of resources van derden. Deze resources kunnen publiceren die gebeurtenissen tooan [Azure event raster](../event-grid/overview.md). Op zijn beurt Hallo gebeurtenis raster pushes die gebeurtenissen toosubscribers waarvoor webhooks, wachtrijen of [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) als eindpunten. Als een abonnee kunt uw logische app die gebeurtenissen uit Hallo gebeurtenis raster wachten voordat u geautomatiseerde werkstromen tooperform taken - uitvoert zonder dat u code schrijven.

Dit zijn bijvoorbeeld sommige gebeurtenissen of uitgevers toosubscribers via hello Azure gebeurtenis raster service kunnen verzenden:

* Maken, lezen, bijwerken of verwijderen van een resource. U kunt bijvoorbeeld de wijzigingen die mogelijk kosten op uw Azure-abonnement en van invloed zijn op uw factuur bewaken. 
* Toevoegen of verwijderen van een persoon van een Azure-abonnement.
* Uw app in uitvoert een bepaalde actie.
* Een nieuw bericht wordt weergegeven in een wachtrij.

Deze zelfstudie maakt een logische app waarmee wijzigingen tooa virtuele machine bewaakt en e-mailberichten over deze wijzigingen worden verzonden. Wanneer u een logische app met een gebeurtenisabonnement voor een Azure-resource maken, stromen gebeurtenissen van die bron via een gebeurtenis raster toohello logische app. Hallo-zelfstudie leert u deze logische app bouwen:

![Overzicht - monitor voor virtuele machine met de gebeurtenis raster en logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een logische app die u gebeurtenissen vanuit een raster gebeurtenis bewaakt.
> * Een voorwaarde die specifiek op wijzigingen van de virtuele machine controleert toevoegen.
> * E-mail verzenden wanneer de virtuele machine wordt gewijzigd.

## <a name="prerequisites"></a>Vereisten

* Een e-mailaccount van [elke e-provider wordt ondersteund door Azure Logic Apps](../connectors/apis-list.md), zoals Outlook van Office 365, Outlook.com of Gmail, voor het verzenden van meldingen. Deze zelfstudie maakt gebruik van Outlook van Office 365.

* Een [virtuele machine](https://azure.microsoft.com/services/virtual-machines). Als u dit nog niet hebt gedaan, maakt u een virtuele machine via een [maken van een VM-zelfstudie](https://docs.microsoft.com/azure/virtual-machines/). toomake hello virtuele machine gebeurtenissen, publiceert u [hoeft niet toodo alles anders](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Een logische app die u gebeurtenissen vanuit een raster gebeurtenis bewaakt maken

Eerst een logische app maken en toevoegen van een trigger voor de gebeurtenis raster dat Hallo resourcegroep voor uw virtuele machine bewaakt. 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com). 

2. Kies Hallo linksboven hello Azure hoofdmenu, **nieuw** > **Enterprise Integration** > **logische App**.

   ![Logische app maken](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Maak uw logische app met Hallo-instellingen die zijn opgegeven in de volgende tabel Hallo:

   ![Geef logic app-details](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Instelling | Voorgestelde waarde | Beschrijving | 
   | ------- | --------------- | ----------- | 
   | **Naam** | *{uw logica-app-naam}* | Geef een unieke logic app-naam. | 
   | **Abonnement** | *{uw Azure-abonnement}* | Selecteer Hallo hetzelfde Azure-abonnement voor alle services in deze zelfstudie. | 
   | **Resourcegroep** | *{uw-Azure-resourcegroep}* | Selecteer Hallo dezelfde Azure-resourcegroep voor alle services in deze zelfstudie. | 
   | **Locatie** | *{uw Azure-regio}* | Selecteer Hallo dezelfde regio voor alle services in deze zelfstudie. | 
   | | | 

4. Wanneer u klaar bent, selecteert u **pincode toodashboard**, en kies **maken**.

   U hebt nu een Azure-resource gemaakt voor uw logische app. 
   Nadat u Azure implementeert uw logische app, ziet Hallo Logic Apps Designer u sjablonen voor algemene patronen zodat u kunt aan de slag sneller.

   > [!NOTE] 
   > Wanneer u selecteert **pincode toodashboard**, uw logische app automatisch wordt geopend in Logic Apps Designer. U kunt anders handmatig zoeken en open uw logische app.

5. Kies nu een sjabloon voor logic Apps. Onder **sjablonen**, kies **lege logische App** zodat u uw logische app maken.

   ![Kies logic app-sjabloon](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   Hallo Logic Apps Designer ziet u nu [ *connectors* ](../connectors/apis-list.md) en [ *triggers* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) waarmee u toostart uw logische app, en ook acties kunt u kunt toevoegen na een trigger tooperform taken. Een trigger is een gebeurtenis die een logic app-exemplaar gemaakt en gestart van uw logische app-werkstroom. 
   Uw logische app moet een trigger als eerste Hallo-item.

6. Voer in het zoekvak hello, 'gebeurtenis raster' als filter. Selecteer deze trigger: **Azure gebeurtenis raster - op een gebeurtenis**

   ![Selecteer deze trigger: 'Azure gebeurtenis raster - op een gebeurtenis'](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Wanneer u wordt gevraagd, meld u aan tooAzure gebeurtenis raster met uw Azure-referenties.

   ![Meld u aan met uw Azure-referenties](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Als u bent aangemeld met een persoonlijk Microsoft-account, zoals @outlook.com of @hotmail.com, Hallo gebeurtenis raster trigger mogelijk niet correct weergegeven. Als tijdelijke oplossing kiezen [verbinding maken met de Service-Principal](/azure-resource-manager/resource-group-create-service-principal-portal.md), of als lid van hello Azure Active Directory die is gekoppeld aan uw Azure-abonnement, bijvoorbeeld verifiëren *gebruikersnaam* @emailoutlook.onmicrosoft.com.

8. Nu uw logische app toopublisher gebeurtenissen abonneren. Hallo-informatie opgeven voor uw abonnement op gebeurtenissen zoals opgegeven in de volgende tabel Hallo:

   ![Informatie opgeven voor een gebeurtenisabonnement](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Instelling | Voorgestelde waarde | Beschrijving | 
   | ------- | --------------- | ----------- | 
   | **Abonnement** | *{virtuele-machine-Azure-abonnement}* | Selecteer Hallo gebeurtenis van de uitgever van Azure-abonnement. Selecteer voor deze zelfstudie hello Azure-abonnement voor uw virtuele machine. | 
   | **Resourcetype** | Microsoft.Resources.resourceGroups | Het brontype Hallo gebeurtenis van de uitgever selecteren. Selecteer Hallo opgegeven waarde voor deze zelfstudie, zodat uw logische app alleen resourcegroepen bewaakt. | 
   | **Resourcenaam** | *{virtuele-machine-resource-group-name}* | Selecteer de resourcenaam van de uitgever van het Hallo. Selecteer de naam van de Hallo van Hallo resourcegroep voor uw virtuele machine voor deze zelfstudie. | 
   | Kies voor optionele instellingen **geavanceerde opties weergeven**. | *{Zie beschrijvingen}* | * **Filter het voorvoegsel**: voor deze zelfstudie laat u deze instelling leeg. Hallo standaardgedrag komt overeen met alle waarden. U kunt echter de voorvoegseltekenreeks opgeven als een filter, bijvoorbeeld een pad en een parameter voor een specifieke bron. <p>* **Filter achtervoegsel**: voor deze zelfstudie laat u deze instelling leeg. Hallo standaardgedrag komt overeen met alle waarden. U kunt echter een achtervoegseltekenreeks opgeven als een filter, bijvoorbeeld een bestandsnaamextensie, als u wilt dat alleen bepaalde bestandstypen.<p>* **De naam van abonnement**: Geef een unieke naam voor uw gebeurtenisabonnement. |
   | | | 

   Wanneer u bent klaar, de gebeurtenis raster trigger als volgt uitzien in dit voorbeeld:
   
   ![Raster voorbeeld-trigger Gebeurtenisdetails](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Sla uw logische app. Kies op de ontwerpfunctie werkbalk Hallo **opslaan**. details van een actie in uw logische app, kies de titelbalk van de actie Hallo toocollapse en verbergen.

   ![Uw logische app opslaan](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Wanneer u uw logische app met een gebeurtenis raster trigger opslaat, maakt Azure automatisch een gebeurtenisabonnement voor uw resource logic app tooyour geselecteerd. Dus wanneer Hallo resource een raster gebeurtenis toohello gebeurtenis publiceert, duwt die gebeurtenis raster automatisch Hallo gebeurtenis tooyour logische app. Deze gebeurtenis geactiveerd uw logische app, en vervolgens maakt en een exemplaar van Hallo werkstroom die u in deze volgende stappen definieert uitvoert.

Uw logische app is nu live en tooevents uit Hallo gebeurtenis raster luistert, maar geen reactie totdat u acties toohello werkstroom toevoegt. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Een voorwaarde waarmee wordt gecontroleerd op wijzigingen van de virtuele machine toevoegen

toorun uw logische app werkstroom alleen als een bepaalde gebeurtenis gebeurt, Voeg een voorwaarde waarmee wordt gecontroleerd of voor de virtuele machine 'schrijfbewerkingen'. Bij deze voorwaarde waar is, wordt uw logische app verzendt dat u een e-mail met meer informatie over de virtuele machine Hallo bijgewerkt.

1. In Logic App Designer Hallo gebeurtenis raster worden geactiveerd, kies onder **nieuwe stap** > **een voorwaarde toevoegen**.

   ![Een voorwaarde tooyour logic app toevoegen](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Hallo Logic App-ontwerper voegt een lege voorwaarde tooyour werkstroom, met inbegrip actie paden toofollow gebaseerd of Hallo voorwaarde waar of ONWAAR is.

   ![Lege voorwaarde](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. In Hallo **voorwaarde** Kies **bewerken in de geavanceerde modus**.
Typ deze expressie:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   De voorwaarde is nu ziet eruit als in dit voorbeeld:

   ![Lege voorwaarde](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Deze expressie controleert Hallo gebeurtenis `body` voor een `data` object waar hello `operationName` eigenschap is Hallo `Microsoft.Compute/virtualMachines/write` bewerking. 
   Meer informatie over [gebeurtenis raster gebeurtenis schema](../event-grid/event-schema.md).

3. tooprovide een beschrijving voor de voorwaarde hello, kies Hallo **weglatingstekens** (**...** ) knop op Hallo voorwaardeshape en kies vervolgens **naam**.

   > [!NOTE] 
   > Hallo bieden latere voorbeelden in deze zelfstudie ook beschrijvingen voor de stappen in Hallo logic app-werkstroom.

4. Nu kiezen **bewerken in de standaardmodus** zodat Hallo-expressie automatisch opgelost, zoals wordt weergegeven:

   ![Logic app voorwaarde](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Sla uw logische app.

## <a name="send-email-when-your-virtual-machine-changes"></a>E-mail verzenden wanneer de virtuele machine wordt gewijzigd

Voeg nu een [ *actie* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) zodat u een e-mailbericht krijgt wanneer Hallo opgegeven voorwaarde wordt voldaan.

1. In Hallo-voorwaarde **als de waarde true** Kies **een actie toevoegen**.

   ![Actie voor wanneer de voorwaarde waar is toevoegen](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Voer in het zoekvak hello, 'e' als filter. Op basis van uw e-mailprovider, zoek en selecteer overeenkomende Hallo-connector. Selecteer vervolgens 'e-mail verzenden' Hallo-actie voor de connector. Bijvoorbeeld: 

   * Voor een Azure werk- of schoolaccount, selecteer Hallo Outlook van Office 365-connector. 
   * Selecteer Hallo Outlook.com-connector voor persoonlijke Microsoft-accounts. 
   * Selecteer Hallo Gmail-connector voor Gmail-accounts. 

   We zullen toocontinue met Hallo Outlook van Office 365-connector. 
   Als u een andere provider gebruikt, blijven stappen Hallo Hallo dezelfde, maar uw gebruikersinterface mogelijk anders weergegeven. 

   ![Selecteer actie 'e-mail verzenden'](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Als u nog een verbinding voor uw e-mailprovider hebt, aanmelden tooyour e-mailaccount wanneer er voor de verificatie wordt gevraagd.

4. Informatie opgeven voor e-mailbericht Hallo zoals opgegeven in de volgende tabel Hallo:

   ![Lege e-mail actie](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect van velden beschikbaar zijn in de werkstroom, klikt u op in een invoervak dus die Hallo **dynamische inhoud** lijst wordt geopend, of kies **dynamische inhoud toevoegen**. Voor meer velden kiezen **Zie voor meer informatie** voor elke sectie in het Hallo-lijst. Hallo tooclose **dynamische inhoud** Kies **dynamische inhoud toevoegen**.

   | Instelling | Voorgestelde waarde | Beschrijving | 
   | ------- | --------------- | ----------- | 
   | **Aan** | *{ontvanger e-mailadres}* |Hallo ontvanger van e-mailadres invoeren. U kunt uw eigen e-mailadres gebruiken voor testdoeleinden. | 
   | **Onderwerp** | Resource bijgewerkt: **onderwerp**| Hallo-inhoud voor onderwerp Hallo e-mailadres invoeren. Voer voor deze zelfstudie Hallo voorgestelde tekst en selecteer Hallo-gebeurtenis **onderwerp** veld. Hier bevat uw e-onderwerp de naam van de Hallo voor Hallo bijgewerkt resource (virtuele machine). | 
   | **Hoofdtekst** | Resourcegroep: **onderwerp** <p>Gebeurtenistype: **gebeurtenistype**<p>Gebeurtenis-ID: **ID**<p>Tijd: **tijd van gebeurtenis** | Hallo-inhoud voor hoofdtekst Hallo e-mailadres invoeren. Voer voor deze zelfstudie Hallo voorgestelde tekst en selecteer Hallo-gebeurtenis **onderwerp**, **gebeurtenistype**, **ID**, en **gebeurtenistijd** velden zodat uw e-mailbericht bevat Resourcegroepnaam hello, gebeurtenistype, tijdstempel van gebeurtenis en gebeurtenis-ID voor het Hallo-update. <p>tooadd lege regels in de inhoud, drukt u op Shift + Enter. | 
   | | | 

   > [!NOTE] 
   > Als u een veld dat een matrix vertegenwoordigt, Hallo designer voegt automatisch een **voor elk** lus rond Hallo-actie die verwijst naar Hallo matrix. Op die manier uw logische app wordt op elk matrixitem die actie uitgevoerd.

   Nu uw e-mail in te grijpen als volgt uitzien in dit voorbeeld:

   ![Selecteer uitvoer tooinclude in e-mailbericht](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   En uw klaar logische app kan eruitzien als in dit voorbeeld:

   ![Voltooide logische app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Sla uw logische app. details van elke actie in uw logische app, kies de titelbalk van de actie Hallo toocollapse en verbergen.

   ![Uw logische app opslaan](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   Uw logische app is nu live, maar wacht voor wijzigingen tooyour virtuele machine voordat u een actie uitvoert. 
   tootest uw logische app nu doorgaan met de volgende sectie toohello.

## <a name="test-your-logic-app-workflow"></a>Testen van uw logische app-werkstroom

1. uw logische app ophalen van Hallo toocheck opgegeven gebeurtenissen, uw virtuele machine bijwerken. 

   Bijvoorbeeld, u kunt de grootte van uw virtuele machine in hello Azure-portal of [vergroten of verkleinen van uw virtuele machine met Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Na enkele ogenblikken krijgt u een e-mailbericht. Bijvoorbeeld:

   ![Stuur een e-mail over de update van virtuele machine](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. tooreview hello wordt uitgevoerd en kiest u de geschiedenis van trigger voor uw logische app, op uw logische app-menu **overzicht**. tooview meer informatie over een uitvoering Hallo rij voor kiezen die worden uitgevoerd.

   ![Logische app geschiedenis wordt uitgevoerd](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. Vouw Hallo stap die u wilt dat tooreview tooview Hallo invoer en uitvoer voor elke stap. Deze informatie kunt u onderzoeken en het opsporen en oplossen in uw logische app.
 
   ![Logische app-geschiedenisdetails uitvoeren](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Gefeliciteerd, u hebt gemaakt en uitvoeren van een logische app die resource gebeurtenissen tot en met een raster gebeurtenis bewaakt en u e-mailberichten wanneer deze gebeurtenissen optreden. U hebt ook geleerd hoe eenvoudig kunt u werkstromen die processen automatiseren en het integreren van systemen en cloudservices.

## <a name="clean-up-resources"></a>Resources opschonen

Deze zelfstudie maakt gebruik van bronnen en acties uitvoert die op uw Azure-abonnement kosten. Wanneer u met het Hallo-zelfstudie en testen bent klaar, zorg er dus dat u uitschakelen of verwijderen van alle resources waarop u niet dat tooincur kosten wilt.

U kunt uw logische app van uitgevoerd en het verzenden van e-mailbericht zonder te verwijderen van Hallo app stoppen. Kies in het menu van uw app logica **overzicht**. Kies op de werkbalk Hallo **uitschakelen**.

![Uw logische app uitschakelen](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>Veelgestelde vragen

**Q**: welke andere virtuele machine controletaken kan ik uitvoeren met de gebeurtenis rasters en logic apps? </br>
**Een**: U kunt bijvoorbeeld andere configuratiewijzigingen bewaken:

* Een virtuele machine opgehaald toegangsgroepen op basis van rechten voor toegangsbeheer (RBAC).
* Wijzigingen zijn aangebracht tooa netwerkbeveiligingsgroep (NSG) op de netwerkinterface (NIC).
* Schijven voor een virtuele machine worden toegevoegd of verwijderd.
* Een openbaar IP-adres is toegewezen tooa virtuele machine NIC.

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van Event raster](../event-grid/overview.md)
* [Gebeurtenis raster concepten](../event-grid/concepts.md)
* [Snelstartgids: Maken en aangepaste gebeurtenissen met de gebeurtenis raster routeren](../event-grid/custom-event-quickstart.md)
* [Gebeurtenis raster gebeurtenis schema](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Logic app werkstromen maken met vooraf gedefinieerde sjablonen](../logic-apps/logic-apps-use-logic-app-templates.md)