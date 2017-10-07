---
title: aaaCall, trigger of nesten van werkstromen met HTTP-eindpunten - Azure Logic Apps | Microsoft Docs
description: HTTP-eindpunten toocall, trigger of geneste werkstromen instellen voor Azure Logic Apps
services: logic-apps
keywords: werkstromen, HTTP-eindpunten
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Bel, trigger of nesten van werkstromen met HTTP-eindpunten in logic apps

U kunt systeemeigen synchrone HTTP-eindpunten weergeven als triggers voor logic apps, zodat u kunt activeren of aanroepen van uw logische apps via een andere URL. U kunt ook de werkstromen in uw logische apps nesten met behulp van een patroon van callable-eindpunten.

toocreate HTTP-eindpunten, kunt u de triggers toevoegen zodat uw logische apps inkomende aanvragen kunnen ontvangen:

* [Aanvraag](../connectors/connectors-native-reqres.md)

* [API-verbinding Webhook](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [HTTP-webhook](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Hoewel onze voorbeelden Hallo gebruiken **aanvragen** worden geactiveerd, kunt u een van Hallo vermeld HTTP-triggers en alle identiek beginselen toohello andere triggertypen.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Een HTTP-eindpunt voor uw logische app instellen

toocreate een HTTP-eindpunt toevoegen een trigger die inkomende aanvragen kan ontvangen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal"). Ga tooyour logische app en open Logic App-ontwerper.

2. Toevoegen van een trigger waarmee uw logische app inkomende aanvragen worden ontvangen. Bijvoorbeeld, voeg Hallo **aanvragen** trigger tooyour logische app.

3.  Onder **aanvraag hoofdtekst JSON-Schema**, kunt u eventueel een JSON-schema voor Hallo nettolading (gegevens), waarop u verwacht Hallo trigger tooreceive dat invoeren.

    Dit schema Hallo designer gebruikt om tokens die uw logische app tooconsume, parse en de gegevens op te geven van Hallo trigger via uw werkstroom gebruiken kunt te genereren. 
    Informatie over [tokens die zijn gegenereerd op basis van de JSON-schema's](#generated-tokens).

    Geef voor dit voorbeeld Hallo-schema in Hallo ontwerpen weergegeven:

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Hallo aanvraagactie toevoegen][1]

    > [!TIP]
    > 
    > U kunt een schema voor een voorbeeld JSON-nettolading genereren vanuit een hulpprogramma zoals [jsonschema.net](http://jsonschema.net/), of in Hallo **aanvragen** trigger door te kiezen **gebruik voorbeeld nettolading toogenerate schema**. 
    > Voer uw payload voorbeeld en kies **gedaan**.

    Bijvoorbeeld, de nettolading van dit voorbeeld:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    Dit schema genereert:

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Sla uw logische app. Onder **HTTP POST toothis URL**, u ziet nu een gegenereerde retouraanroep-URL, zoals in dit voorbeeld:

    ![URL van de gegenereerde retouraanroep voor het eindpunt](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Deze URL bevat een Shared Access Signature (SAS)-sleutel in Hallo queryparameters die worden gebruikt voor verificatie. 
    U kunt ook Hallo HTTP-eindpunt-URL ophalen uit uw logische app overzicht in hello Azure-portal. Onder **Trigger geschiedenis**, selecteer uw trigger:

    ![HTTP-eindpunt-URL ophalen uit Azure-portal][2]

    Of u kunt Hallo-URL ophalen door deze oproep te plaatsen:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Hallo HTTP-methode voor de trigger wijzigen

Standaard Hallo **aanvraag** trigger een HTTP POST-aanvraag verwacht, maar u kunt een andere HTTP-methode. 

> [!NOTE]
> U kunt slechts één methodetype opgeven.

1. Op uw **aanvragen** activeren, kiest u **geavanceerde opties weergeven**.

2. Open Hallo **methode** lijst. Selecteer voor dit voorbeeld **ophalen** zodat u kunt uw HTTP-eindpunt-URL later testen.

    > [!NOTE]
    > U kunt selecteren van een andere HTTP-methode of een aangepaste methode voor uw eigen logische app opgeven.

    ![HTTP-methode wijzigen](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Accepteren parameters via uw HTTP-eindpunt-URL

Als u wilt dat de HTTP-eindpunt-URL tooaccept parameters aanpassen relatieve pad van de trigger.

1. Op uw **aanvragen** activeren, kiest u **geavanceerde opties weergeven**. 

2. Onder **methode**, dat u wilt dat uw aanvraag toouse Hallo HTTP-methode opgeven. Selecteer voor dit voorbeeld Hallo **ophalen** methode, als u nog niet gedaan, hebt zodat u kunt uw HTTP-eindpunt-URL testen.

      > [!NOTE]
      > Wanneer u een relatief pad voor de trigger opgeeft, kunt u een HTTP-methode moet ook expliciet opgeven voor de trigger.

3. Onder **relatief pad**, geef Hallo relatief pad voor Hallo-parameter die de URL, bijvoorbeeld accepteren moet `customers/{customerID}`.

    ![Hallo HTTP-methode en het relatieve pad voor de parameter opgeven](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse Hallo parameter, het toevoegen van een **antwoord** actie tooyour logische app. (Kies onder de trigger **nieuwe stap** > **een actie toevoegen** > **antwoord**) 

5. In uw antwoord **hoofdtekst**, Hallo token voor Hallo-parameter die u hebt opgegeven in de trigger relatief pad opnemen.

    Bijvoorbeeld: tooreturn `Hello {customerID}`, uw antwoord bijwerken **hoofdtekst** met `Hello {customerID token}`. 
    Hallo-lijst met dynamische inhoud moet worden weergegeven en weergeven van Hallo `customerID` token voor u tooselect.

    ![Parameter tooresponse hoofdtekst toevoegen](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    Uw **hoofdtekst** moet eruitzien als in dit voorbeeld:

    ![Antwoordtekst met de parameter](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Sla uw logische app. 

    De HTTP-eindpunt-URL bevat nu Hallo relatief pad, bijvoorbeeld: 

    HTTPS & # 58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest uw HTTP-eindpunt, kopiëren en plakken bijgewerkte URL naar een ander browservenster hello, maar vervang `{customerID}` met `123456`, en druk op Enter.

    Deze tekst moet worden weergegeven in uw browser: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Tokens die zijn gegenereerd op basis van de JSON-schema's voor uw logische app

Wanneer het bieden van een JSON-schema in uw **aanvragen** activeren, hello Logic App-ontwerper-tokens gegenereerd voor de eigenschappen in dat het schema. U kunt deze tokens vervolgens gebruiken voor het doorgeven van gegevens via uw logische app-werkstroom.

Voor dit voorbeeld als u Hallo toevoegt `title` en `name` eigenschappen tooyour JSON-schema, hun tokens zijn nu beschikbaar toouse in latere werkstroomstappen. 

Hier volgt Hallo voltooid JSON-schema:

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Geneste werkstromen voor logic apps maken

U kunt werkstromen in uw logische app nesten door toe te voegen andere logic apps die aanvragen kunnen ontvangen. tooinclude deze logische apps toevoegen Hallo **Azure Logic Apps - kiest u een werkstroom Logic Apps** actie tooyour trigger. U kunt selecteren van in aanmerking komende logic apps.

![Een andere logische app toevoegen](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Aanroepen of activeren van logische apps via HTTP-eindpunten

Nadat u uw HTTP-eindpunt hebt gemaakt, kunt u uw logische app via activeren een `POST` methode toohello volledige URL. Logische apps hebben een ingebouwde ondersteuning voor directe toegang eindpunten.

## <a name="reference-content-from-an-incoming-request"></a>Referentie-inhoud van een binnenkomende aanvraag

Als Hallo inhoud van het type is `application/json`, kunt u verwijzen naar eigenschappen van de binnenkomende aanvraag Hallo. Anders wordt inhoud behandeld als één eenheid binaire dat u tooother API's kunt doorgeven. Deze inhoud binnen de werkstroom Hallo tooreference, moet u die inhoud converteren. Bijvoorbeeld, als u doorgeeft `application/xml` inhoud, kunt u `@xpath()` voor een extractie XPath of `@json()` voor het converteren van XML-tooJSON. Meer informatie over [werken met inhoudstypen](../logic-apps/logic-apps-content-type.md).

tooget Hallo de uitvoer van een binnenkomende aanvraag opgegeven, kunt u Hallo `@triggerOutputs()` functie. Hallo uitvoer lijkt op het volgende voorbeeld:

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

Hallo tooaccess `body` eigenschap specifiek, kunt u Hallo `@triggerBody()` snelkoppeling. 

## <a name="respond-toorequests"></a>Toorequests reageren

U kunt toorespond toocertain aanvragen met een logische app door de aanroeper inhoud toohello terug te starten. tooconstruct hello statuscode, koptekst en hoofdtekst voor uw antwoord, kunt u Hallo **antwoord** in te grijpen. Deze actie kan overal voorkomen in uw logische app, niet alleen aan Hallo einde van uw werkstroom.

> [!NOTE] 
> Als uw logische app geen een **antwoord**, Hallo HTTP-eindpunt reageert *onmiddellijk* met een **202 geaccepteerde** status. Ook voor de oorspronkelijke aanvraag tooget Hallo antwoord Hallo, alle stappen die nodig zijn voor antwoord Hallo moeten zijn voltooid binnen de Hallo [aanvraag time-outlimiet](./logic-apps-limits-and-config.md) tenzij u Hallo werkstroom als een geneste logische app aanroepen. Als er geen reactie binnen deze limiet gebeurt, inkomende hello-aanvraag een time-out optreedt en Hallo HTTP-antwoord ontvangt **408 time-out van de Client**. Voor geneste logic apps blijft Hallo bovenliggende logische app toowait voor een antwoord pas voltooid, ongeacht hoeveel tijd vereist is.

### <a name="construct-hello-response"></a>Antwoord Hallo maken

U kunt meer dan één header en elk type inhoud in de antwoordtekst Hallo opnemen. In ons voorbeeld antwoord Hallo header geeft aan dat antwoord Hallo type inhoud heeft `application/json`. en Hallo hoofdtekst bevat `title` en `name`, op basis van de JSON-schema Hallo eerder bijgewerkt in verband met Hallo **aanvragen** trigger.

![HTTP-antwoord actie][3]

Antwoorden hebben deze eigenschappen:

| Eigenschap | Beschrijving |
| --- | --- |
| statusCode |Hiermee geeft u Hallo HTTP-statuscode voor reageert toohello binnenkomende aanvraag. Deze code kan geldige statuscode die met 2xx, 4xx of 5xx begint zijn. Statuscodes 3xx zijn echter niet toegestaan. |
| Headers |Definieert een willekeurig aantal headers tooinclude Hallo reactie. |
| Hoofdtekst |Hiermee geeft u een instantie-object dat kan bestaan uit een tekenreeks, een JSON-object of zelfs binaire inhoud waarnaar wordt verwezen vanuit de vorige stap. |

Hier ziet u welke Hallo JSON-schema nu voor Hallo lijkt **antwoord** actie:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> tooview hello voltooid JSON-definitie voor uw logische app, op Hallo Logic App-ontwerper, kies **codeweergave**.

## <a name="q--a"></a>Vragen en antwoorden

#### <a name="q-what-about-url-security"></a>V: hoe zit URL beveiliging?

A: azure genereert veilig logic app retouraanroep-URL's met behulp van een Shared Access Signature (SAS). Deze handtekening als een queryparameter passeert en moet worden gevalideerd voordat uw logische app kan worden gestart. Azure genereert Hallo handtekening met een unieke combinatie van een geheime sleutel per logische app, Hallo triggernaam en Hallo-bewerking die wordt uitgevoerd. Dus tenzij iemand toegang toohello geheime logic app-sleutel heeft, deze een geldige handtekening niet genereren kunnen.

   > [!IMPORTANT]
   > Voor productie en beveiligde systemen kunt beter geen aanroepen van uw logische app rechtstreeks vanuit de browser Hallo omdat:
   > 
   > * Hallo gedeelde toegangssleutel wordt weergegeven in Hallo-URL.
   > * U beheren geen beveiligde inhoud beleidsregels vanwege tooshared domeinen voor klanten is logische App.

#### <a name="q-can-i-configure-http-endpoints-further"></a>V: kan ik meer HTTP-eindpunten configureren?

A: Ja, HTTP-eindpunten ondersteuning voor meer geavanceerde configuratie via [ **API Management**](../api-management/api-management-key-concepts.md). Deze service biedt ook Hallo mogelijkheden voor u tooconsistently alle uw API's, met inbegrip van logische apps beheren, instellen van aangepaste domeinnamen, gebruik meer verificatiemethoden en meer, zoals:

* [Hallo aanvraagmethode wijzigen](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Hallo URL-segmenten van Hallo aanvraag wijzigen](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Instellen van uw API Management-domeinen in Hallo [Azure-portal](https://portal.azure.com/ "Azure-portal")
* Beleid toocheck voor basisverificatie instellen

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>V: wat als Hallo schema gemigreerd van Hallo 1 December 2014 preview gewijzigd?

A: Hier volgt een samenvatting over deze wijzigingen:

| Voorbeeld 1 december 2014 | 1 juni 2016 |
| --- | --- |
| Klik op **HTTP-Listener** API-App |Klik op **handmatige trigger** (Er is geen API App vereist) |
| HTTP-Listener-instelling '*automatisch antwoord verzendt*' |Beide omvatten een **antwoord** actie of niet in de workflowdefinitie Hallo |
| Basisverificatie of OAuth-verificatie configureren |via API-beheer |
| Configureren van HTTP-methode |Onder **geavanceerde opties weergeven**, kiest u een HTTP-methode |
| Relatief pad configureren |Onder **geavanceerde opties weergeven**, voegt u een relatief pad |
| Verwijzing Hallo binnenkomende hoofdtekst via`@triggerOutputs().body.Content` |Verwijzing via`@triggerOutputs().body` |
| **HTTP-antwoord verzonden** actie op Hallo HTTP-Listener |Klik op **reageren tooHTTP aanvraag** (Er is geen API App vereist) |

## <a name="get-help"></a>Help opvragen

tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

* [Definities voor logische apps maken](./logic-apps-author-definitions.md)
* [Fouten en uitzonderingen verwerken](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
