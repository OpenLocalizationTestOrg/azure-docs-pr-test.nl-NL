---
title: UI-definitie maken voor beheerde Azure-toepassingen inzicht | Microsoft Docs
description: Hierin wordt beschreven hoe u de definities van de gebruikersinterface voor beheerde Azure-toepassingen maken
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
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a>Aan de slag met CreateUiDefinition
Dit document worden de belangrijkste concepten van een CreateUiDefinition die wordt gebruikt door de Azure-portal voor het genereren van de gebruikersinterface voor het maken van een beheerde toepassing.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

Een CreateUiDefinition bevat altijd drie eigenschappen: 

* handler
* Versie
* Parameters

Voor beheerde toepassingen handler altijd moet `Microsoft.Compute.MultiVm`, en de laatste ondersteunde versie is `0.1.2-preview`.

Het schema van de eigenschap parameters is afhankelijk van de combinatie van de opgegeven handler en versie. Voor beheerde toepassingen, de ondersteunde eigenschappen zijn `basics`, `steps`, en `outputs`. De eigenschappen van de basisprincipes en stappen bevatten de _elementen_ - zoals tekstvakken en vervolgkeuzelijsten - moet worden weergegeven in de Azure portal. De uitvoer-eigenschap wordt gebruikt om de uitvoerwaarden van de opgegeven elementen toewijzen aan de parameters van de Azure Resource Manager-implementatiesjabloon.

Inclusief `$schema` wordt aanbevolen, maar is optioneel. Als u opgeeft, wordt de waarde voor `version` moet overeenkomen met de versie in de `$schema` URI.

## <a name="basics"></a>Basisbeginselen
De grondbeginselen van stap is altijd de eerste stap van de wizard gegenereerd wanneer de Azure portal een CreateUiDefinition wordt geparseerd. Naast het weergeven van de elementen die zijn opgegeven in `basics`, de portal injects-elementen voor gebruikers om te kiezen voor het abonnement, resourcegroep en locatie voor de implementatie. In het algemeen moeten elementen waarmee een query voor distributie-parameters, zoals de naam van een cluster of de administrator-referenties uitvoeren, gaat u in deze stap.

Als het gedrag van een element, is afhankelijk van abonnement, resourcegroep of locatie van de gebruiker, kan niet in basisbeginselen van dat element gebruikt. Bijvoorbeeld: **Microsoft.Compute.SizeSelector** is afhankelijk van het abonnement en de locatie voor het bepalen van de lijst met beschikbare grootten van de gebruiker. Daarom **Microsoft.Compute.SizeSelector** kan alleen worden gebruikt in stappen. In het algemeen alleen elementen in de **Microsoft.Common** naamruimte in basisbeginselen kan worden gebruikt. Hoewel bepaalde elementen in andere naamruimten (zoals **Microsoft.Compute.Credentials**) dat niet afhankelijk zijn van de context van de gebruiker, nog steeds zijn toegestaan.

## <a name="steps"></a>Stappen
De eigenschap stappen kan nul of meer extra stappen om weer te geven nadat de basisbeginselen, die elk een of meer elementen bevat bevatten. Overweeg stappen per rol of laag van de toepassing wordt geïmplementeerd. Voeg bijvoorbeeld een stap voor de invoer voor de hoofdknooppunten, en een voor worker-knooppunten in een cluster.

## <a name="outputs"></a>uitvoer
De Azure portal maakt gebruik van de `outputs` eigenschap toewijzen van elementen uit `basics` en `steps` aan de parameters van de Azure Resource Manager-implementatiesjabloon. De sleutels van deze woordenlijst zijn de namen van de sjabloonparameters en de waarden worden de eigenschappen van de uitvoer-objecten van de elementen waarnaar wordt verwezen.

## <a name="functions"></a>Functies
Net als bij [sjabloonfuncties](resource-group-template-functions.md) in Azure Resource Manager (zowel in de syntaxis en functionaliteit), CreateUiDefinition voorziet in functies voor het werken met in- en uitgangen elementen, evenals functies zoals voorwaardelijke.

## <a name="next-steps"></a>Volgende stappen
CreateUiDefinition zelf is een eenvoudig schema. De echte diepte van het afkomstig is van de ondersteunde elementen en functies, die de volgende documenten wondrous gedetailleerd beschreven:

- [Elementen](managed-application-createuidefinition-elements.md)
- [Functies](managed-application-createuidefinition-functions.md)

Een huidige JSON-schema voor CreateUiDefinition is hier beschikbaar: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Latere versies zijn beschikbaar op dezelfde locatie. Vervang de `0.1.2-preview` deel van de URL en de `version` waarde met de versie-id die u wilt gebruiken. De ondersteunde versie-id's `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, en `0.1.2-preview`.