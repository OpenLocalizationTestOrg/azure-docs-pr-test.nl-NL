---
title: Implementatie van uw app in Azure met opdrachtregelprogramma's automatiseren | Microsoft Docs
description: Detecteren van informatie over hoe u uw Azure-app vanaf de opdrachtregel kunt implementeren
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
ms.openlocfilehash: e0e2e65557911bcac06d4dc355f47e9331934f8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Implementatie van uw app in Azure met opdrachtregelprogramma's automatiseren
U kunt de implementatie van uw Azure-apps met de opdrachtregelprogramma's automatiseren. Dit artikel worden de beschikbare hulpprogramma's en nuttige koppelingen waarin u kunt zien hoe u ze in de implementatiewerkstroom van uw gebruikt. 

## <a name="msbuild"></a>Implementatie met MSBuild automatiseren
Als u de [Visual Studio IDE](#vs) voor ontwikkeling, kunt u [MSBuild](http://msbuildbook.com/) alles wat u in uw IDE doen kunt automatiseren. U kunt configureren MSBuild voor het gebruik van een [Web Deploy](#webdeploy) of [FTP-/ FTPS](#ftp) bestanden te kopiëren. Web implementeren kan ook veel andere implementatie-gerelateerde taken, zoals het implementeren van databases automatiseren.

Zie de volgende bronnen voor meer informatie over opdrachtregelprogramma implementatie met behulp van MSBuild:

* [ASP.NET Web Deployment met Visual Studio: implementatie van de opdrachtregel](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). 10 in een reeks zelfstudies over de implementatie van Azure met Visual Studio. Laat zien hoe het gebruik van de opdrachtregel om te implementeren nadat het instellen van profielen publiceren in Visual Studio.
* [In de Engine voor het bouwen van Microsoft: met behulp van MSBuild en Team Foundation Build](http://msbuildbook.com/). Gedrukte boek met hoofdstukken over het gebruik van MSBuild voor implementatie.

## <a name="powershell"></a>Implementatie met Windows PowerShell automatiseren
U kunt uitvoeren MSBuild- of FTP-implementaties van [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Als u dat doet, kunt u ook een verzameling van Windows PowerShell-cmdlets die de Azure-REST-API gemakkelijker om aan te roepen.

Zie de volgende bronnen voor meer informatie:

* [Een web-app die is gekoppeld aan een GitHub-opslagplaats implementeren](app-service-web-arm-from-github-provision.md)
* [Inrichten van een web-app met een SQL-Database](app-service-web-arm-with-sql-database-provision.md)
* [Inrichten en microservices zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Echte Cloud-Apps bouwen met Azure - automatiseren Alles](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). E-book hoofdstuk waarin wordt uitgelegd hoe de voorbeeldtoepassing wordt weergegeven in het e-book maakt gebruik van Windows PowerShell-scripts naar een Azure-testomgeving maken en implementeren op deze. Zie de [Resources](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sectie voor koppelingen naar aanvullende documentatie van Azure PowerShell.
* [Windows PowerShell-Scripts gebruiken om te publiceren naar de ontwikkeling en testomgevingen](../vs-azure-tools-publishing-using-powershell-scripts.md). Hoe u Windows PowerShell gebruikt implementatie scripts die door Visual Studio gegenereerd.

## <a name="api"></a>Implementatie met .NET management API automatiseren
U kunt de C#-code voor het uitvoeren van MSBuild- of FTP-functies voor implementatie schrijven. Als u dat doet, kunt u toegang tot de Azure management REST API om site-beheerfuncties te voeren.

Zie de volgende bronnen voor meer informatie:

* [Alles automatiseren met de Azure Management-bibliotheken en .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Inleiding tot de API voor .NET-beheer en koppelingen naar meer documentatie.

## <a name="cli"></a>Implementeren vanaf Azure Command-Line Interface (Azure CLI)
U kunt de opdrachtregel gebruiken in Windows, Mac of Linux-machines te implementeren met FTP. Als u dat doet, kunt u ook toegang tot de REST van de Azure management API met behulp van de Azure CLI.

Zie de volgende bronnen voor meer informatie:

* [Azure-opdrachtregelprogramma's voor](https://azure.microsoft.com/downloads/). Portal-pagina in Azure.com voor informatie over het programma van de opdrachtregel.

## <a name="webdeploy"></a>Implementeren vanaf opdrachtregel Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) Microsoft-software voor de implementatie van IIS die niet alleen intelligent bestand sync biedt functies, maar ook kunt uitvoeren of vele andere implementatie-gerelateerde taken die niet automatisch worden uitgevoerd wanneer u FTP coördineren. Bijvoorbeeld, kunt Web Deploy implementeren een nieuwe database of updates van de database samen met uw web-app. Web Deploy kunt ook de benodigde tijd voor het bijwerken van een bestaande site omdat deze alleen gewijzigde bestanden op intelligente wijze kunt kopiëren minimaliseren. Microsoft Visual Studio en Team Foundation Server hebben ondersteuning voor Web Deploy ingebouwde, maar u kunt ook een Web Deploy rechtstreeks vanaf de opdrachtregel gebruiken voor het automatiseren van de implementatie. Web Deploy opdrachten zeer krachtig zijn, maar het leerproces ingewikkeld zijn.

## <a name="more-resources"></a>Meer bronnen
Een andere Implementatieoptie voor het opdrachtregelprogramma automation is om te gebruiken, zoals een cloud-gebaseerde service [Octopus implementeren](http://en.wikipedia.org/wiki/Octopus_Deploy). Zie voor meer informatie [implementeren ASP.NET-toepassingen naar Azure websites](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Zie de volgende bronnen voor meer informatie over opdrachtregelprogramma's:

* [Eenvoudige Web-Apps: Implementatie](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog door David Ebbo over een hulpprogramma dat hij geschreven om eenvoudiger Web Deploy wilt gebruiken.
* [Web Deployment Tool](http://technet.microsoft.com/library/dd568996). Officiële documentatie op de website Microsoft TechNet. De datum maar nog steeds een goede plaats om te starten.
* [Met Web implementeren](http://www.iis.net/learn/publish/using-web-deploy). Officiële documentatie op de site Microsoft IIS.NET. De datum ook maar een goede plaats om te starten.
* [ASP.NET Web Deployment met Visual Studio: implementatie van de opdrachtregel](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild is de build-engine die wordt gebruikt door Visual Studio en kan ook worden gebruikt vanaf de opdrachtregel webtoepassingen voor Web-Apps te implementeren. Deze zelfstudie maakt deel uit van een serie die is hoofdzakelijk over de implementatie van de Visual Studio.

