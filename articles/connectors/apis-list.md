---
title: aaaConnectors voor Azure Logic Apps | Microsoft Docs
description: Kies in alle Hallo beschikbaar door Microsoft beheerde connectors toobuild en logic apps maken
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Lijst van connectors
> [!TIP]
> Hallo [de volledige lijst A-Z](#az) (in dit onderwerp) een lijst met alle Hallo beschikbare connectors kunt u in uw logische Apps. [Details van de connector](/connectors/) geeft een lijst van alle triggers en acties die zijn gedefinieerd in swagger hello en een lijst met beperkingen voor elke connector.

Connectors vormen een integraal onderdeel van het maken van logische apps. Met behulp van deze connectors kunt u echt uw on-premises uitvouwen en cloud-toepassingen toodo verschillende dingen met gegevens die u maakt en gegevens die u al hebt. Hallo-connectors zijn beschikbaar in Hallo volgende categorieën: 

* **Standaardconnectors**: automatisch beschikbaar en inbegrepen wanneer u logische apps gebruikt. Een aantal voorbeelden zijn Service Bus, Power BI, Oracle Database en OneDrive.

* **Integratieaccountconnectors**: beschikbaar wanneer u een integratieaccount aanschaft. Met behulp van deze connectors kunt u XML transformeren en valideren, business-to-business-berichten verwerken met AS2/X12/EDIFACT en platte bestanden coderen en decoderen. Als u met BizTalk Server werkt, zijn deze connectors dat een goede past tooexpand uw BizTalk-werkstromen in Azure.  

    BizTalk Server heeft ook een [Logic Apps adapter](https://msdn.microsoft.com/library/mt787163.aspx) die van een logische app ontvangen en verzenden van tooa logische app bevat.

* **Bedrijfsconnectors**: bevat MQ en SAP. Beschikbaar tegen een meerprijs. 

[Prijzen van Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) en [prijzen model](../logic-apps/logic-apps-pricing.md) vindt u meer informatie over Hallo kosten. 

## <a name="popular-connectors"></a>Populaire connectors
Er zijn duizenden toepassingen en miljoenen uitvoeringen die succesvol data en informatie verwerken met behulp van deze connectors. Hallo volgende tabel ziet u Hallo populairste en sommige favorieten met onze gebruikers:

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Azure Blob<br/>Storage**][AzureBlobStoragedoc] | Als u alle taken tooautomate met uw opslagaccount wilt, moet u deze connector kijken. Ondersteunt CRUD-bewerkingen (maken, lezen, bijwerken en verwijderen). | [![API Icon][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | Hiermee kunt u functies maken die aangepaste fragmenten van C# of node.js uitvoeren en deze functies vervolgens gebruiken in uw logische apps.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Een van de meeste gevraagd voor connectors Hallo. Triggers en acties toohelp automatiseren werkstromen met potentiële klanten en meer heeft. | [![API Icon][Event-Hubs-icon]<br/>**Event Hubs**][event-hubs-doc] | Hiermee kunt u gebeurtenissen gebruiken en publiceren op een Event Hub. U kunt bijvoorbeeld uitvoer ophalen uit uw logische app met behulp van Event Hubs en verzend Hallo uitvoer tooa realtime analytics-provider. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | Als uw FTP-server toegankelijk is vanaf Hallo internet, en vervolgens kunt u werkstromen toowork met bestanden en mappen automatiseren. <br/><br/>SFTP is ook beschikbaar met Hallo SFTP-connector. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Logic apps toocommunicate gebruiken met een willekeurig eindpunt via HTTP. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Veel van triggers en veel meer acties toouse Office 365-e-mailbericht en gebeurtenissen binnen uw werkstromen. <br/><br/>Deze connector omvat een *goedkeuring e* actie tooapprove vakantieaanvragen onkosten rapporten, enzovoort. <br/><br/>Office 365-gebruikers zijn ook leverbaar met Hallo-connector voor Office 365-gebruikers.| [![API Icon][HTTP-Requesticon]<br/>**Aanvraag/antwoord**][HTTP-Requestdoc] | Deze connector biedt een HTTPS-URL. Hallo logische app wordt gestart wanneer Hallo logische app ontvangt een aanvraag-URL toothis. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Eenvoudig aanmelden met uw Salesforce-account tooget toegang tooobjects, zoals potentiële klanten, en meer. |  [![API Icon][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | Hallo populairste-connector in logic apps bevat triggers en acties toodo asynchrone messaging en publiceren/abonneren met wachtrijen, abonnementen en onderwerpen. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | We raden deze connector aan als u met SharePoint werkt en automatisering handig voor u zou zijn. Kan worden gebruikt met een on-premises SharePoint en SharePoint Online. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Een van de Hallo connectors voor het meest gebruikt, deze verbinding kan maken met tooan on-premises SQL Server en een Azure SQL Database. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Hiermee kunt u zich eenvoudig aanmelden met een Twitter-account en vervolgens een werkstroom starten wanneer er een nieuwe tweet wordt geplaatst. Sla deze tweets tooa SQL-database of de SharePoint-lijst. | | | 

## <a name="integration-account-connectors"></a>Integratieaccountconnectoren 

Hallo Enterprise Integration Pack (EIP) omvat connectors die bekende toohello BizTalk Server-community zijn. Wanneer u koopt een [integratie account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), u ook de volgende connectors Hallo ophalen: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**AS2</br>-decodering**][as2decode] | [![API Icon][as2icon]<br/>**AS2</br>-codering**][as2encode] | [![API Icon][x12icon]<br/>**EDIFACT</br>-decodering**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**EDIFACT</br>-codering**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Codering</br> van plat bestand**][flatfiledoc] | [![API Icon][flatfiledecodeicon]<br/>**Decodering</br> van plat bestand**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Integratie-<br/>account**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**XML<br/>transformeren**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**X12</br>-decodering**][x12decode] | [![API Icon][x12icon]<br/>**X12</br>-codering**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**XML<br/>-validatie**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Bedrijfsconnectoren

Verbinding maken met bedrijfstoepassingen tooyour in logic apps.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Volledige alfabetische lijst

[Details van de connector](/connectors/) lijst van alle triggers en acties die zijn gedefinieerd in swagger hello en een lijst met beperkingen voor elke connector.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 Appointment Scheduling<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Azure API Management<br/>Azure App Services<br/>Azure Application<br/>Azure Automation<br/>[Azure Blob Storage][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Azure-wachtrijen<br/>Azure Resource Manager<br/>[Azure SQL Database][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Benchmark Email<br/>Bing Zoeken<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>Cognitive Services - Computer Vision-API<br/>Cognitive Services - Face-API<br/>Cognitive Services - LUIS<br/>Cognitive Services - Tekstanalyse<br/>Common Data Service<br/>Content Conversion<br/>Control-Terminate<br/>[Aangepaste API's/web-apps][api/web-appdoc]<br/><br/><a name="d"></a>Gegevensbewerkingen<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Event Hubs][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[Bestandssysteem][filesystemdoc]<br/>[Plat bestand][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>Freshservice<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google Agenda<br/>Google Contactpersonen<br/>Google Drive<br/>Google Sheets<br/>Google Tasks<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP-webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Integratieaccount<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Middelgroot<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN weer<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365-gebruikers<br/>Office 365 Video<br/>OneDrive<br/>OneDrive voor Bedrijven<br/>OneNote (Bedrijven)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook Customer Manager<br/>Outlook-taken<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Aanvraag/antwoord][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP Application Server][sapconnector]<br/>[SAP Message Server][sapconnector]<br/>[Planning][recurrencedoc]<br/>Bereik<br/>SendGrid<br/>Verzenden van berichten toobatch<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[XML transformeren][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variabelen<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML-validatie][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> voordat u zich aanmeldt voor een Azure-account, de slag met Azure Logic Apps tooget te gaan[probeer Logic Apps](https://tryappservice.azure.com/?appservice=logic). U kunt onmiddellijk een tijdelijke logische app maken. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.

## <a name="connectors-as-triggers-and-actions"></a>Connectors als triggers en acties

Een **trigger** start een exemplaar van uw logische app of voert deze uit. Sommige connectors bieden triggers die aan uw app doorgeven dat er specifieke gebeurtenissen plaatsvinden. Hallo FTP-connector heeft bijvoorbeeld Hallo `OnUpdatedFile` trigger die uw logische app wordt gestart wanneer een bestand wordt bijgewerkt. 

Logische apps zijn onder andere Hallo volgende soorten triggers:  

* *Triggers pollen*: deze triggers pollen uw service met een opgegeven frequentie toocheck voor nieuwe gegevens. 

    Wanneer nieuwe gegevens beschikbaar is, wordt een nieuw exemplaar van uw logische app uitgevoerd met Hallo gegevens als invoer. 

* *Push-triggers*: deze triggers wordt geluisterd naar gegevens op een eindpunt of voor een gebeurtenis toohappen, klikt u vervolgens een nieuw exemplaar van uw logische app getriggerd.

* *Trigger met terugkeerpatroon*: deze trigger start een exemplaar van uw logische app op basis van een voorgeschreven planning.

Connectors bieden ook de **acties** die u in uw werkstroom kunt gebruiken. Uw logische app kan bijvoorbeeld gegevens zoeken en deze gegevens later in uw logische app gebruiken. Meer specifiek, kunt u gegevens van de klant in een SQL-database opzoeken en gebruik vervolgens deze gegevens klant toobuild uw werkstroom. 

> [!TIP]
> In [Overzicht van connectors](connectors-overview.md) vindt u gedetailleerdere informatie over triggers en acties. 


## <a name="message-manipulation-actions"></a>Acties voor berichtbewerking

Logische apps bevatten ingebouwde acties waarmee u nettoladinggegevens kunt wijzigen of bewerken. Hallo ingebouwde **gegevensbewerkingen** connector omvat Hallo van de volgende activiteiten: 

| | |
|---|---|
| **Opstellen** | Bouwen of waarden of objecten toouse later genereren of bouwen als u uw werkstroom. U kunt bijvoorbeeld Maak een JSON-object met waarden uit meerdere stappen of berekenen een constante tooreference verderop in een logische app uitgevoerd. |
| **CSV-tabel maken**<br/>**HTML-tabel maken** | Zet een matrixresultatenset om in een CSV- of HTML-tabel. Bijvoorbeeld Hallo CRM 'Lijst met records' actie toevoegen en voeg een filter voor records die tegenwoordig worden toegevoegd. Verzend Hallo resultaten als een HTML-tabel in een e-mailbericht. |
| **Matrix filteren** (query) | Filteren op een resultaat set toohello vermeldingen die u interesseren. Zoek bijvoorbeeld naar alle tweets met `#Azure`, en vervolgens 'filter' hello tweets tooonly retourneren resultaten gevonden die zijn `Tweeted_by_followers > 50`. |
| **Koppelen** | Koppel een matrix met een delimeter. Bijvoorbeeld, retourneert Hallo detecteren sleutel zinnen bewerking een matrix van sleutel zinnen. U kunt ze 'koppelen' met een `,` of iets vergelijkbaars. In plaats van `["Some", "Phrase"]` hebt u dan `"Some, Phrase"`. |
| **JSON parseren** | Parseren en toegang tot de waarden van een JSON-object in de ontwerpfunctie Hallo. Bijvoorbeeld, als uw Azure-functie een JSON-nettolading retourneert, klikt u deze kan worden geparseerd tooaccess Hallo JSON-eigenschappen later in een andere stap. Hallo actie valideert ook dat Hallo JSON komt overeen met Hallo opgegeven schema tijdens runtime. | 
| **Selecteren** | Selecteer bepaalde eigenschappen van een matrix voor verdere verwerking. Als u records vermeldt vanuit SQL en er 15 kolommen worden geretourneerd, selecteert u slechts enkele van die kolommen voor verdere verwerking. Hallo-uitvoer is een matrix die alleen Hallo-eigenschappen die u selecteert. |

## <a name="custom-connectors-and-azure-certification"></a>Aangepaste connectors en Azure-certificering 

toocall in API's die niet beschikbaar als connectors of aangepaste code uitgevoerd, kunt u Hallo Logic Apps platform door uitbreiden [maken op basis van REST-API Apps als aangepaste connectors](../logic-apps/logic-apps-create-api-app.md). 

Als u wilt dat toomake uw aangepaste API-Apps openbare en beschikbare toouse in Azure, indienen uw benoeming toohello [Microsoft Azure-gecertificeerd programma](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Help opvragen

tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u toohello [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

Ontbreekt er een onderwerp over connectors of bepaalde belangrijke details? Zo ja, ons te helpen met het toevoegen van bestaande onderwerpen tooour of uw eigen schrijven. Onze documentatie is open source en wordt gehost op GitHub. Ga aan de slag in onze [GitHub-opslagplaats](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Volgende stappen
* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Aangepaste API's maken voor logische apps](../logic-apps/logic-apps-create-api-app.md)
* [Uw logische apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Logische apps integreren met App Service API Apps."
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Bestanden in uw blobcontainer beheren met Azure Blob Storage-container."
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Logische apps integreren met Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "Verbinding maken met tooIBM DB2 in Hallo cloud of on-premises. Een rij bijwerken, een tabel ophalen, en meer"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Verbinding maken met tooDynamics CRM Online, zodat u met CRM Online gegevens werken kunt"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Verbinding maken met tooAzure Event Hubs. Gebeurtenissen tussen logische apps en Event Hubs verzenden en ontvangen"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Verbinding maken met tooan on-premises bestandssysteem"
[ftpdoc]: ./connectors-create-api-ftp.md "Verbinding maken met tooan FTP / FTPS-server voor de FTP-taken, zoals het uploaden, ophalen, verwijderen van bestanden"
[httpdoc]: ./connectors-native-http.md "HTTP-aanroepen met Hallo HTTP-connector maken"
[http-requestdoc]: ./connectors-native-reqres.md "Acties voor HTTP-aanvragen en antwoorden tooyour logic apps toevoegen"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "HTTP + Swagger-connector gebruiken voor HTTP-aanroepen"
[informixdoc]: ./connectors-create-api-informix.md "Verbinding maken met tooInformix in Hallo cloud of on-premises. Lezen van een rij en lijst Hallo tabellen"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Logische apps integreren met geneste werkstromen"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Tooyour Office 365-account koppelen. E-mailberichten verzenden en ontvangen, uw agenda en contactpersonen beheren, en meer"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Verbinding maken met tooan Oracle-database tooadd, invoegen en rijen verwijderen"
[mqdoc]: ./connectors-create-api-mq.md "Verbinding maken met tooMQ on-premises of Azure, en berichten verzenden en ontvangen"
[recurrencedoc]:  ./connectors-native-recurrence.md "Terugkerende acties voor logische apps activeren"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Tooyour Salesforce-account koppelen. Accounts, potentiële klanten en verkoopkansen beheren, en meer"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Verbinding maken met tooan on-premises SAP-systeem"
[service-busdoc]: ./connectors-create-api-servicebus.md "Berichten vanuit de Service Bus-wachtrijen en -onderwerpen verzenden en berichten vanuit de Service Bus-wachtrijen en abonnementen ontvangen"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Verbinding maken met tooSharePoint Online. Documenten beheren, items vermelden, en meer"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Verbinding maken met tooSharePoint op de lokale server. Documenten beheren, items vermelden, en meer"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Verbinding maken met tooAzure SQL-Database of SQL server. Vermeldingen in een SQL-databasetabel maken, bijwerken, ophalen en verwijderen."
[twitterdoc]: ./connectors-create-api-twitter.md "Verbinding maken met tooTwitter. Tijdlijnen ophalen, tweets posten, en meer"
[webhookdoc]: ./connectors-native-webhook.md "Webhook acties en triggers tooyour logic apps toevoegen"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Meer informatie over Enterprise Integration AS2."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Meer informatie over Enterprise Integration X12"
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Meer informatie over Enterprise Integration met platte bestanden."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Meer informatie over Enterprise Integration met platte bestanden."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Meer informatie over Enterprise Integration met XML-validatie."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Meer informatie over Enterprise Integration-transformaties."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Meer informatie over AS2-decodering in Enterprise Integration"
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Meer informatie over AS2-codering in Enterprise Integration"
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Meer informatie over X12-decodering in Enterprise Integration"
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Meer informatie over X12-codering in Enterprise Integration"
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Meer informatie over EDIFACT-decodering in Enterprise Integration"
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Meer informatie over EDIFACT-codering in Enterprise Integration"
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Schema's, kaarten, partners en meer opzoeken in uw integratieaccount"


[boxDoc]: ./connectors-create-api-box.md "Verbinding maken met tooBox. Uw bestanden uploaden, ophalen, verwijderen, vermelden, en meer"
[delaydoc]: ./connectors-native-delay.md "Vertraagde acties uitvoeren"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Verbinding maken met tooDropbox. Uw bestanden uploaden, ophalen, verwijderen, vermelden, en meer"
[facebookdoc]: ./connectors-create-api-facebook.md "Verbinding maken met tooFacebook. Tooa tijdlijn te plaatsen, kunt u een paginafeed en meer"
[githubdoc]: ./connectors-create-api-github.md "Verbinding maken met tooGitHub en problemen bijhouden"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Verbinding maken met tooGoogleDrive zodat u met uw gegevens werken kunt"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Verbinding maken met tooGoogle bladen zodat u uw bladen kunt kunt wijzigen"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Verbonden tooGoogle taken zodat u kunt uw taken beheren"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Maakt verbinding tooGoogle agenda en kalender kunt beheren."
[http-responsedoc]: ./connectors-native-reqres.md "Acties voor HTTP-aanvragen en antwoorden tooyour logic apps toevoegen"
[instagramdoc]: ./connectors-create-api-instagram.md "Verbinding maken met tooInstagram. Gebeurtenissen activeren of erop reageren"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Tooyour MailChimp-account koppelen. E-mails beheren en automatiseren"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Verbinding maken met tooMandrill voor communicatie"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Verbinding maken met tooMicrosoft conversieprogramma. Tekst vertalen, talen detecteren, en meer " 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Informatie over video's, videolijsten, videokanalen en URL's voor het afspelen van Office 365-video's ophalen"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Verbinding maken met tooyour persoonlijke Microsoft OneDrive. Bestanden uploaden, verwijderen, vermelden, en meer"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Verbinding maken met tooyour zakelijke Microsoft OneDrive. Uw bestanden uploaden, verwijderen, vermelden, en meer"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Verbinding maken met tooyour Outlook-postvak. Uw e-mail, agenda's en contactpersonen beheren, en meer"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Verbinding maken met tooMicrosoft Project Online. Uw projecten, taken, resources beheren, en meer"
[querydoc]: ./connectors-native-query.md "Selecteer en matrices met Hallo queryactie filteren"
[rssdoc]: ./connectors-create-api-rss.md "Publiceren en feeditems ophalen, bewerkingen activeren wanneer een nieuw item gepubliceerde tooan RSS is-feed."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Verbinding maken met tooSendGrid. E-mail verzenden en lijsten met geadresseerden beheren"
[sftpdoc]: ./connectors-create-api-sftp.md "Tooyour SFTP-account koppelen. Bestanden uploaden, ophalen, verwijderen, en meer"
[slackdoc]: ./connectors-create-api-slack.md "Verbinding maken met tooSlack en berichten plaatsen tooSlack kanalen"
[smtpdoc]: ./connectors-create-api-smtp.md "Verbind tooa SMTP-server en e-mail met bijlagen verzenden"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Maakt verbinding tooSparkPost voor communicatie"
[trellodoc]: ./connectors-create-api-trello.md "Verbinding maken met tooTrello. Uw projecten beheren en dingen organiseren met anderen"
[twiliodoc]: ./connectors-create-api-twilio.md "Verbinding maken met tooTwilio. Berichten verzenden en ophalen, beschikbare nummers ophalen, binnenkomende telefoonnummers beheren, en meer."
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Verbinding maken met tooWunderlist. Uw taken en takenlijsten beheren, alles synchroniseren, en meer"
[yammerdoc]: ./connectors-create-api-yammer.md "Verbinding maken met tooYammer. Berichten posten, nieuwe berichten ophalen, en meer"
[youtubedoc]: ./connectors-create-api-youtube.md "Verbinding maken met tooYouTube. Uw video's en kanalen beheren"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
