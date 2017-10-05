---
title: Azure Event raster beveiligings- en -verificatie
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a>Gebeurtenis raster beveiligings- en -verificatie 

Azure Event raster heeft drie soorten verificatie:

* Gebeurtenisabonnementen
* Gebeurtenis publiceren
* WebHook gebeurtenis levering

## <a name="webhook-event-delivery"></a>WebHook gebeurtenis levering

Webhooks zijn veel manieren voor het ontvangen van gebeurtenissen in realtime uit Azure Event raster.

Elke keer dat er wordt een nieuwe gebeurtenis gereed om te worden geleverd, wordt in gebeurtenis raster een HTTP-aanvraag met verzendt naar uw WebHook met de gebeurtenis in de hoofdtekst.

Wanneer u uw eigen WebHook-eindpunt met raster gebeurtenis registreert, stuurt u een POST-aanvraag met een eenvoudige validatiecode om te bewijzen dat eindpunt eigendom. Uw app moet reageren door echo terug code voor de validatie. Gebeurtenis raster levert geen gebeurtenissen naar WebHook-eindpunten die u hebt de validatie niet doorstaan.
 
### <a name="validation-details"></a>Validatie-details:

* Op het moment van gebeurtenis abonnement maken of bij te werken boekt raster gebeurtenis een gebeurtenis 'SubscriptionValidationEvent' naar het doel-eindpunt.
* De gebeurtenis bevat een waarde voor header 'Validatie Type gebeurtenis:'.
* De hoofdtekst van de gebeurtenis heeft hetzelfde schema als andere gebeurtenissen gebeurtenis raster.
* Gegevens van de gebeurtenis bevat de eigenschap 'ValidationCode' met een willekeurige tekenreeks bv. ' ValidationCode: acb13... '.

Om te bewijzen dat eindpunt eigendom, echo teruggestuurd de validatie code bijvoorbeeld ' ValidationResponse: acb13... '.

Ten slotte is het belangrijk te weten dat Azure gebeurtenis raster biedt alleen ondersteuning voor HTTPS-webhook-eindpunten.
## <a name="event-subscription"></a>Voor een gebeurtenisabonnement

Abonneren op een gebeurtenis, hebt u de **Microsoft.EventGrid/EventSubscriptions/Write** toegang tot de vereiste bron. U moet deze machtiging omdat u bij het schrijven van een nieuw abonnement op het bereik van de resource. De vereiste bron verschilt op basis van of u op een systeemonderwerp of aangepaste onderwerp abonneert zich. Beide typen worden in deze sectie beschreven.

### <a name="system-topics-azure-service-publishers"></a>Systeemonderwerpen (uitgevers Azure-service)

Voor systeemonderwerpen moet u machtigingen voor schrijven van een nieuw gebeurtenisabonnement bij het bereik van de bron voor het publiceren van de gebeurtenis. De indeling van de resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Bijvoorbeeld, om u te abonneren op een gebeurtenis op een opslagaccount met de naam **MIJNACCT**, moet u de machtiging Microsoft.EventGrid/EventSubscriptions/Write op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Aangepaste-onderwerpen

Voor aangepaste onderwerpen moet u machtigingen voor schrijven van een nieuw gebeurtenisabonnement bij het bereik van het onderwerp gebeurtenis raster. De indeling van de resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Bijvoorbeeld, om u te abonneren op een eigen onderwerp met de naam **mytopic**, moet u de machtiging Microsoft.EventGrid/EventSubscriptions/Write op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Onderwerp publiceren

Onderwerpen over Shared Access Signature (SAS) of verificatie met sleutel gebruiken. SAS wordt aangeraden, maar sleutelverificatie biedt eenvoudige programmering en is compatibel met veel bestaande webhook uitgevers. 

De verificatie-waarde in de HTTP-header te nemen. Gebruik voor SAS, **aeg-sas-token** voor de headerwaarde. Gebruik voor sleutelverificatie **aeg-sas-sleutel** voor de headerwaarde.

### <a name="key-authentication"></a>Verificatie met sleutel

Verificatie met een sleutel is de eenvoudigste vorm van verificatie. Gebruik de volgende indeling:`aeg-sas-key: <your key>`

Bijvoorbeeld het doorgeven van een sleutel met: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>SAS-tokens

SAS-tokens voor gebeurtenis raster zijn de resource een verlooptijd en een handtekening. De indeling van het SAS-token is: `r={resource}&e={expiration}&s={signature}`.

De resource is het pad voor het onderwerp waarnaar u gebeurtenissen wilt verzenden. Een geldige resource-pad is bijvoorbeeld:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

U de handtekening van een sleutel gegenereerd.

Bijvoorbeeld, een geldige **aeg-sas-token** waarde is:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Het volgende voorbeeld wordt een SAS-token voor gebruik met gebeurtenis raster:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Toegangsbeheer voor beheer

Azure Event raster kunt u bepalen het niveau van toegang krijgen tot andere gebruikers kunnen verschillende bewerkingen zoals de lijst met abonnementen doen, maakt u nieuwe en genereren van sleutels. Gebeurtenis raster maakt gebruik van Azure toegang controleren RBAC (Role Based) voor deze.

### <a name="operation-types"></a>Bewerkingstypen

Azure event raster ondersteunt de volgende acties:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

De laatste drie bewerkingen mogelijk geheime gegevens die buiten het normale leesbewerkingen opgehaald gefilterd als resultaat. Het is best practice voor u toegang tot deze bewerkingen te beperken. Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), en de [REST-API](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Afdwingen van de rol op basis van de toegangscontrole (RBAC)

Gebruik de volgende stappen uit om af te dwingen RBAC voor verschillende gebruikers:

#### <a name="create-a-custom-role-definition-file-json"></a>Maken van een aangepaste rol-definitiebestand (.json)

Hieronder vindt u voorbeeld gebeurtenis raster roldefinities waarmee gebruikers kunnen verschillende sets van acties uitvoeren.

**EventGridReadOnlyRole.json**: alleen toestaan alleen leesbewerkingen.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: toestaan beperkte post acties maar verwijderingsacties weigeren.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: kunnen alle gebeurtenis raster acties.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-to-azure-cli"></a>Installeren en meld u aan bij de Azure CLI

* Azure CLI versie 0.8.8 of hoger. Zie voor het installeren van de meest recente versie en deze koppelen aan uw Azure-abonnement, [installeren en configureren van de Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager in Azure CLI. Ga naar [met de Azure CLI met Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.

#### <a name="create-a-custom-role"></a>Een aangepaste beveiligingsrol maken

Gebruik het volgende voor het maken van een aangepaste rol:

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a>De rol toewijzen aan een gebruiker


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding tot gebeurtenis raster, [over gebeurtenis raster](overview.md)
