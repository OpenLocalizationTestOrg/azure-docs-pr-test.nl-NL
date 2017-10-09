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
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="517d1-103">Problemen met Visual Studio Docker-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="517d1-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="517d1-104">Wanneer u met Visual Studio Tools voor Docker Preview werkt, kunnen enkele problemen optreden vanwege Hallo aard van Hallo preview.</span><span class="sxs-lookup"><span data-stu-id="517d1-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="517d1-105">Hier volgen enkele veelvoorkomende problemen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="517d1-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="517d1-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="517d1-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="517d1-107">**Linux-containers**</span><span class="sxs-lookup"><span data-stu-id="517d1-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="517d1-108">Bouwen fouten optreden bij foutopsporing in een web- of console toepassing voor .NET Core</span><span class="sxs-lookup"><span data-stu-id="517d1-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="517d1-109">Dit kan zijn gerelateerd toonot Hallo station waar Hallo project zich bevindt in te delen met Docker voor Windows.</span><span class="sxs-lookup"><span data-stu-id="517d1-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="517d1-110">Er kan een foutbericht zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="517d1-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="517d1-111">tooresolve dit probleem:</span><span class="sxs-lookup"><span data-stu-id="517d1-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="517d1-112">Met de rechtermuisknop op **Docker voor Windows** in systeemvak Hallo en selecteer vervolgens **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="517d1-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="517d1-113">Selecteer **gedeelde stations** en delen Hallo station waar Hallo project zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="517d1-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="517d1-114">**Windows-containers**</span><span class="sxs-lookup"><span data-stu-id="517d1-114">**Windows containers**</span></span>

<span data-ttu-id="517d1-115">Hallo zijn volgende problemen specifieke toodebugging .NET Framework console en web-toepassingen in Windows-containers.</span><span class="sxs-lookup"><span data-stu-id="517d1-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="517d1-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="517d1-116">Prerequisites</span></span>

1. <span data-ttu-id="517d1-117">Visual Studio 2017 RC (of hoger) Hallo met .NET Core en Docker Preview werkbelasting moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="517d1-118">Patches van Windows 10 Verjaardag Update die aan de meest recente Windows Update.</span><span class="sxs-lookup"><span data-stu-id="517d1-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="517d1-119">Specifiek [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="517d1-120">[Docker voor Windows](https://docs.docker.com/docker-for-windows/) (1.13.0 bouwen of hoger) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="517d1-121">**Overschakelen van tooWindows containers** moet worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="517d1-122">Klik in het systeemvak hello, **Docker voor Windows**, en selecteer vervolgens **tooWindows containers overschakelen**.</span><span class="sxs-lookup"><span data-stu-id="517d1-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="517d1-123">Zorg ervoor dat deze instelling wordt behouden nadat Hallo machine opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="517d1-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="517d1-124">Console-uitvoer wordt niet weergegeven in het venster Visual Studio tijdens het opsporen van een consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="517d1-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="517d1-125">Dit is een bekend probleem met de Hallo foutopsporingsfunctie (msvsmon.exe), die momenteel niet is ontworpen voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="517d1-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="517d1-126">Ondersteuning voor dit scenario kan worden opgenomen in een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="517d1-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="517d1-127">toosee uitvoer van Hallo-consoletoepassing in Visual Studio, gebruik **Docker: Start-Project**, hetgeen gelijk is te**starten zonder foutopsporing**.</span><span class="sxs-lookup"><span data-stu-id="517d1-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="517d1-128">Foutopsporing webtoepassingen Hello configuratie mislukt (403) verboden release</span><span class="sxs-lookup"><span data-stu-id="517d1-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="517d1-129">toowork oplossing van dit probleem web.release.config openen in Hallo oplossing en uitcommentariëren of te verwijderen van Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="517d1-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="517d1-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="517d1-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="517d1-131">**Linux-containers**</span><span class="sxs-lookup"><span data-stu-id="517d1-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="517d1-132">Kan geen toovalidate toewijzing</span><span class="sxs-lookup"><span data-stu-id="517d1-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="517d1-133">Toewijzing is vereist tooshare Hallo broncode en binaire bestanden van uw toepassing hello app map in container Hallo.</span><span class="sxs-lookup"><span data-stu-id="517d1-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="517d1-134">Toewijzingen voor specifieke volume bevinden zich in een docker-compose.dev.debug.yml en docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="517d1-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="517d1-135">Als er bestanden zijn gewijzigd op de hostmachine, wijzigingen Hallo containers in deze in een vergelijkbare mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="517d1-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="517d1-136">tooenable volume toewijzen:</span><span class="sxs-lookup"><span data-stu-id="517d1-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="517d1-137">Klik op **Moby** in het systeemvak Hallo en selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="517d1-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="517d1-138">Selecteer **gedeelde schijven**.</span><span class="sxs-lookup"><span data-stu-id="517d1-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="517d1-139">Selecteer Hallo station dat als host fungeert voor uw project en Hallo station waar % USERPROFILE % zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="517d1-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="517d1-140">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="517d1-140">Click **Apply**.</span></span>

<span data-ttu-id="517d1-141">tootest als toewijzing functioneert, bouwen en F5 uit vanuit Visual Studio selecteren nadat u een of meer stations hebt gedeeld, of Hallo code volgende vanaf een opdrachtprompt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="517d1-142">In dit voorbeeld wordt ervan uitgegaan dat de map van uw gebruikers zich op station C bevindt en dat deze is gedeeld.</span><span class="sxs-lookup"><span data-stu-id="517d1-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="517d1-143">Wijzig zo nodig als u een ander station hebt gedeeld.</span><span class="sxs-lookup"><span data-stu-id="517d1-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="517d1-144">Hallo na de code in Hallo Linux container worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="517d1-145">U ziet een mappenlijst weergegeven uit Hallo gebruikers/openbare map.</span><span class="sxs-lookup"><span data-stu-id="517d1-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="517d1-146">Als er worden geen bestanden worden weergegeven en de map /c/Users/Public niet leeg is, wordt toewijzing is niet juist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="517d1-147">Wijzigen van toohello wormhole toosee Hallo Mapinhoud Hallo `/c/Users/Public` directory:</span><span class="sxs-lookup"><span data-stu-id="517d1-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="517d1-148">Wanneer u met virtuele Linux-machines werkt, is Hallo container bestandssysteem is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="517d1-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="517d1-149">: 'PrepareForBuild' opbouwtaak is onverwacht mislukt</span><span class="sxs-lookup"><span data-stu-id="517d1-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="517d1-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Is een fout opgetreden tijdens het tooconnect.</span><span class="sxs-lookup"><span data-stu-id="517d1-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="517d1-151">Controleer of dat deze Hallo standaard Docker-host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="517d1-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="517d1-152">Open een opdrachtprompt en voer:</span><span class="sxs-lookup"><span data-stu-id="517d1-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="517d1-153">Als dit een fout retourneert, probeert toostart hello **Docker voor Windows** bureaublad-app.</span><span class="sxs-lookup"><span data-stu-id="517d1-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="517d1-154">Als Hallo bureaublad-app wordt uitgevoerd, klikt u vervolgens **Moby** moeten worden weergegeven in het systeemvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="517d1-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="517d1-155">Met de rechtermuisknop op **Moby** en open **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="517d1-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="517d1-156">Klik op **opnieuw**, en start vervolgens opnieuw Docker.</span><span class="sxs-lookup"><span data-stu-id="517d1-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="517d1-157">Een foutdialoogvenster treedt op tijdens een poging de tooadd Docker-ondersteuning of een ASP.NET Core-toepassing in een container voor foutopsporing (F5)</span><span class="sxs-lookup"><span data-stu-id="517d1-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="517d1-158">Na het verwijderen en installeren van extensies, raken Hallo beheerd uitbreidbaarheid Framework (MEF)-cache in Visual Studio beschadigd.</span><span class="sxs-lookup"><span data-stu-id="517d1-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="517d1-159">Wanneer dit gebeurt, kan leiden tot diverse foutberichten worden weergegeven wanneer u bent Docker-ondersteuning toe te voegen en/of toorun probeert of opsporen (F5) in uw toepassing ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="517d1-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="517d1-160">Gebruik als tijdelijke oplossing Hallo stappen toodelete en opnieuw genereren Hallo MEF cache te volgen.</span><span class="sxs-lookup"><span data-stu-id="517d1-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="517d1-161">Sluit alle exemplaren van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="517d1-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="517d1-162">Open % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="517d1-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="517d1-163">Hallo volgende mappen te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="517d1-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="517d1-164">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="517d1-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="517d1-165">Hallo scenario opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="517d1-165">Attempt hello scenario again.</span></span>
