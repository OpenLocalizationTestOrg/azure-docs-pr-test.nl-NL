---
title: UI-definitie voor Azure Managed toepassingen maken aaaUnderstand | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate UI definities voor beheerde Azure-toepassingen
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Aan de slag met CreateUiDefinition
Dit document bevat Hallo belangrijkste concepten van een CreateUiDefinition die wordt gebruikt door hello Azure portal toogenerate Hallo-gebruikersinterface voor het maken van een beheerde toepassing.

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
* parameters

Voor beheerde toepassingen handler altijd moet `Microsoft.Compute.MultiVm`, Hallo ondersteund meest recente versie en `0.1.2-preview`.

Hallo-schema van de eigenschap parameters hello, is afhankelijk van Hallo combinatie van de opgegeven handler Hallo en versie. Voor beheerde toepassingen Hallo ondersteund eigenschappen zijn `basics`, `steps`, en `outputs`. Hallo basisbeginselen en stappen eigenschappen bevatten Hallo _elementen_ - zoals tekstvakken en vervolgkeuzelijsten - toobe in weergegeven hello Azure-portal. Hallo-uitvoer eigenschap gebruikte toomap Hallo uitvoerwaarden van is Hallo opgegeven elementen toohello parameters van hello Azure Resource Manager-implementatiesjabloon.

Inclusief `$schema` wordt aanbevolen, maar is optioneel. Indien opgegeven, de waarde voor Hallo `version` moet overeenkomen met de versie Hallo binnen Hallo `$schema` URI.

## <a name="basics"></a>Basisbeginselen
Hallo basisbeginselen stap is altijd de eerste stap Hallo van Hallo wizard gegenereerd wanneer hello Azure-portal een CreateUiDefinition parseert. Bovendien toodisplaying Hallo elementen is opgegeven in `basics`, Hallo portal injects-elementen voor gebruikers toochoose Hallo abonnement, resourcegroep en locatie voor Hallo-implementatie. In het algemeen moeten elementen waarmee een query voor distributie-parameters, zoals Hallo-naam van een cluster of de administrator-referenties uitvoeren, gaat u in deze stap.

Als het gedrag van een element afhankelijk is van de gebruiker van het Hallo-abonnement, resourcegroep of locatie, worden niet dat element gebruikt in basisbeginselen. Bijvoorbeeld: **Microsoft.Compute.SizeSelector** afhankelijk van de gebruiker Hallo abonnement en de locatie toodetermine Hallo lijst met beschikbare grootten. Daarom **Microsoft.Compute.SizeSelector** kan alleen worden gebruikt in stappen. In het algemeen alleen elementen in Hallo **Microsoft.Common** naamruimte in basisbeginselen kan worden gebruikt. Hoewel bepaalde elementen in andere naamruimten (zoals **Microsoft.Compute.Credentials**) dat niet afhankelijk zijn van de context van de gebruiker hello, nog steeds zijn toegestaan.

## <a name="steps"></a>Stappen
Hallo stappen eigenschap kan nul of meer extra stappen toodisplay na de basisbeginselen, die elk een of meer elementen bevat bevatten. Overweeg stappen per rol of laag van Hallo-toepassing wordt geïmplementeerd. Bijvoorbeeld, een stap voor de invoer voor de hoofdknooppunten hello, en een voor Hallo worker-knooppunten in een cluster toevoegen.

## <a name="outputs"></a>uitvoer
Hello Azure portal maakt gebruik van Hallo `outputs` toomap eigenschapselementen van `basics` en `steps` toohello parameters van hello Azure Resource Manager-implementatiesjabloon. Hallo-sleutels van deze woordenlijst zijn Hallo namen van de sjabloonparameters Hallo en Hallo-waarden zijn eigenschappen van Hallo uitvoer objecten van de elementen Hallo waarnaar wordt verwezen.

## <a name="functions"></a>Functies
Vergelijkbare te[sjabloonfuncties](resource-group-template-functions.md) in Azure Resource Manager (zowel in de syntaxis en functionaliteit), CreateUiDefinition voorziet in functies voor het werken met in- en uitgangen elementen, evenals functies zoals voorwaardelijke.

## <a name="next-steps"></a>Volgende stappen
CreateUiDefinition zelf is een eenvoudig schema. Hallo echte diepte van het afkomstig is van alle elementen Hallo ondersteund en functies, welke Hallo documenten te volgen in wondrous detail beschrijven:

- [Elementen](managed-application-createuidefinition-elements.md)
- [Functies](managed-application-createuidefinition-functions.md)

Een huidige JSON-schema voor CreateUiDefinition is hier beschikbaar: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Latere versies zijn beschikbaar op Hallo dezelfde locatie. Vervang Hallo `0.1.2-preview` gedeelte van het Hallo-URL en Hallo `version` waarde met de versie-id Hallo u van plan bent toouse. Hallo momenteel ondersteund versie-id's zijn `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, en `0.1.2-preview`.
