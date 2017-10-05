---
title: Azure beheerde toepassing PublicIpAddressCombo UI-element | Microsoft Docs
description: Beschrijft het Microsoft.Network.PublicIpAddressCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="6b17c-103">Microsoft.Network.PublicIpAddressCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="6b17c-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="6b17c-104">Een groep besturingselementen voor het selecteren van een nieuw of bestaand openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6b17c-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="6b17c-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6b17c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6b17c-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6b17c-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="6b17c-108">Als de gebruiker 'None' voor openbare IP-adres selecteert, wordt het tekstvak domain name label verborgen.</span><span class="sxs-lookup"><span data-stu-id="6b17c-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="6b17c-109">Als de gebruiker selecteert een bestaand openbaar IP-adres, is het tekstvak label domein uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6b17c-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="6b17c-110">De waarde is het domeinnaamlabel van het geselecteerde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6b17c-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="6b17c-111">De domain name achtervoegsel (bijvoorbeeld westus.cloudapp.azure.com)-updates automatisch op basis van de geselecteerde locatie.</span><span class="sxs-lookup"><span data-stu-id="6b17c-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="6b17c-112">Schema</span><span class="sxs-lookup"><span data-stu-id="6b17c-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6b17c-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6b17c-113">Remarks</span></span>
- <span data-ttu-id="6b17c-114">Als `constraints.required.domainNameLabel` is ingesteld op **true**, de gebruiker moet een domeinnaamlabel opgeven bij het maken van een nieuw openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6b17c-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="6b17c-115">Bestaande openbare IP-adressen zonder een label zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="6b17c-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="6b17c-116">Als `options.hideNone` is ingesteld op **true**, klikt u vervolgens de optie te selecteren **geen** voor het openbare IP-adres wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="6b17c-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="6b17c-117">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="6b17c-117">The default value is **false**.</span></span>
- <span data-ttu-id="6b17c-118">Als `options.hideDomainNameLabel` is ingesteld op **true**, en vervolgens in het tekstvak voor domeinnaamlabel wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="6b17c-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="6b17c-119">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="6b17c-119">The default value is **false**.</span></span>
- <span data-ttu-id="6b17c-120">Als `options.hideExisting` is ingesteld op true, wordt de gebruiker is geen kunnen kiezen een bestaand openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="6b17c-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="6b17c-121">De standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="6b17c-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6b17c-122">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="6b17c-122">Sample output</span></span>
<span data-ttu-id="6b17c-123">Als de gebruiker heeft geen openbare IP-adres geselecteerd, worden de volgende uitvoer wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="6b17c-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="6b17c-124">Als de gebruiker een nieuwe of bestaande IP-adres selecteert, wordt de volgende uitvoer verwacht:</span><span class="sxs-lookup"><span data-stu-id="6b17c-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="6b17c-125">Wanneer `options.hideNone` is opgegeven, `newOrExistingOrNone` retourneert altijd **geen**.</span><span class="sxs-lookup"><span data-stu-id="6b17c-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="6b17c-126">Wanneer `options.hideDomainNameLabel` is opgegeven, `domainNameLabel` is niet gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="6b17c-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b17c-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b17c-127">Next steps</span></span>
* <span data-ttu-id="6b17c-128">Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b17c-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6b17c-129">Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b17c-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6b17c-130">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6b17c-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
