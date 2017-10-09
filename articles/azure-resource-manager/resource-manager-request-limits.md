---
title: Resource Manager-aanvraaglimieten aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse beperking met Azure Resource Manager vraagt als abonnementen is bereikt.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Beperking van Resource Manager-aanvragen
Voor elk abonnement en de tenant, limieten voor Resource Manager aanvragen too15, 000 per uur lezen en schrijven aanvragen too1, 200 per uur. Deze limieten gelden tooeach Azure Resource Manager-instantie; Er zijn meerdere exemplaren in elke Azure-regio en Azure Resource Manager geïmplementeerde tooall Azure is regio's.  Dus in de praktijk limieten effectief veel hoger dan de zijn hierboven vermelde, als gebruiker worden aanvragen doorgaans afgehandeld door veel verschillende exemplaren.

Als uw toepassing of het script is deze limiet bereikt, moet u toothrottle uw aanvragen. Dit onderwerp leest u hoe toodetermine Hallo resterende aanvragen voordat het Hallo-limiet bereikt, en hoe toorespond wanneer u Hallo limiet hebt bereikt.

Wanneer u Hallo-limiet bereikt, ontvangt u Hallo HTTP-statuscode **429 te veel aanvragen**.

het aantal aanvragen Hallo bereik tooeither is uw abonnement of uw tenant. Als er meerdere, gelijktijdige toepassingen voor aanvragen die in uw abonnement Hallo aanvragen van deze toepassingen opgeteld toodetermine Hallo aantal resterende aanvragen.

Verzoeken om abonnementen binnen het bereik zijn toepassingsgroepen Hallo betrekking hebben op uw abonnements-id, zoals bij het ophalen van Hallo resourcegroepen in uw abonnement wordt doorgegeven. Aanvragen van de tenant die binnen het bereik van opnemen uw abonnements-id, zoals bij het ophalen van geldige Azure locaties niet.

## <a name="remaining-requests"></a>Overige aanvragen
Het aantal resterende aanvragen Hallo kunt u bepalen aan de hand van antwoordheaders. Elke aanvraag bevat de waarden voor Hallo aantal resterende lees- en schrijfaanvragen. Hallo staan volgende tabel Hallo antwoordheaders die u voor deze waarden kunt controleren:

| Reactieheader | Beschrijving |
| --- | --- |
| x-MS-ratelimit-Remaining-Subscription-reads |Abonnement bereik leest resterende |
| x-MS-ratelimit-Remaining-Subscription-Writes |Abonnement bereik schrijft resterende |
| x-MS-ratelimit-Remaining-tenant-reads |Tenant bereik leest resterende |
| x-MS-ratelimit-Remaining-tenant-Writes |Tenant bereik schrijft resterende |
| x-MS-ratelimit-Remaining-Subscription-resource-Requests |Abonnement binnen het bereik van aanvragen van het type resource resterende.<br /><br />Deze headerwaarde wordt alleen geretourneerd als een service Hallo standaardlimiet is genegeerd. Resource Manager wordt toegevoegd voor deze waarde in plaats van Hallo abonnement lees- of schrijfbewerkingen. |
| x-MS-ratelimit-Remaining-Subscription-resource-ENTITIES-Read |Abonnement resource type verzameling aanvragen resterende binnen het bereik.<br /><br />Deze headerwaarde wordt alleen geretourneerd als een service Hallo standaardlimiet is genegeerd. Deze waarde biedt Hallo aantal aanvragen voor resterende (lijst met resources). |
| x-MS-ratelimit-Remaining-tenant-resource-Requests |Tenant aanvragen van het type resource resterende binnen het bereik.<br /><br />Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet hallo overschreven. Resource Manager wordt toegevoegd voor deze waarde in plaats van Hallo tenant lees- of schrijfbewerkingen. |
| x-MS-ratelimit-Remaining-tenant-resource-ENTITIES-Read |Tenant resource type verzameling aanvragen resterende binnen het bereik.<br /><br />Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet hallo overschreven. |

## <a name="retrieving-hello-header-values"></a>Hallo-headerwaarden ophalen
Bij het ophalen van deze headerwaarden in uw code of het script is niet anders dan bij het ophalen van een headerwaarde. 

Bijvoorbeeld in **C#**, ophalen van Hallo header-waarde van een **HttpWebResponse** object met de naam **antwoord** Hello code te volgen:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

In **PowerShell**, u Hallo header-waarde wordt opgehaald uit een bewerking Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Of, indien het gewenste toosee Hallo resterende aanvragen voor foutopsporing, kunt u Hallo bieden **-Debug** parameter op uw **PowerShell** cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

Die veel waarden, waaronder Hallo na antwoord-waarde geretourneerd:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

In **Azure CLI**, u Hallo headerwaarde ophalen met behulp van Hallo uitgebreidere optie.

```azurecli
azure group list -vv --json
```

Die veel waarden, waaronder Hallo na-object geretourneerd:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Wacht voordat het volgende aanvraag verzenden
Wanneer u Hallo aanvraaglimiet heeft bereikt, Resource Manager Hallo retourneert **429** HTTP-statuscode en een **opnieuw proberen na** waarde in Hallo-header. Hallo **opnieuw proberen na** waarde geeft Hallo aantal seconden dat uw toepassing moet wachten (of slaapstand) voordat u de volgende aanvraag Hallo verzendt. Als u een aanvraag verzenden voordat het Hallo-waarde voor opnieuw proberen is verstreken, wordt uw aanvraag is niet verwerkt en wordt een nieuwe retry-waarde geretourneerd.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over limieten en quota's [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).
* toolearn over het verwerken van aanvragen voor asynchrone REST, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).
