---
title: Beheerde toepassing PublicIpAddressCombo UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Network.PublicIpAddressCombo UI-element voor beheerde Azure-toepassingen
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="a2f26-103">Microsoft.Network.PublicIpAddressCombo UI-element</span><span class="sxs-lookup"><span data-stu-id="a2f26-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="a2f26-104">Een groep besturingselementen voor het selecteren van een nieuw of bestaand openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a2f26-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="a2f26-105">Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a2f26-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a2f26-106">Voorbeeld van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="a2f26-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="a2f26-108">Als de gebruiker Hallo 'None' voor openbare IP-adres selecteert, is Hallo label tekstvak domeinnaam verborgen.</span><span class="sxs-lookup"><span data-stu-id="a2f26-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="a2f26-109">Als het Hallo-gebruiker selecteert een bestaand openbaar IP-adres, is Hallo label tekstvak domeinnaam uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a2f26-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="a2f26-110">De waarde ervan Hallo domeinnaamlabel van Hallo geselecteerd IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a2f26-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="a2f26-111">Hallo domain name achtervoegsel (bijvoorbeeld westus.cloudapp.azure.com) updates automatisch op basis van locatie Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a2f26-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="a2f26-112">Schema</span><span class="sxs-lookup"><span data-stu-id="a2f26-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="a2f26-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a2f26-113">Remarks</span></span>
- <span data-ttu-id="a2f26-114">Als `constraints.required.domainNameLabel` te is ingesteld,**true**, Hallo-gebruiker moet een domeinnaamlabel opgeven bij het maken van een nieuw openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a2f26-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="a2f26-115">Bestaande openbare IP-adressen zonder een label zijn niet beschikbaar voor selectie.</span><span class="sxs-lookup"><span data-stu-id="a2f26-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="a2f26-116">Als `options.hideNone` te is ingesteld,**true**, vervolgens Hallo optie tooselect **geen** voor Hallo openbare IP-adres wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="a2f26-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="a2f26-117">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="a2f26-117">hello default value is **false**.</span></span>
- <span data-ttu-id="a2f26-118">Als `options.hideDomainNameLabel` te is ingesteld,**true**, en vervolgens in het tekstvak voor domeinnaamlabel hello wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="a2f26-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="a2f26-119">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="a2f26-119">hello default value is **false**.</span></span>
- <span data-ttu-id="a2f26-120">Als `options.hideExisting` is ingesteld op true, en vervolgens het Hallo-gebruiker is geen kunnen toochoose een bestaand openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a2f26-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="a2f26-121">de standaardwaarde Hallo is **false**.</span><span class="sxs-lookup"><span data-stu-id="a2f26-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a2f26-122">Voorbeelduitvoer</span><span class="sxs-lookup"><span data-stu-id="a2f26-122">Sample output</span></span>
<span data-ttu-id="a2f26-123">Als het Hallo-gebruiker selecteert geen openbare IP-adres, wordt hello volgende uitvoer verwacht.</span><span class="sxs-lookup"><span data-stu-id="a2f26-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="a2f26-124">Als het Hallo-gebruiker selecteert een nieuwe of bestaande IP-adres, wordt hello volgende uitvoer verwacht.</span><span class="sxs-lookup"><span data-stu-id="a2f26-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="a2f26-125">Wanneer `options.hideNone` is opgegeven, `newOrExistingOrNone` retourneert altijd **geen**.</span><span class="sxs-lookup"><span data-stu-id="a2f26-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="a2f26-126">Wanneer `options.hideDomainNameLabel` is opgegeven, `domainNameLabel` is niet gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="a2f26-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2f26-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2f26-127">Next steps</span></span>
* <span data-ttu-id="a2f26-128">Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f26-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a2f26-129">Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f26-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a2f26-130">Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a2f26-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
