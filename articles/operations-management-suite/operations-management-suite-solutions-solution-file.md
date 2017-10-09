---
title: oplossingen voor aaaCreating in Operations Management Suite (OMS) | Microsoft Docs
description: Beheeroplossingen Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door verpakte beheerscenario dat klanten tootheir OMS-werkruimte kunnen toevoegen.  Dit artikel bevat informatie over hoe u management oplossingen toobe kunt maken in uw eigen omgeving gebruikt of beschikbaar tooyour klanten worden gemaakt.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Maken van een bestand van de oplossing voor beheer in Operations Management Suite (OMS) (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.  

Oplossingen voor het beheer in de Operations Management Suite (OMS) worden geïmplementeerd als [Resource Manager-sjablonen](../azure-resource-manager/resource-manager-template-walkthrough.md).  de belangrijkste taak Hallo weten hoe tooauthor beheeroplossingen hoe te leren[ontwerpen van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md).  Dit artikel vindt u unieke gegevens van sjablonen die worden gebruikt voor oplossingen en hoe tooconfigure standaardoplossing resources.


## <a name="tools"></a>Hulpprogramma's

U kunt tekst editor toowork oplossingsbestanden, maar we raden gebruik Hallo-functies die in Visual Studio of Visual Studio Code, zoals beschreven in de volgende artikelen Hallo.

- [Maken en implementeren van Azure-resourcegroepen met Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Werken met Azure Resource Manager-sjablonen in Visual Studio Code](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>structuur
Hallo basisstructuur van een management-oplossing-bestand is Hallo dezelfde zijn als een [Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md#template-format) die is als volgt.  Elk van de volgende secties voor Hallo Hallo hoogste niveau elementen beschrijft en en de inhoud in een oplossing.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Parameters
[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) zijn waarden die u nodig van de gebruiker Hallo hebt wanneer ze Hallo-beheeroplossing installeren.  Er zijn standaard parameters die alle oplossingen hebben en u kunt zo nodig extra parameters toevoegen voor uw specifieke oplossing.  Hoe gebruikers parameterwaarden wordt opgeven bij de installatie van uw oplossing afhankelijk van bepaalde Hallo-parameter en hoe de oplossing hello wordt geïnstalleerd.

Wanneer een gebruiker uw beheeroplossing voor via Hallo installeert [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) of [Azure-snelstartsjablonen](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ze na vragen aan gebruiker tooselect zijn een [OMS werkruimte en de Automation-account ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Dit zijn gebruikte toopopulate Hallo waarden van elk van de standaardparameters Hallo.  Hallo-gebruiker niet gevraagd toodirectly waarden opgeven voor de standaardparameters hello, maar ze na vragen aan gebruiker tooprovide waarden voor eventuele extra parameters zijn.

Wanneer Hallo gebruiker installeert voor uw oplossing [een andere methode](operations-management-suite-solutions.md#finding-and-installing-management-solutions), moeten deze een waarde opgeven voor alle standaardparameters en alle extra parameters.

Een voorbeeld-parameter worden hieronder weergegeven.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Hallo volgende tabel beschrijft Hallo kenmerken van een parameter.

| Kenmerk | Beschrijving |
|:--- |:--- |
| type |Het gegevenstype voor Hallo-parameter. Hallo invoer besturingselement weergegeven voor gebruiker hello, is afhankelijk van Hallo-gegevenstype.<br><br>Boole - vervolgkeuzelijst<br>String - tekstvak<br>int - tekstvak<br>SecureString - wachtwoordveld<br> |
| category |Optionele categorie voor Hallo-parameter.  De parameters in dezelfde categorie zijn gegroepeerd Hallo. |
| Besturingselement |Aanvullende functionaliteit voor string-parameters.<br><br>datum/tijd - datum/tijd-besturingselement wordt weergegeven.<br>GUID - Guid-waarde wordt automatisch gegenereerd en Hallo-parameter niet wordt weergegeven. |
| description |Optionele beschrijving voor het Hallo-parameter.  In een volgende toohello-parameter van informatie ballon weergegeven. |

### <a name="standard-parameters"></a>Standaard-parameters
Hallo bevat volgende tabel de standaardparameters Hallo voor alle beheeroplossingen voor.  Deze waarden worden ingevuld voor Hallo-gebruiker in plaats van het betreffende bevestigingsvenster wanneer uw oplossing wordt geïnstalleerd vanuit hello Azure Marketplace of Quick Start-sjablonen.  Hallo-gebruiker moet waarden opgeven voor deze als Hallo-oplossing is geïnstalleerd met een andere methode.

> [!NOTE]
> Hallo-gebruikersinterface in hello Azure Marketplace en Quick Start-sjablonen verwacht in de tabel Hallo Hallo parameternamen.  Als u verschillende parameternamen vervolgens Hallo gebruiker wordt gevraagd om deze en ze niet automatisch ingevuld.
>
>

| Parameter | Type | Beschrijving |
|:--- |:--- |:--- |
| Accountnaam |Tekenreeks |Azure Automation-accountnaam. |
| pricingTier |Tekenreeks |De prijscategorie van de werkruimte voor logboekanalyse zowel Azure Automation-account. |
| regionId |Tekenreeks |De regio van hello Azure Automation-account. |
| SolutionName |Tekenreeks |Naam van het Hallo-oplossing.  Als u uw oplossing via snelstartsjablonen implementeert, moet vervolgens u definiëren solutionName als een parameter zodat u kunt een tekenreeks in plaats daarvan vereisen Hallo gebruiker toospecify een definiëren. |
| workspaceName |Tekenreeks |Meld u aan de naam van de werkruimte Analytics. |
| workspaceRegionId |Tekenreeks |De regio van de werkruimte voor logboekanalyse Hallo. |


Hieronder volgt Hallo structuur Hallo standaard parameters die u kunt kopiëren en plakken in uw oplossingsbestand.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


Raadpleeg van tooparameter waarden in andere elementen van de oplossing Hallo met Hallo syntaxis **parameters (parameter name)**.  Bijvoorbeeld: tooaccess Hallo Werkruimtenaam, gebruikt u **parameters('workspaceName')**

## <a name="variables"></a>Variabelen
[Variabelen](../azure-resource-manager/resource-group-authoring-templates.md#variables) zijn waarden die u in de rest van de beheeroplossing Hallo Hallo gebruikt.  Deze waarden zijn niet blootgestelde toohello gebruiker Hallo oplossing installeren.  Ze zijn bedoeld tooprovide Hallo auteur met één locatie waar ze de waarden die u mogelijk meerdere keren worden gebruikt in de gehele Hallo oplossing kunnen beheren. U moet een specifieke tooyour waarden oplossing in variabelen plaatsen als tegengestelde toohard ze coderen in Hallo **resources** element.  Dit maakt het Hallo-code beter leesbaar en kunt u deze waarden in latere versies tooeasily te wijzigen.

Hieronder volgt een voorbeeld van een **variabelen** element met de gangbare parameters die worden gebruikt in oplossingen.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Raadpleeg van toovariable waarden via Hallo-oplossing met Hallo syntaxis **variabelen ('variabele name')**.  Bijvoorbeeld: tooaccess Hallo SolutionName variabele, gebruikt u **variables('SolutionName')**.

U kunt ook complexe variabelen definiëren die meerdere sets met waarden.  Dit zijn vooral handig beheersystemen waar het definiëren van meerdere eigenschappen voor verschillende soorten resources.  U kan bijvoorbeeld opnieuw indelen Hallo oplossing variabelen hierboven toohello hieronder weergegeven.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

In dit geval u toovariable waarden via Hallo-oplossing met Hallo syntaxis verwijzen **variables('variable name').property**.  Bijvoorbeeld: tooaccess Hallo oplossingsnaam variabele, gebruikt u **variables('Solution'). Naam**.

## <a name="resources"></a>Resources
[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) Hallo andere middelen opgeven die uw beheeroplossing voor installeren en configureren.  Dit is de grootste Hallo en meest complexe gedeelte van het Hallo-sjabloon.  U krijgt Hallo structuur en volledige beschrijving van de resource-elementen in [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Verschillende bronnen die u doorgaans definieert zijn aangegeven in de andere artikelen in deze documentatie. 


### <a name="dependencies"></a>Afhankelijkheden
Hallo **dependsOn** elementen bevat een [afhankelijkheid](../azure-resource-manager/resource-group-define-dependencies.md) op een andere resource.  Wanneer het Hallo-oplossing is geïnstalleerd, wordt een bron is niet gemaakt totdat alle afhankelijkheden ervan zijn gemaakt.  Bijvoorbeeld: uw oplossing mogelijk [een runbook start](operations-management-suite-solutions-resources-automation.md#runbooks) wanneer deze geïnstalleerd met behulp van een [taak resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).  Hallo taak resource, zijn afhankelijk van Hallo runbook resource toomake ervoor dat Hallo-runbook is gemaakt voordat het Hallo-taak is gemaakt.

### <a name="oms-workspace-and-automation-account"></a>OMS-werkruimte en de Automation-account
Oplossingen vereisen een [OMS-werkruimte](../log-analytics/log-analytics-manage-access.md) toocontain weergaven en een [Automation-account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks en verwante resources.  Deze moeten worden voordat Hallo resources in Hallo oplossing worden gemaakt en moeten niet worden gedefinieerd in Hallo oplossing zelf beschikbaar.  Hallo-gebruiker wordt [een werkruimte en de account opgeven](operations-management-suite-solutions.md#oms-workspace-and-automation-account) wanneer ze uw oplossing implementeren, maar als de auteur van het Hallo kunt u overwegen Hallo punten te volgen.

## <a name="solution-resource"></a>Oplossing resource
Elke oplossing vereist een resource-vermelding in Hallo **resources** element waarmee wordt gedefinieerd Hallo oplossing zelf.  Dit heeft een type **Microsoft.OperationsManagement/solutions** en hebben Hallo structuur te volgen. Dit omvat [standaardparameters](#parameters) en [variabelen](#variables) die gewoonlijk gebruikte toodefine eigenschappen van Hallo oplossing zijn.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Afhankelijkheden
Hallo oplossing resource moet hebben een [afhankelijkheid](../azure-resource-manager/resource-group-define-dependencies.md) op alle andere bronnen in Hallo oplossing omdat ze tooexist moeten voordat Hallo oplossing kan worden gemaakt.  U dit doen door het toevoegen van een vermelding voor elke resource in Hallo **dependsOn** element.

### <a name="properties"></a>Eigenschappen
Hallo oplossing resource heeft Hallo eigenschappen in de volgende tabel Hallo.  Dit omvat Hallo resources waarnaar wordt verwezen en deel uitmaken van het Hallo-oplossing waarmee wordt gedefinieerd hoe Hallo resource wordt beheerd nadat het Hallo-oplossing is geïnstalleerd.  Elke resource in Hallo oplossing moet worden opgenomen in beide Hallo **referencedResources** of Hallo **containedResources** eigenschap.

| Eigenschap | Beschrijving |
|:--- |:--- |
| workspaceResourceId |ID van Hallo werkruimte voor logboekanalyse Hallo vorm  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Werkruimtenaam\>*. |
| referencedResources |Lijst met resources in het Hallo-oplossing die mogen niet worden verwijderd wanneer het Hallo-oplossing is verwijderd. |
| containedResources |Lijst met resources in het Hallo-oplossing die moet worden verwijderd als het Hallo-oplossing is verwijderd. |

Hallo in bovenstaand voorbeeld is voor een oplossing met een runbook, een schema en de weergave.  Hallo-planning en runbook zijn *waarnaar wordt verwezen* in Hallo **eigenschappen** element zodat ze worden niet verwijderd wanneer het Hallo-oplossing is verwijderd.  Hallo-weergave is *opgenomen* zodat het wordt verwijderd wanneer het Hallo-oplossing is verwijderd.

### <a name="plan"></a>Plannen
Hallo **plan** entiteit van het Hallo-oplossing resource heeft Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| naam |Naam van het Hallo-oplossing. |
| Versie |Versie van oplossing Hallo zoals wordt bepaald door de auteur van het Hallo. |
| Product |Unieke tekenreeks tooidentify Hallo oplossing. |
| Uitgever |Uitgever van Hallo-oplossing. |



## <a name="sample"></a>Voorbeeld
U kunt voorbeelden van oplossingsbestanden met een resource oplossing Hallo volgende locaties bekijken.

- [Automation-resources](operations-management-suite-solutions-resources-automation.md#sample)
- [Resources zoeken en waarschuwingen](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Volgende stappen
* [Opgeslagen zoekopdrachten en waarschuwingen toevoegen](operations-management-suite-solutions-resources-searches-alerts.md) tooyour-beheeroplossing.
* [Weergaven toevoegen](operations-management-suite-solutions-resources-views.md) tooyour-beheeroplossing.
* [Runbooks en andere Automation-resources toevoegen](operations-management-suite-solutions-resources-automation.md) tooyour-beheeroplossing.
* Meer details op Hallo van [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).
* Search [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates) voor voorbeelden van andere Resource Manager-sjablonen.
