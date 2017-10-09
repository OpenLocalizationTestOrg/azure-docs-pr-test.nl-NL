---
title: Beheerde toepassing FileUpload UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Common.FileUpload UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Microsoft.Common.FileUpload UI-element
Een besturingselement waarmee een gebruiker toospecify kan een of meer bestanden tooupload. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Opmerkingen
- `constraints.accept`Hiermee geeft u Hallo typen bestanden die worden weergegeven in het dialoogvenster van de browser van het Hallo-bestand. Zie Hallo [HTML5-specificatie](http://www.w3.org/TR/html5/forms.html#attr-input-accept) voor toegestane waarden. de standaardwaarde Hallo is **null**.
- Als `options.multiple` te is ingesteld,**true**, Hallo gebruiker tooselect meer dan één bestand in een bestandsdialoogvenster Hallo van de browser is toegestaan. de standaardwaarde Hallo is **false**.
- Dit element ondersteunt bestanden zijn geüpload in twee modi gebaseerd op Hallo-waarde van `options.uploadMode`. Als **bestand** is opgegeven, Hallo uitvoer Hallo inhoud van Hallo-bestand als een blob bevat. Als **url** is opgegeven, dan Hallo bestand geüploade tooa tijdelijke locatie en Hallo uitvoer Hallo-URL van Hallo blob bevat. Tijdelijke blobs wordt opgeschoond na 24 uur. de standaardwaarde Hallo is **bestand**.
- waarde van Hallo `options.openMode` bepaalt hoe Hallo-bestand wordt gelezen. Als Hallo bestand verwachte toobe als tekst zonder opmaak, geef **tekst**; anders is, geef **binaire**. de standaardwaarde Hallo is **tekst**.
- Als `options.uploadMode` te is ingesteld,**bestand** en `options.openMode` te is ingesteld,**binaire**, Hallo uitvoer is base64-gecodeerd.
- `options.encoding`Hiermee geeft u Hallo codering toouse wanneer het Hallo-bestand te lezen. de standaardwaarde Hallo is **UTF-8**, en wordt gebruikt alleen wanneer `options.openMode` te is ingesteld**tekst**.

## <a name="sample-output"></a>Voorbeelduitvoer
Als options.multiple ingesteld op false is en options.uploadMode bestand is, bevat de uitvoer van de inhoud van de Hallo van Hallo-bestand als een JSON-tekenreeks:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Als options.multiple ingesteld op true is and'options.uploadMode bestand is, wordt de uitvoer bevat Hallo inhoud van Hallo bestanden als een JSON-matrix:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Als options.multiple ingesteld op false is en options.uploadMode url, bevat de uitvoer een URL als een JSON-tekenreeks:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Als options.multiple ingesteld op true is en options.uploadMode url, bevat de uitvoer een lijst met URL's als een JSON-matrix:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Bij het testen van een CreateUiDefinition afkappen sommige browsers (zoals Google Chrome) URL's die worden gegenereerd door Hallo Microsoft.Common.FileUpload element in Hallo browserconsole. Mogelijk moet u tooright en klik op afzonderlijke koppelingen toocopy Hallo volledige URL's.


## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
