---
title: aaaAzure SDK voor .NET 2.8 Release-opmerkingen
description: Azure SDK voor .NET 2.8 Release-opmerkingen
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK voor .NET 2.8, 2.8.1 en 2.8.2
## <a name="overview"></a>Overzicht
In dit artikel bevat Hallo release-opmerkingen (met bekende problemen en grote wijzigingen) voor hello Azure SDK voor .NET 2.8, 2.8.1 en 2.8.2 worden vrijgegeven. 

Zie voor een volledige lijst met nieuwe functies en wijzigingen in deze release, Hallo [Azure SDK 2.8 voor Visual Studio 2013 en Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) aankondiging. 

## <a name="azure-sdk-for-net-28"></a>Azure SDK voor .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Download de Azure SDK voor .NET 2.8
[Azure SDK voor .NET 2.8 voor Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Azure SDK voor .NET 2.8 voor Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Ondersteuning voor .NET 4.5.2
#### <a name="known-issues"></a>Bekende problemen
Azure .NET SDK 2.8 kunt u toocreate .NET 4.5.2 Cloudservice pakketten. Echter 4.5.2 .NET framework wordt niet geïnstalleerd op Hallo standaard Gast OS installatiekopieën vanaf januari 2016 Gastbesturingssysteem release. Voordat u met .NET 4.5.2 framework is beschikbaar via een afzonderlijke Gastbesturingssysteem releaseversie – November 2015-02. Zie Hallo [Azure Gast OS Releases en SDK compatibiliteit Matrix](../cloud-services/cloud-services-guestos-update-matrix.md) pagina tootrack wanneer Hallo installatiekopie worden uitgebracht.  Zodra het Hallo November 2015-02-installatiekopie wordt vrijgegeven kunt u toouse die installatiekopie door uw Service in de Cloud-configuratiebestand (.cscfg)-bestand bij te werken. In de serviceconfiguratie Hallo bestand Hallo osVersion kenmerk van Hallo serviceconfiguration zijn element toohello tekenreeks instellen "WA-GUEST-OS-4.26_201511-02 '. Als u deze installatiekopie tooopt in toouse kiest vervolgens krijgt niet meer u automatische updates toohello Gastbesturingssysteem. tooget hello automatische updates Hallo osVersion te moet worden ingesteld ' * ' en .NET 4.5.2 is alleen beschikbaar via Automatische updates van januari 2016.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Bekende problemen
Tijdens een **Data Factory sjabloon** project maken met betrekking tot voorbeeldgegevens azure power shell-script kan mislukken als azure power shell-versie is geïnstalleerd op de computer Hallo na 0.9.8.

In de volgorde toosuccessfully dit type project maakt, moet u installeren [azure power shell-versie 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Azure Resource Manager-hulpprogramma 's
#### <a name="breaking-changes"></a>Wijzigingen op te splitsen
Hallo geleverd door hello Azure-resourcegroepproject PowerShell-script is in deze release toowork met Hallo nieuwe Azure PowerShell-cmdlets versie 1.0 bijgewerkt.  Dit nieuwe script werkt niet uit met Visual Studio wanneer u een versie van Hallo SDK voorafgaande too2.8.  

Scripts van de projecten die zijn gemaakt in eerdere versies van Hallo SDK wordt niet uitvoeren vanuit Visual Studio wanneer met behulp van Hallo 2,8 SDK.  Alle scripts blijven toowork buiten Visual Studio met de juiste versie Hallo van hello Azure PowerShell-cmdlets.  

Hallo vereist 2,8 SDK versie 1.0 van hello Azure PowerShell-cmdlets.  Alle andere versies van Hallo SDK vereist versie 0.9.8 van hello Azure PowerShell-cmdlets.  Zie voor meer informatie [dit](http://go.microsoft.com/fwlink/?LinkID=623011) blog.

### <a name="web-tools-extensions"></a>Web hulpprogramma's voor uitbreidingen
#### <a name="known-issues"></a>Bekende problemen
Hallo volgen bekende problemen in na de release Hallo verholpen.

* App Service gerelateerde Cloud en het Server Explorer gebaar voor niet-productieve omgevingen (zoals Azure China of Azure Stack klanten) werken niet. Voor klanten in deze gevolgen gebieden downloaden Hallo publiceren wordt profiel van hello Azure-portal publiceren mogelijkheid ingeschakeld. Een toekomstige release wordt gebaren zoals 'Foutopsporingsprogramma koppelen' en 'Weergave Streaming Logs' herstellen voor Azure China en Stack-klanten. 
* Klanten kunnen fouten tijdens het App-Service gemaakt wanneer Hallo App Insights exemplaar toowhich die ze implementeert een andere regio dan VS-Oost wordt zien. In deze scenario's, het maken van een App Service in Hallo-portal en het downloaden van Hallo publicatieprofiel wordt publishing scenario's mogelijk. 

### <a name="azure-hdinsight-tools"></a>Azure HDInsight-hulpprogramma 's
#### <a name="new-updates"></a>Nieuwe updates
* U kunt uw Hive-query uitvoeren in Hallo-cluster via HiveServer2 met bijna geen overhead en Zie Hallo taak logboeken realtime.
* Hallo met nieuwe Hive Taakuitvoeringsweergave kunt u uw taak diepere, nader meer informatie en potentiële problemen te identificeren.

Zie voor informatie [Azure SDK 2.8 voor Visual Studio 2013 en Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Azure SDK voor .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Bekende problemen voor Visual Studio 2013 en Visual Studio 2015
1. Geactiveerde webtaak publiceert tooslots wordt weergegeven en de fout en won't set een planning, maar zendt Hallo webtaak tooAzure. Klanten die worden een geplande taak moeten kunnen hello Azure Portal tooset up Hallo planning vervolgens voor Hallo webtaak gebruiken. 
2. Python-klanten kunnen foutopsporingsprogramma problemen. Service-team rolt een oplossing voor dit maar als klanten worden beïnvloed, laat Microsoft in Hallo forums of op Hallo aankondiging blog weten of het gedeelte met opmerkingen opmerkingen bij de release. 
3. Klanten in bepaalde regio's (zoals Zuid-India) krijgen met App Service-fouten bij het inrichten. Dit komt overeen met het Hallo-portal en klanten die met dit probleem hello Azure portal toorequest toegang toopublish toothese geo-regio's kunnen gebruiken. Nadat zij toegang toothese regio's met behulp van aanvragen moet hello Azure portal inrichting werken. 

## <a name="azure-sdk-for-net-282"></a>Azure SDK voor .NET 2.8.2
Klanten ondervinden na de installatie van extra Hallo 2.8.2 Hallo Hallo na.         

* Als u van Windows 10 gebruikmaakt en Internet Explorer niet hebt geïnstalleerd, verschijnt het foutbericht 'Internet Explorer kan niet worden gevonden'.
  tooresolve hello probleem, installeer Internet Explorer met behulp van Hallo toevoegen of verwijderen van dialoogvenster Windows-onderdelen.

Als u dit probleem ziet, Hallo verzenden een glimlach functie tooreport gebruiken deze.

Zie voor meer informatie [dit](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) plaatsen.

## <a name="other-updates"></a>Andere Updates
Zie voor andere updates [Azure SDK 2.8 aankondiging post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Zie ook
[Azure SDK 2.8 aankondiging post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Ondersteuning en buiten gebruik stellen informatie voor hello Azure SDK voor .NET- en API 's](https://msdn.microsoft.com/library/azure/dn479282.aspx)

