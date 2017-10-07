---
title: aaaAzure gebeurtenis raster beveiligings- en -verificatie
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Gebeurtenis raster beveiligings- en -verificatie 

Azure Event raster heeft drie soorten verificatie:

* Gebeurtenisabonnementen
* Gebeurtenis publiceren
* WebHook gebeurtenis levering

## <a name="webhook-event-delivery"></a>WebHook gebeurtenis levering

Webhooks zijn veel manieren tooreceive gebeurtenissen in realtime uit Azure Event raster.

Elke keer dat er wordt een nieuwe gebeurtenis gereed toobe geleverd, verzendt gebeurtenis raster een HTTP-aanvraag met tooyour WebHook met Hallo-gebeurtenis in de hoofdtekst van het Hallo.

Wanneer u uw eigen WebHook-eindpunt met raster gebeurtenis registreert, stuurt u een POST-aanvraag met een eenvoudige validatie-code in volgorde tooprove eindpunt eigendom. Uw app moet toorespond door echo back Hallo validatiecode. Gebeurtenis raster levert niet gebeurtenissen tooWebHook-eindpunten die u hebt de Hallo validatie niet doorstaan.
 
### <a name="validation-details"></a>Validatie-details:

* Gebeurtenis raster boekt bij Hallo gebeurtenis abonnement maken of bij te werken, een 'SubscriptionValidationEvent' gebeurtenis toohello doel-eindpunt.
* Hallo-gebeurtenis bevat een waarde voor header 'Validatie Type gebeurtenis:'.
* hoofdtekst van de gebeurtenis Hallo Hallo heeft hetzelfde schema als andere gebeurtenissen gebeurtenis raster.
* Hallo-gebeurtenisgegevens bevat de eigenschap 'ValidationCode' met een willekeurige tekenreeks bv. ' ValidationCode: acb13... '.

In de volgorde tooprove eindpunt eigendom echo back Hallo validatie code bijvoorbeeld ' ValidationResponse: acb13... '.

Ten slotte is het belangrijk toonote Azure gebeurtenis raster ondersteunt alleen HTTPS-webhook-eindpunten.
## <a name="event-subscription"></a>Voor een gebeurtenisabonnement

toosubscribe tooan gebeurtenis, hebt u Hallo **Microsoft.EventGrid/EventSubscriptions/Write** machtiging op Hallo resource vereist. U moet deze machtiging omdat u een nieuw abonnement bij Hallo bereik van de resource Hallo schrijft. Hallo vereist resource verschilt op basis van of u tooa systeemonderwerp of aangepaste onderwerp abonneert zich. Beide typen worden in deze sectie beschreven.

### <a name="system-topics-azure-service-publishers"></a>Systeemonderwerpen (uitgevers Azure-service)

Voor systeemonderwerpen moet u de machtiging toowrite een nieuw gebeurtenisabonnement bij Hallo bereik van Hallo resource publishing Hallo gebeurtenis. Hallo-indeling van het Hallo-resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Bijvoorbeeld: toosubscribe tooan gebeurtenis op een opslagaccount met de naam **MIJNACCT**, moet u de Hallo Microsoft.EventGrid/EventSubscriptions/Write machtiging op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Aangepaste-onderwerpen

Voor aangepaste onderwerpen moet u de machtiging toowrite een nieuw gebeurtenisabonnement bij Hallo bereik van Hallo gebeurtenis raster onderwerp. Hallo-indeling van het Hallo-resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Bijvoorbeeld: toosubscribe tooa aangepaste onderwerp met de naam **mytopic**, moet u de Hallo Microsoft.EventGrid/EventSubscriptions/Write machtiging op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Onderwerp publiceren

Onderwerpen over Shared Access Signature (SAS) of verificatie met sleutel gebruiken. SAS wordt aangeraden, maar sleutelverificatie biedt eenvoudige programmering en is compatibel met veel bestaande webhook uitgevers. 

In HTTP-header Hallo Hallo verificatie waarde te nemen. Gebruik voor SAS, **aeg-sas-token** voor Hallo header-waarde. Gebruik voor sleutelverificatie **aeg-sas-sleutel** voor Hallo header-waarde.

### <a name="key-authentication"></a>Verificatie met sleutel

Verificatie met een sleutel is Hallo eenvoudigste vorm van verificatie. Hallo-indeling gebruiken:`aeg-sas-key: <your key>`

Bijvoorbeeld het doorgeven van een sleutel met: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>SAS-tokens

SAS-tokens voor gebeurtenis raster bevatten Hallo resource, een verlooptijd en een handtekening. Hallo indeling van Hallo SAS-token is: `r={resource}&e={expiration}&s={signature}`.

Hallo resource is Hallo pad voor Hallo onderwerp toowhich u gebeurtenissen wilt verzenden. Een geldige resource-pad is bijvoorbeeld:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

U Hallo handtekening van een sleutel gegenereerd.

Bijvoorbeeld, een geldige **aeg-sas-token** waarde is:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Hallo volgende voorbeeld maakt een SAS-token voor gebruik met gebeurtenis raster:

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

Azure Event raster kunt u toocontrol Hallo niveau van toegang gegeven toodifferent gebruikers toodo verschillende bewerkingen zoals de lijst met abonnementen, maakt u nieuwe en sleutels te genereren. Gebeurtenis raster maakt gebruik van Azure toegang controleren RBAC (Role Based) voor deze.

### <a name="operation-types"></a>Bewerkingstypen

Azure event raster ondersteunt Hallo van de volgende activiteiten:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Hallo laatste drie bewerkingen return mogelijk geheime informatie dat buiten het normale leesbewerkingen opgehaald gefilterd. Het is best practice voor u toorestrict toothese toegangsbewerkingen. Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), en Hallo [REST-API](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Afdwingen van de rol op basis van de toegangscontrole (RBAC)

Volgende stappen tooenforce RBAC voor verschillende gebruikers hello gebruiken:

#### <a name="create-a-custom-role-definition-file-json"></a>Maken van een aangepaste rol-definitiebestand (.json)

Hallo hieronder vindt u voorbeeld gebeurtenis raster roldefinities waarmee gebruikers tooperform verschillende sets van acties.

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

#### <a name="install-and-login-tooazure-cli"></a>Installatie en aanmelding tooAzure CLI

* Azure CLI versie 0.8.8 of hoger. meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).
* Azure Resource Manager in Azure CLI. Ga te[Using hello Azure CLI Hello Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.

#### <a name="create-a-custom-role"></a>Een aangepaste beveiligingsrol maken

een aangepaste beveiligingsrol toocreate gebruiken:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Hallo rol tooa gebruiker toewijzen


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding-tooEvent raster [over gebeurtenis raster](overview.md)
