---
title: 'Zelfstudie: Verwerken EDIFACT facturen met behulp van Azure BizTalk Services | Microsoft Docs'
description: Hoe toocreate en Hallo vak Connector of API-app configureren en deze gebruiken in een logische app in Azure App Service
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Zelfstudie: Proces EDIFACT facturen met Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

U kunt gebruiken Hallo BizTalk Services-Portal tooconfigure en implementeren van X12 en EDIFACT-overeenkomsten. In deze zelfstudie bekijken we hoe toocreate een EDIFACT overeenkomst voor het uitwisselen van tussen handelspartners facturen. Deze zelfstudie is geschreven rond een end-to-end oplossing met betrekking tot twee handelspartners, Northwind en Contoso die EDIFACT berichten uitwisselen.  

## <a name="sample-based-on-this-tutorial"></a>Steekproef op basis van deze zelfstudie
Deze zelfstudie is geschreven om een steekproef **EDIFACT facturen met behulp van BizTalk-Services verzenden**, namelijk beschikbaar toodownload van Hallo [MSDN-Codegalerie](http://go.microsoft.com/fwlink/?LinkId=401005). Hallo voorbeeld te gebruiken en deze zelfstudie toounderstand doorlopen hoe Hallo voorbeeld is opgebouwd. Of u kunt gebruiken om deze zelfstudie toocreate uw eigen oplossing a t/m. Deze zelfstudie is gericht op de tweede oplossing Hallo zodat u begrijpen hoe deze oplossing is opgebouwd. Bovendien zo veel mogelijk Hallo-zelfstudie is consistent met de Hallo voorbeeld en maakt gebruik van dezelfde namen voor artefacten (bijvoorbeeld, schema's, transformaties) als in voorbeeld Hallo Hallo.  

> [!NOTE]
> Omdat deze oplossing een bericht verzenden vanuit een EAI bridge tooan EDI bridge omvat, er wordt gebruikgemaakt van Hallo [BizTalk Services Bridge chaining voorbeeld](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) voorbeeld.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Wat doet Hallo-oplossing?
In deze oplossing ontvangt Northwind EDIFACT facturen van Contoso. Deze facturen zijn niet in een standaard EDI-indeling. Dus voordat Hallo factuur tooNorthwind wordt verzonden, moet dit getransformeerde tooan EDIFACT factuur (ook wel INVOIC)-document. Ontvangen, moet Northwind Hallo EDIFACT factuur verwerken en een besturingselement bericht (ook wel CONTRL) tooContoso retourneren.

![][1]  

tooachieve hello functies van Microsoft Azure BizTalk Services maakt gebruik van deze bedrijfsscenario, Contoso.

* Contoso maakt gebruik van EAI-bruggen tootransform Hallo oorspronkelijke factuur tooEDIFACT INVOIC.
* Hallo EAI bridge verzendt vervolgens Hallo-bericht tooan EDI verzenden bridge geïmplementeerd als onderdeel van een overeenkomst is geconfigureerd in Hallo BizTalk Services-Portal.
* Hallo EDI verzenden bridge Hallo EDIFACT INVOIC verwerkt en stuurt deze tooNorthwind.
* Na de ontvangst Hallo factuur, retourneert Northwind een CONTRL bericht toohello EDI bridge geïmplementeerd als onderdeel van de overeenkomst Hallo ontvangen.  

> [!NOTE]
> Eventueel deze oplossing ook laat zien hoe toouse toosend Hallo batchverwerking facturen in batches, in plaats van elke factuur afzonderlijk sturen.  
> 
> 

toocomplete hello scenario, gebruiken we Service Bus-wachtrijen toosend factuur van Contoso tooNorthwind of bevestiging ontvangen van Northwind. Deze wachtrijen kunnen worden gemaakt met een clienttoepassing die wordt gedownload en is opgenomen in Hallo Voorbeeldpakket die beschikbaar is als onderdeel van deze zelfstudie.  

## <a name="prerequisites"></a>Vereisten
* U moet een Service Bus-naamruimte hebben. Zie voor instructies over het maken van een naamruimte [How To: maken of wijzigen van een Service Bus-Service Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx). Laat het ons wordt ervan uitgegaan dat er al een Service Bus-naamruimte die is ingericht, aangeroepen **edifactbts**.
* U moet een BizTalk Services-abonnement hebben. Zie voor instructies [een BizTalk Service met behulp van de klassieke Azure-portal maakt](http://go.microsoft.com/fwlink/?LinkID=302280). Voor deze zelfstudie laat het ons wordt ervan uitgegaan dat u hebt een abonnement van BizTalk Services, aangeroepen **contosowabs**.
* Registreer uw abonnement BizTalk Services op Hallo BizTalk Services-Portal. Zie voor instructies [registreren van een BizTalk Service-implementatie op Hallo BizTalk Services-Portal](https://msdn.microsoft.com/library/hh689837.aspx)
* Visual Studio is geïnstalleerd, moet u hebben.
* BizTalk Services SDK is geïnstalleerd, moet u hebben. U kunt downloaden Hallo SDK uit [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Stap 1: Maak Hallo Service Bus-wachtrijen
Deze oplossing maakt gebruik van Service Bus-wachtrijen tooexchange berichten tussen handelspartners. Contoso en Northwind verzenden berichten toohello wachtrijen uit waarbij Hallo EAI-en/of EDI-bruggen gebruiken. Voor deze oplossing moet u drie Service Bus-wachtrijen:

* **northwindreceive** – Northwind ontvangt Hallo factuur van Contoso via deze wachtrij.
* **contosoreceive** – Contoso ontvangt Hallo bevestiging van Northwind via deze wachtrij.
* **onderbroken** – alle berichten die onderbroken zijn gerouteerde toothis wachtrij. Berichten worden onderbroken als ze tijdens de verwerking mislukken.

U kunt deze Service Bus-wachtrijen maken met behulp van een clienttoepassing in Hallo Voorbeeldpakket opgenomen.  

1. Open in het Hallo-locatie waar u Hallo voorbeeld hebt gedownload, **zelfstudie verzenden van facturen met behulp van BizTalk Services EDI Bridges.sln**.
2. Druk op **F5** toobuild en begin Hallo **zelfstudie Client** toepassing.
3. Voer in het welkomstscherm, Hallo Service Bus ACS-naamruimte, de naam van de verlener en sleutel van verlener.
   
   ![][2]  
4. Een bericht waarin wordt gevraagd dat drie wachtrijen in uw Service Bus-naamruimte wordt gemaakt. Klik op **OK**.
5. Laat Hallo zelfstudie-Client wordt uitgevoerd. Hallo openen, klikt u op **Service Bus** > ***uw Service Bus-naamruimte*** > **wachtrijen**, en controleer of Hallo drie wachtrijen zijn gemaakt.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Stap 2: Maken en implementeren van handelspartnerovereenkomst
Maak een handelspartnerovereenkomst tussen Contoso en Northwind. Een handelspartnerovereenkomst definieert een servicecontract handel tussen twee Hallo zakelijke partners, zoals welke bericht schema-toouse die messaging protocol toouse, enzovoort. Een handelspartnerovereenkomst bevat twee EDI-bruggen, één toosend berichten tootrading partners (Hallo aangeroepen **bridge EDI verzenden**) en één tooreceive berichten van handelspartners (Hallo aangeroepen **EDI ontvangen bridge**).

In de context van de Hallo van deze oplossing, Hallo EDI verzenden over de sitekoppelingsbrug toohello verzenden aan clientzijde van de overeenkomst Hallo komt overeen en gebruikte toosend Hallo EDIFACT factuur van Contoso tooNorthwind is. Op deze manier Hallo EDI bridge ontvangen overeenkomt met toohello aan de ontvangstzijde van Hallo overeenkomst en gebruikte tooreceive bevestigingen van Northwind is.  

### <a name="create-hello-trading-partners"></a>Hallo handelspartners maken
toostart, maak handelspartners voor Contoso en Northwind.  

1. In Hallo BizTalk Services-Portal op Hallo **Partners** tabblad **toevoegen**.
2. Voer nieuwe partner pagina Hallo **Contoso** als een Partnernaam en klik vervolgens op **opslaan**.
3. Herhalingen Hallo stap toocreate Hallo tweede partner **Northwind**.  

### <a name="create-hello-agreement"></a>Hallo overeenkomst maken
Handelspartnerovereenkomsten worden gemaakt tussen bedrijven-profielen van de handelspartners. Deze oplossing gebruikt Hallo partner standaardprofielen die automatisch worden gemaakt wanneer we Hallo partners hebt gemaakt.  

1. Klik in het Hallo BizTalk Services-Portal, op **overeenkomsten** > **toevoegen**.
2. In Hallo nieuwe overeenkomst **algemene instellingen** pagina en klik vervolgens op Hallo waarden opgeven, zoals wordt weergegeven in onderstaande afbeelding voor Hallo **doorgaan**.
   
   ![][3]  
   
   Nadat u op **doorgaan**, twee tabbladen **instellingen ontvangen** en **instellingen voor verzenden** beschikbaar.
3. Hallo verzenden overeenkomst tussen Contoso en Northwind maken. Deze overeenkomst beheerst hoe Contoso Hallo EDIFACT factuur tooNorthwind verzendt.
   
   1. Klik op **verzenden instellingen**.
   2. Hallo standaardwaarden op Hallo behouden **binnenkomende URL**, **transformeren**, en **Batching** tabbladen.
   3. Op Hallo **Protocol** tabblad onder Hallo **schema's** sectie, uploadt Hallo **EFACT_D93A_INVOIC.xsd** schema. Dit schema is beschikbaar bij Hallo Voorbeeldpakket.
      
      ![][4]  
   4. Op Hallo **Transport** tabblad, Hallo details opgeven voor Hallo Service Bus-wachtrijen. Voor Hallo verzendkant overeenkomst, gebruiken we Hallo **northwindreceive** toosend Hallo EDIFACT factuur tooNorthwind wachtrij en Hallo **onderbroken** tooroute wachtrij de berichten die tijdens de verwerking en zijn mislukt onderbroken. U hebt gemaakt deze wachtrijen in **stap 1: Maak Hallo Service Bus-wachtrijen** (in dit onderwerp).
      
      ![][5]  
      
      Onder **Transport instellingen > transporttype** en **opschorten berichtinstellingen > transporttype**en selecteer Azure Service Bus Hallo waarden opgeven, zoals in afbeelding Hallo.
4. Hallo maken overeenkomst tussen Contoso en Northwind ontvangen. Deze overeenkomst beheerst hoe Contoso Hallo bevestiging van Northwind ontvangt.
   
   1. Klik op **ontvangen instellingen**.
   2. Hallo standaardwaarden op Hallo behouden **Transport** en **transformeren** tabbladen.
   3. Op Hallo **Protocol** tabblad onder Hallo **schema's** sectie, uploadt Hallo **EFACT_4.1_CONTRL.xsd** schema. Dit schema is beschikbaar bij Hallo Voorbeeldpakket.
   4. Op Hallo **Route** tabblad, maakt u een filter tooensure die alleen bevestigingen van Northwind gerouteerde tooContoso zijn. Onder **Route instellingen**, klikt u op **toevoegen** toocreate Hallo routering filter.
      
      ![][6]  
      
      1. Waarden opgeven voor **regelnaam**, **Route regel**, en **Route bestemming** zoals in afbeelding Hallo.
      2. Klik op **Opslaan**.
   5. Op Hallo **Route** tabblad opnieuw, Geef waar onderbroken bevestigingen (bevestigingen die niet voldoen aan tijdens de verwerking), worden doorgestuurd naar. Hallo transport type tooAzure Service Bus ingesteld, type bestemming te routeren**wachtrij**, typt u verificatie te**Shared Access Signature** (SAS) Hallo SAS-verbindingsreeks opgeven voor Hallo Service Bus naamruimte, en voer vervolgens de wachtrijnaam Hallo als **onderbroken**.
5. Tot slot op **implementeren** toodeploy Hallo overeenkomst. Opmerking Hallo eindpunten waar Hallo verzenden en ontvangen van overeenkomsten geïmplementeerd.
   
   * Op Hallo **instellingen voor verzenden** tabblad onder **binnenkomende URL**, houd er rekening mee Hallo-eindpunt. toosend een bericht van Contoso tooNorthwind met Hallo EDI brug verzenden, moet u het eindpunt van een bericht toothis verzenden.
   * Op Hallo **instellingen ontvangen** tabblad onder **Transport**, houd er rekening mee Hallo-eindpunt. een bericht van Northwind tooContoso met Hallo EDI toosend bridge ontvangen, moet u het eindpunt van een bericht toothis verzenden.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Stap 3: Maken en implementeren van Hallo BizTalk Services-project
In de vorige stap hello, moet u Hallo EDI verzenden en ontvangen overeenkomsten tooprocess EDIFACT facturen en bevestigingen geïmplementeerd. Deze overeenkomsten kunnen alleen berichten verwerken die toohello standaard EDIFACT berichtschema voldoen. Echter per Hallo scenario voor deze oplossing verzendt Contoso een factuur tooNorthwind in een intern bedrijfseigen schema. Dus voordat het Hallo-bericht is verzonden toohello EDI brug verzenden, moet deze worden omgezet vanuit Hallo intern schema toohello standaard EDIFACT factuur schema. Hallo BizTalk Services EAI-project biedt die.

Hallo BizTalk Services-project **InvoiceProcessingBridge**, dat transformaties bericht Hallo is ook opgenomen als onderdeel van Hallo voorbeeld die u hebt gedownload. Hallo-project bevat Hallo artefacten te volgen:

* **INHOUSEINVOICE. XSD** – Schema van Hallo intern factuur dat tooNorthwind wordt verzonden.
* **EFACT_D93A_INVOIC. XSD** – Schema van Hallo standaard EDIFACT factuur.
* **EFACT_4.1_CONTRL. XSD** – Schema van Hallo EDIFACT bevestiging dat Northwind tooContoso verzendt.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** – Hallo transformatie die Hallo intern factuur schema toohello standaard EDIFACT factuur schema wordt toegewezen.  

### <a name="create-hello-biztalk-services-project"></a>Hallo BizTalk Services-project maken
1. In Visual Studio-oplossing hello, Hallo InvoiceProcessingBridge project uitvouwen en open vervolgens Hallo **MessageFlowItinerary.bcs** bestand.
2. Klik ergens op Hallo canvas en stel Hallo **BizTalk Service-URL** Hallo in eigenschap vak toospecify de naam van uw BizTalk Services-abonnement. Bijvoorbeeld `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Vanuit de werkset Hallo Sleep een **Xml One-Way Bridge** toohello canvas. Set Hallo **entiteitnaam** en **relatief adres** eigenschappen van hello te overbruggen**ProcessInvoiceBridge**. Dubbelklik op **ProcessInvoiceBridge** tooopen Hallo bridge configuratie voor aanvallen.
4. Binnen Hallo **berichttypen** Klik Hallo plus (**+**) knop toospecify Hallo schema van het binnenkomende Hallo-bericht. Omdat Hallo inkomende bericht voor Hallo EAI bridge altijd Hallo intern factuur, stel dit in te**INHOUSEINVOICE**.
   
   ![][8]  
5. Klikt u op Hallo **XML-transformatie** vorm, en in Hallo-eigenschap voor Hallo **Maps** eigenschap, klikt u op Hallo weglatingsteken (**...** ) knop. In Hallo **Maps selectie** dialoogvenster, selecteer Hallo **INHOUSEINVOICE_to_D93AINVOIC** transformatiebestand en klik vervolgens op **OK**.
   
   ![][9]  
6. Ga terug te**MessageFlowItinerary.bcs**, en sleep vanuit de werkset Hallo een **tweerichtings externe Service-eindpunt** toohello rechts van Hallo **ProcessInvoiceBridge**. Stel de **entiteitnaam** eigenschap te**EDIBridge**.
7. Vouw in Solution Explorer hello, Hallo **MessageFlowItinerary.bcs** en dubbelklikt u op Hallo **EDIBridge.config** bestand. Hallo-inhoud van Hallo vervangen **EDIBridge.config** door Hallo volgende.
   
   > [!NOTE]
   > Waarom moet ik tooedit Hallo .config-bestand Hallo externe service-eindpunt dat we toohello bridge designer-canvas toegevoegd vertegenwoordigt Hallo EDI bruggen die we eerder hebt geïmplementeerd. EDI-bruggen zijn wederzijdse bruggen, met een verzenden en ontvangen aan clientzijde. Hallo is EAI bridge dat we toegevoegd toohello bridge designer echter een eenzijdige brug. Dus toohandle Hallo ander bericht exchange patronen van twee bruggen Hallo we gebruiken een aangepaste bridge gedrag door de configuratie in Hallo .config-bestand. Bovendien verwerkt Hallo aangepaste gedrag tevens Hallo verificatie toohello EDI verzenden bridge eindpunt. Dit gedrag is beschikbaar als een afzonderlijke voorbeeld bij [BizTalk Services Bridge chaining voorbeeld - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Deze oplossing hergebruikt Hallo-voorbeeld.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Details van Hallo EDIBridge.config bestand tooinclude configuratie bijwerken
   
   * Onder  *<behaviors>* geleverd Hallo ACS-naamruimte en sleutel die is gekoppeld aan Hallo BizTalk Services-abonnement.
   * Onder  *<client>* , bieden Hallo eindpunt waarop Hallo EDI overeenkomst verzenden wordt geïmplementeerd.
   
   Wijzigingen opslaan en sluiten Hallo-configuratiebestand.
9. Klik op Hallo van Hallo werkset, **Connector** en join Hallo **ProcessInvoiceBridge** en **EDIBridge** onderdelen. Hallo connector selecteren en in eigenschappen instellen **filtervoorwaarde** te**overeen met alle**. Dit zorgt ervoor dat alle berichten die zijn verwerkt door Hallo EAI bridge worden gerouteerd toohello EDI bridge.
   
   ![][10]  
10. Sla de wijzigingen toohello oplossing.  

### <a name="deploy-hello-project"></a>Hallo-project implementeert
1. Op Hallo-computer waarop u Hallo BizTalk Services-project hebt gemaakt, downloadt en installeert Hallo SSL-certificaat voor uw abonnement BizTalk Services. Uit, klik onder BizTalk Services op **Dashboard**, en klik vervolgens op **SSL-certificaat downloaden**. Dubbelklik op Hallo-certificaat en volg Hallo vragen toocomplete Hallo-installatie. Zorg ervoor dat u Hallo certificaat installeert in **Trusted Root Certification Authorities** certificaatarchief.
2. Klik in Visual Studio Solution Explorer met de rechtermuisknop op Hallo **InvoiceProcessingBridge** project en klik vervolgens op **implementeren**.
3. Hallo-waarden opgeven, zoals in afbeelding Hallo en klik vervolgens op **implementeren**. U kunt Hallo ACS referenties ophalen voor BizTalk Services door te klikken op **verbindingsgegevens** vanuit Hallo BizTalk Services dashboard.
   
   ![][11]  
   
   Kopiëren van het deelvenster Uitvoer hello, Hallo eindpunt waarop Hallo EAI bridge wordt geïmplementeerd, bijvoorbeeld `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. U kunt dit eindpunt-URL wordt later nodig.  

## <a name="step-4-test-hello-solution"></a>Stap 4: Testen Hallo-oplossing
In dit onderwerp kijken we hoe tootest oplossing met behulp van Hallo Hallo **zelfstudie Client** toepassing geleverd als onderdeel van het Hallo-voorbeeld.  

1. Druk in Visual Studio op F5 toostart hello **zelfstudie Client**.
2. welkomstscherm moet Hallo waarden vooraf worden ingevuld uit stap Hallo hebben waar we Hallo Service Bus-wachtrijen gemaakt. Klik op **Volgende**.
3. In het volgende venster hello, ACS-referenties opgeven voor het abonnement van BizTalk Services en eindpunten Hallo waar EAI- en EDI (ontvangen) bruggen zijn geïmplementeerd.
   
   U had Hallo EAI bridge eindpunt in de vorige stap Hallo gekopieerd. Voor EDI ontvangen over de sitekoppelingsbrug eindpunt, Hallo BizTalk Services-Portal, gaat u toohello overeenkomst > ontvangen instellingen > Transport > eindpunt.
   
   ![][12]  
4. Klik in het volgende venster hello, onder Contoso, op Hallo **intern factuur verzenden** knop. Open het dialoogvenster in Hallo bestand, Hallo INHOUSEINVOICE.txt bestand openen. Hallo-inhoud van het Hallo-bestand en klik vervolgens op **OK** toosend Hallo factuur.
   
   ![][13]  
5. In enkele seconden Hallo factuur ontvangen voor Northwind. Klik op Hallo **bericht weergeven** koppeling toosee Hallo factuur is ontvangen door Northwind. U ziet hoe Hallo factuur is ontvangen door Northwind in het schema van de standaard EDIFACT tijdens het Hallo een verzonden door Contoso is is een interne schema.
   
   ![][14]  
6. Selecteer Hallo factuur en klik vervolgens op **bevestiging verzenden**. U ziet dat Hallo DIF-ID is hetzelfde in Hallo ontvangen factuur- en Hallo bevestiging verzonden hello in het dialoogvenster dat wordt weergegeven. Klik op OK in Hallo **bevestiging verzenden** in het dialoogvenster.
   
   ![][15]  
7. Binnen een paar seconden Hallo bevestiging is ontvangen voor Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Stap 5 (optioneel): verzenden EDIFACT factuur in batches
BizTalk Services EDI-bruggen ondersteunt ook batchverwerking van uitgaande berichten. Deze functie is handig voor het ontvangen van partners die liever tooreceive berichten (voldoen aan bepaalde criteria) in plaats van afzonderlijke berichten batchgewijs.

Hallo meest belangrijk aspect bij het werken met batches is Hallo werkelijke release van Hallo batch, ook wel Hallo release criteria. Hallo release criteria kunnen worden gebaseerd op hoe de ontvangende partner Hallo tooreceive berichten wil. Als batchverwerking is ingeschakeld, verzendt Hallo EDI-bridge geen Hallo uitgaande bericht toohello partner ontvangen totdat hello release criteria wordt voldaan. Bijvoorbeeld, een batchen criteria op basis van bericht grootte verzendingen een batch alleen wanneer "n" berichten in batch worden opgenomen. Een batchcriteria kunnen op basis van tijd ook worden, zodat een batch op een vaste tijd elke dag wordt verzonden. We proberen Hallo berichtgrootte gebaseerde criteria in deze oplossing.

1. Klik in de Hallo BizTalk Services-Portal, op Hallo overeenkomst die u eerder hebt gemaakt. Klik op verzendinstellingen > batchverwerking > Batch toevoegen.
2. Voer voor de batchnaam van de, **InvoiceBatch**, Geef een beschrijving en klik vervolgens op **volgende**.
3. Geef de batchcriteria van een, waarmee wordt gedefinieerd welke berichten moeten in batch worden opgenomen. We batch alle berichten in deze oplossing. Dus selecteer Hallo geavanceerde optie definities gebruiken en voer **1 = 1**. Dit is een voorwaarde die wordt altijd de waarde true en daarmee alle berichten worden in batch worden opgenomen. Klik op **Volgende**.
   
   ![][17]  
4. Geef de criteria van een batch release. Selecteer in het Hallo-keuzelijst **MessageCountBased**, en voor **aantal**, geef **3**. Dit betekent dat drie berichten batchgewijs tooNorthwind worden verzonden. Klik op **Volgende**.
   
   ![][18]  
5. Hallo staat een overzicht en klik vervolgens op **opslaan**. Klik op **implementeren** tooredeploy Hallo overeenkomst.
6. Ga terug toohello **zelfstudie Client**, klikt u op **intern factuur verzenden**, en volg Hallo prompts toosend Hallo factuur. U ziet dat geen factuur is ontvangen door Northwind omdat Hallo batchgrootte niet wordt voldaan. Herhaal deze stap twee keer, zodat u drie factuur berichten tooNorthwind hebben. Dit voldoet aan de criteria voor batch-release van 3 berichten Hallo en u ziet nu een factuur op Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

