---
title: aaaTroubleshooting Docker client fouten in Windows met behulp van Visual Studio | Microsoft Docs
description: Oplossen van problemen die kunnen optreden bij gebruik van Visual Studio toocreate en tooDocker voor web-apps op Windows implementeren met behulp van Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Problemen met Visual Studio Docker-ontwikkeling

Wanneer u met Visual Studio Tools voor Docker Preview werkt, kunnen enkele problemen optreden vanwege Hallo aard van Hallo preview.
Hier volgen enkele veelvoorkomende problemen en oplossingen.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Linux-containers**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Bouwen fouten optreden bij foutopsporing in een web- of console toepassing voor .NET Core  

Dit kan zijn gerelateerd toonot Hallo station waar Hallo project zich bevindt in te delen met Docker voor Windows.  Er kan een foutbericht zoals Hallo volgende:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve dit probleem:

1. Met de rechtermuisknop op **Docker voor Windows** in systeemvak Hallo en selecteer vervolgens **instellingen**.  
2. Selecteer **gedeelde stations** en delen Hallo station waar Hallo project zich bevindt.

### <a name="windows-containers"></a>**Windows-containers**

Hallo zijn volgende problemen specifieke toodebugging .NET Framework console en web-toepassingen in Windows-containers.

#### <a name="prerequisites"></a>Vereisten

1. Visual Studio 2017 RC (of hoger) Hallo met .NET Core en Docker Preview werkbelasting moet worden geïnstalleerd.
2. Patches van Windows 10 Verjaardag Update die aan de meest recente Windows Update. Specifiek [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) moet worden geïnstalleerd. 
3. [Docker voor Windows](https://docs.docker.com/docker-for-windows/) (1.13.0 bouwen of hoger) moet worden geïnstalleerd.
4. **Overschakelen van tooWindows containers** moet worden geselecteerd. Klik in het systeemvak hello, **Docker voor Windows**, en selecteer vervolgens **tooWindows containers overschakelen**. Zorg ervoor dat deze instelling wordt behouden nadat Hallo machine opnieuw is opgestart.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>Console-uitvoer wordt niet weergegeven in het venster Visual Studio tijdens het opsporen van een consoletoepassing

Dit is een bekend probleem met de Hallo foutopsporingsfunctie (msvsmon.exe), die momenteel niet is ontworpen voor dit scenario. Ondersteuning voor dit scenario kan worden opgenomen in een toekomstige release. toosee uitvoer van Hallo-consoletoepassing in Visual Studio, gebruik **Docker: Start-Project**, hetgeen gelijk is te**starten zonder foutopsporing**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Foutopsporing webtoepassingen Hello configuratie mislukt (403) verboden release

toowork oplossing van dit probleem web.release.config openen in Hallo oplossing en uitcommentariëren of te verwijderen van Hallo volgende regels:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Linux-containers**

#### <a name="unable-toovalidate-volume-mapping"></a>Kan geen toovalidate toewijzing
Toewijzing is vereist tooshare Hallo broncode en binaire bestanden van uw toepassing hello app map in container Hallo.  Toewijzingen voor specifieke volume bevinden zich in een docker-compose.dev.debug.yml en docker-compose.dev.release.yml. Als er bestanden zijn gewijzigd op de hostmachine, wijzigingen Hallo containers in deze in een vergelijkbare mapstructuur.

tooenable volume toewijzen:

1. Klik op **Moby** in het systeemvak Hallo en selecteer **instellingen**.
2. Selecteer **gedeelde schijven**.
3. Selecteer Hallo station dat als host fungeert voor uw project en Hallo station waar % USERPROFILE % zich bevindt.
4. Klik op **Toepassen**.

tootest als toewijzing functioneert, bouwen en F5 uit vanuit Visual Studio selecteren nadat u een of meer stations hebt gedeeld, of Hallo code volgende vanaf een opdrachtprompt worden uitgevoerd.

> [!NOTE]
> In dit voorbeeld wordt ervan uitgegaan dat de map van uw gebruikers zich op station C bevindt en dat deze is gedeeld.
> Wijzig zo nodig als u een ander station hebt gedeeld.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Hallo na de code in Hallo Linux container worden uitgevoerd.

```
/ # ls
```

U ziet een mappenlijst weergegeven uit Hallo gebruikers/openbare map. Als er worden geen bestanden worden weergegeven en de map /c/Users/Public niet leeg is, wordt toewijzing is niet juist geconfigureerd.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Wijzigen van toohello wormhole toosee Hallo Mapinhoud Hallo `/c/Users/Public` directory:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Wanneer u met virtuele Linux-machines werkt, is Hallo container bestandssysteem is hoofdlettergevoelig.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>: 'PrepareForBuild' opbouwtaak is onverwacht mislukt

Microsoft.DotNet.Docker.CommandLine.ClientException: Is een fout opgetreden tijdens het tooconnect.

Controleer of dat deze Hallo standaard Docker-host wordt uitgevoerd. Open een opdrachtprompt en voer:

```
docker info
```

Als dit een fout retourneert, probeert toostart hello **Docker voor Windows** bureaublad-app. Als Hallo bureaublad-app wordt uitgevoerd, klikt u vervolgens **Moby** moeten worden weergegeven in het systeemvak Hallo. Met de rechtermuisknop op **Moby** en open **instellingen**. Klik op **opnieuw**, en start vervolgens opnieuw Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Een foutdialoogvenster treedt op tijdens een poging de tooadd Docker-ondersteuning of een ASP.NET Core-toepassing in een container voor foutopsporing (F5)

Na het verwijderen en installeren van extensies, raken Hallo beheerd uitbreidbaarheid Framework (MEF)-cache in Visual Studio beschadigd. Wanneer dit gebeurt, kan leiden tot diverse foutberichten worden weergegeven wanneer u bent Docker-ondersteuning toe te voegen en/of toorun probeert of opsporen (F5) in uw toepassing ASP.NET Core. Gebruik als tijdelijke oplossing Hallo stappen toodelete en opnieuw genereren Hallo MEF cache te volgen.

1. Sluit alle exemplaren van Visual Studio.
1. Open % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Hallo volgende mappen te verwijderen:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Open Visual Studio.
1. Hallo scenario opnieuw proberen.
