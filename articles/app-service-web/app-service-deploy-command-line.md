---
title: implementatie van uw Azure-app met de opdrachtregelprogramma's aaaAutomate | Microsoft Docs
description: Detecteren van informatie over hoe u uw Azure-app uit Hallo opdrachtregelprogramma kunt implementeren
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Implementatie van uw app in Azure met opdrachtregelprogramma's automatiseren
U kunt de implementatie van uw Azure-apps met de opdrachtregelprogramma's automatiseren. In dit artikel worden de beschikbare hulpprogramma's en Hallo nuttig koppelingen die laten hoe u zien toouse ze in uw implementatiewerkstroom. 

## <a name="msbuild"></a>Implementatie met MSBuild automatiseren
Als u Hallo [Visual Studio IDE](#vs) voor ontwikkeling, kunt u [MSBuild](http://msbuildbook.com/) tooautomate alles wat u in uw IDE doen kunt. U kunt ofwel MSBuild toouse configureren [Web Deploy](#webdeploy) of [FTP-/ FTPS](#ftp) toocopy bestanden. Web implementeren kan ook veel andere implementatie-gerelateerde taken, zoals het implementeren van databases automatiseren.

Zie voor meer informatie over opdrachtregelprogramma implementatie met behulp van MSBuild Hallo resources te volgen:

* [ASP.NET Web Deployment met Visual Studio: implementatie van de opdrachtregel](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). 10 in een reeks zelfstudies over implementatie tooAzure met Visual Studio. Toont hoe toouse opdrachtregel toodeploy Hallo na het instellen van publiceren profielen in Visual Studio.
* [Hallo binnen Microsoft bouwen Engine: met behulp van MSBuild en Team Foundation bouwen](http://msbuildbook.com/). Gedrukte boek met hoofdstukken over het toouse MSBuild voor implementatie.

## <a name="powershell"></a>Implementatie met Windows PowerShell automatiseren
U kunt uitvoeren MSBuild- of FTP-implementaties van [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Als u dat doet, kunt u ook een verzameling van Windows PowerShell-cmdlets die hello Azure REST management API eenvoudig toocall maken.

Zie voor meer informatie Hallo resources te volgen:

* [Een web-app gekoppelde tooa GitHub-opslagplaats implementeren](app-service-web-arm-from-github-provision.md)
* [Inrichten van een web-app met een SQL-Database](app-service-web-arm-with-sql-database-provision.md)
* [Inrichten en microservices zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Echte Cloud-Apps bouwen met Azure - automatiseren Alles](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). E-book hoofdstuk waarin wordt uitgelegd hoe Hallo-voorbeeldtoepassing die is weergegeven in Hallo e-book gebruikmaakt van Windows PowerShell-scripts toocreate een Azure omgeving testen en implementeren van tooit. Zie Hallo [Resources](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sectie voor koppelingen tooadditional documentatie van Azure PowerShell.
* [Met behulp van Windows PowerShell-Scripts tooPublish tooDev en testomgevingen](../vs-azure-tools-publishing-using-powershell-scripts.md). Hoe toouse implementatie van Windows PowerShell scripts die Visual Studio gegenereerd.

## <a name="api"></a>Implementatie met .NET management API automatiseren
U kunt C#-code schrijven tooperform MSBuild- of FTP-functies voor implementatie. Als u dat doet, kunt u de beheerfuncties van hello Azure management REST API tooperform site openen.

Zie voor meer informatie Hallo resource te volgen:

* [Alles automatiseren met hello Azure Management-bibliotheken en .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Inleiding toohello .NET management API en koppelingen toomore-documentatie.

## <a name="cli"></a>Implementeren vanaf Azure Command-Line Interface (Azure CLI)
U kunt Hallo vanaf de opdrachtregel in toodeploy van Windows, Mac of Linux-machines gebruiken met FTP. Als u dat doet, kunt u ook toegang tot hello Azure REST management API met behulp van hello Azure CLI.

Zie voor meer informatie Hallo resource te volgen:

* [Azure-opdrachtregelprogramma's voor](https://azure.microsoft.com/downloads/). Portal-pagina in Azure.com voor informatie over het programma van de opdrachtregel.

## <a name="webdeploy"></a>Implementeren vanaf opdrachtregel Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) is Microsoft-software voor implementatie tooIIS die niet alleen intelligent bestand biedt functies synchroniseren, maar ook kunt uitvoeren of vele andere implementatie-gerelateerde taken die niet automatisch worden uitgevoerd wanneer u FTP coördineren. Bijvoorbeeld, kunt Web Deploy implementeren een nieuwe database of updates van de database samen met uw web-app. Web Deploy kunt Hallo tijd die nodig is tooupdate een bestaande site ook minimaliseren, omdat deze alleen gewijzigde bestanden op intelligente wijze kunt kopiëren. Microsoft Visual Studio en Team Foundation Server hebben ondersteuning voor Web Deploy ingebouwde, maar u kunt ook Web Deploy rechtstreeks vanuit Hallo opdrachtregel tooautomate implementatie. Web Deploy-opdrachten zijn zeer krachtige maar Hallo leerproces ingewikkeld zijn.

## <a name="more-resources"></a>Meer bronnen
Een andere implementatie optie toocommand regel automation is toouse cloud-gebaseerde service zoals [Octopus implementeren](http://en.wikipedia.org/wiki/Octopus_Deploy). Zie voor meer informatie [implementeren ASP.NET-toepassingen tooAzure websites](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Zie voor meer informatie over opdrachtregelprogramma's Hallo resource te volgen:

* [Eenvoudige Web-Apps: Implementatie](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog door David Ebbo over een hulpprogramma dat hij toomake geschreven deze eenvoudiger toouse Web Deploy.
* [Web Deployment Tool](http://technet.microsoft.com/library/dd568996). Officiële documentatie op Microsoft TechNet-website Hallo. De datum maar nog steeds een goede plaats toostart.
* [Met Web implementeren](http://www.iis.net/learn/publish/using-web-deploy). Officiële documentatie op Hallo IIS.NET Microsoft-site. De datum ook maar een goede plaats toostart.
* [ASP.NET Web Deployment met Visual Studio: implementatie van de opdrachtregel](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild is Hallo bouwen engine die wordt gebruikt door Visual Studio en kan ook worden gebruikt vanuit Hallo opdrachtregel toodeploy web applications tooWeb Apps. Deze zelfstudie maakt deel uit van een serie die is hoofdzakelijk over de implementatie van de Visual Studio.

