---
title: aaaSet van een ontwikkelomgeving voor Azure microservices | Microsoft Docs
description: Installeer Hallo runtime, SDK en hulpprogramma's en maak een lokaal ontwikkelcluster. Na het voltooien van deze installatie, kunt u zich gereed toobuild toepassingen.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Uw ontwikkelomgeving voorbereiden
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild en voer [Azure Service Fabric-toepassingen] [ 1] installeren op uw ontwikkelcomputer Hallo runtime, SDK en hulpprogramma's. U moet ook tooenable uitvoering van Windows PowerShell-scripts Hallo opgenomen in Hallo SDK.

## <a name="prerequisites"></a>Vereisten
### <a name="supported-operating-system-versions"></a>Ondersteunde versies van besturingssystemen
Hallo volgende versies van besturingssystemen worden ondersteund voor ontwikkeling:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 bevat standaard alleen Windows PowerShell 2.0. Voor Service Fabric PowerShell-cmdlets is PowerShell 3.0 of hoger vereist. U kunt [Windows PowerShell 5.0 downloaden] [ powershell5-download] van Hallo Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Hallo SDK en hulpprogramma's installeren
### <a name="toouse-visual-studio-2017"></a>Visual Studio 2017 toouse
Service Fabric-programma's maken deel uit van de Azure-ontwikkeling en het beheer werkbelasting Hallo in Visual Studio 2017. Schakel deze workload in als onderdeel van de Visual Studio-installatie.
Bovendien moet u tooinstall Hallo Microsoft Azure Service Fabric SDK, met behulp van Web Platform Installer.

* [Hallo Microsoft Azure Service Fabric SDK installeren][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (Visual Studio 2015 Update 2 of hoger vereist)
Service Fabric-hulpprogramma's zijn voor Visual Studio 2015 geïnstalleerd samen met de Hallo SDK, met behulp van Hallo Web Platform Installer:

* [Hallo Microsoft Azure Service Fabric SDK en hulpprogramma's installeren][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Alleen SDK-installatie
Als u alleen Hallo SDK hoeft, kunt u dit pakket installeren:
* [Hallo Microsoft Azure Service Fabric SDK installeren][core-sdk]

Hallo huidige versies zijn:
* Service Fabric SDK 2.7.198
* Service Fabric runtime 5.7.198
* Service Fabric Tools voor Visual Studio 2015 1.7.50721
* Visual Studio 2017 Update 2 bevat Service Fabric Tools voor Visual Studio 1.6.20170504
* Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) bevat Service Fabric Tools voor Visual Studio 1.7.20170721

Zie [Ondersteuning voor Service Fabric](service-fabric-support.md) voor een lijst met ondersteunde versies.

## <a name="enable-powershell-script-execution"></a>Uitvoering van PowerShell-script inschakelen
Service Fabric gebruikt Windows PowerShell-scripts om een lokaal ontwikkelcluster te maken en om toepassingen vanuit Visual Studio te implementeren. Standaard worden deze scripts door Windows geblokkeerd zodat ze niet worden uitgevoerd. tooenable ze, moet u uw PowerShell-uitvoeringsbeleid wijzigen. Open PowerShell als beheerder en voert u Hallo volgende opdracht:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Volgende stappen
Nu u uw ontwikkelingsomgeving hebt ingesteld, kunt u apps ontwikkelen en uitvoeren.

* [Uw eerste Service Fabric-toepassing in Visual Studio maken](service-fabric-create-your-first-application-in-visual-studio.md)
* [Meer informatie over hoe toodeploy en beheren van toepassingen op uw lokale cluster](service-fabric-get-started-with-a-local-cluster.md)
* [Meer informatie over Hallo programming modellen: Reliable Services en Reliable Actors](service-fabric-choose-framework.md)
* [Bekijk Hallo Service Fabric-codevoorbeelden op GitHub](https://aka.ms/servicefabricsamples)
* [Uw cluster visualiseren door gebruik te maken van Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Ga als volgt Hallo Service Fabric learning pad tooget een brede inleiding toohello platform](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric-campagnepagina"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI-koppeling"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI-koppeling"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI-koppeling"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
