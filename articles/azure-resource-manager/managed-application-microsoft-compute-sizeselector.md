---
title: Beheerde toepassing SizeSelector UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Compute.SizeSelector UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
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
- `recommendedSizes`moet ten minste één grootte bevatten. Hallo eerst aanbevolen grootte Hallo standaard wordt gebruikt.
- Als een aanbevolen grootte niet beschikbaar op de locatie Hallo geselecteerd is, wordt automatisch Hallo grootte overgeslagen. In plaats daarvan wordt hello volgende aanbevolen grootte gebruikt.
- Elke grootte niet is opgegeven in Hallo `constraints.allowedSizes` is verborgen, en elke grootte niet is opgegeven in `constraints.excludedSizes` wordt weergegeven.
`constraints.allowedSizes`en `constraints.excludedSizes` zijn beide optioneel, maar niet gelijktijdig worden gebruikt. lijst met beschikbare grootten Hallo kan worden bepaald door het aanroepen van [lijst met beschikbare virtuele machine grootten voor een abonnement](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform`moet worden opgegeven en kan **Windows** of **Linux**. Deze toodetermine Hallo hardwarekosten van Hallo virtuele machines gebruikt.
- `imageReference`wordt weggelaten voor directe installatiekopieën, maar de opgegeven voor de installatiekopieën van derden. Deze toodetermine Hallo softwarekosten van Hallo virtuele machines gebruikt.
- `count`gebruikte tooset Hallo juiste vermenigvuldiger voor Hallo-element is. Een statische waarde, zoals ondersteunt **2**, of een dynamische waarde van een ander element, zoals `[steps('step1').vmCount]`. de standaardwaarde Hallo is **1**.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
"Standard_D1"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
