---
title: Azure beheerde toepassing SizeSelector UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Compute.SizeSelector UI-element voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Microsoft.Compute.SizeSelector UI-element
Een besturingselement voor het selecteren van een grootte voor een of meer exemplaren van de virtuele machine. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Opmerkingen
- `recommendedSizes`moet ten minste één grootte bevatten. De eerste aanbevolen grootte wordt als standaardwaarde gebruikt.
- Als een aanbevolen grootte niet beschikbaar in de geselecteerde locatie is, wordt de grootte automatisch overgeslagen. In plaats daarvan wordt de volgende aanbevolen grootte gebruikt.
- Elke grootte niet is opgegeven in de `constraints.allowedSizes` is verborgen, en elke grootte niet is opgegeven in `constraints.excludedSizes` wordt weergegeven.
`constraints.allowedSizes`en `constraints.excludedSizes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt. Kan de lijst met beschikbare grootten worden bepaald door het aanroepen van [lijst met beschikbare virtuele machine grootten voor een abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform`moet worden opgegeven en kan **Windows** of **Linux**. Wordt gebruikt om de hardwarekosten van de virtuele machines te bepalen.
- `imageReference`wordt weggelaten voor directe installatiekopieën, maar de opgegeven voor de installatiekopieën van derden. Wordt gebruikt om de softwarekosten van de virtuele machines te bepalen.
- `count`wordt gebruikt om de juiste vermenigvuldiger voor het element. Een statische waarde, zoals ondersteunt **2**, of een dynamische waarde van een ander element, zoals `[steps('step1').vmCount]`. De standaardwaarde is **1**.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
"Standard_D1"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
