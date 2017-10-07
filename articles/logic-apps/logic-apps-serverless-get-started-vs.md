---
title: aaaBuild een zonder server-app in Visual Studio | Microsoft Docs
description: Aan de slag met uw eerste zonder server-app met deze handleiding voor het maken, implementeren en beheren van Hallo-app in Visual Studio.
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Een zonder server-App in Visual Studio met Logic Apps en functies

Zonder server en -mogelijkheden in Azure kunnen voor snelle ontwikkeling en implementatie van cloud-toepassingen.  Dit document is gericht op het tooget in Visual Studio voor het bouwen van een toepassing zonder server gestart.  Een overzicht van zonder server in Azure [vindt u in dit artikel](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Alles voorbereiden

Hier volgen Hallo vereisten nodig toobuild van een toepassing zonder server vanuit Visual Studio:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) of Visual Studio 2015 - Community, Professional of Enterprise
* [Logic Apps-Tools voor Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Azure Functions kernonderdelen](https://www.npmjs.com/package/azure-functions-core-tools) toodebug lokaal werkt
* Toegang toohello web bij gebruik van Hallo ingesloten logische App designer

## <a name="getting-started-with-a-deployment-template"></a>Aan de slag met een sjabloon voor de implementatie

Het beheer van resources in Azure worden uitgevoerd binnen een resourcegroep.  Een resourcegroep is een logische groepering van resources.  Resourcegroepen toestaan implementatie en beheer van een verzameling resources.  Voor een toepassing zonder server in Azure bevat onze resourcegroep Azure Logic Apps en Azure Functions.  Met behulp van Hallo resourcegroepproject vanuit Visual Studio, we kunnen toodevelop zijn, beheren en implementeren van de gehele toepassing hello als een enkel actief.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Maak een resourcegroep-project in Visual Studio

1. Klik in Visual Studio, tooadd een **nieuw Project**
1. In Hallo **Cloud** categorie, selecteer toocreate een Azure **resourcegroep** project  
 * Als u Hallo categorie of opgenomen project niet ziet, zorg er hello Azure SDK voor Visual Studio is geïnstalleerd
1. Hallo project geven een naam en locatie en selecteer **Ok** toocreate Visual Studio vraagt tooselect een sjabloon.  U kunt toostart selecteren uit leeg, beginnen met een logische App of andere resources.  Echter in dit geval wordt een Snelstartsjabloon met de Azure-tooget die ons met een app zonder server gestart gebruiken.
1. Selecteer tooshow sjablonen van **Azure Quickstart** ![Azure-snelstartsjablonen selecteren][1]
1. Selecteer Hallo zonder server snelstartsjabloon: **101-logic-app-and-function-app** en klik op **Ok**

Hallo Quick Start-sjabloon maakt u een sjabloon voor de implementatie in uw resourcegroepproject.  Hallo-sjabloon bevat een eenvoudige logische App, die een Azure-functies aanroepen en Hallo resultaat retourneert.  Als u Hallo openen `azuredeploy.json` bestand in Solution Explorer hello, ziet u Hallo-resources voor Hallo zonder server-app.

## <a name="deploying-hello-serverless-application"></a>Hallo zonder server-toepassing implementeren

Voordat u Hallo logische App visuele ontwerper in Visual Studio openen kunt, moeten er toobe vooraf geïmplementeerde Azure-resourcegroep.  Hierdoor kunnen Hallo designer toocreate en gebruik verbindingen tooresources en services in Hallo logische app.  tooget gestart, moet u toodeploy Hallo oplossing is gemaakt.

1. Klik met de rechtermuisknop Hallo-project in Visual Studio, selecteer **implementeren**, en maak een **nieuw** implementatie ![nieuwe resource implementatie selecteren][2]
1. Selecteer een geldige Azure-abonnement en resourcegroep
1. Selecteer het te**implementeren** Hallo oplossing
1. Voer in het Hallo-naam voor de logische App Hallo en hello Azure functie-App.  de naam van de Azure-functie Hallo hoeft toobe globaal uniek zijn

Hallo zonder Server oplossing worden geïmplementeerd in de opgegeven resourcegroep Hallo.  Als u hello bekijkt **uitvoer** in Visual Studio ziet u Hallo status van Hallo-implementatie.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Hallo logische app in Visual Studio bewerken

Zodra het Hallo-oplossing is geïmplementeerd in elke willekeurige resourcegroep, de visuele ontwerpfunctie hello worden gebruikt tooedit en wijzigingen toohello logische app maken.

1. Klik met de rechtermuisknop Hallo `azuredeploy.json` bestand in Hallo Solution Explorer en selecteer **met Logic Apps Designer openen**
1. Selecteer Hallo **resourcegroep** en **locatie** Hallo-oplossing is geïmplementeerd tooand Selecteer **OK**

Hallo logische App visuele ontwerper worden nu weergegeven met Visual Studio.  U kunt gaan tooadd stappen Hallo werkstroom wijzigen en wijzigingen opslaan.  U kunt ook logische apps maken vanuit Visual Studio.  Als u met de rechtermuisknop op Hallo **Resources** in Hallo sjabloon navigator, kunt u tooadd een **logische App** toohello project.  Lege logische apps laden in de visuele ontwerpfunctie Hallo zonder een implementeren in een resourcegroep.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Uitvoeringsgeschiedenis voor een geïmplementeerde logische app beheren en weergeven

U kunt ook beheren en weergeven van de geschiedenis Hallo uitvoeren voor logic apps die zijn geïmplementeerd in Azure.  Als u Hallo openen **Cloud Explorer** hulpprogramma in Visual Studio kunt u met de rechtermuisknop op een logische App en kies tooedit, uitschakelen, eigenschappen weergeven of uitvoeringsgeschiedenis weergeven.  Klik op bewerken kunt u ook toodownload een gepubliceerde logische app in een resourcegroep met Visual Studio-project.  Dit betekent dat zelfs als u het bouwen van uw logische app in hello Azure-portal hebt gestart, u kunt nog steeds importeren en het beheren van Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Een Azure-functie in Visual Studio ontwikkelen

Hallo implementatiesjabloon implementeert geen Azure-functies die zijn opgenomen in het Hallo-oplossing voor Hallo git-opslagplaats is opgegeven in Hallo `azuredeploy.json` variabelen.  Als u een functie-project binnen Hallo oplossing ontwerpt, inchecken bij broncodebeheer (GitHub, Visual Studio Team Services, enz.), en werk Hallo `repo` variabele, Hallo sjabloon implementeert hello Azure-functie.

### <a name="creating-an-azure-function-project"></a>Een Azure-functie-project maken

Als u JavaScript, Python, F #, Bash, Batch of PowerShell gebruikt, voert u de Hallo [stappen voor het Hallo functies CLI](../azure-functions/functions-run-local.md) toocreate een project.  Als een functie in C# ontwikkelt, kunt u een [C#-klassenbibliotheek](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) in de huidige oplossing Hallo voor hello Azure-functie.

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over hoe toobuild een zonder server sociale dashboard](logic-apps-scenario-social-serverless.md)
* [Een logische app beheren vanuit Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Definitietaal van Logic App werkstroom](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
