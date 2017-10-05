---
title: Azure beheerde toepassing FileUpload UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Common.FileUpload UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="04030-103">Microsoft.Common.FileUpload UI-element</span><span class="sxs-lookup"><span data-stu-id="04030-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="04030-104">Een besturingselement waarmee een gebruiker om op te geven van een of meer bestanden te uploaden.</span><span class="sxs-lookup"><span data-stu-id="04030-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="04030-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="04030-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="04030-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="04030-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="04030-108">Schema</span><span class="sxs-lookup"><span data-stu-id="04030-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="04030-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="04030-109">Remarks</span></span>
- <span data-ttu-id="04030-110">`constraints.accept`Hiermee geeft u de typen bestanden die worden weergegeven in het dialoogvenster bestand van de browser.</span><span class="sxs-lookup"><span data-stu-id="04030-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="04030-111">Zie de [HTML5-specificatie](http://www.w3.org/TR/html5/forms.html#attr-input-accept) voor toegestane waarden.</span><span class="sxs-lookup"><span data-stu-id="04030-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="04030-112">De standaardwaarde is **null**.</span><span class="sxs-lookup"><span data-stu-id="04030-112">The default value is **null**.</span></span>
- <span data-ttu-id="04030-113">Als `options.multiple` is ingesteld op **true**, de gebruiker kan meer dan één bestand selecteren in het dialoogvenster bestand van de browser.</span><span class="sxs-lookup"><span data-stu-id="04030-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="04030-114">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="04030-114">The default value is **false**.</span></span>
- <span data-ttu-id="04030-115">Dit element ondersteunt bestanden zijn geüpload in twee modi, afhankelijk van de waarde van `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="04030-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="04030-116">Als **bestand** is opgegeven, wordt de uitvoer bevat de inhoud van het bestand als een blob.</span><span class="sxs-lookup"><span data-stu-id="04030-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="04030-117">Als **url** is opgegeven, wordt het bestand is geüpload naar een tijdelijke locatie en de uitvoer de URL van de blob bevat.</span><span class="sxs-lookup"><span data-stu-id="04030-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="04030-118">Tijdelijke blobs wordt opgeschoond na 24 uur.</span><span class="sxs-lookup"><span data-stu-id="04030-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="04030-119">De standaardwaarde is **bestand**.</span><span class="sxs-lookup"><span data-stu-id="04030-119">The default value is **file**.</span></span>
- <span data-ttu-id="04030-120">De waarde van `options.openMode` bepaalt hoe het bestand wordt gelezen.</span><span class="sxs-lookup"><span data-stu-id="04030-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="04030-121">Als het bestand wordt verwacht als tekst zonder opmaak, geeft u **tekst**; anders is, geef **binaire**.</span><span class="sxs-lookup"><span data-stu-id="04030-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="04030-122">De standaardwaarde is **tekst**.</span><span class="sxs-lookup"><span data-stu-id="04030-122">The default value is **text**.</span></span>
- <span data-ttu-id="04030-123">Als `options.uploadMode` is ingesteld op **bestand** en `options.openMode` is ingesteld op **binaire**, de uitvoer is base64-gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="04030-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="04030-124">`options.encoding`Hiermee geeft u de codering die moet worden gebruikt bij het lezen van het bestand.</span><span class="sxs-lookup"><span data-stu-id="04030-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="04030-125">De standaardwaarde is **UTF-8**, en dient alleen wanneer `options.openMode` is ingesteld op **tekst**.</span><span class="sxs-lookup"><span data-stu-id="04030-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="04030-126">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="04030-126">Sample output</span></span>
<span data-ttu-id="04030-127">Als options.multiple ingesteld op false is en options.uploadMode bestand is, bevat de uitvoer de inhoud van het bestand als een JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="04030-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="04030-128">Als options.multiple ingesteld op true is and'options.uploadMode bestand is, wordt de uitvoer bevat de inhoud van de bestanden als een JSON-matrix:</span><span class="sxs-lookup"><span data-stu-id="04030-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="04030-129">Als options.multiple ingesteld op false is en options.uploadMode url, bevat de uitvoer een URL als een JSON-tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="04030-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="04030-130">Als options.multiple ingesteld op true is en options.uploadMode url, bevat de uitvoer een lijst met URL's als een JSON-matrix:</span><span class="sxs-lookup"><span data-stu-id="04030-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="04030-131">Bij het testen van een CreateUiDefinition afkappen sommige browsers (zoals Google Chrome) URL's die worden gegenereerd door het element Microsoft.Common.FileUpload in de browserconsole.</span><span class="sxs-lookup"><span data-stu-id="04030-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="04030-132">U moet mogelijk met de rechtermuisknop op afzonderlijke koppelingen voor het kopiëren van de volledige URL's.</span><span class="sxs-lookup"><span data-stu-id="04030-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="04030-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04030-133">Next steps</span></span>
* <span data-ttu-id="04030-134">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04030-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="04030-135">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04030-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="04030-136">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="04030-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
