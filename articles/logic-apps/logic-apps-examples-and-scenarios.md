---
title: aaaExamples & algemene scenario's - Azure Logic Apps | Microsoft Docs
description: Meer informatie over logische apps met voorbeelden, scenario's en zelfstudies
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Voorbeelden en algemene scenario's voor Azure Logic Apps

u meer informatie over toohelp Hallo veel patronen en mogelijkheden in Azure Logic Apps, Hier vindt u algemene voorbeelden en scenario's.

## <a name="key-scenarios-for-logic-apps"></a>Belangrijkste scenario's voor logische apps

Logische Apps van Azure biedt flexibele orchestration en integratie voor verschillende services. Hallo Logic Apps-service is zonder ' Server', zodat er geen tooworry over scale of exemplaren – een alle toodo Hallo-werkstroom (trigger en acties) definiëren. het onderliggende platform Hallo verwerkt schaal, beschikbaarheid en prestaties. Een scenario waarin u toocoordinate meerdere acties moet met name tussen meerdere systemen is een geweldige gebruiksvoorbeeld voor Azure Logic Apps. Hier volgen enkele patronen en voorbeelden.

## <a name="respond-tootriggers-and-extend-actions"></a>Tootriggers reageren en acties uit te breiden

Elke logische app begint met een trigger. Bijvoorbeeld, uw werkstroom kunt beginnen met een schema-gebeurtenis, een handmatige aanroep of een gebeurtenis op basis van een extern systeem, zoals Hallo "wanneer een bestand wordt toegevoegd tooan FTP-server" trigger. Logische Apps van Azure ondersteunt momenteel meer dan 100 kant-en-klare connectors, variërend van lokale SAP tooMicrosoft cognitieve Services. Voor systemen en services die mogelijk niet connectors hebt gepubliceerd, kunt u ook logische apps uitbreiden.

* [Maken van aangepaste triggers of acties](../logic-apps/logic-apps-create-api-app.md)
* [Instellen van langlopende acties voor de werkstroom wordt uitgevoerd](../logic-apps/logic-apps-create-api-app.md)
* [Reageren tooexternal gebeurtenissen en acties met webhooks.](../logic-apps/logic-apps-create-api-app.md)
* [Bel, trigger of nesten van werkstromen met synchrone antwoorden tooHTTP aanvragen](../logic-apps/logic-apps-http-endpoint.md)
* [Zelfstudie: TooTwilio SMS webhooks reageren en verzendt een tekstantwoord](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Zelfstudie: Bouw een AI ingeschakeld sociale dashboard in minuten met Logic Apps en Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Foutafhandeling, logboekregistratie en controle stroom mogelijkheden

Logische apps bevatten uitgebreide mogelijkheden voor geavanceerde Controlestroom, zoals voorwaarden, switches, lussen en -scopes. flexibele oplossingen voor tooensure, kunt u ook implementeren fout en afhandeling van uitzonderingen in uw werkstromen. Meldingen en logboeken met diagnostische gegevens voor werkstroom uitvoeringsstatus biedt Azure Logic Apps ook controle en waarschuwingen.

* [Andere acties uitvoeren in het switch-instructies](../logic-apps/logic-apps-switch-case.md)
* [Proces-items in de arrays en verzamelingen met lussen en batches in logic apps](../logic-apps/logic-apps-loops-and-scopes.md)
* [Fout van de auteur en afhandeling van uitzonderingen in een werkstroom](../logic-apps/logic-apps-exception-handling.md)
* [Bewaking, logboekregistratie en waarschuwingen voor bestaande logische apps inschakelen](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Controle en logboekregistratie van diagnostische gegevens inschakelen bij het maken van logische apps](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Gebruiksvoorbeeld: hoe een bedrijf gezondheidszorg logic app uitzonderingsverwerking voor HL7 FHIR werkstromen gebruikt](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Logic apps implementeren en beheren

U kunt volledig ontwikkelen en logic apps implementeren met Visual Studio, Visual Studio Team Services, of een andere broncodebeheer en geautomatiseerde build tools. toosupport-implementatie voor werkstromen en afhankelijke verbindingen in de sjabloon van een resource, logische apps gebruiken implementatiesjablonen Azure-resource. Deze sjablonen, u in toosource-besturingselement voor versiebeheer controleren kunt automatisch worden gegenereerd in Visual Studio-hulpprogramma's.

* [Een sjabloon voor automatische implementatie maken](../logic-apps/logic-apps-create-deploy-template.md)
* [Bouwen en implementeren van logische apps vanuit Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Hallo-status van uw logische apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Typen inhoud, conversies en transformaties binnen een uitvoering

U kunt toegang tot, converteren en transformatie van verschillende typen inhoud met behulp van Hallo veel functies in hello Azure Logic Apps [werkstroom definition language](http://aka.ms/logicappsdocs). Bijvoorbeeld, u kunt converteren tussen een tekenreeks, JSON en XML Hello `@json()` en `@xml()` expressies. Hallo Logic Apps-engine bewaart inhoudstypen toosupport inhoudsoverdracht op een manier zonder verlies tussen services.

* [Typen niet JSON-inhoud verwerken](../logic-apps/logic-apps-content-type.md), bijvoorbeeld `application/xml`, `application/octet-stream`, en`multipart/formdata`
* [De werking van expressies in logic apps](../logic-apps/logic-apps-author-definitions.md)
* [Referentie: Definitietaal van de werkstroom met logische Apps van Azure](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Andere integraties en mogelijkheden

Logische apps bieden ook integratie met veel services, zoals Azure Functions, Azure API Management, Azure App Services en aangepaste HTTP-eindpunten, bijvoorbeeld REST en SOAP.

* [Maak een realtime sociale dashboard met Azure zonder server](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Azure-functies aanroepen vanuit logic apps](../logic-apps/logic-apps-azure-functions.md)
* [Scenario: Trigger logic apps met Azure Functions](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Call SOAP-eindpunten vanuit logic apps](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>End-to-end scenario 's

* [Technisch document: Enterprise integration end-to-end aanvraagbeheer met Azure-services, zoals Logic Apps](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Volgende stappen

- [Voor het afhandelen van fouten en uitzonderingen in logic apps](../logic-apps/logic-apps-exception-handling.md)
- [De workflowdefinitie auteur met Hallo werkstroom definitietaal](../logic-apps/logic-apps-author-definitions.md)
- [Verzenden van uw opmerkingen, vragen, feedback of suggesties voor hoe kunnen we Azure Logic Apps verbeteren](https://feedback.azure.com/forums/287593-logic-apps)