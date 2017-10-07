---
title: aaaContinuous leveringsmethode voor cloud services met TFS in Azure | Microsoft Docs
description: Meer informatie over hoe tooset up continue leveringsmethode voor Azure cloud-apps. Codevoorbeelden voor opdrachtregelprogramma MSBuild-instructies en PowerShell-scripts.
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="4f832-104">Continue leveringsmethode voor Cloudservices in Azure</span><span class="sxs-lookup"><span data-stu-id="4f832-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="4f832-105">Hallo proces dat wordt beschreven in dit artikel leest u hoe tooset up continue leveringsmethode voor Azure cloud-apps.</span><span class="sxs-lookup"><span data-stu-id="4f832-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="4f832-106">Dit proces kunt u automatisch pakketten maken en implementeren van Hallo pakket tooAzure na elke code incheckt.</span><span class="sxs-lookup"><span data-stu-id="4f832-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="4f832-107">Hallo pakket buildproces beschreven in dit artikel is gelijkwaardig toohello **pakket** opdracht in Visual Studio en de publicatie stappen zijn equivalent toohello **publiceren** opdracht in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f832-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="4f832-108">Hallo artikel behandelt Hallo methoden die u zou ook toocreate een installatieserver met opdrachtregelprogramma MSBuild-instructies en Windows PowerShell-scripts gebruiken laat zien hoe toooptionally Visual Studio Team Foundation Server - Team bouwen definities configureren toouse hello MSBuild-opdrachten en PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="4f832-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="4f832-109">Hallo-proces kan worden aangepast voor uw build-omgeving en de doel-Azure-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="4f832-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="4f832-110">U kunt ook Visual Studio Team Services, een versie van TFS die wordt gehost in Azure, toodo dit eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="4f832-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="4f832-111">Voordat u begint, moet u uw toepassing vanuit Visual Studio publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="4f832-112">Dit zorgt ervoor dat alle Hallo resources beschikbaar en geïnitialiseerd zijn wanneer u probeert tooautomate Hallo publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="4f832-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="4f832-113">1: Hallo bouwen Server configureren</span><span class="sxs-lookup"><span data-stu-id="4f832-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="4f832-114">Voordat u een Azure-pakket maken kunt met behulp van MSBuild, moet u Hallo vereiste software en hulpprogramma's installeren op Hallo build-server.</span><span class="sxs-lookup"><span data-stu-id="4f832-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="4f832-115">Visual Studio is niet vereist toobe op Hallo build-server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="4f832-116">Als u uw buildserver toouse Team Foundation bouwen Service toomanage wilt, volgt u de instructies Hallo in Hallo [Team Foundation bouwen Service] [ Team Foundation Build Service] documentatie.</span><span class="sxs-lookup"><span data-stu-id="4f832-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="4f832-117">Installeer op Hallo buildserver Hallo [.NET Framework 4.5.2][.NET Framework 4.5.2], waaronder MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4f832-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="4f832-118">Meest recente Hallo installeren [Authoring hulpprogramma's van Azure voor .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="4f832-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="4f832-119">Hallo installeren [Azure-bibliotheken voor .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="4f832-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="4f832-120">Hallo Microsoft.WebApplication.targets bestandskopie van een installatie van Visual Studio toohello bouwen server.</span><span class="sxs-lookup"><span data-stu-id="4f832-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="4f832-121">Op een computer met Visual Studio is geïnstalleerd, dit bestand bevindt zich in de directory Hallo C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="4f832-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="4f832-122">Kopieer deze toohello dezelfde directory op Hallo build-server.</span><span class="sxs-lookup"><span data-stu-id="4f832-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="4f832-123">Hallo installeren [Azure-Tools voor Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f832-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="4f832-124">2: een pakket met MSBuild-opdrachten maken</span><span class="sxs-lookup"><span data-stu-id="4f832-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="4f832-125">Deze sectie wordt beschreven hoe een MSBuild tooconstruct opdracht die wordt gemaakt van een Azure-pakket.</span><span class="sxs-lookup"><span data-stu-id="4f832-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="4f832-126">Deze stap uitvoeren op Hallo build server tooverify dat alles juist is geconfigureerd en dat Hallo MSBuild-opdracht is wat u wilt deze toodo.</span><span class="sxs-lookup"><span data-stu-id="4f832-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="4f832-127">U kunt deze opdrachtregel tooexisting bouwscripts op Hallo build-server of Hallo vanaf de opdrachtregel in een definitie TFS bouwen, kunt u ofwel toevoegen zoals beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4f832-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="4f832-128">Zie voor meer informatie over opdrachtregelparameters en MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f832-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="4f832-129">Als Visual Studio op Hallo build-server is geïnstalleerd, zoekt en kies **Visual Studio-opdrachtprompt** in Hallo **Visual Studio Tools** map in Windows.</span><span class="sxs-lookup"><span data-stu-id="4f832-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="4f832-130">Als Visual Studio op Hallo build-server niet is geïnstalleerd, open een opdrachtprompt en zorg ervoor dat MSBuild.exe toegankelijk is op het pad.</span><span class="sxs-lookup"><span data-stu-id="4f832-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="4f832-131">MSBuild is geïnstalleerd met hello .NET Framework in Hallo pad % WINDIR %\\Microsoft.NET\\Framework\\*versie*.</span><span class="sxs-lookup"><span data-stu-id="4f832-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="4f832-132">Bijvoorbeeld om toe te voegen MSBuild.exe toohello pad omgevingsvariabele wanneer u .NET Framework 4 geïnstalleerd hebt, typt u de volgende opdracht achter de opdrachtprompt Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="4f832-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="4f832-133">Ga bij de opdrachtprompt Hallo toohello map met het Azure-project-bestand dat u wilt dat toobuild.</span><span class="sxs-lookup"><span data-stu-id="4f832-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="4f832-134">MSBuild uitvoeren met Hallo/target: optie zoals in het volgende voorbeeld Hallo publiceren:</span><span class="sxs-lookup"><span data-stu-id="4f832-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="4f832-135">Deze optie kan worden afgekort tot /t: publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="4f832-136">Hallo /t:Publish optie in MSBuild moet niet verwarren met Hallo publiceren opdrachten die beschikbaar zijn in Visual Studio wanneer u hello die Azure SDK geïnstalleerd hebt.</span><span class="sxs-lookup"><span data-stu-id="4f832-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="4f832-137">Hallo /t: publicatieoptie alleen bij builds hello Azure pakketten.</span><span class="sxs-lookup"><span data-stu-id="4f832-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="4f832-138">Deze implementeert geen hello-pakketten zoals Hallo publiceren opdrachten in Visual Studio doet.</span><span class="sxs-lookup"><span data-stu-id="4f832-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="4f832-139">U kunt eventueel Hallo projectnaam opgeven als een MSBuild-parameter.</span><span class="sxs-lookup"><span data-stu-id="4f832-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="4f832-140">Als niet wordt opgegeven, wordt de huidige map Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4f832-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="4f832-141">Zie voor meer informatie over de opdrachtregelopties MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f832-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="4f832-142">Zoek Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f832-142">Locate hello output.</span></span> <span data-ttu-id="4f832-143">Met deze opdracht maakt standaard een map in de relatie toohello-hoofdmap voor Hallo-project, zoals *ProjectDir*\\bin\\*configuratie* \\ App.publish\\.</span><span class="sxs-lookup"><span data-stu-id="4f832-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="4f832-144">Wanneer u een Azure-project maakt, u twee bestanden: Hallo pakketbestand zelf en bijbehorende configuratiebestand Hallo genereren:</span><span class="sxs-lookup"><span data-stu-id="4f832-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="4f832-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="4f832-145">Project.cspkg</span></span>
   * <span data-ttu-id="4f832-146">Serviceconfiguration zijn. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="4f832-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="4f832-147">Standaard elke Azure-project bevat één serviceconfiguratiebestand (.cscfg-bestand) voor de lokale (foutopsporing) builds en een andere voor builds cloud (fasering of productie), maar u kunt toevoegen of verwijderen van service configuratiebestanden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="4f832-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="4f832-148">Wanneer u een pakket vanuit Visual Studio maakt, wordt u gevraagd welke service configuration file tooinclude naast Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="4f832-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="4f832-149">Hallo serviceconfiguratiebestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="4f832-149">Specify hello service configuration file.</span></span> <span data-ttu-id="4f832-150">Als u een pakket met behulp van MSBuild bouwen, is Hallo lokale service-configuratiebestand standaard.</span><span class="sxs-lookup"><span data-stu-id="4f832-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="4f832-151">tooinclude een andere service-configuratiebestand, stel de eigenschap TargetProfile van Hallo MSBuild-opdracht, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="4f832-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="4f832-152">Geef de locatie Hallo voor Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f832-152">Specify hello location for hello output.</span></span> <span data-ttu-id="4f832-153">Hallo pad instellen met behulp van de /p:PublishDir =*Directory* \\ optie, met inbegrip van Hallo afsluitende backslash scheidingsteken, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="4f832-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="4f832-154">Nadat u hebt gemaakt en getest een juiste MSBuild command line toobuild projecten en ze combineren in een Azure-pakket, kunt u deze opdrachtregel tooyour build scripts toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f832-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="4f832-155">Als uw buildserver gebruikmaakt van aangepaste scripts, wordt dit proces afhankelijk van de details van uw aangepaste buildproces.</span><span class="sxs-lookup"><span data-stu-id="4f832-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="4f832-156">Als u TFS gebruikt als een build-omgeving, kunt u Hallo-instructies in Hallo volgende stap tooadd hello Azure-pakket build tooyour buildproces volgen.</span><span class="sxs-lookup"><span data-stu-id="4f832-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="4f832-157">3: bouwen van een pakket met TFS-Team maken</span><span class="sxs-lookup"><span data-stu-id="4f832-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="4f832-158">Als u hebt Team Foundation Server (TFS) instellen terwijl een controller bouwen en Hallo server maakt die zijn ingesteld als een TFS-build-machine en u kunt desgewenst een geautomatiseerde build instellen voor uw Azure-pakket op.</span><span class="sxs-lookup"><span data-stu-id="4f832-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="4f832-159">Voor informatie over hoe tooset up en Team Foundation server gebruiken als een build-systeem zien [Scale-out uw build-systeem][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="4f832-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="4f832-160">Met name de volgende procedure wordt ervan uitgegaan dat u uw buildserver hebt geconfigureerd zoals beschreven in [implementeren en configureren van een buildserver][Deploy and configure a build server], en dat u hebt gemaakt dat een teamproject gemaakt een cloud Service-project in Hallo teamproject.</span><span class="sxs-lookup"><span data-stu-id="4f832-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="4f832-161">tooconfigure TFS toobuild Azure-pakketten voeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4f832-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="4f832-162">Kies in Visual Studio op uw ontwikkelcomputer in menu Beeld Hallo **Team Explorer**, of kies Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="4f832-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="4f832-163">Vouw in het venster Team Explorer Hallo **Builds** knooppunt of kies Hallo **Builds** pagina en kies **nieuwe bouwen definitie**.</span><span class="sxs-lookup"><span data-stu-id="4f832-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Nieuwe bouwen definitie-optie][0]
2. <span data-ttu-id="4f832-165">Kies Hallo **Trigger** tabblad en geef Hallo gewenst voorwaarden voor als u wilt dat Hallo pakket toobe gebouwd.</span><span class="sxs-lookup"><span data-stu-id="4f832-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="4f832-166">Geef bijvoorbeeld **continue integratie** toobuild Hallo pakket wanneer een bron beheren inchecken optreedt.</span><span class="sxs-lookup"><span data-stu-id="4f832-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="4f832-167">Kies Hallo **broninstellingen** tabblad en zorg ervoor dat de projectmap wordt vermeld in Hallo **bronmap van het besturingselement** kolom en Hallo status **Active**.</span><span class="sxs-lookup"><span data-stu-id="4f832-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="4f832-168">Kies Hallo **bouwen standaard** tabblad en controleer onder Build-controller Hallo-naam van Hallo build-server.</span><span class="sxs-lookup"><span data-stu-id="4f832-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="4f832-169">Hallo ook optie **kopie build uitvoer toohello volgende doelmap** Hallo gewenst neerzetten locatie op te geven.</span><span class="sxs-lookup"><span data-stu-id="4f832-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="4f832-170">Kies Hallo **proces** tabblad. Kies op Hallo proces tabblad Hallo standaardsjabloon onder **bouwen**, Hallo project kiezen als deze nog niet is geselecteerd, en vouw Hallo **Geavanceerd** sectie in Hallo **bouwen**sectie Hallo raster.</span><span class="sxs-lookup"><span data-stu-id="4f832-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="4f832-171">Kies **MSBuild-argumenten**, en Hallo juiste MSBuild opdrachtregelargumenten ingesteld zoals beschreven in stap 2 hierboven.</span><span class="sxs-lookup"><span data-stu-id="4f832-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="4f832-172">Voer bijvoorbeeld **/t: publiceren /p:PublishDir =\\\\MijnServer\\zakt\\**  toobuild een pakket en kopieer Hallo pakket bestanden toohello locatie \\ \\MijnServer\\zakt\\:</span><span class="sxs-lookup"><span data-stu-id="4f832-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![MSBuild-argumenten][2]

   > [!NOTE]
   > <span data-ttu-id="4f832-174">Openbare share kopiëren Hallo bestanden tooa maakt het eenvoudiger toomanually implementeren hello-pakketten uit uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="4f832-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="4f832-175">Hallo succes van uw build-stap door te controleren in een wijziging tooyour project testen of een nieuwe build in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="4f832-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="4f832-176">tooqueue van een nieuwe build, in de Explorer-Team met de rechtermuisknop op **alle bouwen definities** en kies vervolgens **wachtrij nieuwe bouwen**.</span><span class="sxs-lookup"><span data-stu-id="4f832-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="4f832-177">4: een pakket met een PowerShell-Script publiceren</span><span class="sxs-lookup"><span data-stu-id="4f832-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="4f832-178">Deze sectie wordt beschreven hoe Windows PowerShell-script die Hallo Cloud-app-pakket publiceert tooconstruct tooAzure met optionele parameters uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f832-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="4f832-179">Dit script kan worden aangeroepen na Hallo build stap in uw aangepaste build automation.</span><span class="sxs-lookup"><span data-stu-id="4f832-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="4f832-180">Het kan ook worden aangeroepen vanuit de werkstroomactiviteiten processjabloon in Visual Studio TFS Team bouwen.</span><span class="sxs-lookup"><span data-stu-id="4f832-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="4f832-181">Hallo installeren [Azure PowerShell-cmdlets] [ Azure PowerShell cmdlets] (v0.6.1 of hoger).</span><span class="sxs-lookup"><span data-stu-id="4f832-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="4f832-182">Tijdens de installatiefase Hallo-cmdlet, kiest u tooinstall als een module.</span><span class="sxs-lookup"><span data-stu-id="4f832-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="4f832-183">Houd er rekening mee dat deze officieel ondersteunde versie Hallo oudere versie die worden aangeboden via CodePlex, vervangt Hoewel Hallo eerdere versies werden 2.x.x genummerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="4f832-184">Azure PowerShell Hallo startmenu of startpagina starten.</span><span class="sxs-lookup"><span data-stu-id="4f832-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="4f832-185">Als u op deze manier wordt gestart, worden hello Azure PowerShell-cmdlets geladen.</span><span class="sxs-lookup"><span data-stu-id="4f832-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="4f832-186">Controleren of Hallo PowerShell-cmdlets zijn geladen met Hallo gedeeltelijke opdracht bij de PowerShell-prompt Hallo `Get-Azure` en drukt u vervolgens op Tab-toets voor voltooiing van instructie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4f832-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="4f832-187">Als u herhaaldelijk op Hallo Tab-toets drukt, ziet u diverse Azure PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4f832-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="4f832-188">Controleer of u verbinding tooyour Azure-abonnement maken kunt via uw abonnementsgegevens van Hallo .publishsettings-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="4f832-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="4f832-189">Voer de opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="4f832-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="4f832-190">Dit toont informatie over uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4f832-190">This shows information about your subscription.</span></span> <span data-ttu-id="4f832-191">Controleer of alles juist is.</span><span class="sxs-lookup"><span data-stu-id="4f832-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="4f832-192">Hallo script sjabloon tijdens het Hallo-einde van dit artikel naar uw scriptmap als c: opgegeven opslaan\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="4f832-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="4f832-193">Raadpleeg Hallo parameters sectie Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="4f832-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="4f832-194">Toevoegen of wijzigen van de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="4f832-194">Add or modify any default values.</span></span> <span data-ttu-id="4f832-195">Deze waarden kunnen altijd worden genegeerd door door te geven in expliciete parameters.</span><span class="sxs-lookup"><span data-stu-id="4f832-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="4f832-196">Zorg ervoor dat er geldige cloudservice en storage-accounts die zijn gemaakt in uw abonnement die kan worden geselecteerd door de Hallo script publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="4f832-197">Het opslagaccount (blobopslag) wordt gebruikt tooupload en tijdelijk Hallo-implementatie van pakket en config-bestand op te slaan tijdens de implementatie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4f832-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="4f832-198">een nieuwe cloudservice toocreate, kunt u dit script of gebruik Hallo aanroepen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f832-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f832-199">Hallo cloudservicenaam wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="4f832-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="4f832-200">een nieuw opslagaccount toocreate, kunt u dit script of gebruik Hallo aanroepen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f832-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f832-201">Hallo opslagaccountnaam wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="4f832-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="4f832-202">U kunt proberen Hallo dezelfde naam als de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4f832-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="4f832-203">Hallo script aanroepen rechtstreeks vanuit Azure PowerShell, of op wire om dit script tooyour host build automation toooccur na Hallo pakket build.</span><span class="sxs-lookup"><span data-stu-id="4f832-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4f832-204">Hallo-script wordt altijd verwijderen of uw bestaande implementaties vervangen standaard als ze worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="4f832-205">Dit is nodig om in te schakelen continue van automatisering geen gebruiker wordt gevraagd wanneer mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="4f832-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="4f832-206">**Voorbeeldscenario 1:** continue implementatie toohello staging-omgeving van een service:</span><span class="sxs-lookup"><span data-stu-id="4f832-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="4f832-207">Dit is doorgaans opgevolgd door testuitvoering verificatie en geen VIP's wisselen.</span><span class="sxs-lookup"><span data-stu-id="4f832-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="4f832-208">Hallo VIP wisselen kan worden uitgevoerd via Hallo [Azure-portal](https://portal.azure.com) of met behulp van de cmdlet Hallo Move-implementatie.</span><span class="sxs-lookup"><span data-stu-id="4f832-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="4f832-209">**Voorbeeldscenario 2:** continue implementatie toohello productie-omgeving van een speciale test-service</span><span class="sxs-lookup"><span data-stu-id="4f832-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="4f832-210">**Extern bureaublad:**</span><span class="sxs-lookup"><span data-stu-id="4f832-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="4f832-211">U moet tooperform extra eenmalige stappen tooensure Hallo die juiste Cloud Service-certificaat is geüpload tooall cloudservices gericht door dit script als extern bureaublad is ingeschakeld in uw Azure-project.</span><span class="sxs-lookup"><span data-stu-id="4f832-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="4f832-212">Zoek Hallo certificaat vingerafdruk waarden door uw rollen wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="4f832-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="4f832-213">De vingerafdruk-waarden zijn niet zichtbaar in Hallo certificaten sectie van het configuratiebestand van de cloud (dat wil zeggen ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="4f832-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="4f832-214">Het is ook zichtbaar in de configuratie voor extern bureaublad-dialoogvenster Hallo in Visual Studio wanneer u opties weergeven en bekijkt hello certificaat geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="4f832-215">Extern bureaublad-certificaten als een eenmalige instellingsstap met behulp van de volgende cmdlet script Hallo uploaden:</span><span class="sxs-lookup"><span data-stu-id="4f832-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="4f832-216">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4f832-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="4f832-217">Ook kunt u Hallo bestand PFX-certificaat met persoonlijke sleutel en het uploaden van certificaten tooeach doel cloud service exporteren de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f832-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="4f832-218">**Upgraden versus van de implementatie. Verwijderen van implementatie -\> nieuwe implementatie**</span><span class="sxs-lookup"><span data-stu-id="4f832-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="4f832-219">Hallo-script wordt standaard uitvoeren een Upgrade-implementatie ($enableDeploymentUpgrade = 1) als er is geen parameter is doorgegeven, of de waarde 1 expliciet wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="4f832-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="4f832-220">Dit heeft het voordeel van het minder tijd nodig dan een volledige implementatie voor enkele exemplaren.</span><span class="sxs-lookup"><span data-stu-id="4f832-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="4f832-221">Voor exemplaren waarvoor hoge beschikbaarheid die dit ook Hallo profiteren heeft van het verlaten van sommige gevallen terwijl anderen kunnen worden bijgewerkt (roulatie van uw updatedomein), plus de VIP wordt niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4f832-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="4f832-222">Upgrade-implementatie kan worden uitgeschakeld in het Hallo-script ($enableDeploymentUpgrade = 0) of door het doorgeven van *- enableDeploymentUpgrade 0* als een parameter die wordt gewijzigd van het script gedrag toofirst verwijderen alle bestaande implementatie en maak vervolgens een nieuwe implementatie.</span><span class="sxs-lookup"><span data-stu-id="4f832-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4f832-223">Hallo-script wordt altijd verwijderen of uw bestaande implementaties vervangen standaard als ze worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="4f832-224">Dit is nodig om in te schakelen continue van automatisering wanneer er geen gebruiker/operator vragen mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="4f832-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="4f832-225">5: een pakket met behulp van TFS-Team bouwen publiceren</span><span class="sxs-lookup"><span data-stu-id="4f832-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="4f832-226">Deze optionele stap maakt u verbinding maken van TFS-Team toohello script gemaakt in stap 4, die worden gepubliceerd Hallo pakket build tooAzure verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4f832-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="4f832-227">Dit houdt in dat wijzigen Hallo processjabloon gebruikt door de definitie van de build zodat deze wordt uitgevoerd een activiteit publiceren achter Hallo Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="4f832-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="4f832-228">Hallo publiceren activiteit kan uw PowerShell-opdracht wordt doorgegeven in parameters van Hallo-versie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4f832-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="4f832-229">Uitvoer van Hallo MSBuild-doelen en publiceren van script zal worden doorgesluisd naar Hallo standaard builduitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f832-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="4f832-230">Hallo definitie bouwen die verantwoordelijk is voor bewerken continue implementeren.</span><span class="sxs-lookup"><span data-stu-id="4f832-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="4f832-231">Selecteer Hallo **proces** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4f832-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="4f832-232">Ga als volgt [deze instructies](http://msdn.microsoft.com/library/dd647551.aspx) tooadd een activiteit-project voor Hallo processjabloon bouwen, Hallo standaardsjabloon downloaden, toe te voegen aan het Hallo-project en incheckt.</span><span class="sxs-lookup"><span data-stu-id="4f832-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="4f832-233">Hallo build processjabloon een nieuwe naam, zoals AzureBuildProcessTemplate opgeven.</span><span class="sxs-lookup"><span data-stu-id="4f832-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="4f832-234">Retourneren van toohello **proces** tabblad en gebruik **Details weergeven** tooshow een lijst met beschikbare build processjablonen.</span><span class="sxs-lookup"><span data-stu-id="4f832-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="4f832-235">Kies Hallo **nieuw...**  knop en navigeer toohello project u zojuist hebt toegevoegd en ingecheckt.</span><span class="sxs-lookup"><span data-stu-id="4f832-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="4f832-236">Zoek Hallo-sjabloon die u zojuist hebt gemaakt en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f832-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="4f832-237">Open Hallo geselecteerd processjabloon voor bewerking.</span><span class="sxs-lookup"><span data-stu-id="4f832-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="4f832-238">U kunt rechtstreeks in de werkstroomontwerper Hallo of in Hallo XML-editor toowork Hello XAML openen.</span><span class="sxs-lookup"><span data-stu-id="4f832-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="4f832-239">Lijst met nieuwe argumenten volgen als afzonderlijke regels op Hallo argumenten tabblad van de werkstroomontwerper Hallo Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f832-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="4f832-240">Alle argumenten moet richting = In en typ = tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4f832-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="4f832-241">Deze worden gebruikt tooflow parameters van Hallo build definitie in de werkstroom hello, welke vervolgens get gebruikte toocall Hallo script publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lijst met argumenten][3]

   <span data-ttu-id="4f832-243">Hallo die bijbehorende XAML uitziet:</span><span class="sxs-lookup"><span data-stu-id="4f832-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="4f832-244">Een nieuwe reeks toevoegen aan Hallo einde van de Agent worden uitgevoerd op:</span><span class="sxs-lookup"><span data-stu-id="4f832-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="4f832-245">Gestart door een If-instructie activiteit toocheck voor een geldige scriptbestand toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="4f832-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="4f832-246">Hallo voorwaarde toothis waarde instellen:</span><span class="sxs-lookup"><span data-stu-id="4f832-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="4f832-247">Hallo vervolgens geval Hallo If-instructie, Voeg een nieuwe Sequence-activiteit.</span><span class="sxs-lookup"><span data-stu-id="4f832-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="4f832-248">Set Hallo weergegeven naam too'Start publiceren '</span><span class="sxs-lookup"><span data-stu-id="4f832-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="4f832-249">De volgende lijst met nieuwe variabelen Hallo Start publiceren reeks nog steeds is geselecteerd, toevoegen als afzonderlijke regels in het tabblad variabelen van Hallo workflow designer.</span><span class="sxs-lookup"><span data-stu-id="4f832-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="4f832-250">Alle variabelen moet type variabele = tekenreeks en bereik = Start publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="4f832-251">Deze worden gebruikt tooflow parameters van Hallo build definitie in de werkstroom, welke vervolgens get gebruikte toocall Hallo script publiceren.</span><span class="sxs-lookup"><span data-stu-id="4f832-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="4f832-252">SubscriptionDataFilePath van het type tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4f832-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="4f832-253">PublishScriptFilePath van het type tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4f832-253">PublishScriptFilePath, of type String</span></span>

        ![Nieuwe variabelen][4]
   4. <span data-ttu-id="4f832-255">Als u met behulp van TFS 2012 of eerder een ConvertWorkspaceItem-activiteit aan begin van Hallo toevoegen Hallo nieuwe tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4f832-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="4f832-256">Als u TFS 2013 of later gebruikt, voegt u een activiteit GetLocalPath aan begin van de nieuwe tekenreeks Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4f832-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="4f832-257">Voor een ConvertWorkspaceItem Hallo eigenschappen als volgt instellen: richting = ServerToLocal, DisplayName = 'Converteren publiceren script filename', invoer PublishScriptLocation, resultaat = = PublishScriptFilePath, werkruimte = 'Werkruimte'.</span><span class="sxs-lookup"><span data-stu-id="4f832-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="4f832-258">Voor een activiteit GetLocalPath ingesteld Hallo eigenschap IncomingPath too'PublishScriptLocation', en het resultaat too'PublishScriptFilePath Hallo ".</span><span class="sxs-lookup"><span data-stu-id="4f832-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="4f832-259">Deze activiteit kunnen worden geconverteerd Hallo pad toohello publiceren script vanaf locaties voor TFS-server (indien van toepassing) tooa schijfpad met lokale.</span><span class="sxs-lookup"><span data-stu-id="4f832-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="4f832-260">Als u met behulp van TFS 2012 of ouder, een andere ConvertWorkspaceItem activiteit aan Hallo einde van toevoegen Hallo nieuwe tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4f832-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="4f832-261">Richting = ServerToLocal, DisplayName = 'Converteren abonnement filename', invoer = SubscriptionDataFileLocation, resultaat = SubscriptionDataFilePath, werkruimte = 'Werkruimte'.</span><span class="sxs-lookup"><span data-stu-id="4f832-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="4f832-262">Als u TFS 2013 of later gebruikt, voegt u een andere GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="4f832-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="4f832-263">IncomingPath = 'SubscriptionDataFileLocation' en resultaat = 'SubscriptionDataFilePath'.</span><span class="sxs-lookup"><span data-stu-id="4f832-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="4f832-264">Een activiteit InvokeProcess toevoegen aan einde Hallo Hallo nieuwe tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4f832-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="4f832-265">Deze activiteit oproepen PowerShell.exe met Hallo argumenten doorgegeven door Hallo definitie bouwen.</span><span class="sxs-lookup"><span data-stu-id="4f832-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="4f832-266">Argumenten String.Format = ('-'' {0}' ' - serviceName {1} - storageAccountName {2} - packageLocation '' {3}' ' - cloudConfigLocation '' {4}' ' - subscriptionDataFile '' {5}' ' - selectedSubscription {6} bestand-omgeving '' {7}' ' ",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, SubscriptionName, omgeving)</span><span class="sxs-lookup"><span data-stu-id="4f832-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="4f832-267">DisplayName = Execute script publiceren</span><span class="sxs-lookup"><span data-stu-id="4f832-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="4f832-268">FileName = 'PowerShell' (inclusief Hallo aanhalingstekens)</span><span class="sxs-lookup"><span data-stu-id="4f832-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="4f832-269">OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =</span><span class="sxs-lookup"><span data-stu-id="4f832-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="4f832-270">In Hallo **standaarduitvoer verwerken** sectie textbox van de InvokeProcess, stelt u Hallo textbox waarde too'data'.</span><span class="sxs-lookup"><span data-stu-id="4f832-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="4f832-271">Dit is een variabele toostore Hallo standaarduitvoer.</span><span class="sxs-lookup"><span data-stu-id="4f832-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="4f832-272">Toevoegen van een activiteit WriteBuildMessage onder Hallo **standaarduitvoer verwerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="4f832-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="4f832-273">Hallo belang ingesteld = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' en het Hallo-bericht = 'data'.</span><span class="sxs-lookup"><span data-stu-id="4f832-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="4f832-274">Dit zorgt ervoor Hallo standaarduitvoer van het script ophalen toohello builduitvoer wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="4f832-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="4f832-275">In Hallo **foutuitvoer verwerken** sectie textbox van de InvokeProcess, stelt u Hallo textbox waarde too'data'.</span><span class="sxs-lookup"><span data-stu-id="4f832-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="4f832-276">Dit is een variabele toostore Hallo standaardfout gegevens.</span><span class="sxs-lookup"><span data-stu-id="4f832-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="4f832-277">Toevoegen van een activiteit WriteBuildError onder Hallo **foutuitvoer verwerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="4f832-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="4f832-278">Hallo-bericht instellen = 'data'.</span><span class="sxs-lookup"><span data-stu-id="4f832-278">Set hello Message='data'.</span></span> <span data-ttu-id="4f832-279">Dit zorgt ervoor Hallo standaardfouten van Hallo script toohello fout builduitvoer ophalen geschreven.</span><span class="sxs-lookup"><span data-stu-id="4f832-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="4f832-280">Corrigeer eventuele fouten, aangegeven door blauw uitroepteken aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="4f832-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="4f832-281">Beweeg de muisaanwijzer over de tooget uitroepteken markeert een aanwijzing over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="4f832-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="4f832-282">Hallo workflow om te wissen fouten niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="4f832-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="4f832-283">eindresultaat Hallo Hallo publiceren workflow-activiteiten in de ontwerpfunctie Hallo er als volgt:</span><span class="sxs-lookup"><span data-stu-id="4f832-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Workflow-activiteiten][5]

   <span data-ttu-id="4f832-285">eindresultaat Hallo Hallo publiceren workflow-activiteiten in XAML er als volgt:</span><span class="sxs-lookup"><span data-stu-id="4f832-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="4f832-286">Hallo build proces sjabloon werkstroom en controleer In dit bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="4f832-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="4f832-287">Bewerk Hallo build-definitie (sluit als het al geopend is), en selecteer Hallo **nieuw** knop als u nog niet Hallo nieuwe sjabloon in de lijst Hallo van processjablonen ziet.</span><span class="sxs-lookup"><span data-stu-id="4f832-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="4f832-288">Hallo eigenschap parameterwaarden in Hallo div sectie als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="4f832-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="4f832-289">CloudConfigLocation ='c:\\zakt\\app.publish\\ServiceConfiguration.Cloud.cscfg' *deze waarde is afgeleid van: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="4f832-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="4f832-290">PackageLocation = ' c:\\zakt\\app.publish\\ContactManager.Azure.cspkg' *deze waarde is afgeleid van: ($PublishDir)($ProjectName) .cspkg*</span><span class="sxs-lookup"><span data-stu-id="4f832-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="4f832-291">PublishScriptLocation = ' c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="4f832-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="4f832-292">ServiceName = 'mycloudservicename' *gebruik Hallo juiste cloudservicenaam hier*</span><span class="sxs-lookup"><span data-stu-id="4f832-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="4f832-293">Omgeving = 'Fasering'</span><span class="sxs-lookup"><span data-stu-id="4f832-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="4f832-294">StorageAccountName = 'mystorageaccountname' *gebruik Hallo juiste opslagaccountnaam hier*</span><span class="sxs-lookup"><span data-stu-id="4f832-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="4f832-295">SubscriptionDataFileLocation = ' c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="4f832-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="4f832-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="4f832-296">SubscriptionName = 'default'</span></span>

    ![Eigenschap parameterwaarden][6]
11. <span data-ttu-id="4f832-298">Hallo wijzigingen toohello bouwen definitie opslaan.</span><span class="sxs-lookup"><span data-stu-id="4f832-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="4f832-299">Een Build tooexecute beide Hallo pakket build en publiceren van de verzendwachtrij.</span><span class="sxs-lookup"><span data-stu-id="4f832-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="4f832-300">Als u een trigger tooContinuous integratie ingesteld, kunt u dit gedrag wordt uitgevoerd bij elke controle.</span><span class="sxs-lookup"><span data-stu-id="4f832-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="4f832-301">PublishCloudService.ps1 script sjabloon</span><span class="sxs-lookup"><span data-stu-id="4f832-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="4f832-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f832-302">Next steps</span></span>
<span data-ttu-id="4f832-303">Zie tooenable foutopsporing op afstand bij gebruik van doorlopende levering [foutopsporing op afstand inschakelen wanneer u doorlopende levering toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="4f832-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
