---
title: een CI/CD-pijplijn in Azure met Team Services aaaCreate | Microsoft Docs
description: "Meer informatie over hoe een Visual Studio Team Services toocreate pijplijn voor continue integratie en aflevering waarmee een tooIIS web-app op een Windows-virtuele machine wordt geïmplementeerd"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="e6352-103">Een continue integratie-pijplijn maken met Visual Studio Team Services en IIS</span><span class="sxs-lookup"><span data-stu-id="e6352-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="e6352-104">tooautomate hello build, test en fasen van de implementatie van de ontwikkeling van toepassingen, kunt u een continue integratie en implementatie (CI/CD) pijplijn.</span><span class="sxs-lookup"><span data-stu-id="e6352-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="e6352-105">In deze zelfstudie maakt u een CI/CD-pijplijn met Visual Studio Team Services en virtuele Windows-machine (VM) in Azure waarop IIS wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="e6352-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="e6352-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e6352-107">Een ASP.NET-toepassing tooa Team Services webproject publiceren</span><span class="sxs-lookup"><span data-stu-id="e6352-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="e6352-108">Een build-definitie die wordt geactiveerd door doorvoeracties code maken</span><span class="sxs-lookup"><span data-stu-id="e6352-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="e6352-109">IIS installeren en configureren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="e6352-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="e6352-110">Hallo IIS tooa implementatie instantiegroep in Team Services toevoegen</span><span class="sxs-lookup"><span data-stu-id="e6352-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="e6352-111">Maak een nieuwe website voor release definitie toopublish pakketten tooIIS implementeren</span><span class="sxs-lookup"><span data-stu-id="e6352-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="e6352-112">Test Hallo CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="e6352-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="e6352-113">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e6352-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e6352-114">Voer `Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="e6352-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="e6352-115">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e6352-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="e6352-116">Project maken in een Team Services</span><span class="sxs-lookup"><span data-stu-id="e6352-116">Create project in Team Services</span></span>
<span data-ttu-id="e6352-117">Visual Studio Team Services kunt u eenvoudig samenwerking en ontwikkeling zonder het onderhouden van een on-premises-oplossing voor het beheer van code.</span><span class="sxs-lookup"><span data-stu-id="e6352-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="e6352-118">Teamservices biedt cloud code testen, build en application insights.</span><span class="sxs-lookup"><span data-stu-id="e6352-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="e6352-119">U kunt een besturingselement-repo-versie en IDE die het beste past bij de ontwikkeling van uw code.</span><span class="sxs-lookup"><span data-stu-id="e6352-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="e6352-120">Voor deze zelfstudie kunt u een gratis account toocreate een eenvoudige ASP.NET-web-app en CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="e6352-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="e6352-121">Als u nog geen een Team Services-account [maken van een](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="e6352-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="e6352-122">toomanage hello code commit proces definities, bouwen en definities release, in een project maakt Team Services als volgt:</span><span class="sxs-lookup"><span data-stu-id="e6352-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="e6352-123">Open uw dashboard Team Services in een webbrowser en kies **nieuw project**.</span><span class="sxs-lookup"><span data-stu-id="e6352-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="e6352-124">Voer *myWebApp* voor Hallo **projectnaam**.</span><span class="sxs-lookup"><span data-stu-id="e6352-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="e6352-125">Andere toouse voor de waarden standaard laat *Git* versiebeheer en *Agile* proces werkitem.</span><span class="sxs-lookup"><span data-stu-id="e6352-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="e6352-126">Hallo-optie te kiezen**delen met** *teamleden*, selecteer daarna **maken**.</span><span class="sxs-lookup"><span data-stu-id="e6352-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="e6352-127">Wanneer uw project is gemaakt, kiest u Hallo optie te**initialiseren met een Leesmij-bestand of gitignore**, klikt u vervolgens **initialiseren**.</span><span class="sxs-lookup"><span data-stu-id="e6352-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="e6352-128">Kies in het nieuwe project **Dashboards** aan de bovenkant hello, selecteer **openen in Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="e6352-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="e6352-129">ASP.NET-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e6352-129">Create ASP.NET web application</span></span>
<span data-ttu-id="e6352-130">In de vorige stap hello, moet u een project in Team Services gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6352-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="e6352-131">de laatste stap Hallo Hiermee opent u het nieuwe project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6352-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="e6352-132">Beheren van uw code doorvoeringen in Hallo **Team Explorer** venster.</span><span class="sxs-lookup"><span data-stu-id="e6352-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="e6352-133">Maken van een lokale kopie van het nieuwe project en maak vervolgens een ASP.NET-webtoepassing vanuit een sjabloon als volgt:</span><span class="sxs-lookup"><span data-stu-id="e6352-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="e6352-134">Selecteer **kloon** toocreate een lokale git-opslagplaats van uw Team Services-project.</span><span class="sxs-lookup"><span data-stu-id="e6352-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![De opslagplaats klonen uit Team Services-project](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="e6352-136">Onder **oplossingen**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e6352-136">Under **Solutions**, select **New**.</span></span>

    ![Oplossing voor webtoepassing maken](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="e6352-138">Selecteer **Web** sjablonen, en kies vervolgens Hallo **ASP.NET-webtoepassing** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e6352-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="e6352-139">Voer een naam voor uw toepassing, zoals *myWebApp*, en schakel Hallo selectievakje uit voor **map voor oplossing maken**.</span><span class="sxs-lookup"><span data-stu-id="e6352-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="e6352-140">Als het Hallo-optie beschikbaar is, schakelt u Hallo vak te**Application Insights toevoegen tooproject**.</span><span class="sxs-lookup"><span data-stu-id="e6352-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="e6352-141">Application Insights vereist tooauthorize u uw webtoepassing met Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e6352-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="e6352-142">tookeep het eenvoudig is in deze zelfstudie dit proces overslaan.</span><span class="sxs-lookup"><span data-stu-id="e6352-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="e6352-143">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6352-143">Select **OK**.</span></span>
4. <span data-ttu-id="e6352-144">Kies **MVC** in lijst Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e6352-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="e6352-145">Selecteer **verificatie wijzigen**, kies **geen verificatie**, selecteer daarna **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6352-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="e6352-146">Selecteer **OK** toocreate uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="e6352-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="e6352-147">In Hallo **Team Explorer** venster kiezen **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="e6352-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Lokale wijzigingen tooTeam Services git-opslagplaats doorvoeren](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="e6352-149">Voer in het tekstvak Hallo doorvoeren, een bericht zoals *initiële doorvoeren*.</span><span class="sxs-lookup"><span data-stu-id="e6352-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="e6352-150">Kies **alle doorvoeren en Sync** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6352-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="e6352-151">Build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="e6352-151">Create build definition</span></span>
<span data-ttu-id="e6352-152">In het Team Services gebruikt u een build definitie toooutline hoe uw toepassing moet worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="e6352-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="e6352-153">In deze zelfstudie maken we een basisdefinitie dat vergt onze broncode Hallo oplossing bouwt en maakt vervolgens web pakket gebruiken we toorun Hallo web-app op een IIS-server implementeren.</span><span class="sxs-lookup"><span data-stu-id="e6352-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="e6352-154">Kies in het project Team Services **bouwen & Release** aan de bovenkant hello, selecteer **Builds**.</span><span class="sxs-lookup"><span data-stu-id="e6352-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="e6352-155">Selecteer **+ nieuwe definitie**.</span><span class="sxs-lookup"><span data-stu-id="e6352-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="e6352-156">Kies Hallo **ASP.NET (PREVIEW)** sjabloon en selecteer **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="e6352-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="e6352-157">Laat alle Hallo standaard waarden van de taak.</span><span class="sxs-lookup"><span data-stu-id="e6352-157">Leave all hello default task values.</span></span> <span data-ttu-id="e6352-158">Onder **bronnen ophalen**, zorg ervoor dat Hallo *myWebApp* opslagplaats en *master* vertakking worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Definitie van de build in Team Services-project maken](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="e6352-160">Op Hallo **Triggers** tabblad, verplaats de schuifregelaar Hallo voor **inschakelen van deze trigger** te*ingeschakeld*.</span><span class="sxs-lookup"><span data-stu-id="e6352-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="e6352-161">Hallo build definitie en wachtrij een nieuwe build opslaan door **opslaan en wachtrij** , klikt u vervolgens **opslaan en wachtrij** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e6352-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="e6352-162">Hallo standaardinstellingen laten staan en selecteer **wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="e6352-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="e6352-163">Bekijk begint zoals Hallo build is gepland op een gehoste agent vervolgens toobuild.</span><span class="sxs-lookup"><span data-stu-id="e6352-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="e6352-164">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e6352-164">hello output is similar toohello following example:</span></span>

![Geslaagde build van het Team Services-project](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="e6352-166">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="e6352-166">Create virtual machine</span></span>
<span data-ttu-id="e6352-167">een platform toorun tooprovide uw ASP.NET-web-app, moet u een virtuele Windows-machine waarop IIS wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="e6352-168">Teamservices maakt gebruik van een agent toointeract met Hallo IIS-exemplaar als u code doorvoert en builds worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="e6352-169">Maak een VM van Windows Server 2016 met [dit voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e6352-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="e6352-170">Het duurt enkele minuten voor Hallo script toorun en Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="e6352-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="e6352-171">Zodra het Hallo VM is gemaakt, opent u poort 80 voor internetverkeer met [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) als volgt:</span><span class="sxs-lookup"><span data-stu-id="e6352-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="e6352-172">tooconnect tooyour VM, verkrijgen Hallo openbare IP-adres met [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) als volgt:</span><span class="sxs-lookup"><span data-stu-id="e6352-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="e6352-173">Een extern bureaublad-sessiehost tooyour VM maken:</span><span class="sxs-lookup"><span data-stu-id="e6352-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="e6352-174">Open op Hallo VM, een **beheerder PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e6352-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="e6352-175">IIS en de vereiste .NET-functies als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="e6352-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="e6352-176">Implementatiegroep maken</span><span class="sxs-lookup"><span data-stu-id="e6352-176">Create deployment group</span></span>
<span data-ttu-id="e6352-177">toopush uit Hallo web pakket toohello IIS-server implementeren, het definiëren van een implementatiegroep in een Team Services.</span><span class="sxs-lookup"><span data-stu-id="e6352-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="e6352-178">Deze groep kunt u toospecify welke servers Hallo doel van de nieuwe builds worden als het doorvoeren van code tooTeam Services en builds zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="e6352-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="e6352-179">Kies in het Team Services, **bouwen & Release** en selecteer vervolgens **implementatiegroepen**.</span><span class="sxs-lookup"><span data-stu-id="e6352-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="e6352-180">Kies **implementatie toevoegen groep**.</span><span class="sxs-lookup"><span data-stu-id="e6352-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="e6352-181">Voer een naam voor de groep hello, zoals *myIIS*, selecteer daarna **maken**.</span><span class="sxs-lookup"><span data-stu-id="e6352-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="e6352-182">In Hallo **machines registreren** sectie, moet u zorgen *Windows* is ingeschakeld, wordt het selectievakje hello te**een persoonlijk toegangstoken in Hallo script gebruiken voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="e6352-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="e6352-183">Selecteer **tooclipboard script kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="e6352-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="e6352-184">IIS VM toohello implementatiegroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="e6352-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="e6352-185">Elke groep van IIS-exemplaar toohello Hallo implementatie-groep is gemaakt, toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e6352-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="e6352-186">Teamservices genereert een script dat downloadt en configureert u een agent op Hallo implementeren van virtuele machine die u ontvangt van de nieuwe web-pakketten en vervolgens tooIIS wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="e6352-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="e6352-187">Terug in Hallo **beheerder PowerShell** sessie op de virtuele machine, plakken en opgehaald uit het Team Services Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e6352-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="e6352-188">Wanneer de vraag tooconfigure labels voor Hallo-agent, optie *Y* en voer *web*.</span><span class="sxs-lookup"><span data-stu-id="e6352-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="e6352-189">Wanneer u wordt gevraagd voor het gebruikersaccount hello, drukt u op *retourneren* tooaccept Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="e6352-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="e6352-190">Wachten op Hallo script toofinish met een bericht *vstsagent.account.computername Service is gestart*.</span><span class="sxs-lookup"><span data-stu-id="e6352-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="e6352-191">In Hallo **implementatiegroepen** pagina Hallo **bouwen & Release** menu, open Hallo *myIIS* implementatiegroep.</span><span class="sxs-lookup"><span data-stu-id="e6352-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="e6352-192">Op Hallo **Machines** tabblad, controleert u of uw virtuele machine wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e6352-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![Virtuele machine toegevoegd tooTeam Services implementatiegroep](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="e6352-194">Release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="e6352-194">Create release definition</span></span>
<span data-ttu-id="e6352-195">toopublish uw builds u de definitie van een release maken in een Team Services.</span><span class="sxs-lookup"><span data-stu-id="e6352-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="e6352-196">Deze definitie wordt automatisch geactiveerd door een geslaagde build van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e6352-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="e6352-197">U kiest Hallo implementatie groep toopush uw web-pakket te implementeren en de juiste IIS-instellingen Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="e6352-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="e6352-198">Kies **bouwen & Release**, selecteer daarna **Builds**.</span><span class="sxs-lookup"><span data-stu-id="e6352-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="e6352-199">Kies Hallo build definitie die is gemaakt in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="e6352-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="e6352-200">Onder **onlangs voltooid**, kies de meest recente build hello, en selecteer **Release**.</span><span class="sxs-lookup"><span data-stu-id="e6352-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="e6352-201">Kies **Ja** toocreate een release-definitie.</span><span class="sxs-lookup"><span data-stu-id="e6352-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="e6352-202">Kies Hallo **leeg** sjabloon, selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e6352-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="e6352-203">Controleer of het Hallo-project en de brontabel build-definitie zijn gevuld met uw project.</span><span class="sxs-lookup"><span data-stu-id="e6352-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="e6352-204">Selecteer Hallo **continue implementatie** in en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="e6352-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="e6352-205">Selecteer de vervolgkeuzelijst Hallo naast te**+ taken toevoegen** en kies *toevoegen van een groep implementatiefase*.</span><span class="sxs-lookup"><span data-stu-id="e6352-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Toorelease taakdefinitie in Team Services toevoegen](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="e6352-207">Kies **toevoegen** volgende te**IIS Web-App Deploy(Preview)**, selecteer daarna **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="e6352-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="e6352-208">Selecteer Hallo **uitvoeren op implementatiegroep** bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="e6352-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="e6352-209">Voor **Implementatiegroep**, selecteer Hallo implementatie groep die u hebt gemaakt uit eerder, zoals *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="e6352-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="e6352-210">In Hallo **Machine labels** de optie **toevoegen** en kies Hallo *web* label.</span><span class="sxs-lookup"><span data-stu-id="e6352-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![De definitie van implementatie groepstaak vrijgeven voor IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="e6352-212">Selecteer Hallo **implementeren: IIS Web-App implementeren** taak tooconfigure uw IIS-instantie instellingen als volgt:</span><span class="sxs-lookup"><span data-stu-id="e6352-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="e6352-213">Voor **Websitenaam**, voer *standaardwebsite*.</span><span class="sxs-lookup"><span data-stu-id="e6352-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="e6352-214">Laat alle Hallo andere standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="e6352-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="e6352-215">Kies **opslaan**, selecteer daarna **OK** twee keer.</span><span class="sxs-lookup"><span data-stu-id="e6352-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="e6352-216">Een releaserecord maken en publiceren</span><span class="sxs-lookup"><span data-stu-id="e6352-216">Create a release and publish</span></span>
<span data-ttu-id="e6352-217">U kunt nu uw web-push pakket als een nieuwe release implementeren.</span><span class="sxs-lookup"><span data-stu-id="e6352-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="e6352-218">Deze stap communiceert met de Hallo-agent op elke instantie die deel uitmaakt van de implementatiegroep hello, pushes Hallo web pakket implementeren en vervolgens configureert u IIS-webtoepassing voor toorun Hallo bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e6352-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="e6352-219">Selecteer in de definitie van de release **+ Release**, en kies vervolgens **maken Release**.</span><span class="sxs-lookup"><span data-stu-id="e6352-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="e6352-220">Controleer of de laatste build Hallo is geselecteerd in de vervolgkeuzelijst hello, samen met **geautomatiseerde implementatie: na het maken van de release**.</span><span class="sxs-lookup"><span data-stu-id="e6352-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="e6352-221">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="e6352-221">Select **Create**.</span></span>
3. <span data-ttu-id="e6352-222">Een kleine weergegeven dat aan de bovenkant Hallo van de definitie van de release, zoals *Release Release-1 is aangemaakt*.</span><span class="sxs-lookup"><span data-stu-id="e6352-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="e6352-223">Selecteer Hallo release-koppeling.</span><span class="sxs-lookup"><span data-stu-id="e6352-223">Select hello release link.</span></span>
4. <span data-ttu-id="e6352-224">Open Hallo **logboeken** tabblad toowatch Hallo release uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Geslaagde teamservices release en web implementeren push pakket](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="e6352-226">Nadat het Hallo-release is voltooid, open een webbrowser en Voer Hallo openbare IPP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e6352-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="e6352-227">Uw ASP.NET-webtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-227">Your ASP.NET web application is running.</span></span>

    ![ASP.NET-web-app uitgevoerd op IIS VM](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="e6352-229">Test Hallo hele CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="e6352-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="e6352-230">Met uw webtoepassing die wordt uitgevoerd op IIS, probeer het nu Hallo hele CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="e6352-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="e6352-231">Nadat u een wijziging aanbrengt in Visual Studio en doorvoeren uw code, een build wordt geactiveerd, die vervolgens een versie van uw web-bijgewerkte activeert, pakket tooIIS implementeren:</span><span class="sxs-lookup"><span data-stu-id="e6352-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="e6352-232">Open in Visual Studio Hallo **Solution Explorer** venster.</span><span class="sxs-lookup"><span data-stu-id="e6352-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="e6352-233">Navigeer tooand open *myWebApp | Weergaven | Start | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="e6352-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="e6352-234">Regel 6 tooread bewerken:</span><span class="sxs-lookup"><span data-stu-id="e6352-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="e6352-235">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="e6352-235">Save hello file.</span></span>
5. <span data-ttu-id="e6352-236">Open Hallo **Team Explorer** venster, selecteer Hallo *myWebApp* project en kies vervolgens **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="e6352-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="e6352-237">Voer een bericht doorvoeren, zoals *testen CI/CD-pijplijn*, en kies vervolgens **alle doorvoeren en Sync** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6352-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="e6352-238">In de werkruimte Team Services, wordt een nieuwe build van Hallo code commit geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="e6352-239">Kies **bouwen & Release**, selecteer daarna **Builds**.</span><span class="sxs-lookup"><span data-stu-id="e6352-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="e6352-240">Kies de definitie van de build en selecteer vervolgens Hallo **in de wachtrij geplaatst & uitgevoerd** build toowatch als Hallo bouwen verloopt.</span><span class="sxs-lookup"><span data-stu-id="e6352-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="e6352-241">Wanneer Hallo build voltooid is, wordt een nieuwe release wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="e6352-242">Kies **bouwen & Release**, klikt u vervolgens **Releases** toosee hello webimplementatiepakket tooyour IIS VM gepusht.</span><span class="sxs-lookup"><span data-stu-id="e6352-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="e6352-243">Selecteer Hallo **vernieuwen** pictogram tooupdate Hallo status.</span><span class="sxs-lookup"><span data-stu-id="e6352-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="e6352-244">Wanneer Hallo *omgevingen* kolom ziet u een groen vinkje, Hallo release tooIIS is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e6352-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="e6352-245">de wijzigingen toegepast, toosee, vernieuw uw IIS-website in een browser.</span><span class="sxs-lookup"><span data-stu-id="e6352-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![ASP.NET-web-app uitgevoerd op IIS VM vanuit CI/CD-pipeline](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="e6352-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6352-247">Next steps</span></span>

<span data-ttu-id="e6352-248">In deze zelfstudie maakt u een ASP.NET-webtoepassing hebt gemaakt in Team Services en geconfigureerde build en release definities toodeploy nieuwe web implementeert pakketten tooIIS op elke doorvoer code.</span><span class="sxs-lookup"><span data-stu-id="e6352-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="e6352-249">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="e6352-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e6352-250">Een ASP.NET-toepassing tooa Team Services webproject publiceren</span><span class="sxs-lookup"><span data-stu-id="e6352-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="e6352-251">Een build-definitie die wordt geactiveerd door doorvoeracties code maken</span><span class="sxs-lookup"><span data-stu-id="e6352-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="e6352-252">IIS installeren en configureren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="e6352-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="e6352-253">Hallo IIS tooa implementatie instantiegroep in Team Services toevoegen</span><span class="sxs-lookup"><span data-stu-id="e6352-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="e6352-254">Maak een nieuwe website voor release definitie toopublish pakketten tooIIS implementeren</span><span class="sxs-lookup"><span data-stu-id="e6352-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="e6352-255">Test Hallo CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="e6352-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="e6352-256">Hoe gaan van de volgende zelfstudie toolearn toohello toosecure een webserver met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="e6352-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6352-257">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="e6352-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)