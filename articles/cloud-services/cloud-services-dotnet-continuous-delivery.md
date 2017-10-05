---
title: Continue leveringsmethode voor cloud services met TFS in Azure | Microsoft Docs
description: Informatie over het instellen van continue leveringsmethode voor Azure cloud-apps. Codevoorbeelden voor opdrachtregelprogramma MSBuild-instructies en PowerShell-scripts.
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="16d99-104">Continue leveringsmethode voor Cloudservices in Azure</span><span class="sxs-lookup"><span data-stu-id="16d99-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="16d99-105">De procedure beschreven in dit artikel wordt beschreven hoe u voor het instellen van continue leveringsmethode voor Azure cloud-apps.</span><span class="sxs-lookup"><span data-stu-id="16d99-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="16d99-106">Met dit proces kunt u automatisch pakketten maken en het pakket implementeren op Azure nadat de afzonderlijke code is ingecheckt.</span><span class="sxs-lookup"><span data-stu-id="16d99-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="16d99-107">Het pakket buildproces beschreven in dit artikel is gelijk aan de **pakket** opdracht in Visual Studio en de publicatie stappen gelijk zijn aan de **publiceren** opdracht in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16d99-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="16d99-108">Het artikel bevat informatie over de methoden die u gebruiken wilt voor het maken van een installatieserver opdrachtregelprogramma MSBuild-instructies en Windows PowerShell-scripts en ook laat zien hoe Configureer desgewenst Visual Studio Team Foundation Server - definities Team maken gebruik van de MSBuild-opdrachten en PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="16d99-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="16d99-109">Het proces kan worden aangepast voor uw build-omgeving en de doel-Azure-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="16d99-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="16d99-110">U kunt ook Visual Studio Team Services, een versie van TFS die wordt gehost in Azure, eenvoudiger hiervoor gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16d99-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="16d99-111">Voordat u begint, moet u uw toepassing vanuit Visual Studio publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="16d99-112">Dit zorgt ervoor dat alle resources beschikbaar en geïnitialiseerd zijn wanneer u probeert om de publicatieproces te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="16d99-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="16d99-113">1: de Buildserver configureren</span><span class="sxs-lookup"><span data-stu-id="16d99-113">1: Configure the Build Server</span></span>
<span data-ttu-id="16d99-114">Voordat u een Azure-pakket maken kunt met behulp van MSBuild, moet u de vereiste software en hulpprogramma's installeren op de buildserver.</span><span class="sxs-lookup"><span data-stu-id="16d99-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="16d99-115">Visual Studio is niet vereist om te worden geïnstalleerd op de buildserver.</span><span class="sxs-lookup"><span data-stu-id="16d99-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="16d99-116">Als u gebruiken van Team Foundation bouwen Service wilt voor het beheren van uw buildserver, volg de instructies in de [Team Foundation bouwen Service] [ Team Foundation Build Service] documentatie.</span><span class="sxs-lookup"><span data-stu-id="16d99-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="16d99-117">Installeer op de buildserver de [.NET Framework 4.5.2][.NET Framework 4.5.2], waaronder MSBuild.</span><span class="sxs-lookup"><span data-stu-id="16d99-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="16d99-118">Installeer de meest recente [Authoring hulpprogramma's van Azure voor .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="16d99-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="16d99-119">Installeer de [Azure-bibliotheken voor .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="16d99-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="16d99-120">Kopieer het bestand Microsoft.WebApplication.targets van een installatie voor Visual Studio met de buildserver.</span><span class="sxs-lookup"><span data-stu-id="16d99-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="16d99-121">Op een computer met Visual Studio is geïnstalleerd, wordt dit bestand zich in de map C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="16d99-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="16d99-122">Kopieer deze naar dezelfde map op de buildserver.</span><span class="sxs-lookup"><span data-stu-id="16d99-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="16d99-123">Installeer de [Azure-hulpprogramma's voor Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="16d99-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="16d99-124">2: een pakket met MSBuild-opdrachten maken</span><span class="sxs-lookup"><span data-stu-id="16d99-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="16d99-125">Deze sectie beschrijft het maken van een MSBuild-opdracht die wordt gemaakt van een Azure-pakket.</span><span class="sxs-lookup"><span data-stu-id="16d99-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="16d99-126">Deze stap uitvoeren op de server maken om te controleren of alles correct is geconfigureerd en dat de MSBuild-opdracht biedt u de gewenste te doen.</span><span class="sxs-lookup"><span data-stu-id="16d99-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="16d99-127">U kunt met deze opdrachtregel voor installatie zonder toezicht toevoegen aan bestaande build scripts op de buildserver of kunt u de opdrachtregel in een definitie TFS bouwen, zoals beschreven in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="16d99-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="16d99-128">Zie voor meer informatie over opdrachtregelparameters en MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="16d99-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="16d99-129">Als Visual Studio is geïnstalleerd op de buildserver, zoekt en kies **Visual Studio-opdrachtprompt** in de **Visual Studio Tools** map in Windows.</span><span class="sxs-lookup"><span data-stu-id="16d99-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="16d99-130">Als Visual Studio niet is geïnstalleerd op de buildserver, open een opdrachtprompt en zorg ervoor dat MSBuild.exe toegankelijk is op het pad.</span><span class="sxs-lookup"><span data-stu-id="16d99-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="16d99-131">MSBuild is geïnstalleerd met de .NET Framework in het pad % WINDIR %\\Microsoft.NET\\Framework\\*versie*.</span><span class="sxs-lookup"><span data-stu-id="16d99-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="16d99-132">Bijvoorbeeld als u wilt toevoegen aan de omgevingsvariabele PATH MSBuild.exe wanneer u .NET Framework 4 geïnstalleerd hebt, typt u de volgende opdracht achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="16d99-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="16d99-133">Navigeer naar de map met het Azure-project-bestand dat u wilt maken bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="16d99-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="16d99-134">MSBuild uitvoeren met de/target: publicatieoptie zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="16d99-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="16d99-135">Deze optie kan worden afgekort tot /t: publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="16d99-136">De optie /t:Publish in MSBuild Verwar niet met de opdrachten publiceren in Visual Studio beschikbaar wanneer u de Azure-SDK geïnstalleerd hebt.</span><span class="sxs-lookup"><span data-stu-id="16d99-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="16d99-137">De /t: optie alleen builds publiceren de Azure-pakketten.</span><span class="sxs-lookup"><span data-stu-id="16d99-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="16d99-138">Dit biedt de pakketten niet implementeren als de opdrachten publiceren in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16d99-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="16d99-139">U kunt eventueel de projectnaam opgeven als een MSBuild-parameter.</span><span class="sxs-lookup"><span data-stu-id="16d99-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="16d99-140">Als niet wordt opgegeven, wordt de huidige map gebruikt.</span><span class="sxs-lookup"><span data-stu-id="16d99-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="16d99-141">Zie voor meer informatie over de opdrachtregelopties MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="16d99-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="16d99-142">Zoek de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d99-142">Locate the output.</span></span> <span data-ttu-id="16d99-143">Met deze opdracht maakt standaard een map ten opzichte van de hoofdmap voor het project, zoals *ProjectDir*\\bin\\*configuratie*\\app.publish \\.</span><span class="sxs-lookup"><span data-stu-id="16d99-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="16d99-144">Wanneer u een Azure-project maakt, genereert u twee bestanden: het pakketbestand zelf en het bijbehorende configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="16d99-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="16d99-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="16d99-145">Project.cspkg</span></span>
   * <span data-ttu-id="16d99-146">Serviceconfiguration zijn. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="16d99-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="16d99-147">Standaard elke Azure-project bevat één serviceconfiguratiebestand (.cscfg-bestand) voor de lokale (foutopsporing) builds en een andere voor builds cloud (fasering of productie), maar u kunt toevoegen of verwijderen van service configuratiebestanden zo nodig.</span><span class="sxs-lookup"><span data-stu-id="16d99-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="16d99-148">Wanneer u een pakket vanuit Visual Studio maakt, wordt u gevraagd welke serviceconfiguratiebestand om op te nemen samen met het pakket.</span><span class="sxs-lookup"><span data-stu-id="16d99-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="16d99-149">Geef het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="16d99-149">Specify the service configuration file.</span></span> <span data-ttu-id="16d99-150">Als u een pakket met behulp van MSBuild bouwen, wordt het configuratiebestand van de lokale service standaard opgenomen.</span><span class="sxs-lookup"><span data-stu-id="16d99-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="16d99-151">Als u wilt opnemen in een andere service-configuratiebestand, stelt u de eigenschap TargetProfile de MSBuild-opdracht:</span><span class="sxs-lookup"><span data-stu-id="16d99-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="16d99-152">Geef de locatie voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d99-152">Specify the location for the output.</span></span> <span data-ttu-id="16d99-153">Het pad worden ingesteld met behulp van de /p:PublishDir =*Directory* \\ optie, met inbegrip van het afsluitende backslash scheidingsteken, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="16d99-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="16d99-154">Nadat u hebt gemaakt en een juiste MSBuild-opdrachtregel voor het bouwen van uw projecten en ze combineren in een Azure-pakket getest, kunt u met deze opdrachtregel toevoegen aan uw build-scripts.</span><span class="sxs-lookup"><span data-stu-id="16d99-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="16d99-155">Als uw buildserver gebruikmaakt van aangepaste scripts, wordt dit proces afhankelijk van de details van uw aangepaste buildproces.</span><span class="sxs-lookup"><span data-stu-id="16d99-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="16d99-156">Als u TFS gebruikt als een build-omgeving, kunt u de instructies in de volgende stap de Azure-pakket build toevoegen aan uw buildproces volgen.</span><span class="sxs-lookup"><span data-stu-id="16d99-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="16d99-157">3: bouwen van een pakket met TFS-Team maken</span><span class="sxs-lookup"><span data-stu-id="16d99-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="16d99-158">Als u hebt Team Foundation Server (TFS) ingesteld als een controller bouwen en de buildserver instellen als een TFS-build-machine en u kunt desgewenst een geautomatiseerde build instellen voor uw Azure-pakket op.</span><span class="sxs-lookup"><span data-stu-id="16d99-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="16d99-159">Zie voor meer informatie over het instellen en Team Foundation server gebruiken als een build-systeem [Scale-out uw build-systeem][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="16d99-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="16d99-160">Met name de volgende procedure wordt ervan uitgegaan dat u uw buildserver hebt geconfigureerd zoals beschreven in [implementeren en configureren van een buildserver][Deploy and configure a build server], en dat u hebt gemaakt dat een teamproject gemaakt een cloud Service-project in het teamproject.</span><span class="sxs-lookup"><span data-stu-id="16d99-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="16d99-161">Voer de volgende stappen uit voor het configureren van TFS om samen te stellen Azure pakketten:</span><span class="sxs-lookup"><span data-stu-id="16d99-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="16d99-162">Kies in Visual Studio op uw ontwikkelcomputer, in het menu Beeld **Team Explorer**, of kies Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="16d99-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="16d99-163">Vouw in het Team Explorer-venster, de **Builds** knooppunt of kies de **Builds** pagina en kies **nieuwe bouwen definitie**.</span><span class="sxs-lookup"><span data-stu-id="16d99-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Nieuwe bouwen definitie-optie][0]
2. <span data-ttu-id="16d99-165">Kies de **Trigger** tabblad en geef de gewenste voorwaarden voor als u wilt dat het pakket kunnen worden gebouwd.</span><span class="sxs-lookup"><span data-stu-id="16d99-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="16d99-166">Geef bijvoorbeeld **continue integratie** optreedt voor het bouwen van het pakket wanneer een bron inchecken beheren.</span><span class="sxs-lookup"><span data-stu-id="16d99-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="16d99-167">Kies de **broninstellingen** tabblad en zorg ervoor dat de projectmap wordt vermeld in de **bronmap van het besturingselement** kolom en de status **Active**.</span><span class="sxs-lookup"><span data-stu-id="16d99-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="16d99-168">Kies de **bouwen standaard** tabblad en controleer of de naam van de buildserver onder Build-controller.</span><span class="sxs-lookup"><span data-stu-id="16d99-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="16d99-169">Ook de optie **kopie bouwen uitvoer voor de volgende doelmap** en geef de gewenste doellocatie.</span><span class="sxs-lookup"><span data-stu-id="16d99-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="16d99-170">Kies de **proces** tabblad. Kies op het tabblad proces de standaardsjabloon onder **bouwen**, kiest u het project als deze nog niet is geselecteerd, en vouw de **Geavanceerd** sectie het **bouwen** sectie van het raster.</span><span class="sxs-lookup"><span data-stu-id="16d99-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="16d99-171">Kies **MSBuild-argumenten**, en stel de juiste MSBuild-opdrachtregelargumenten, zoals beschreven in stap 2 hierboven.</span><span class="sxs-lookup"><span data-stu-id="16d99-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="16d99-172">Voer bijvoorbeeld **/t: publiceren /p:PublishDir =\\\\MijnServer\\zakt\\**  het bouwen van een pakket en kopieer de pakketbestanden naar de locatie \\ \\ MijnServer\\zakt\\:</span><span class="sxs-lookup"><span data-stu-id="16d99-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![MSBuild-argumenten][2]

   > [!NOTE]
   > <span data-ttu-id="16d99-174">De bestanden zijn gekopieerd naar een openbare share gemakkelijker handmatig implementeren van de pakketten van uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="16d99-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="16d99-175">Het succes van uw build-stap testen door te controleren in een wijziging in uw project, of een nieuwe build in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="16d99-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="16d99-176">Als u wilt een nieuwe build, in de Explorer-Team in de wachtrij met de rechtermuisknop op **alle bouwen definities** en kies vervolgens **wachtrij nieuwe bouwen**.</span><span class="sxs-lookup"><span data-stu-id="16d99-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="16d99-177">4: een pakket met een PowerShell-Script publiceren</span><span class="sxs-lookup"><span data-stu-id="16d99-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="16d99-178">Deze sectie wordt beschreven hoe een Windows PowerShell-script die de uitvoer van de Cloud-app-pakket worden gepubliceerd naar Azure met optionele parameters.</span><span class="sxs-lookup"><span data-stu-id="16d99-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="16d99-179">Dit script kan worden aangeroepen na de build stap in uw aangepaste build automation.</span><span class="sxs-lookup"><span data-stu-id="16d99-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="16d99-180">Het kan ook worden aangeroepen vanuit de werkstroomactiviteiten processjabloon in Visual Studio TFS Team bouwen.</span><span class="sxs-lookup"><span data-stu-id="16d99-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="16d99-181">Installeer de [Azure PowerShell-cmdlets] [ Azure PowerShell cmdlets] (v0.6.1 of hoger).</span><span class="sxs-lookup"><span data-stu-id="16d99-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="16d99-182">Kiezen tijdens de installatiefase cmdlet te installeren als een module.</span><span class="sxs-lookup"><span data-stu-id="16d99-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="16d99-183">Houd er rekening mee dat deze officieel ondersteunde versie wordt vervangen door de oudere versie die worden aangeboden via CodePlex, hoewel de vorige versies 2.x.x nummer.</span><span class="sxs-lookup"><span data-stu-id="16d99-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="16d99-184">Azure PowerShell via het menu Start begint of pagina.</span><span class="sxs-lookup"><span data-stu-id="16d99-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="16d99-185">Als u op deze manier wordt gestart, wordt de Azure PowerShell-cmdlets worden geladen.</span><span class="sxs-lookup"><span data-stu-id="16d99-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="16d99-186">Controleren of de PowerShell-cmdlets zijn geladen met de gedeeltelijke opdracht achter de PowerShell-prompt `Get-Azure` en drukt u op de Tab-toets voor de instructie was voltooid.</span><span class="sxs-lookup"><span data-stu-id="16d99-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="16d99-187">Als u herhaaldelijk op de Tab-toets drukt, ziet u diverse Azure PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="16d99-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="16d99-188">Controleer of dat u verbinding met uw Azure-abonnement maken kunt met uw abonnementsgegevens importeren uit de .publishsettings-bestand.</span><span class="sxs-lookup"><span data-stu-id="16d99-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="16d99-189">Voer de opdracht</span><span class="sxs-lookup"><span data-stu-id="16d99-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="16d99-190">Dit toont informatie over uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="16d99-190">This shows information about your subscription.</span></span> <span data-ttu-id="16d99-191">Controleer of alles juist is.</span><span class="sxs-lookup"><span data-stu-id="16d99-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="16d99-192">Sla de script-sjabloon opgegeven aan het einde van dit artikel om uw scriptmap als c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="16d99-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="16d99-193">Bekijk het gedeelte parameters van het script.</span><span class="sxs-lookup"><span data-stu-id="16d99-193">Review the parameters section of the script.</span></span> <span data-ttu-id="16d99-194">Toevoegen of wijzigen van de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="16d99-194">Add or modify any default values.</span></span> <span data-ttu-id="16d99-195">Deze waarden kunnen altijd worden genegeerd door door te geven in expliciete parameters.</span><span class="sxs-lookup"><span data-stu-id="16d99-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="16d99-196">Zorg dat er geldige cloud service- en storage accounts worden gemaakt in uw abonnement die kan worden gericht door het script publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="16d99-197">Het opslagaccount (blobopslag) wordt gebruikt om te uploaden en de implementatie van pakket en config-bestand tijdelijk op te slaan tijdens de implementatie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16d99-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="16d99-198">Voor het maken van een nieuwe cloudservice, kunt u dit script aanroepen of de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16d99-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16d99-199">De naam van de cloud-service wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="16d99-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="16d99-200">Als u wilt een nieuw opslagaccount maakt, kunt u dit script aanroepen of de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16d99-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="16d99-201">Naam van het opslagaccount wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="16d99-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="16d99-202">U kunt met dezelfde naam als de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="16d99-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="16d99-203">Aanroepen van het script rechtstreeks vanuit de Azure PowerShell, of op wire dit script op uw host build automation na het opbouwen van het pakket.</span><span class="sxs-lookup"><span data-stu-id="16d99-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="16d99-204">Het script wordt altijd Verwijder of vervang de bestaande implementaties standaard als ze worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="16d99-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="16d99-205">Dit is nodig om in te schakelen continue van automatisering geen gebruiker wordt gevraagd wanneer mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="16d99-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="16d99-206">**Voorbeeldscenario 1:** continue implementatie bij de faseringsomgeving van een service:</span><span class="sxs-lookup"><span data-stu-id="16d99-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="16d99-207">Dit is doorgaans opgevolgd door testuitvoering verificatie en geen VIP's wisselen.</span><span class="sxs-lookup"><span data-stu-id="16d99-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="16d99-208">Het wisselen van VIP kan worden uitgevoerd via de [Azure-portal](https://portal.azure.com) of met behulp van de cmdlet Move-implementatie.</span><span class="sxs-lookup"><span data-stu-id="16d99-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="16d99-209">**Voorbeeldscenario 2:** continue implementatie naar de productieomgeving van een speciale test-service</span><span class="sxs-lookup"><span data-stu-id="16d99-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="16d99-210">**Extern bureaublad:**</span><span class="sxs-lookup"><span data-stu-id="16d99-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="16d99-211">Als Extern bureaublad is ingeschakeld in uw Azure-project u aanvullende eenmalige stappen moet om te controleren of dat de juiste Cloud Service-certificaat is geüpload naar alle cloudservices waarop dit script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16d99-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="16d99-212">Zoek de certificaat vingerafdruk waarden door uw rollen wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="16d99-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="16d99-213">De vingerafdruk-waarden zijn zichtbaar in de sectie certificaten van het configuratiebestand van de cloud (dat wil zeggen ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="16d99-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="16d99-214">Het is ook zichtbaar in het dialoogvenster configuratie van extern bureaublad in Visual Studio wanneer u opties en bekijk het geselecteerde certificaat.</span><span class="sxs-lookup"><span data-stu-id="16d99-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="16d99-215">Extern bureaublad-certificaten uploaden als een eenmalige instellingsstap met behulp van de volgende cmdlet-script:</span><span class="sxs-lookup"><span data-stu-id="16d99-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="16d99-216">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="16d99-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="16d99-217">U kunt ook het certificaatbestand PFX met persoonlijke sleutel exporteren en certificaten uploaden naar elk doel cloud service met behulp van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16d99-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="16d99-218">**Upgraden versus van de implementatie. Verwijderen van implementatie -\> nieuwe implementatie**</span><span class="sxs-lookup"><span data-stu-id="16d99-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="16d99-219">Het script wordt standaard uitvoeren een Upgrade-implementatie ($enableDeploymentUpgrade = 1) als er is geen parameter is doorgegeven, of de waarde 1 expliciet wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="16d99-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="16d99-220">Dit heeft het voordeel van het minder tijd nodig dan een volledige implementatie voor enkele exemplaren.</span><span class="sxs-lookup"><span data-stu-id="16d99-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="16d99-221">Voor exemplaren waarvoor hoge beschikbaarheid, dit ook het voordeel heeft van het verlaten van sommige gevallen terwijl anderen kunnen worden bijgewerkt (roulatie van uw updatedomein), plus de VIP wordt niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="16d99-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="16d99-222">Upgrade-implementatie kan worden uitgeschakeld in het script ($enableDeploymentUpgrade = 0) of door het doorgeven van *- enableDeploymentUpgrade 0* als een parameter die het gedrag van het script moet eerst alle bestaande implementatie verwijderen en maak vervolgens een nieuwe wordt gewijzigd de implementatie.</span><span class="sxs-lookup"><span data-stu-id="16d99-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="16d99-223">Het script wordt altijd Verwijder of vervang de bestaande implementaties standaard als ze worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="16d99-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="16d99-224">Dit is nodig om in te schakelen continue van automatisering wanneer er geen gebruiker/operator vragen mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="16d99-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="16d99-225">5: een pakket met behulp van TFS-Team bouwen publiceren</span><span class="sxs-lookup"><span data-stu-id="16d99-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="16d99-226">Deze optionele stap maakt verbinding met TFS-Team bouwen aan het script dat is gemaakt in stap 4, die het publiceren van de build van het pakket naar Azure verwerkt.</span><span class="sxs-lookup"><span data-stu-id="16d99-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="16d99-227">Dit houdt in dat de sjabloon die wordt gebruikt door de definitie van de build zodat deze wordt uitgevoerd een activiteit publiceren aan het einde van de werkstroom wijzigen.</span><span class="sxs-lookup"><span data-stu-id="16d99-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="16d99-228">De activiteit publiceren wordt uw PowerShell-opdracht wordt doorgegeven in parameters van de build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16d99-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="16d99-229">Uitvoer van de MSBuild-doelen en publiceren van script zal worden doorgesluisd naar de standaard build-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d99-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="16d99-230">Bewerk de definitie bouwen die verantwoordelijk is voor continue implementeren.</span><span class="sxs-lookup"><span data-stu-id="16d99-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="16d99-231">Selecteer de **proces** tabblad.</span><span class="sxs-lookup"><span data-stu-id="16d99-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="16d99-232">Ga als volgt [deze instructies](http://msdn.microsoft.com/library/dd647551.aspx) om toe te voegen in een activiteit-project voor de build processjabloon, downloaden de standaardsjabloon, toe te voegen aan het project en inchecken in.</span><span class="sxs-lookup"><span data-stu-id="16d99-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="16d99-233">Geeft de build processjabloon een nieuwe naam, zoals AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="16d99-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="16d99-234">Ga terug naar de **proces** tabblad en gebruik **Details weergeven** om een lijst met beschikbare build processjablonen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="16d99-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="16d99-235">Kies de **nieuwe...**  knop en navigeer naar het project dat u zojuist hebt toegevoegd en ingecheckt.</span><span class="sxs-lookup"><span data-stu-id="16d99-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="16d99-236">Zoek de sjabloon die u zojuist hebt gemaakt en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="16d99-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="16d99-237">Open de geselecteerde sjabloon proces voor het bewerken.</span><span class="sxs-lookup"><span data-stu-id="16d99-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="16d99-238">U kunt rechtstreeks in de Workflow designer of in de XML-editor om te werken met de XAML openen.</span><span class="sxs-lookup"><span data-stu-id="16d99-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="16d99-239">De volgende lijst met nieuwe argumenten toevoegen als afzonderlijke regels op het tabblad argumenten van de workflow designer.</span><span class="sxs-lookup"><span data-stu-id="16d99-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="16d99-240">Alle argumenten moet richting = In en typ = tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="16d99-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="16d99-241">Deze wordt gebruikt voor parameters van de stroom van de definitie van de build in de werkstroom, die vervolgens gebruikt ophalen voor het aanroepen van het script publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lijst met argumenten][3]

   <span data-ttu-id="16d99-243">De bijbehorende XAML ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="16d99-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="16d99-244">Een nieuwe reeks toevoegen aan het einde van de Agent uitvoeren op:</span><span class="sxs-lookup"><span data-stu-id="16d99-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="16d99-245">Start op het toevoegen van een activiteit If-instructie om te controleren op een geldige scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="16d99-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="16d99-246">De voorwaarde op deze waarde wordt ingesteld:</span><span class="sxs-lookup"><span data-stu-id="16d99-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="16d99-247">Wanneer de vervolgens van de instructie als een nieuwe Sequence-activiteit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16d99-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="16d99-248">De weergavenaam 'Start publiceren' instellen</span><span class="sxs-lookup"><span data-stu-id="16d99-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="16d99-249">Met het begin publiceren reeks nog steeds is geselecteerd, voeg de volgende lijst met nieuwe variabelen als afzonderlijke regels op het tabblad variabelen van de workflow designer.</span><span class="sxs-lookup"><span data-stu-id="16d99-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="16d99-250">Alle variabelen moet type variabele = tekenreeks en bereik = Start publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="16d99-251">Deze wordt gebruikt voor parameters van de stroom van de definitie van de build in de werkstroom, die vervolgens gebruikt ophalen voor het aanroepen van het script publiceren.</span><span class="sxs-lookup"><span data-stu-id="16d99-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="16d99-252">SubscriptionDataFilePath van het type tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16d99-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="16d99-253">PublishScriptFilePath van het type tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16d99-253">PublishScriptFilePath, of type String</span></span>

        ![Nieuwe variabelen][4]
   4. <span data-ttu-id="16d99-255">Als u TFS 2012 of ouder gebruikt, moet u een ConvertWorkspaceItem-activiteit toevoegen aan het begin van de nieuwe volgorde.</span><span class="sxs-lookup"><span data-stu-id="16d99-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="16d99-256">Als u TFS 2013 of later gebruikt, moet u een GetLocalPath-activiteit toevoegen aan het begin van de nieuwe volgorde.</span><span class="sxs-lookup"><span data-stu-id="16d99-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="16d99-257">Voor een ConvertWorkspaceItem als volgt de eigenschappen instellen: richting = ServerToLocal, DisplayName = 'Converteren publiceren script filename', invoer = PublishScriptLocation, resultaat = PublishScriptFilePath, werkruimte = 'Werkruimte'.</span><span class="sxs-lookup"><span data-stu-id="16d99-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="16d99-258">Stel de eigenschap IncomingPath naar 'PublishScriptLocation' en het resultaat 'PublishScriptFilePath' voor een activiteit GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="16d99-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="16d99-259">Deze activiteit zet het pad naar het script publiceren van TFS-serverlocaties (indien van toepassing) naar een pad standaard lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="16d99-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="16d99-260">Als u TFS 2012 of ouder gebruikt, moet u een andere ConvertWorkspaceItem activiteit toevoegen aan het einde van de nieuwe volgorde.</span><span class="sxs-lookup"><span data-stu-id="16d99-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="16d99-261">Richting = ServerToLocal, DisplayName = 'Converteren abonnement filename', invoer = SubscriptionDataFileLocation, resultaat = SubscriptionDataFilePath, werkruimte = 'Werkruimte'.</span><span class="sxs-lookup"><span data-stu-id="16d99-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="16d99-262">Als u TFS 2013 of later gebruikt, voegt u een andere GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="16d99-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="16d99-263">IncomingPath = 'SubscriptionDataFileLocation' en resultaat = 'SubscriptionDataFilePath'.</span><span class="sxs-lookup"><span data-stu-id="16d99-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="16d99-264">Een activiteit InvokeProcess toevoegen aan het einde van de nieuwe volgorde.</span><span class="sxs-lookup"><span data-stu-id="16d99-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="16d99-265">Deze activiteit roept PowerShell.exe met de argumenten doorgegeven aan de definitie bouwen.</span><span class="sxs-lookup"><span data-stu-id="16d99-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="16d99-266">Argumenten String.Format = ('-'' {0}' ' - serviceName {1} - storageAccountName {2} - packageLocation '' {3}' ' - cloudConfigLocation '' {4}' ' - subscriptionDataFile '' {5}' ' - selectedSubscription {6} bestand-omgeving '' {7}' ' ",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, SubscriptionName, omgeving)</span><span class="sxs-lookup"><span data-stu-id="16d99-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="16d99-267">DisplayName = Execute script publiceren</span><span class="sxs-lookup"><span data-stu-id="16d99-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="16d99-268">FileName = 'PowerShell' (inclusief de aanhalingstekens)</span><span class="sxs-lookup"><span data-stu-id="16d99-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="16d99-269">OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =</span><span class="sxs-lookup"><span data-stu-id="16d99-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="16d99-270">In de **standaarduitvoer verwerken** sectie textbox van de InvokeProcess, stelt u de waarde van het tekstvak naar 'data'.</span><span class="sxs-lookup"><span data-stu-id="16d99-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="16d99-271">Dit is een variabele voor het opslaan van de standaarduitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d99-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="16d99-272">Toevoegen van een activiteit WriteBuildMessage NET hieronder de **standaarduitvoer verwerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="16d99-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="16d99-273">De urgentie = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' en het bericht = 'data'.</span><span class="sxs-lookup"><span data-stu-id="16d99-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="16d99-274">Hierdoor worden de standaarduitvoer van het script wordt weggeschreven naar de builduitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d99-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="16d99-275">In de **foutuitvoer verwerken** sectie textbox van de InvokeProcess, stelt u de waarde van het tekstvak naar 'data'.</span><span class="sxs-lookup"><span data-stu-id="16d99-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="16d99-276">Dit is een variabele voor het opslaan van de standaardfout-gegevens.</span><span class="sxs-lookup"><span data-stu-id="16d99-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="16d99-277">Toevoegen van een activiteit WriteBuildError NET hieronder de **foutuitvoer verwerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="16d99-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="16d99-278">Het bericht instellen = 'data'.</span><span class="sxs-lookup"><span data-stu-id="16d99-278">Set the Message='data'.</span></span> <span data-ttu-id="16d99-279">Hierdoor worden dat de standaard-fouten van het script wordt weggeschreven naar de uitvoer van de build-fout.</span><span class="sxs-lookup"><span data-stu-id="16d99-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="16d99-280">Corrigeer eventuele fouten, aangegeven door blauw uitroepteken aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="16d99-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="16d99-281">Beweeg de muisaanwijzer over de merken uitroepteken ophalen van een aanwijzing over de fout.</span><span class="sxs-lookup"><span data-stu-id="16d99-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="16d99-282">De workflow om te wissen fouten niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="16d99-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="16d99-283">In de ontwerpfunctie voor er het uiteindelijke resultaat van de werkstroomactiviteiten publiceren als volgt:</span><span class="sxs-lookup"><span data-stu-id="16d99-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Workflow-activiteiten][5]

   <span data-ttu-id="16d99-285">Het uiteindelijke resultaat van de werkstroomactiviteiten publiceren ziet er als volgt in XAML:</span><span class="sxs-lookup"><span data-stu-id="16d99-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="16d99-286">De werkstroom van sjabloon build en controleren In dit bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="16d99-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="16d99-287">Bewerk de build-definitie (sluit als het al geopend is), en selecteer de **nieuw** knop als u de nieuwe sjabloon in de lijst met processjablonen niet nog ziet.</span><span class="sxs-lookup"><span data-stu-id="16d99-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="16d99-288">De parameter eigenschapswaarden in de sectie div als volgt instellen:</span><span class="sxs-lookup"><span data-stu-id="16d99-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="16d99-289">CloudConfigLocation ='c:\\zakt\\app.publish\\ServiceConfiguration.Cloud.cscfg' *deze waarde is afgeleid van: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="16d99-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="16d99-290">PackageLocation = ' c:\\zakt\\app.publish\\ContactManager.Azure.cspkg' *deze waarde is afgeleid van: ($PublishDir)($ProjectName) .cspkg*</span><span class="sxs-lookup"><span data-stu-id="16d99-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="16d99-291">PublishScriptLocation = ' c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="16d99-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="16d99-292">ServiceName = 'mycloudservicename' *hier de naam van de juiste cloud-service gebruiken*</span><span class="sxs-lookup"><span data-stu-id="16d99-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="16d99-293">Omgeving = 'Fasering'</span><span class="sxs-lookup"><span data-stu-id="16d99-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="16d99-294">StorageAccountName = 'mystorageaccountname' *hier de naam van het juiste opslagaccount gebruiken*</span><span class="sxs-lookup"><span data-stu-id="16d99-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="16d99-295">SubscriptionDataFileLocation = ' c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="16d99-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="16d99-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="16d99-296">SubscriptionName = 'default'</span></span>

    ![Eigenschap parameterwaarden][6]
11. <span data-ttu-id="16d99-298">Sla de wijzigingen aan de definitie bouwen.</span><span class="sxs-lookup"><span data-stu-id="16d99-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="16d99-299">Een Build voor het uitvoeren van zowel de pakket-build en publiceren van de verzendwachtrij.</span><span class="sxs-lookup"><span data-stu-id="16d99-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="16d99-300">Als u een trigger die is ingesteld op doorlopende integratie hebt, kunt u dit gedrag wordt uitgevoerd bij elke controle.</span><span class="sxs-lookup"><span data-stu-id="16d99-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="16d99-301">PublishCloudService.ps1 script sjabloon</span><span class="sxs-lookup"><span data-stu-id="16d99-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="16d99-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16d99-302">Next steps</span></span>
<span data-ttu-id="16d99-303">Zie inschakelen foutopsporing op afstand bij gebruik van doorlopende levering [foutopsporing op afstand inschakelen wanneer publiceren naar Azure met behulp van continue levering](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="16d99-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
