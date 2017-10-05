---
title: Azure-beheerde toepassing UI definitie functies maken | Microsoft Docs
description: Beschrijft de functies voor gebruik bij het samenstellen van UI-definities voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 635e44a7ec6f9244f5fe75eb5ad947cdd8ae59a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition elementen
Dit artikel wordt beschreven voor het schema en de eigenschappen voor alle ondersteunde elementen van een CreateUiDefinition. Gebruik van deze elementen wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md). Het schema voor de meeste elementen is als volgt:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Eigenschap | Vereist | Beschrijving |
| -------- | -------- | ----------- |
| naam | Ja | Een interne id om te verwijzen naar een specifiek exemplaar van een element. Het meest voorkomende gebruik van de naam van het element is in `outputs`, waarbij de uitvoerwaarden van de opgegeven elementen zijn toegewezen aan de parameters van de sjabloon. U kunt het ook gebruiken binden van de uitvoerwaarde van een element op de `defaultValue` van een ander element. |
| type | Ja | De UI-besturingselement om weer te geven voor het element. Zie voor een lijst van ondersteunde typen [elementen](#elements). |
| Label | Ja | De weergavetekst van het element. Sommige elementtypen bevatten meerdere labels, zodat de waarde kan een object met meerdere tekenreeksen zijn. |
| Standaardwaarde | Nee | De standaardwaarde van het element. Sommige elementtypen ondersteuning voor complexe standaardwaarden, zodat de waarde kan een object zijn. |
| Knopinfo | Nee | De tekst die moet worden weergegeven in de knopinfo van het element. Net als bij `label`, bepaalde onderdelen van de ondersteuning van meerdere hulpprogramma tip tekenreeksen. Inline koppelingen kunnen worden ingesloten met Markdown-syntaxis.
| Beperkingen | Nee | Een of meer eigenschappen die worden gebruikt voor het validatiegedrag van het element aanpassen. De ondersteunde eigenschappen voor beperkingen verschillen per elementtype. Sommige elementtypen doen geen ondersteuning voor aanpassing van het validatiegedrag en hebben dus geen beperkingen-eigenschap. |
| Opties | Nee | Aanvullende eigenschappen die het gedrag van het element aanpassen. Net als bij `constraints`, de ondersteunde eigenschappen is afhankelijk van elementtype. |
| Zichtbaar | Nee | Hiermee wordt aangegeven of het element wordt weergegeven. Als `true`, het element en de betreffende onderliggende elementen worden weergegeven. De standaardwaarde is `true`. Gebruik [logische functies](managed-application-createuidefinition-functions.md#logical-functions) waarde van de eigenschap dynamisch kunt bepalen.

## <a name="elements"></a>Elementen

De documentatie voor elk element bevat een voorbeeld van een gebruikersinterface, schema, opmerkingen van het gedrag van het element (meestal met betrekking tot validatie en ondersteunde aanpassing) en een voorbeeld van uitvoer.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
