---
title: implementatiesjablonen aaaCreate voor Azure Logic Apps | Microsoft Docs
description: Implementatie en release management voor Azure Resource Manager-sjablonen voor logic apps maken
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Sjablonen maken voor logische apps implementatie en release management

Nadat een logische app is gemaakt, kunt u toocreate als een Azure Resource Manager-sjabloon.
Op deze manier kunt u eenvoudig implementeren Hallo logic app tooany omgeving of resourcegroep wanneer u deze mogelijk nodig.
Zie voor meer informatie over de Resource Manager-sjablonen, [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md) en [resources implementeren met behulp van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Sjabloon Logic app-implementatie

Een logische app bevat drie basiscomponenten:

* **Resource-Logic app**: bevat informatie over zaken als het plan, locatie en de workflowdefinitie Hallo prijzen.
* **De workflowdefinitie**: Beschrijving van uw logische app werkstroomstappen en hoe Hallo Logic Apps-engine Hallo werkstroom moet worden uitgevoerd.
U kunt deze definitie weergeven in uw logische app **codeweergave** venster.
In resource-Hallo logic app, kunt u deze definitie vinden in Hallo `definition` eigenschap.
* **Verbindingen**: tooseparate resources die veilig opslaan metagegevens over de connector-verbindingen, zoals een verbindingsreeks en een toegangstoken verwijst.
In resource-Hallo logic app, uw logische app verwijst naar deze bronnen in Hallo `parameters` sectie.

U kunt deze informatie van bestaande logic apps weergeven met behulp van een hulpprogramma zoals [Azure Resource Explorer](http://resources.azure.com).

toomake een sjabloon voor een logische app toouse met resourcegroepimplementaties, moet u Hallo resources definiëren en naar behoefte te voorzien.
Bijvoorbeeld, als u tooa ontwikkeling, testen en productie-omgeving implementeert, wilt waarschijnlijk u toouse andere verbinding tekenreeksen tooa SQL-database in elke omgeving.
Of u wellicht toodeploy in verschillende abonnementen of resourcegroepen.  

## <a name="create-a-logic-app-deployment-template"></a>Maken van een sjabloon logic app-implementatie

Hallo gemakkelijkste manier toohave een geldige logic app-implementatiesjabloon is toouse de [Visual Studio Tools voor Logic Apps](logic-apps-deploy-from-vs.md).
Hallo Visual Studio tools genereren een geldige implementatie-sjabloon die via een abonnement of een locatie kan worden gebruikt.

Enkele andere hulpprogramma's kunnen u helpen bij het maken van een sjabloon logic app-implementatie.
Kunt u handmatig schrijven, dat wil zeggen, met behulp van Hallo resources al die hier worden besproken toocreate parameters indien nodig.
Een andere optie is toouse een [logic app sjabloon Maker](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell-module. Deze open source-module wordt eerst geëvalueerd Hallo logische app en dat het wordt gebruikt en vervolgens sjabloonresources met Hallo benodigde parameters op voor de implementatie van genereert verbindingen.
Bijvoorbeeld, als er een logische app die via een bericht ontvangt van een Azure Service Bus-wachtrij en gegevens tooan Azure SQL-database toegevoegd, Hallo hulpprogramma behoudt alle Hallo orchestration logica en parameterizes hello SQL- en Service Bus-verbindingsreeksen zodat ze kunnen worden ingesteld bij de implementatie.

> [!NOTE]
> Verbindingen moet binnen Hallo dezelfde resourcegroep als Hallo logische app.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Hallo logic app sjabloon PowerShell-module installeren
Hallo gemakkelijkste manier tooinstall Hallo-module is via Hallo [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), met behulp van de opdracht Hallo `Install-Module -Name LogicAppTemplate`.  

Ook kunt u de PowerShell-module Hallo handmatig installeren:

1. Download de meest recente versie Hallo Hallo [logic app sjabloon Maker](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Pak Hallo-map van uw PowerShell-module (meestal `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Voor Hallo module toowork elke tenant en -abonnement toegang token, het is raadzaam dat u deze Hello [ARMClient](https://github.com/projectkudu/ARMClient) opdrachtregelprogramma.  Dit [blogbericht](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) ARMClient in meer detail besproken.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Genereren van een sjabloon voor logische Apps met behulp van PowerShell
Nadat u PowerShell is geïnstalleerd, kunt u een sjabloon genereren met behulp van de volgende opdracht Hallo:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`hello Azure-abonnement-id is. Deze regel voor de eerste keer een toegang via ARMClient, token en vervolgens het doorgesluisd via toohello PowerShell-script en maakt vervolgens Hallo-sjabloon in een JSON-bestand.

## <a name="add-parameters-tooa-logic-app-template"></a>Parameters tooa logic app-sjabloon toevoegen
Nadat u uw logische app-sjabloon maakt, kunt u doorgaan tooadd of parameters die u moet wijzigen. Bijvoorbeeld, als de definitie van de bevat een resource-ID tooan Azure functie of geneste werkstroom dat u van plan toodeploy in een implementatie met één bent, kunt u meer bronnen tooyour sjabloon toevoegen en voorzien van id's, indien nodig. Hallo geldt tooany verwijzingen toocustom API's of Swagger-eindpunten u toodeploy verwacht met elke resourcegroep.

## <a name="deploy-a-logic-app-template"></a>Een logische app-sjabloon implementeren

U kunt uw sjabloon implementeren met behulp van hulpprogramma's zoals PowerShell, REST-API [Visual Studio Team Services Release Management](#team-services), en sjabloonimplementatie via hello Azure-portal.
Bovendien toostore Hallo waarden voor parameters, wordt aangeraden dat u maakt een [parameterbestand](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Meer informatie over hoe te[implementeren van resources met Azure Resource Manager-sjablonen en PowerShell](../azure-resource-manager/resource-group-template-deploy.md) of [implementeren van resources met Azure Resource Manager-sjablonen en Azure-portal Hallo](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>OAuth-verbindingen toestaan

Na de implementatie werkt Hallo logische app end-to-end met geldige parameters op.
U moet echter nog steeds OAuth verbindingen toogenerate een geldige toegangstoken autoriseren.
tooauthorize OAuth-verbindingen, opent u Hallo logische app in Hallo Logic Apps Designer en autoriseren van deze verbindingen. Of voor automatische implementatie, kunt u een script tooconsent tooeach OAuth-verbinding.
Er is een voorbeeldscript op GitHub onder de [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) project.

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Een veelvoorkomend scenario voor het implementeren en beheren van een omgeving is toouse een hulpprogramma zoals Release Management in Visual Studio Team Services, met een sjabloon logic app-implementatie. Visual Studio Team Services bevat een [implementeren Azure Resource Group](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) taak tooany build toevoegen of vrijgeven van de pijplijn. U moet toohave een [service-principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) voor autorisatie toodeploy, waarna u Hallo release definitie kan genereren.

1. Selecteer in de Release Management **leeg** zodat u de definitie van een leeg maken.

    ![Lege definitie maken][1]

2. Kies alle resources die u nodig hebt voor deze, waarschijnlijk inclusief Hallo logic app sjabloon die wordt gegenereerd handmatig of als onderdeel van het Hallo-buildproces.
3. Voeg een **Azure Resource Group Deployment** taak.
4. Configureren met een [service-principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), en verwijzen naar de sjabloon en sjabloonparameters bestanden Hallo.
5. Verder toobuild stappen uit in Hallo release proces voor de omgeving, geautomatiseerde test of goedkeurders indien nodig.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
