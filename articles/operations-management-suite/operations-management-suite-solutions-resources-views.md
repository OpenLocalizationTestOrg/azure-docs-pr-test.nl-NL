---
title: aaaViews beheersystemen Operations Management Suite (OMS) | Microsoft Docs
description: 'Oplossingen voor het beheer in de Operations Management Suite (OMS) wordt gewoonlijk een of meer weergaven toovisualize gegevens bevatten.  In dit artikel wordt beschreven hoe tooexport een weergave gemaakt door Hallo Designer bekijken en deze opnemen in een oplossing. '
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Weergaven in de Operations Management Suite (OMS) oplossingen (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.    
>
>

[Oplossingen voor het beheer in de Operations Management Suite (OMS)](operations-management-suite-solutions.md) doorgaans bevat een of meer weergaven toovisualize gegevens.  Dit artikel wordt beschreven hoe tooexport een weergave gemaakt door Hallo [ontwerper](../log-analytics/log-analytics-view-designer.md) en deze opnemen in een oplossing.  

> [!NOTE]
> Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al bekend met het te bent[maken van een beheeroplossing](operations-management-suite-solutions-creating.md) en Hallo-structuur van een oplossingsbestand.

## <a name="overview"></a>Overzicht
een weergave in een oplossing voor tooinclude, die u maakt een **resource** voor in Hallo [oplossingsbestand](operations-management-suite-solutions-creating.md).  Hallo JSON die de gedetailleerde configuratie van de weergave van de Hallo beschrijft is doorgaans complexe echter en niet iets dat de auteur van een standaardoplossing handmatig kunnen toocreate zou zijn.  Hallo wordt meestal toocreate Hallo weergeven met behulp van Hallo [ontwerper](../log-analytics/log-analytics-view-designer.md), exporteren en voeg vervolgens de gedetailleerde configuratie toohello oplossing.

Hallo basisstappen tooadd een weergave tooa oplossing zijn als volgt.  Elke stap wordt beschreven in de volgende secties voor Hallo nader.

1. Hallo weergave tooa-bestand exporteren.
2. Hallo weergave resource maken in Hallo-oplossing.
3. Hallo weergavedetails toevoegen.

## <a name="export-hello-view-tooa-file"></a>Hallo weergave tooa-bestand exporteren
Volg de instructies Hallo voor [Log Analytics-ontwerper](../log-analytics/log-analytics-view-designer.md) tooexport een weergave tooa-bestand.  Hallo geëxporteerde bestand zal worden in JSON-indeling met Hallo dezelfde [elementen als Hallo oplossingsbestand](operations-management-suite-solutions-solution-file.md).  

Hallo **resources** element van Hallo weergavebestand heeft een resource met een type **Microsoft.OperationalInsights/workspaces** dat vertegenwoordigt Hallo OMS-werkruimte.  Dit element heeft een subelement van het type **weergaven** die staat voor Hallo weergeven en de gedetailleerde configuratie bevat.  U Hallo details van dit element kopiëren en kopieert u deze naar uw oplossing.

## <a name="create-hello-view-resource-in-hello-solution"></a>Hallo weergave resource maken in Hallo-oplossing
Hallo na weergave resource toohello toevoegen **resources** element van het oplossingsbestand van uw.  Dit maakt gebruik van variabelen die hieronder worden beschreven die u ook moet toevoegen.  Houd er rekening mee dat Hallo **Dashboard** en **OverviewTile** eigenschappen zijn tijdelijke aanduidingen die u met de bijbehorende eigenschappen Hallo uit Hallo geëxporteerde weergavebestand wordt overschreven.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Toevoegen van de volgende variabelen toohello variabelen element van het oplossingsbestand Hallo Hallo en vervang Hallo waarden toothose voor uw oplossing.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Houd er rekening mee dat u Hallo gehele weergave resource vanuit het bestand met geëxporteerde weergave kopiëren kan, maar moet u toomake Hallo volgende wijzigingen voor het toowork in uw oplossing.  

* Hallo **type** voor Hallo weergave resource moet toobe gewijzigd van **weergaven** te**Microsoft.OperationalInsights/workspaces**.
* Hallo **naam** voor Hallo weergave resource-eigenschap moet toobe gewijzigd tooinclude Hallo Werkruimtenaam.
* Hallo-afhankelijkheid van Hallo werkruimte moet toobe sinds Hallo werkruimte resource is niet gedefinieerd in Hallo-oplossing verwijderd.
* **DisplayName** eigenschap behoeften toobe toohello weergave toegevoegd.  Hallo **Id**, **naam**, en **DisplayName** moeten alle overeenkomen.
* Namen van parameters moeten worden gewijzigd toomatch Hallo set parameters vereist.
* Variabelen moeten worden gedefinieerd in Hallo oplossing en gebruikt in de juiste Hallo-eigenschappen.

## <a name="add-hello-view-details"></a>Hallo weergavedetails toevoegen
Hallo weergave bron in Hallo geëxporteerd weergave bestand bevat twee elementen in Hallo **eigenschappen** element met de naam **Dashboard** en **OverviewTile** die Hallo bevatten gedetailleerde configuratie van Hallo weergeven.  Deze twee elementen en hun inhoud kopiëren naar Hallo **eigenschappen** element van de resource van Hallo weergeven in uw oplossingsbestand.

## <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld ziet u bijvoorbeeld een eenvoudige oplossing-bestand met een weergave.  Weglatingstekens (...) worden weergegeven voor Hallo **Dashboard** en **OverviewTile** inhoud omwille van de ruimte.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>Volgende stappen
* Meer informatie over alle details van het maken van [beheeroplossingen](operations-management-suite-solutions-creating.md).
* Omvatten [Automation-runbooks in uw beheeroplossing](operations-management-suite-solutions-resources-automation.md).
