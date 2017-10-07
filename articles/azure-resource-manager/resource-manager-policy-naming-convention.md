---
title: bronbeleid aaaAzure voor naamconventies | Microsoft Docs
description: Beschrijving van het Azure Resource Manager-beleid voor de naamgeving van de resource.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Resource-beleid toepassen op namen en tekst
Dit onderwerp bevat verschillende [bronbeleid](resource-manager-policy.md) u tooestablish naming en tekst conventies kunt toepassen. Deze beleidsregels consistentie voor resourcenamen en labelwaarden. 

## <a name="set-naming-convention-with-wildcard"></a>Stel naamconventie met jokerteken
Hallo volgende voorbeeld ziet u Hallo gebruik van jokertekens, die wordt ondersteund door Hallo **zoals** voorwaarde. Hallo voorwaarde aangegeven dat als hello naam komt overeen met de genoemde patroon hello (namePrefix\*nameSuffix) vervolgens weigeren Hallo-aanvraag:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Stel de naamgevingsconventie met patroon

toospecify of resourcenamen overeenkomen met een patroon, gebruik Hallo overeenkomen met de voorwaarde. Hallo volgende voorbeeld vereist dat namen toostart met `contoso` en zes aanvullende letters bevatten:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Patroon voor de labelwaarde datum instellen

een datum-patroon van twee cijfers, streepjes, drie letters, streepjes en vier cijfers gebruik toorequire:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel (zoals weergegeven in de voorgaande voorbeelden Hallo), u moet toocreate hello beleidsdefinitie en wijs deze tooa bereik. Hallo bereik mag een abonnement, resourcegroep of resource. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md). 
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

