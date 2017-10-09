---
title: Automation-resources aaaAzure in OMS-oplossingen | Microsoft Docs
description: Oplossingen in OMS omvatten meestal runbooks in Azure Automation tooautomate processen zoals het verzamelen en bewakingsgegevens verwerken.  Dit artikel wordt beschreven hoe tooinclude runbooks en hun verwante resources in een oplossing.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Toevoegen van Azure Automation-resources tooan OMS beheeroplossing (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.   


[Oplossingen voor het beheer in OMS](operations-management-suite-solutions.md) omvatten meestal runbooks in Azure Automation tooautomate processen zoals het verzamelen en bewakingsgegevens verwerken.  Bovendien toorunbooks, omvat Automation-accounts activa zoals variabelen en schema's die ondersteuning bieden voor Hallo runbooks gebruikt in Hallo-oplossing.  Dit artikel wordt beschreven hoe tooinclude runbooks en hun verwante resources in een oplossing.

> [!NOTE]
> Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al bekend bent met Hallo informatie te volgen.

- Hoe te[maken van een beheeroplossing](operations-management-suite-solutions-creating.md).
- Hallo structuur van een [oplossingsbestand](operations-management-suite-solutions-solution-file.md).
- Hoe te[Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Automation-account
Alle resources in Azure Automation zijn opgenomen in een [Automation-account](../automation/automation-security-overview.md#automation-account-overview).  Zoals beschreven in [OMS werkruimte en de Automation-account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hallo Automation-account niet is opgenomen in de oplossing voor het beheer van hello, maar moet bestaan voordat het Hallo-oplossing is geïnstalleerd.  Als het is niet beschikbaar, mislukken Hallo oplossing installatie.

Hallo-naam van elke resource Automation omvat Hallo-naam van de Automation-account.  Dit wordt gedaan Hallo-oplossing met Hallo **accountName** parameter zoals in Hallo voorbeeld van een runbook-resource te volgen.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbooks
Alle runbooks die wordt gebruikt door Hallo-oplossing in het oplossingsbestand hello, zodat ze worden gemaakt wanneer het Hallo-oplossing is geïnstalleerd, moet u opnemen.  U mag geen Hallo-hoofdtekst van het runbook in de sjabloon Hallo Hallo echter bevatten zodat u Hallo runbook tooa openbaar toegankelijke locatie waar deze kan worden geopend door elke gebruiker installeren van uw oplossing moet publiceren.

[Azure Automation-runbook](../automation/automation-runbook-types.md) resources zijn een type **Microsoft.Automation/automationAccounts/runbooks** en hebben Hallo structuur te volgen. Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


Hallo-eigenschappen voor runbooks worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| runbookType |Hiermee geeft u Hallo Hallo runbook typen. <br><br> Script - PowerShell-script <br>PowerShell - PowerShell-werkstroom <br> GraphPowerShell - grafische PowerShell-script runbook <br> GraphPowerShellWorkflow - grafische PowerShell workflow-runbook |
| logProgress |Hiermee geeft u op of [records voortgang](../automation/automation-runbook-output-and-messages.md) voor Hallo runbook moet worden gegenereerd. |
| logVerbose |Hiermee geeft u op of [uitgebreide records](../automation/automation-runbook-output-and-messages.md) voor Hallo runbook moet worden gegenereerd. |
| description |Optionele beschrijving voor het Hallo-runbook. |
| publishContentLink |Hiermee geeft u Hallo inhoud van het Hallo-runbook. <br><br>URI - inhoud-Uri toohello van Hallo runbook.  Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.  <br> versie - versie van de runbook Hallo voor uw eigen bijhouden. |


## <a name="automation-jobs"></a>Automation-taken
Wanneer u een runbook in Azure Automation start, wordt een automation-taak gemaakt.  U kunt een automation-taak resource tooyour oplossing tooautomatically start een runbook toevoegen als oplossing voor het beheer van Hallo is geïnstalleerd.  Deze methode is gewoonlijk gebruikte toostart runbooks die worden gebruikt voor de initiële configuratie van Hallo-oplossing.  maken van een runbook met regelmatige tussenpozen toostart een [planning](#schedules) en een [taakschema](#job-schedules)

Taak resources zijn een type **Microsoft.Automation/automationAccounts/jobs** en hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

Hallo-eigenschappen voor automatisering taken worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| runbook |Één naam-entiteit met de naam van de Hallo van Hallo runbook toostart. |
| parameters |De entiteit voor elke parameterwaarde vereist voor Hallo runbook. |

Hallo-taak bevat Hallo runbooknaam en elke parameter waarden toobe toohello runbook verzonden.  Hallo-taak moet [afhankelijk](operations-management-suite-solutions-solution-file.md#resources) hello runbook dat deze wordt gestart sinds Hallo runbook moet worden gemaakt voordat het Hallo-taak.  Als er meerdere runbooks die moet worden gestart, kunt u de volgorde definiëren wanneer er een taak die afhankelijk zijn van andere taken die eerst moeten worden uitgevoerd.

Hallo-naam van een resource van de taak moet een GUID die doorgaans wordt toegewezen door een parameter bevatten.  Meer informatie over parameters in GUID [om oplossingen te maken in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certificaten
[Azure Automation-certificaten](../automation/automation-certificates.md) een soort **Microsoft.Automation/automationAccounts/certificates** en hebben Hallo structuur te volgen. Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



Hallo-eigenschappen van bronnen van de certificaten worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| base64Value |De waarde van de Base 64 voor Hallo certificaat. |
| vingerafdruk |Vingerafdruk voor Hallo certificaat. |



## <a name="credentials"></a>Referenties
[Azure Automation-referenties](../automation/automation-credentials.md) een soort **Microsoft.Automation/automationAccounts/credentials** en hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

Hallo-eigenschappen voor de referentie-bronnen worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Gebruikersnaam |De gebruikersnaam voor Hallo referentie. |
| wachtwoord |Wachtwoord voor het Hallo-referentie. |


## <a name="schedules"></a>Planningen
[Azure Automation-planningen](../automation/automation-schedules.md) een soort **Microsoft.Automation/automationAccounts/schedules** en hebben Hallo Hallo structuur te volgen. Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

Hallo-eigenschappen voor schema-bronnen worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| description |Optionele beschrijving voor Hallo planning. |
| startTime |Hiermee geeft u de begintijd Hallo van een planning als een datum/tijd-object. Een tekenreeks kan worden opgegeven als geconverteerde tooa geldige DateTime. |
| IsEnabled |Hiermee geeft u op of het Hallo-schema is ingeschakeld. |
| interval |Hallo type interval voor Hallo planning.<br><br>dag<br>uur |
| frequency |Frequentie waarmee Hallo planning moet worden geactiveerd in aantal dagen of uren. |

Schema's moeten een begintijd met een waarde groter dan Hallo huidige tijd hebben.  U kunt deze waarde kan niet opgeven met een variabele omdat u er niet toe van weten wanneer het gaat toobe geïnstalleerd is.

Gebruik een van de Hallo twee strategieën bij gebruik van resources plannen in een oplossing te volgen.

- Gebruik een parameter voor de begintijd Hallo van Hallo planning.  Dit wordt gevraagd om Hallo gebruiker tooprovide een waarde wanneer ze Hallo-oplossing installeren.  Als u meerdere schema's hebt, kunt u een enkele parameterwaarde kunt gebruiken voor meer dan één.
- Maak Hallo schema's met behulp van een runbook dat wordt gestart wanneer het Hallo-oplossing is geïnstalleerd.  Hiermee verwijdert u de vereiste Hallo van Hallo gebruiker toospecify, maar u mag niet Hallo plannen in uw oplossing zodat deze worden verwijderd wanneer het Hallo-oplossing is verwijderd.


### <a name="job-schedules"></a>Jobplanningen
Taak schema resources koppelen een runbook met een schema.  Ze hebben een soort **Microsoft.Automation/automationAccounts/jobSchedules** en hebben Hallo Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


Hallo-eigenschappen voor taakschema's worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| de naam van de planning |Één **naam** entiteit met de naam van het schema Hallo Hallo. |
| Runbooknaam  |Één **naam** entiteit met de naam van de runbook Hallo Hallo.  |



## <a name="variables"></a>Variabelen
[Azure Automation-variabelen](../automation/automation-variables.md) een soort **Microsoft.Automation/automationAccounts/variables** en hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

Hallo-eigenschappen voor de variabele resources worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| description | Optionele beschrijving voor Hallo-variabele. |
| isEncrypted | Hiermee geeft u op of Hallo variabele moet worden versleuteld. |
| type | Deze eigenschap heeft momenteel geen effect.  Hallo-gegevenstype van Hallo variabele wordt bepaald door de beginwaarde Hallo. |
| waarde | De waarde voor Hallo-variabele. |

> [!NOTE]
> Hallo **type** eigenschap heeft momenteel geen effect op Hallo variabele wordt gemaakt.  Hallo-gegevenstype voor Hallo variabele wordt bepaald door het Hallo-waarde.  

Als u de beginwaarde voor de variabele Hallo Hallo instelt, moet deze worden geconfigureerd als het juiste gegevenstype Hallo.  Hallo volgende tabel biedt Hallo verschillende gegevenstypen toegestane en de syntaxis.  Er rekening mee dat de waarden in JSON verwachte tooalways tussen aanhalingstekens met de speciale tekens in Hallo aanhalingstekens staan.  Bijvoorbeeld, zou een string-waarde worden opgegeven door aanhalingstekens rond het Hallo-tekenreeks (met behulp van Hallo escape-teken (\\)) tijdens een numerieke waarde zou worden opgegeven met een set van aanhalingstekens.

| Gegevenstype | Beschrijving | Voorbeeld | Wordt omgezet te|
|:--|:--|:--|:--|
| Tekenreeks   | Waarde moet tussen dubbele aanhalingstekens.  | '\"Hallo wereld\"' | "Hallo wereld" |
| numerieke  | Numerieke waarde met enkele aanhalingstekens.| "64" | 64 |
| Booleaanse waarde  | **de waarde True** of **false** tussen aanhalingstekens.  Houd er rekening mee dat deze waarde een kleine letter moet. | 'true' | De waarde True |
| Datum/tijd | Geserialiseerde date-waarde.<br>U kunt op deze waarde Hallo ConvertTo-Json cmdlet in PowerShell toogenerate gebruiken voor een bepaalde datum.<br>Voorbeeld: get-date ' 24/5/2017 13:14:57 "\| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Modules
Uw beheeroplossing voor hoeft niet toodefine [globale modules](../automation/automation-integration-modules.md) gebruikt door uw runbooks omdat ze altijd beschikbaar zijn in uw Automation-account.  U hoeft tooinclude een resource voor elke andere module die wordt gebruikt door uw runbooks.

[Integratiemodules](../automation/automation-integration-modules.md) een soort **Microsoft.Automation/automationAccounts/modules** en hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


Hallo-eigenschappen van bronnen van de module worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| contentLink |Hiermee geeft u Hallo inhoud van het Hallo-module. <br><br>URI - Uri toohello inhoud van het Hallo-module.  Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.  <br> versie - versie van de module Hallo voor uw eigen bijhouden. |

Hallo runbook moet afhankelijk van Hallo module resource tooensure voordat Hallo runbook gemaakt.

### <a name="updating-modules"></a>Bijwerken van modules
Als u een oplossing met een runbook dat gebruikmaakt van een schema bijwerken en Hallo nieuwe versie van uw oplossing een nieuwe module die wordt gebruikt door dat runbook heeft, kan Hallo runbook Hallo oude versie van de module hello gebruiken.  U moet nemen Hallo runbooks in uw oplossing te volgen en maken van een taak toorun toe voordat alle andere runbooks.  Dit zorgt ervoor dat alle modules die worden bijgewerkt als vereist voordat Hallo runbooks zijn geladen.

* [Update ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) zorgt ervoor dat alle Hallo-modules die worden gebruikt door runbooks in uw oplossing de meest recente versie Hallo zijn.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) alle Hallo planning resources tooensure dat Hallo runbooks toothem met gebruik Hallo nieuwste modules gekoppeld opnieuw registreren.




## <a name="sample"></a>Voorbeeld
Hier volgt een voorbeeld van een oplossing die bevatten die Hallo resources te volgen:

- Runbook.  Dit is een voorbeeldrunbook dat is opgeslagen in een openbare GitHub-opslagplaats.
- Automation-taak die Hallo runbook wordt gestart wanneer Hallo-oplossing is geïnstalleerd.
- Planning en taak plannen toostart hello runbook met regelmatige tussenpozen.
- Certificaat.
- De referentie.
- Variabele.
- Module.  Dit is Hallo [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) voor het schrijven van gegevens tooLog Analytics. 

voorbeeld gebruikt Hallo [standaardoplossing parameters](operations-management-suite-solutions-solution-file.md#parameters) variabelen die meestal in een oplossing als gebruikt wordt toohardcoding waarden in de resourcedefinities Hallo geboden.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Volgende stappen
* [Toevoegen van een oplossing voor weergave tooyour](operations-management-suite-solutions-resources-views.md) toovisualize gegevens verzameld.
