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
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Microsoft.Network.PublicIpAddressCombo UI-element
Een groep besturingselementen voor het selecteren van een nieuw of bestaand openbaar IP-adres. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Als de gebruiker Hallo 'None' voor openbare IP-adres selecteert, is Hallo label tekstvak domeinnaam verborgen.
- Als het Hallo-gebruiker selecteert een bestaand openbaar IP-adres, is Hallo label tekstvak domeinnaam uitgeschakeld. De waarde ervan Hallo domeinnaamlabel van Hallo geselecteerd IP-adres.
- Hallo domain name achtervoegsel (bijvoorbeeld westus.cloudapp.azure.com) updates automatisch op basis van locatie Hallo geselecteerd.

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
- Als `constraints.required.domainNameLabel` te is ingesteld,**true**, Hallo-gebruiker moet een domeinnaamlabel opgeven bij het maken van een nieuw openbaar IP-adres. Bestaande openbare IP-adressen zonder een label zijn niet beschikbaar voor selectie.
- Als `options.hideNone` te is ingesteld,**true**, vervolgens Hallo optie tooselect **geen** voor Hallo openbare IP-adres wordt verborgen. de standaardwaarde Hallo is **false**.
- Als `options.hideDomainNameLabel` te is ingesteld,**true**, en vervolgens in het tekstvak voor domeinnaamlabel hello wordt verborgen. de standaardwaarde Hallo is **false**.
- Als `options.hideExisting` is ingesteld op true, en vervolgens het Hallo-gebruiker is geen kunnen toochoose een bestaand openbaar IP-adres. de standaardwaarde Hallo is **false**.

## <a name="sample-output"></a>Voorbeelduitvoer
Als het Hallo-gebruiker selecteert geen openbare IP-adres, wordt hello volgende uitvoer verwacht.
```json
{
  "newOrExistingOrNone": "none"
}
```

Als het Hallo-gebruiker selecteert een nieuwe of bestaande IP-adres, wordt hello volgende uitvoer verwacht.
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
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
