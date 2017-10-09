---
title: Fout bij het bronbeleid Azure aaaRequestDisallowedByPolicy | Microsoft Docs
description: Hallo oorzaak Hallo RequestDisallowedByPolicy fout beschrijft.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Fout bij het bronbeleid Azure RequestDisallowedByPolicy

Dit artikel wordt beschreven Hallo oorzaak van Hallo RequestDisallowedByPolicy fout, het bevat ook oplossing voor deze fout.

## <a name="symptom"></a>Symptoom

Wanneer u een actie tijdens de implementatie van toodo probeert, verschijnt er een **RequestDisallowedByPolicy** fout waardoor het Hallo-actie worden uitgevoerd. Hallo volgt een voorbeeld van Hallo-fout:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Problemen oplossen

tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd Hallo na een Hallo methoden gebruiken:

### <a name="method-1"></a>Methode 1

In PowerShell bieden die beleids-id als Hallo **Id** parameter tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Methode 2 

Geef in de Azure CLI 2.0, Hallo-naam van de beleidsdefinitie Hallo: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Oplossing

Voor beveiliging of naleving uw IT-afdeling kan resource beleid afdwingen dat verbiedt het openbare IP-adressen, Netwerkbeveiligingsgroepen, door de gebruiker gedefinieerde Routes of routetabellen maken. In voorbeeld van Hallo foutbericht dat wordt beschreven in de sectie 'Symptomen' Hallo HALLO hallo-beleid heet **regionPolicyDefinition**, maar het zou kunnen verschillen.
tooresolve dit probleem werken met uw IT-afdeling tooreview Hallo bronbeleid en bepalen hoe tooperform Hallo aangevraagd in overeenstemming met deze beleidsregels in te grijpen.


Zie voor meer informatie Hallo artikelen te volgen:

- [Overzicht van de resource-beleid](resource-manager-policy.md)
- [Algemene implementatie fouten RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


