---
title: Het oplossen van fouten van Docker-client op Windows met behulp van Visual Studio | Microsoft Docs
description: Problemen met het oplossen van problemen die kunnen optreden bij gebruik van Visual Studio maken en implementeren van web-apps op Docker in Windows met behulp van Visual Studio.
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
ms.openlocfilehash: 89fa04a1107b6abb49aefd68066443717ac9b731
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="0df90-103">Problemen met Visual Studio Docker-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="0df90-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="0df90-104">Wanneer u met Visual Studio Tools voor Docker Preview werkt, kunnen enkele problemen optreden vanwege de aard van de preview.</span><span class="sxs-lookup"><span data-stu-id="0df90-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of the nature of the preview.</span></span>
<span data-ttu-id="0df90-105">Hier volgen enkele veelvoorkomende problemen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="0df90-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="0df90-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="0df90-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="0df90-107">**Linux-containers**</span><span class="sxs-lookup"><span data-stu-id="0df90-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="0df90-108">Bouwen fouten optreden bij foutopsporing in een web- of console toepassing voor .NET Core</span><span class="sxs-lookup"><span data-stu-id="0df90-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="0df90-109">Dit kan zijn gerelateerd aan het station waar het project bevindt zich niet delen met Docker voor Windows.</span><span class="sxs-lookup"><span data-stu-id="0df90-109">This could be related to not sharing the drive where the project resides with Docker for Windows.</span></span>  <span data-ttu-id="0df90-110">Er wordt een fout als volgt:</span><span class="sxs-lookup"><span data-stu-id="0df90-110">You may receive an error like the following:</span></span>

```
The "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with the default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="0df90-111">Dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="0df90-111">To resolve this issue:</span></span>

1. <span data-ttu-id="0df90-112">Met de rechtermuisknop op **Docker voor Windows** in het systeemvak en selecteer vervolgens **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0df90-112">Right-click **Docker for Windows** in the notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="0df90-113">Selecteer **gedeelde stations** en delen van het station waarop het project zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="0df90-113">Select **Shared Drives** and share the drive where the project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="0df90-114">**Windows-containers**</span><span class="sxs-lookup"><span data-stu-id="0df90-114">**Windows containers**</span></span>

<span data-ttu-id="0df90-115">De volgende problemen zijn specifiek voor foutopsporing van .NET Framework-console en web toepassingen in Windows-containers.</span><span class="sxs-lookup"><span data-stu-id="0df90-115">The following issues are specific to debugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="0df90-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0df90-116">Prerequisites</span></span>

1. <span data-ttu-id="0df90-117">Visual Studio 2017 RC (of hoger) met de .NET Core en Docker Preview werkbelasting moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-117">Visual Studio 2017 RC (or later) with the .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="0df90-118">Patches van Windows 10 Verjaardag Update die aan de meest recente Windows Update.</span><span class="sxs-lookup"><span data-stu-id="0df90-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="0df90-119">Specifiek [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="0df90-120">[Docker voor Windows](https://docs.docker.com/docker-for-windows/) (1.13.0 bouwen of hoger) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="0df90-121">**Overschakelen naar de Windows-containers** moet worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-121">**Switch to Windows containers** must be selected.</span></span> <span data-ttu-id="0df90-122">Klik in het systeemvak op **Docker voor Windows**, en selecteer vervolgens **overschakelen naar de Windows-containers**.</span><span class="sxs-lookup"><span data-stu-id="0df90-122">In the notification area, click **Docker for Windows**, and then select **Switch to Windows containers**.</span></span> <span data-ttu-id="0df90-123">Nadat de computer opnieuw is opgestart, moet u ervoor zorgen dat deze instelling wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="0df90-123">After the machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="0df90-124">Console-uitvoer wordt niet weergegeven in het venster Visual Studio tijdens het opsporen van een consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="0df90-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="0df90-125">Dit is een bekend probleem met de foutopsporingsfunctie (msvsmon.exe), die momenteel niet is ontworpen voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="0df90-125">This is a known issue with the Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="0df90-126">Ondersteuning voor dit scenario kan worden opgenomen in een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="0df90-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="0df90-127">Als de uitvoer van de consoletoepassing in Visual Studio wilt weergeven, gebruikt **Docker: Start-Project**, hetgeen gelijk is aan **starten zonder foutopsporing**.</span><span class="sxs-lookup"><span data-stu-id="0df90-127">To see output from the console application in Visual Studio, use **Docker: Start Project**, which is equivalent to **Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-the-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="0df90-128">Webtoepassingen met de release-configuratie mislukt met fout voor (403) verboden foutopsporing</span><span class="sxs-lookup"><span data-stu-id="0df90-128">Debugging web applications with the release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="0df90-129">Om dit probleem omzeilen web.release.config openen in de oplossing en commentaar of verwijderen van de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="0df90-129">To work around this issue, open web.release.config in the solution and comment out or delete the following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="0df90-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0df90-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="0df90-131">**Linux-containers**</span><span class="sxs-lookup"><span data-stu-id="0df90-131">**Linux containers**</span></span>

#### <a name="unable-to-validate-volume-mapping"></a><span data-ttu-id="0df90-132">Kan toewijzing valideren</span><span class="sxs-lookup"><span data-stu-id="0df90-132">Unable to validate volume mapping</span></span>
<span data-ttu-id="0df90-133">Toewijzing is vereist voor het delen van de broncode en binaire bestanden van uw toepassing met de app-map in de container.</span><span class="sxs-lookup"><span data-stu-id="0df90-133">Volume mapping is required to share the source code and binaries of your application with the app folder in the container.</span></span>  <span data-ttu-id="0df90-134">Toewijzingen voor specifieke volume bevinden zich in een docker-compose.dev.debug.yml en docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="0df90-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="0df90-135">Als er bestanden zijn gewijzigd op de hostmachine, weerspiegelen de containers deze wijzigingen in een vergelijkbare mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="0df90-135">As files are changed on your host machine, the containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="0df90-136">Toewijzing inschakelen:</span><span class="sxs-lookup"><span data-stu-id="0df90-136">To enable volume mapping:</span></span>

1. <span data-ttu-id="0df90-137">Klik op **Moby** in het systeemvak en selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0df90-137">Click **Moby** in the notification area and select **Settings**.</span></span>
2. <span data-ttu-id="0df90-138">Selecteer **gedeelde schijven**.</span><span class="sxs-lookup"><span data-stu-id="0df90-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="0df90-139">Selecteer het station dat als host fungeert voor uw project en het station waar % USERPROFILE % zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="0df90-139">Select the drive that hosts your project and the drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="0df90-140">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="0df90-140">Click **Apply**.</span></span>

<span data-ttu-id="0df90-141">U kunt controleren of de toewijzing werkt, opnieuw en selecteer F5 uit vanuit Visual Studio nadat u een of meer stations hebt gedeeld, of voert u de volgende code vanaf een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="0df90-141">To test if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run the following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="0df90-142">In dit voorbeeld wordt ervan uitgegaan dat de map van uw gebruikers zich op station C bevindt en dat deze is gedeeld.</span><span class="sxs-lookup"><span data-stu-id="0df90-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="0df90-143">Wijzig zo nodig als u een ander station hebt gedeeld.</span><span class="sxs-lookup"><span data-stu-id="0df90-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="0df90-144">Voer de volgende code in de Linux-container.</span><span class="sxs-lookup"><span data-stu-id="0df90-144">Run the following code in the Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="0df90-145">U ziet een mappenlijst weergegeven in de map gebruikers/openbaar.</span><span class="sxs-lookup"><span data-stu-id="0df90-145">You should see a directory listing from the Users/Public folder.</span></span> <span data-ttu-id="0df90-146">Als er worden geen bestanden worden weergegeven en de map /c/Users/Public niet leeg is, wordt toewijzing is niet juist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="0df90-147">Ga naar de map wormhole om te zien van de inhoud van de `/c/Users/Public` directory:</span><span class="sxs-lookup"><span data-stu-id="0df90-147">Change to the wormhole directory to see the contents of the `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="0df90-148">Wanneer u met virtuele Linux-machines werkt, is de container-bestandssysteem is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="0df90-148">When you're working with Linux VMs, the container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="0df90-149">: 'PrepareForBuild' opbouwtaak is onverwacht mislukt</span><span class="sxs-lookup"><span data-stu-id="0df90-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="0df90-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Een fout opgetreden tijdens het verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="0df90-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying to connect.</span></span>

<span data-ttu-id="0df90-151">Controleren of de standaard Docker-host wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0df90-151">Verify that the default Docker host is running.</span></span> <span data-ttu-id="0df90-152">Open een opdrachtprompt en voer:</span><span class="sxs-lookup"><span data-stu-id="0df90-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="0df90-153">Als dit een fout retourneert, probeert te starten de **Docker voor Windows** bureaublad-app.</span><span class="sxs-lookup"><span data-stu-id="0df90-153">If this returns an error, then attempt to start the **Docker for Windows** desktop app.</span></span> <span data-ttu-id="0df90-154">Als de bureaublad-app wordt uitgevoerd, klikt u vervolgens **Moby** moeten worden weergegeven in het systeemvak.</span><span class="sxs-lookup"><span data-stu-id="0df90-154">If the desktop app is running, then **Moby** should be visible in the notification area.</span></span> <span data-ttu-id="0df90-155">Met de rechtermuisknop op **Moby** en open **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0df90-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="0df90-156">Klik op **opnieuw**, en start vervolgens opnieuw Docker.</span><span class="sxs-lookup"><span data-stu-id="0df90-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-to-add-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="0df90-157">Een dialoogvenster voor standaardfouten van deze gebeurtenis treedt op bij een poging tot Docker-ondersteuning toevoegen of een toepassing ASP.NET Core in een container voor foutopsporing (F5)</span><span class="sxs-lookup"><span data-stu-id="0df90-157">An error dialog occurs when attempting to add Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="0df90-158">Na het verwijderen en extensies installeert, kan de cache beheerd uitbreidbaarheid Framework (MEF) in Visual Studio beschadigd raken.</span><span class="sxs-lookup"><span data-stu-id="0df90-158">After uninstalling and installing extensions, the Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="0df90-159">Wanneer dit het geval is, kunnen er diverse foutberichten worden weergegeven wanneer u bent Docker-ondersteuning toe te voegen en/of probeert uit te voeren of opsporen (F5) in uw toepassing ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0df90-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting to run or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="0df90-160">Gebruik de volgende stappen uit om te verwijderen en opnieuw genereren van de cache MEF als tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="0df90-160">As a temporary workaround, use the following steps to delete and regenerate the MEF cache.</span></span>

1. <span data-ttu-id="0df90-161">Sluit alle exemplaren van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0df90-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="0df90-162">Open % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="0df90-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="0df90-163">Verwijder de volgende mappen:</span><span class="sxs-lookup"><span data-stu-id="0df90-163">Delete the following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="0df90-164">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0df90-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="0df90-165">Het scenario opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="0df90-165">Attempt the scenario again.</span></span>
