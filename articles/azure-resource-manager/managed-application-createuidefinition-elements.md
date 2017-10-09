---
title: UI-definitie functies maken voor aaaAzure beheerde toepassingen | Microsoft Docs
description: Hierin wordt beschreven Hallo functies toouse tijdens het construeren van UI-definities voor beheerde Azure-toepassingen
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
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition elementen
In dit artikel beschrijft Hallo schema en eigenschappen voor alle ondersteunde elementen van een CreateUiDefinition. Gebruik van deze elementen wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md). Hallo-schema voor de meeste elementen is als volgt:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Eigenschap | Vereist | Beschrijving |
| -------- | -------- | ----------- |
| naam | Ja | Een interne id tooreference een specifiek exemplaar van een element. Hallo meest voorkomende gebruik van Hallo elementnaam is in `outputs`, waarbij de uitvoerwaarden Hallo Hallo opgegeven elementen zijn toegewezen toohello parameters van de sjabloon Hallo. U kunt deze ook gebruiken toobind Hallo uitvoerwaarde van een element toohello `defaultValue` van een ander element. |
| type | Ja | Hallo toorender van UI-besturingselement voor Hallo-element. Zie voor een lijst van ondersteunde typen [elementen](#elements). |
| Label | Ja | Hallo weergavetekst van Hallo-element. Sommige elementtypen bevatten meerdere labels dus Hallo-waarde kan een object met meerdere tekenreeksen zijn. |
| Standaardwaarde | Nee | de standaardwaarde Hallo van Hallo-element. Sommige elementtypen ondersteuning voor complexe standaardwaarden, zodat het Hallo-waarde kan een object worden. |
| Knopinfo | Nee | Hallo toodisplay tekst in de knopinfo Hallo van Hallo-element. Vergelijkbare te`label`, bepaalde onderdelen van de ondersteuning van meerdere hulpprogramma tip tekenreeksen. Inline koppelingen kunnen worden ingesloten met Markdown-syntaxis.
| Beperkingen | Nee | Een of meer eigenschappen die gebruikt toocustomize hello validatiegedrag van Hallo-element zijn. Eigenschappen voor beperkingen Hallo ondersteund verschillen per elementtype. Sommige elementtypen doen geen ondersteuning voor aanpassing van Hallo validatiegedrag en hebben dus geen beperkingen-eigenschap. |
| Opties | Nee | Aanvullende eigenschappen die Hallo gedrag van Hallo element aanpassen. Vergelijkbare te`constraints`, Hallo ondersteund eigenschappen verschillen per elementtype. |
| Zichtbaar | Nee | Hiermee wordt aangegeven of het Hallo-element wordt weergegeven. Als `true`, Hallo-element en de betreffende onderliggende elementen worden weergegeven. de standaardwaarde Hallo is `true`. Gebruik [logische functies](managed-application-createuidefinition-functions.md#logical-functions) toodynamically bepalen de waarde van deze eigenschap.

## <a name="elements"></a>Elementen

Hallo-documentatie voor elk element bevat een voorbeeld van een gebruikersinterface, schema, opmerkingen op Hallo gedrag van het Hallo-element (meestal met betrekking tot validatie en ondersteunde aanpassing) en voorbeeld van uitvoer.

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
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
