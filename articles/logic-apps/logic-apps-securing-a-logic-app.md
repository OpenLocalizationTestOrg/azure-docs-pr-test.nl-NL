---
title: aaaSecure tooAzure Logic Apps toegang | Microsoft Docs
description: Beveiliging voor de beveiliging van toegang tootriggers, invoer en uitvoer, actieparameters en services die worden gebruikt met werkstromen in Azure Logic Apps toevoegen.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Toegang tot beveiligde tooyour logic apps

Er zijn veel hulpprogramma's beschikbaar toohelp beveiligen van uw logische app.

* Beveiliging van toegang tootrigger een logische app (HTTP-aanvragen Trigger)
* Beveiliging van toegang toomanage bewerken of een logische app lezen
* Toocontents van invoer en uitvoer voor een run toegang beveiligen
* Parameters of invoer binnen acties in een werkstroom beveiligen
* Beveiliging van toegang tooservices die aanvragen van een werkstroom ontvangen

## <a name="secure-access-tootrigger"></a>Veilige toegang tootrigger

Wanneer u werkt met een logische app, die wordt geactiveerd op een HTTP-aanvraag ([aanvragen](../connectors/connectors-native-reqres.md) of [Webhook](../connectors/connectors-native-webhook.md)), kunt u de toegang beperken zodat alleen geautoriseerde clients Hallo logische app kunnen worden gestart. Alle aanvragen in een logische app zijn versleuteld en beveiligd via SSL.

### <a name="shared-access-signature"></a>Shared Access Signature

Elk eindpunt van de aanvraag voor een logische app bevat een [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) als onderdeel van het Hallo-URL. Elke URL bevat een `sp`, `sv`, en `sig` queryparameter. Machtigingen zijn opgegeven door `sp`, en overeen tooHTTP methoden die zijn toegestaan, `sv` toogenerate Hallo versie die wordt gebruikt, is en `sig` gebruikte tooauthenticate toegang tootrigger is. Hallo-handtekening wordt gegenereerd met behulp van Hallo SHA256-algoritme met een geheime sleutel op alle Hallo URL-paden en eigenschappen. Hallo geheime sleutel wordt nooit beschikbaar gemaakt en gepubliceerd, en versleuteld en opgeslagen als onderdeel van Hallo logische app wordt opgeslagen. Uw logische app machtigt alleen triggers die een geldige handtekening gemaakt met de geheime sleutel Hallo bevatten.

#### <a name="regenerate-access-keys"></a>Toegangstoetsen genereren

U kunt een nieuwe beveiligde sleutel aan op elk gewenst moment via Hallo REST-API of Azure-portal opnieuw genereren. Alle huidige URL's die eerder met de oude sleutel Hallo zijn gegenereerd zijn ongeldig en niet langer gemachtigde toofire Hallo logische app.

1. Open in hello Azure-portal, Hallo logische app die u wilt dat tooregenerate een sleutel
1. Klik op Hallo **toegangssleutels** menu-item onder **instellingen**
1. Kies Hallo sleutel tooregenerate en volledige Hallo-proces

URL's die u na het opnieuw genereren ophalen zijn met de nieuwe toegangssleutel Hallo ondertekend.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Callback URL's maken met een vervaldatum

Als u Hallo URL met andere partijen deelt, kunt u URL's genereren met de specifieke sleutels en vervaldatums indien nodig. U kunt vervolgens probleemloos sleutels rouleert of zorg ervoor dat toegang toofire een app is beperkt tooa bepaalde timespan. U kunt een vervaldatum opgeven voor een URL via Hallo [logische apps REST-API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Opnemen in de hoofdtekst van het Hallo Hallo eigenschap `NotAfter` als een JSON-datumtekenreeks, die een callback-URL die is alleen geldig tot Hallo resulteert `NotAfter` datum en tijd.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>URL's maken met primaire of secundaire geheime sleutel

Wanneer u genereren of URL van de callback voor triggers op aanvraag gebaseerde, kunt u ook welke sleutel toouse toosign Hallo-URL opgeven.  U kunt een URL die is ondertekend door een specifieke sleutel via Hallo genereren [logische apps REST-API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) als volgt:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Opnemen in de hoofdtekst van het Hallo Hallo eigenschap `KeyType` als `Primary` of `Secondary`.  Hiermee wordt een URL die is ondertekend door Hallo beveiligde sleutel die is opgegeven.

### <a name="restrict-incoming-ip-addresses"></a>Binnenkomende IP-adressen beperken

Bovendien toohello Shared Access Signature, u kunt desgewenst toorestrict aanroepen van een logische app alleen van specifieke clients.  Als u uw eindpunt via Azure API Management beheren, kunt u bijvoorbeeld Hallo logica beperken app tooonly Hallo aanvraag accepteren als Hallo aanvraag afkomstig is van Hallo API Management-exemplaar IP-adres.

Deze instelling kan worden geconfigureerd in Hallo logic app-instellingen:

1. Open in hello Azure-portal, Hallo logische app die u wilt dat tooadd IP-adresbeperkingen
1. Klik op Hallo **configuratie voor toegangsbeheer** menu-item onder **instellingen**
1. Hallo-lijst met IP-adresbereiken toobe geaccepteerd door de trigger Hallo opgeven

Een geldig IP-bereik heeft Hallo notatie `192.168.1.1/255`. Als u Hallo logic app tooonly fire als een geneste logische app wilt, selecteer Hallo **alleen andere logic apps** optie. Deze optie wordt een lege matrix toohello bron, wat betekent dat alleen aanroepen vanuit Hallo-service zelf (bovenliggende logic apps) fire is.

> [!NOTE]
> U kunt nog steeds een logische app met een aanvraag-trigger uitvoeren via Hallo REST-API / Management `/triggers/{triggerName}/run` ongeacht IP. Dit scenario is vereist voor verificatie op basis van hello Azure REST-API en alle gebeurtenissen in hello Azure controlelogboek wordt weergegeven. Toegang instellen toegangsbeheerbeleid dienovereenkomstig.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Het instellen van IP-adresbereiken op Hallo resourcedefinitie

Als u een [implementatiesjabloon](logic-apps-create-deploy-template.md) tooautomate uw implementaties, Hallo IP-bereik instellingen kunnen worden geconfigureerd op Hallo resource-sjabloon.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Azure Active Directory, OAuth of andere beveiliging toevoegen

meer autorisatie boven op een logische app protocollen, tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) biedt uitgebreide controle, beveiliging, beleid en documentatie voor een willekeurig eindpunt met Hallo mogelijkheid tooexpose een logische app als een API. Azure API Management kan een openbare of particuliere eindpunt voor Hallo logische app, die gebruik Azure Active Directory, certificaat, OAuth of andere beveiligingsstandaarden maken kan worden blootgesteld. Wanneer een aanvraag wordt ontvangen, stuurt Azure API Management Hallo aanvraag toohello logic app (voor het uitvoeren van alle benodigde transformaties en beperkingen onderweg). U kunt Hallo binnenkomende IP-adresbereik instellingen op Hallo logic app tooonly kunt Hallo logic app toobe geactiveerd van API Management gebruiken.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Toegang tot beveiligde toomanage of bewerken logic apps

U kunt toegang toomanagement bewerkingen op een logische app beperken zodat alleen bepaalde gebruikers of groepen kunnen tooperform bewerkingen op Hallo resource. Logische apps gebruiken hello Azure [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) functie en kunnen worden aangepast met Hallo dezelfde hulpmiddelen.  Er zijn enkele ingebouwde rollen die kunt u ook leden van uw abonnement tooas toewijzen:

* **Logic App Inzender** -toegang tooview, bewerken en bijwerken van een logische app biedt.  Kan resource Hallo verwijderen of admin bewerkingen uitvoeren.
* **Logic App Operator** : kan hello logische app en uitvoeringsgeschiedenis weergeven en in-of uitschakelen.  Niet kunt bewerken of Hallo-definitie bijwerken.

U kunt ook [Azure Resource vergrendeling](../azure-resource-manager/resource-group-lock-resources.md) tooprevent wijzigen of verwijderen van logische apps. Deze mogelijkheid is waardevolle tooprevent productiebronnen niet gewijzigd of verwijderd.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Veilige toegang toocontents Hallo geschiedenis uitvoeren

U kunt toegang toocontents van in- of uitgangen beperken van vorige uitgevoerd toospecific IP-adresbereiken.  

Alle gegevens binnen een werkstroom uitgevoerd is versleuteld in rust en onderweg. Wanneer een toorun gespreksgeschiedenis wordt gedaan, wordt Hallo service verifieert Hallo-aanvraag en biedt koppelingen toohello aanvraag en antwoord-invoer en uitvoer. Deze koppeling kan worden beveiligd zodat alleen aanvragen tooview inhoud uit een aangewezen IP-adresbereik Hallo inhoud retourneren. Voor extra toegangsbeheer kunt u deze mogelijkheid. U kunt zelfs opgeven met een IP-adres zoals `0.0.0.0` zodat niemand toegang de invoer/uitvoer tot heeft. Alleen gebruikers met beheerdersmachtigingen kan deze beperking Hallo mogelijkheid bieden voor 'just in time' toegang tooworkflow inhoud verwijderen.

Deze instelling kan worden geconfigureerd in de broninstellingen Hallo Hallo Azure-portal:

1. Open in hello Azure-portal, Hallo logische app die u wilt dat tooadd IP-adresbeperkingen
1. Klik op Hallo **configuratie voor toegangsbeheer** menu-item onder **instellingen**
1. Lijst met IP-adresbereiken voor toegang tot toocontent Hallo opgeven

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Het instellen van IP-adresbereiken op Hallo resourcedefinitie

Als u een [implementatiesjabloon](logic-apps-create-deploy-template.md) tooautomate uw implementaties, Hallo IP-bereik instellingen kunnen worden geconfigureerd op Hallo resource-sjabloon.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Beveiligde parameters en invoer binnen een werkstroom

U kunt tooparameterize sommige aspecten van de werkstroomdefinitie van een voor implementatie in omgevingen. Sommige parameters mogelijk ook beveiligde parameters die u niet wilt dat tooappear bij het bewerken van een werkstroom, zoals een client-ID en clientgeheim voor [Azure Active Directory-verificatie](../connectors/connectors-native-http.md#authentication) van een HTTP-actie.

### <a name="using-parameters-and-secure-parameters"></a>Parameters en beveiligde parameters gebruiken

tooaccess Hallo waarde van een resourceparameter tijdens runtime hello [werkstroom definition language](http://aka.ms/logicappsdocs) biedt een `@parameters()` bewerking. U kunt ook [parameters opgeven in de sjabloon voor de implementatie van Hallo resource](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Maar als u Hallo parametertype als opgeeft `securestring`, Hallo-parameter niet geretourneerd met de rest van de resourcedefinitie Hallo Hallo en niet toegankelijk door Hallo resource na implementatie weer te geven.

> [!NOTE]
> Als de parameter wordt gebruikt in Hallo headers of de hoofdtekst van een aanvraag, Hallo parameter mogelijk zichtbaar via Hallo uitvoeren geschiedenis en uitgaande HTTP-aanvraag. Zorg ervoor dat tooset uw beleid voor toegang tot inhoud dienovereenkomstig.
> Autorisatie-header zijn nooit zichtbaar via in- of uitgangen. Als er Hallo geheim wordt gebruikt, is Hallo geheim dus niet worden opgehaald.

#### <a name="resource-deployment-template-with-secrets"></a>Resource-implementatiesjabloon met geheimen

Hallo volgende voorbeeld ziet u een implementatie die verwijst naar een veilige parameter van het `secret` tijdens runtime. U kan Hallo omgevingswaarde voor Hallo opgeven in een afzonderlijke parameterbestand `secret`, of gebruik [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve geheimen op tijd implementeren.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Toegang tot beveiligde tooservices ontvangende aanvragen van een werkstroom

Er zijn veel manieren toohelp veilig dat eindpunt Hallo logic Apps moet tooaccess.

### <a name="using-authentication-on-outbound-requests"></a>Met behulp van verificatie voor uitgaande aanvragen

Als u werkt met een HTTP-, HTTP + Swagger (Open API) of Webhook actie, kunt u toevoegen toohello verificatieaanvraag wordt verzonden. U kunt opnemen basisverificatie, verificatie via certificaat of Azure Active Directory-verificatie. Meer informatie over hoe tooconfigure deze verificatie vindt [in dit artikel](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Beperken van toegang toologic app IP-adressen

Alle aanroepen vanuit logic apps is afkomstig van een specifieke set IP-adressen per regio. U kunt ook aanvullende filters toevoegen tooonly accepteren van aanvragen van het aangewezen IP-adressen. Zie voor een lijst van deze IP-adressen, [logic app en -configuratie](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>On-premises connectiviteit

Logische apps bieden integratie met verschillende services tooprovide veilige en betrouwbare lokale communicatie.

#### <a name="on-premises-data-gateway"></a>On-premises gegevensgateway

Veel beheerde connectors voor logic apps bieden beveiligde verbindingen tooon-premises systemen, met inbegrip van bestandssysteem, SQL, SharePoint, DB2 en meer. Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus. Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent. Meer informatie over [de werking van de gegevensgateway Hallo](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Azure API Management

[Azure API Management](https://azure.microsoft.com/services/api-management/) heeft lokale connectiviteitsopties, met inbegrip van site-naar-site-VPN en ExpressRoute-integratie voor beveiligde proxy en communicatie tooon-premises systemen. In Hallo Logic App-ontwerper, kunt u snel een API blootgesteld aan Azure API Management binnen een werkstroom die snelle toegang tooon-premises systemen selecteren.

#### <a name="hybrid-connections-from-azure-app-service"></a>Hybride verbindingen van Azure App Service

U kunt Hallo lokale hybride verbinding functie gebruiken voor Azure-API en Web-apps toocommunicate on-premises.  Meer informatie over hybride verbindingen en hoe tooconfigure vindt [in dit artikel](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Volgende stappen
[Maken van een sjabloon voor de implementatie](logic-apps-create-deploy-template.md)  
[Afhandeling van uitzonderingen](logic-apps-exception-handling.md)  
[Uw logische apps bewaken](logic-apps-monitor-your-logic-apps.md)  
[Logic app fouten en problemen oplossen](logic-apps-diagnosing-failures.md)  
