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
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Microsoft.Network.PublicIpAddressCombo UI-element
Een groep besturingselementen voor het selecteren van een nieuw of bestaand openbaar IP-adres. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Als de gebruiker 'None' voor openbare IP-adres selecteert, wordt het tekstvak domain name label verborgen.
- Als de gebruiker selecteert een bestaand openbaar IP-adres, is het tekstvak label domein uitgeschakeld. De waarde is het domeinnaamlabel van het geselecteerde IP-adres.
- De domain name achtervoegsel (bijvoorbeeld westus.cloudapp.azure.com)-updates automatisch op basis van de geselecteerde locatie.

## <a name="schema"></a>Schema
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

## <a name="remarks"></a>Opmerkingen
- Als `constraints.required.domainNameLabel` is ingesteld op **true**, de gebruiker moet een domeinnaamlabel opgeven bij het maken van een nieuw openbaar IP-adres. Bestaande openbare IP-adressen zonder een label zijn niet beschikbaar voor selectie.
- Als `options.hideNone` is ingesteld op **true**, klikt u vervolgens de optie te selecteren **geen** voor het openbare IP-adres wordt verborgen. De standaardwaarde is **false**.
- Als `options.hideDomainNameLabel` is ingesteld op **true**, en vervolgens in het tekstvak voor domeinnaamlabel wordt verborgen. De standaardwaarde is **false**.
- Als `options.hideExisting` is ingesteld op true, wordt de gebruiker is geen kunnen kiezen een bestaand openbaar IP-adres. De standaardwaarde is **false**.

## <a name="sample-output"></a>Voorbeelduitvoer
Als de gebruiker heeft geen openbare IP-adres geselecteerd, worden de volgende uitvoer wordt verwacht.
```json
{
  "newOrExistingOrNone": "none"
}
```

Als de gebruiker een nieuwe of bestaande IP-adres selecteert, wordt de volgende uitvoer verwacht:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Wanneer `options.hideNone` is opgegeven, `newOrExistingOrNone` retourneert altijd **geen**.
- Wanneer `options.hideDomainNameLabel` is opgegeven, `domainNameLabel` is niet gedeclareerd.

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding tot beheerde toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding tot het maken van de definities van de gebruikersinterface, [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
