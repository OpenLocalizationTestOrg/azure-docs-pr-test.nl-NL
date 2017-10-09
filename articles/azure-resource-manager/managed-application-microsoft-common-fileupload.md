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
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="5ca20-103">Microsoft.Common.FileUpload UI-element</span><span class="sxs-lookup"><span data-stu-id="5ca20-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="5ca20-104">Een besturingselement waarmee een gebruiker toospecify kan een of meer bestanden tooupload.</span><span class="sxs-lookup"><span data-stu-id="5ca20-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="5ca20-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5ca20-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5ca20-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5ca20-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="5ca20-108">Schema</span><span class="sxs-lookup"><span data-stu-id="5ca20-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="5ca20-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5ca20-109">Remarks</span></span>
- <span data-ttu-id="5ca20-110">`constraints.accept`Hiermee geeft u Hallo typen bestanden die worden weergegeven in het dialoogvenster van de browser van het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5ca20-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="5ca20-111">Zie Hallo [HTML5-specificatie](http://www.w3.org/TR/html5/forms.html#attr-input-accept) voor toegestane waarden.</span><span class="sxs-lookup"><span data-stu-id="5ca20-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="5ca20-112">de standaardwaarde Hallo is **null**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-112">hello default value is **null**.</span></span>
- <span data-ttu-id="5ca20-113">Als `options.multiple` te is ingesteld,**true**, Hallo gebruiker tooselect meer dan één bestand in een bestandsdialoogvenster Hallo van de browser is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="5ca20-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="5ca20-114">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-114">hello default value is **false**.</span></span>
- <span data-ttu-id="5ca20-115">Dit element ondersteunt bestanden zijn geüpload in twee modi gebaseerd op Hallo-waarde van `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="5ca20-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="5ca20-116">Als **bestand** is opgegeven, Hallo uitvoer Hallo inhoud van Hallo-bestand als een blob bevat.</span><span class="sxs-lookup"><span data-stu-id="5ca20-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="5ca20-117">Als **url** is opgegeven, dan Hallo bestand geüploade tooa tijdelijke locatie en Hallo uitvoer Hallo-URL van Hallo blob bevat.</span><span class="sxs-lookup"><span data-stu-id="5ca20-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="5ca20-118">Tijdelijke blobs wordt opgeschoond na 24 uur.</span><span class="sxs-lookup"><span data-stu-id="5ca20-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="5ca20-119">de standaardwaarde Hallo is **bestand**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-119">hello default value is **file**.</span></span>
- <span data-ttu-id="5ca20-120">waarde van Hallo `options.openMode` bepaalt hoe Hallo-bestand wordt gelezen.</span><span class="sxs-lookup"><span data-stu-id="5ca20-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="5ca20-121">Als Hallo bestand verwachte toobe als tekst zonder opmaak, geef **tekst**; anders is, geef **binaire**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="5ca20-122">de standaardwaarde Hallo is **tekst**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-122">hello default value is **text**.</span></span>
- <span data-ttu-id="5ca20-123">Als `options.uploadMode` te is ingesteld,**bestand** en `options.openMode` te is ingesteld,**binaire**, Hallo uitvoer is base64-gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="5ca20-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="5ca20-124">`options.encoding`Hiermee geeft u Hallo codering toouse wanneer het Hallo-bestand te lezen.</span><span class="sxs-lookup"><span data-stu-id="5ca20-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="5ca20-125">de standaardwaarde Hallo is **UTF-8**, en wordt gebruikt alleen wanneer `options.openMode` te is ingesteld**tekst**.</span><span class="sxs-lookup"><span data-stu-id="5ca20-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5ca20-126">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="5ca20-126">Sample output</span></span>
<span data-ttu-id="5ca20-127">Als options.multiple ingesteld op false is en options.uploadMode bestand is, bevat de uitvoer van de inhoud van de Hallo van Hallo-bestand als een JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="5ca20-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="5ca20-128">Als options.multiple ingesteld op true is and'options.uploadMode bestand is, wordt de uitvoer bevat Hallo inhoud van Hallo bestanden als een JSON-matrix:</span><span class="sxs-lookup"><span data-stu-id="5ca20-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="5ca20-129">Als options.multiple ingesteld op false is en options.uploadMode url, bevat de uitvoer een URL als een JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="5ca20-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="5ca20-130">Als options.multiple ingesteld op true is en options.uploadMode url, bevat de uitvoer een lijst met URL's als een JSON-matrix:</span><span class="sxs-lookup"><span data-stu-id="5ca20-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="5ca20-131">Bij het testen van een CreateUiDefinition afkappen sommige browsers (zoals Google Chrome) URL's die worden gegenereerd door Hallo Microsoft.Common.FileUpload element in Hallo browserconsole.</span><span class="sxs-lookup"><span data-stu-id="5ca20-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="5ca20-132">Mogelijk moet u tooright en klik op afzonderlijke koppelingen toocopy Hallo volledige URL's.</span><span class="sxs-lookup"><span data-stu-id="5ca20-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ca20-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ca20-133">Next steps</span></span>
* <span data-ttu-id="5ca20-134">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ca20-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5ca20-135">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ca20-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5ca20-136">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5ca20-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
