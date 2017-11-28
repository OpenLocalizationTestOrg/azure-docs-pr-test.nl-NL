---
title: Een CI/CD-pijplijn maken in Azure met Team Services | Microsoft Docs
description: Informatie over het maken van een pijplijn Visual Studio Team Services voor continue integratie en levering die een web-app in IIS op een virtuele machine van Windows implementeert
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
ms.openlocfilehash: a587f58fad2ec74c7633823c4d34f900e7c01f7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="2af9f-103">Een continue integratie-pijplijn maken met Visual Studio Team Services en IIS</span><span class="sxs-lookup"><span data-stu-id="2af9f-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="2af9f-104">Voor het automatiseren van de build-, test- en implementatie fasen van de ontwikkeling van toepassingen, kunt u een continue integratie en implementatie (CI/CD) pijplijn.</span><span class="sxs-lookup"><span data-stu-id="2af9f-104">To automate the build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="2af9f-105">In deze zelfstudie maakt u een CI/CD-pijplijn met Visual Studio Team Services en virtuele Windows-machine (VM) in Azure waarop IIS wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="2af9f-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="2af9f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2af9f-107">ASP.NET-webtoepassing op een project Team Services publiceren</span><span class="sxs-lookup"><span data-stu-id="2af9f-107">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="2af9f-108">Een build-definitie die wordt geactiveerd door doorvoeracties code maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="2af9f-109">IIS installeren en configureren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="2af9f-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="2af9f-110">Het IIS-exemplaar toevoegen aan een implementatiegroep in Team Services</span><span class="sxs-lookup"><span data-stu-id="2af9f-110">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="2af9f-111">Maken van een release definitie voor het publiceren van nieuwe web implementeren van pakketten naar IIS</span><span class="sxs-lookup"><span data-stu-id="2af9f-111">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="2af9f-112">De pijplijn CI/CD testen</span><span class="sxs-lookup"><span data-stu-id="2af9f-112">Test the CI/CD pipeline</span></span>

<span data-ttu-id="2af9f-113">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="2af9f-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2af9f-114">Voer `Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-114">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="2af9f-115">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2af9f-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="2af9f-116">Project maken in een Team Services</span><span class="sxs-lookup"><span data-stu-id="2af9f-116">Create project in Team Services</span></span>
<span data-ttu-id="2af9f-117">Visual Studio Team Services kunt u eenvoudig samenwerking en ontwikkeling zonder het onderhouden van een on-premises-oplossing voor het beheer van code.</span><span class="sxs-lookup"><span data-stu-id="2af9f-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="2af9f-118">Teamservices biedt cloud code testen, build en application insights.</span><span class="sxs-lookup"><span data-stu-id="2af9f-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="2af9f-119">U kunt een besturingselement-repo-versie en IDE die het beste past bij de ontwikkeling van uw code.</span><span class="sxs-lookup"><span data-stu-id="2af9f-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="2af9f-120">Voor deze zelfstudie kunt u een gratis account om een eenvoudige ASP.NET-web-app en CI/CD-pijplijn te maken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-120">For this tutorial, you can use a free account to create a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="2af9f-121">Als u nog geen een Team Services-account [maken van een](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="2af9f-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="2af9f-122">Het proces van de commit code beheren, definities bouwen en definities release, in een project maakt Team Services als volgt:</span><span class="sxs-lookup"><span data-stu-id="2af9f-122">To manage the code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="2af9f-123">Open uw dashboard Team Services in een webbrowser en kies **nieuw project**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="2af9f-124">Voer *myWebApp* voor de **projectnaam**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-124">Enter *myWebApp* for the **Project name**.</span></span> <span data-ttu-id="2af9f-125">Alle andere standaardwaarden gebruiken laat *Git* versiebeheer en *Agile* proces werkitem.</span><span class="sxs-lookup"><span data-stu-id="2af9f-125">Leave all other default values to use *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="2af9f-126">Kies de optie **delen met** *teamleden*, selecteer daarna **maken**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-126">Choose the option to **Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="2af9f-127">Wanneer uw project is gemaakt, kiest u de optie voor het **initialiseren met een Leesmij-bestand of gitignore**, klikt u vervolgens **initialiseren**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-127">Once your project has been created, choose the option to **Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="2af9f-128">Kies in het nieuwe project **Dashboards** aan de bovenkant Selecteer **openen in Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-128">Inside your new project, choose **Dashboards** across the top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="2af9f-129">ASP.NET-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-129">Create ASP.NET web application</span></span>
<span data-ttu-id="2af9f-130">In de vorige stap hebt u een project in Team Services gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2af9f-130">In the previous step, you created a project in Team Services.</span></span> <span data-ttu-id="2af9f-131">De laatste stap wordt het nieuwe project in Visual Studio geopend.</span><span class="sxs-lookup"><span data-stu-id="2af9f-131">The final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="2af9f-132">Beheren van uw code doorvoeringen in de **Team Explorer** venster.</span><span class="sxs-lookup"><span data-stu-id="2af9f-132">You manage your code commits in the **Team Explorer** window.</span></span> <span data-ttu-id="2af9f-133">Maken van een lokale kopie van het nieuwe project en maak vervolgens een ASP.NET-webtoepassing vanuit een sjabloon als volgt:</span><span class="sxs-lookup"><span data-stu-id="2af9f-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="2af9f-134">Selecteer **kloon** naar een lokale git-opslagplaats van uw Team Services-project maken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-134">Select **Clone** to create a local git repo of your Team Services project.</span></span>
    
    ![De opslagplaats klonen uit Team Services-project](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="2af9f-136">Onder **oplossingen**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-136">Under **Solutions**, select **New**.</span></span>

    ![Oplossing voor webtoepassing maken](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="2af9f-138">Selecteer **Web** sjablonen, en kies vervolgens de **ASP.NET-webtoepassing** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="2af9f-138">Select **Web** templates, and then choose the **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="2af9f-139">Voer een naam voor uw toepassing, zoals *myWebApp*, en schakel het selectievakje uit voor **map voor oplossing maken**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-139">Enter a name for your application, such as *myWebApp*, and uncheck the box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="2af9f-140">Als de optie beschikbaar is, schakelt u het selectievakje **Application Insights toevoegen aan project**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-140">If the option is available, uncheck the box to **Add Application Insights to project**.</span></span> <span data-ttu-id="2af9f-141">Application Insights moet u uw webtoepassing met Azure Application Insights autoriseren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-141">Application Insights requires you to authorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="2af9f-142">Het gemak in deze zelfstudie houden, moet u dit proces overslaan.</span><span class="sxs-lookup"><span data-stu-id="2af9f-142">To keep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="2af9f-143">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-143">Select **OK**.</span></span>
4. <span data-ttu-id="2af9f-144">Kies **MVC** uit de lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2af9f-144">Choose **MVC** from the template list.</span></span>
    1. <span data-ttu-id="2af9f-145">Selecteer **verificatie wijzigen**, kies **geen verificatie**, selecteer daarna **OK**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="2af9f-146">Selecteer **OK** om uw oplossing te maken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-146">Select **OK** to create your solution.</span></span>
5. <span data-ttu-id="2af9f-147">In de **Team Explorer** venster kiezen **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-147">In the **Team Explorer** window, choose **Changes**.</span></span>

    ![Lokale wijzigingen doorvoeren aan Team Services git-opslagplaats](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="2af9f-149">Voer in het tekstvak commit een bericht zoals *initiële doorvoeren*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-149">In the commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="2af9f-150">Kies **alle doorvoeren en Sync** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2af9f-150">Choose **Commit All and Sync** from the drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="2af9f-151">Build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-151">Create build definition</span></span>
<span data-ttu-id="2af9f-152">In het Team Services gebruikt u de definitie van een build als overzicht van hoe uw toepassing moet worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="2af9f-152">In Team Services, you use a build definition to outline how your application should be built.</span></span> <span data-ttu-id="2af9f-153">In deze zelfstudie maken we een basisdefinitie die vergt onze broncode, bouwt de oplossing en maakt vervolgens web pakket die we gebruiken kunnen voor het uitvoeren van de web-app op een IIS-server implementeren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-153">In this tutorial, we create a basic definition that takes our source code, builds the solution, then creates web deploy package we can use to run the web app on an IIS server.</span></span>

1. <span data-ttu-id="2af9f-154">Kies in het project Team Services **bouwen & Release** bovenaan, selecteer **Builds**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-154">In your Team Services project, choose **Build & Release** across the top, then select **Builds**.</span></span>
3. <span data-ttu-id="2af9f-155">Selecteer **+ nieuwe definitie**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="2af9f-156">Kies de **ASP.NET (PREVIEW)** sjabloon en selecteer **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-156">Choose the **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="2af9f-157">Laat de standaardwaarde taak waarden.</span><span class="sxs-lookup"><span data-stu-id="2af9f-157">Leave all the default task values.</span></span> <span data-ttu-id="2af9f-158">Onder **bronnen ophalen**, zorg ervoor dat de *myWebApp* opslagplaats en *master* vertakking worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-158">Under **Get sources**, ensure that the *myWebApp* repository and *master* branch are selected.</span></span>

    ![Definitie van de build in Team Services-project maken](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="2af9f-160">Op de **Triggers** tabblad, verplaats de schuifregelaar voor **inschakelen van deze trigger** naar *ingeschakeld*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-160">On the **Triggers** tab, move the slider for **Enable this trigger** to *Enabled*.</span></span>
7. <span data-ttu-id="2af9f-161">De definitie van de build en de wachtrij een nieuwe build opslaan door **opslaan en wachtrij** , vervolgens **opslaan en wachtrij** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2af9f-161">Save the build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="2af9f-162">Laat de standaardwaarden en selecteer **wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-162">Leave the defaults and select **Queue**.</span></span>

<span data-ttu-id="2af9f-163">Bekijk begint als de build is gepland op een gehoste agent vervolgens om samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="2af9f-163">Watch as the build is scheduled on a hosted agent, then begins to build.</span></span> <span data-ttu-id="2af9f-164">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2af9f-164">The output is similar to the following example:</span></span>

![Geslaagde build van het Team Services-project](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="2af9f-166">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-166">Create virtual machine</span></span>
<span data-ttu-id="2af9f-167">Als u een platform voor het uitvoeren van uw ASP.NET-web-app maken, moet u een virtuele Windows-machine waarop IIS wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-167">To provide a platform to run your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="2af9f-168">Teamservices maakt gebruik van een agent om te communiceren met het IIS-exemplaar als u code doorvoert en builds worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-168">Team Services uses an agent to interact with the IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="2af9f-169">Maak een VM van Windows Server 2016 met [dit voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2af9f-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="2af9f-170">Het duurt enkele minuten duren voordat het script uitvoeren en de virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-170">It takes a few minutes for the script to run and create the VM.</span></span> <span data-ttu-id="2af9f-171">Zodra de virtuele machine is gemaakt, opent u poort 80 voor internetverkeer met [toevoegen AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) als volgt:</span><span class="sxs-lookup"><span data-stu-id="2af9f-171">Once the VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

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

<span data-ttu-id="2af9f-172">Verkrijgen voor verbinding met uw virtuele machine, het openbare IP-adres met [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) als volgt:</span><span class="sxs-lookup"><span data-stu-id="2af9f-172">To connect to your VM, obtain the public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="2af9f-173">Een extern-bureaubladsessie met uw virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="2af9f-173">Create a remote desktop session to your VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="2af9f-174">Open op de virtuele machine, een **beheerder PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="2af9f-174">On the VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="2af9f-175">IIS en de vereiste .NET-functies als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="2af9f-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="2af9f-176">Implementatiegroep maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-176">Create deployment group</span></span>
<span data-ttu-id="2af9f-177">Voor de push-uit het web pakket implementeren op de IIS-server, het definiëren van een implementatiegroep in een Team Services.</span><span class="sxs-lookup"><span data-stu-id="2af9f-177">To push out the web deploy package to the IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="2af9f-178">Deze groep kunt u opgeven welke servers zijn het doel van de nieuwe builds u code doorvoert naar Team Services en builds zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="2af9f-178">This group allows you to specify which servers are the target of new builds as you commit code to Team Services and builds are completed.</span></span>

1. <span data-ttu-id="2af9f-179">Kies in het Team Services, **bouwen & Release** en selecteer vervolgens **implementatiegroepen**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="2af9f-180">Kies **implementatie toevoegen groep**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="2af9f-181">Voer een naam voor de groep, zoals *myIIS*, selecteer daarna **maken**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-181">Enter a name for the group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="2af9f-182">In de **machines registreren** sectie, moet u zorgen *Windows* is ingeschakeld, wordt het selectievakje **gebruiken een persoonlijk toegangstoken in het script voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-182">In the **Register machines** section, ensure *Windows* is selected, then check the box to **Use a personal access token in the script for authentication**.</span></span>
5. <span data-ttu-id="2af9f-183">Selecteer **script kopiëren naar Klembord**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-183">Select **Copy script to clipboard**.</span></span>


### <a name="add-iis-vm-to-the-deployment-group"></a><span data-ttu-id="2af9f-184">IIS VM toevoegen aan de implementatiegroep</span><span class="sxs-lookup"><span data-stu-id="2af9f-184">Add IIS VM to the deployment group</span></span>
<span data-ttu-id="2af9f-185">Toevoegen aan de implementatiegroep is gemaakt, elke IIS-exemplaar aan de groep.</span><span class="sxs-lookup"><span data-stu-id="2af9f-185">With the deployment group created, add each IIS instance to the group.</span></span> <span data-ttu-id="2af9f-186">Teamservices genereert een script dat downloadt en configureert u een agent op de virtuele machine die nieuw web ontvangt pakketten implementeren en vervolgens toegepast op IIS.</span><span class="sxs-lookup"><span data-stu-id="2af9f-186">Team Services generates a script that downloads and configures an agent on the VM that receives new web deploy packages then applies it to IIS.</span></span>

1. <span data-ttu-id="2af9f-187">Terug in de **beheerder PowerShell** sessie op de virtuele machine, plakken en voer het script dat is opgehaald uit het Team Services.</span><span class="sxs-lookup"><span data-stu-id="2af9f-187">Back in the **Administrator PowerShell** session on your VM, paste and run the script copied from Team Services.</span></span>
2. <span data-ttu-id="2af9f-188">Wanneer u wordt gevraagd voor het configureren van de labels voor de agent, kies *Y* en voer *web*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-188">When prompted to configure tags for the agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="2af9f-189">Wanneer u daarom wordt gevraagd voor het gebruikersaccount op te geven, drukt u op *retourneren* de standaardwaarden accepteren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-189">When prompted for the user account, press *Return* to accept the defaults.</span></span>
4. <span data-ttu-id="2af9f-190">Wacht totdat het script voltooid met een bericht *vstsagent.account.computername Service is gestart*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-190">Wait for the script to finish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="2af9f-191">In de **implementatiegroepen** pagina van de **bouwen & Release** menu openen de *myIIS* implementatiegroep.</span><span class="sxs-lookup"><span data-stu-id="2af9f-191">In the **Deployment groups** page of the **Build & Release** menu, open the *myIIS* deployment group.</span></span> <span data-ttu-id="2af9f-192">Op de **Machines** tabblad, controleert u of uw virtuele machine wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2af9f-192">On the **Machines** tab, verify that your VM is listed.</span></span>

    ![Virtuele machine is toegevoegd aan het Team Services, implementatiegroep](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="2af9f-194">Release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-194">Create release definition</span></span>
<span data-ttu-id="2af9f-195">Voor het publiceren van uw builds, maakt u een definitie van een release in Team Services.</span><span class="sxs-lookup"><span data-stu-id="2af9f-195">To publish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="2af9f-196">Deze definitie wordt automatisch geactiveerd door een geslaagde build van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2af9f-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="2af9f-197">Kies van de implementatiegroep voor de push-uw web-pakket te implementeren en de juiste IIS-instellingen te definiëren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-197">You choose the deployment group to push your web deploy package to, and define the appropriate IIS settings.</span></span>

1. <span data-ttu-id="2af9f-198">Kies **bouwen & Release**, selecteer daarna **Builds**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="2af9f-199">Kies de definitie van de build in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2af9f-199">Choose the build definition created in a previous step.</span></span>
2. <span data-ttu-id="2af9f-200">Onder **onlangs voltooid**, kiest u de meest recente build en selecteer vervolgens **Release**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-200">Under **Recently completed**, choose the most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="2af9f-201">Kies **Ja** een release-definitie maken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-201">Choose **Yes** to create a release definition.</span></span>
4. <span data-ttu-id="2af9f-202">Kies de **leeg** sjabloon, selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-202">Choose the **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="2af9f-203">Controleer of de definitie van de build-project en de bron zijn gevuld met uw project.</span><span class="sxs-lookup"><span data-stu-id="2af9f-203">Verify the project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="2af9f-204">Selecteer de **continue implementatie** in en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-204">Select the **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="2af9f-205">Selecteer de vervolgkeuzelijst naast **+ taken toevoegen** en kies *toevoegen van een groep implementatiefase*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-205">Select the drop-down box next to **+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Taak release definitie in Team Services toevoegen](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="2af9f-207">Kies **toevoegen** naast **IIS Web-App Deploy(Preview)**, selecteer daarna **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-207">Choose **Add** next to **IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="2af9f-208">Selecteer de **uitvoeren op implementatiegroep** bovenliggende taak.</span><span class="sxs-lookup"><span data-stu-id="2af9f-208">Select the **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="2af9f-209">Voor **Implementatiegroep**, selecteert u de implementatiegroep die u eerder hebt gemaakt, zoals *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-209">For **Deployment Group**, select the deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="2af9f-210">In de **Machine labels** de optie **toevoegen** en kies de *web* label.</span><span class="sxs-lookup"><span data-stu-id="2af9f-210">In the **Machine tags** box, select **Add** and choose the *web* tag.</span></span>
    
    ![De definitie van implementatie groepstaak vrijgeven voor IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="2af9f-212">Selecteer de **implementeren: IIS Web-App implementeren** taak voor het configureren van de IIS-exemplaar-instellingen als volgt:</span><span class="sxs-lookup"><span data-stu-id="2af9f-212">Select the **Deploy: IIS Web App Deploy** task to configure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="2af9f-213">Voor **Websitenaam**, voer *standaardwebsite*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="2af9f-214">Laat alle andere standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="2af9f-214">Leave all the other default settings.</span></span>
12. <span data-ttu-id="2af9f-215">Kies **opslaan**, selecteer daarna **OK** twee keer.</span><span class="sxs-lookup"><span data-stu-id="2af9f-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="2af9f-216">Een releaserecord maken en publiceren</span><span class="sxs-lookup"><span data-stu-id="2af9f-216">Create a release and publish</span></span>
<span data-ttu-id="2af9f-217">U kunt nu uw web-push pakket als een nieuwe release implementeren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="2af9f-218">Deze stap communiceert met de agent op elke instantie die deel uitmaakt van de implementatiegroep, stuurt het web pakket implementeren en vervolgens configureert u IIS voor het uitvoeren van de bijgewerkte webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2af9f-218">This step communicates with the agent on each instance that is part of the deployment group, pushes the web deploy package, then configures IIS to run the updated web application.</span></span>

1. <span data-ttu-id="2af9f-219">Selecteer in de definitie van de release **+ Release**, en kies vervolgens **maken Release**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="2af9f-220">Controleer of de laatste build is geselecteerd in de vervolgkeuzelijst samen met **geautomatiseerde implementatie: na het maken van de release**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-220">Verify that the latest build is selected in the drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="2af9f-221">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-221">Select **Create**.</span></span>
3. <span data-ttu-id="2af9f-222">Een kort weergegeven dat aan de bovenkant van de definitie van de release, zoals *Release Release-1 is aangemaakt*.</span><span class="sxs-lookup"><span data-stu-id="2af9f-222">A small banner appears across the top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="2af9f-223">Selecteer de koppeling release.</span><span class="sxs-lookup"><span data-stu-id="2af9f-223">Select the release link.</span></span>
4. <span data-ttu-id="2af9f-224">Open de **logboeken** tabblad bekijkt u de voortgang van de release.</span><span class="sxs-lookup"><span data-stu-id="2af9f-224">Open the **Logs** tab to watch the release progress.</span></span>
    
    ![Geslaagde teamservices release en web implementeren push pakket](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="2af9f-226">Nadat de release voltooid is, open een webbrowser en voer het openbare IPP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2af9f-226">After the release is complete, open a web browser and enter the public IIP address of your VM.</span></span> <span data-ttu-id="2af9f-227">Uw ASP.NET-webtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-227">Your ASP.NET web application is running.</span></span>

    ![ASP.NET-web-app uitgevoerd op IIS VM](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-the-whole-cicd-pipeline"></a><span data-ttu-id="2af9f-229">Testen van de hele CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="2af9f-229">Test the whole CI/CD pipeline</span></span>
<span data-ttu-id="2af9f-230">Bij uw webtoepassing die wordt uitgevoerd op IIS, probeert u nu de hele CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="2af9f-230">With your web application running on IIS, now try the whole CI/CD pipeline.</span></span> <span data-ttu-id="2af9f-231">Nadat u een wijziging aanbrengt in Visual Studio en doorvoeren uw code, een build wordt geactiveerd, die vervolgens een versie van uw web-bijgewerkte activeert, pakket implementeren naar IIS:</span><span class="sxs-lookup"><span data-stu-id="2af9f-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package to IIS:</span></span>

1. <span data-ttu-id="2af9f-232">Open in Visual Studio de **Solution Explorer** venster.</span><span class="sxs-lookup"><span data-stu-id="2af9f-232">In Visual Studio, open the **Solution Explorer** window.</span></span>
2. <span data-ttu-id="2af9f-233">Blader naar en open *myWebApp | Weergaven | Start | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="2af9f-233">Navigate to and open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="2af9f-234">Regel 6 lezen bewerken:</span><span class="sxs-lookup"><span data-stu-id="2af9f-234">Edit line 6 to read:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="2af9f-235">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="2af9f-235">Save the file.</span></span>
5. <span data-ttu-id="2af9f-236">Open de **Team Explorer** Selecteer de *myWebApp* project en kies vervolgens **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-236">Open the **Team Explorer** window, select the *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="2af9f-237">Voer een bericht doorvoeren, zoals *testen CI/CD-pijplijn*, en kies vervolgens **alle doorvoeren en Sync** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2af9f-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from the drop-down menu.</span></span>
7. <span data-ttu-id="2af9f-238">In de werkruimte Team Services, wordt een nieuwe build van het code-doorvoeren geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-238">In Team Services workspace, a new build is triggered from the code commit.</span></span> 
    - <span data-ttu-id="2af9f-239">Kies **bouwen & Release**, selecteer daarna **Builds**.</span><span class="sxs-lookup"><span data-stu-id="2af9f-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="2af9f-240">Kies de definitie van de build en selecteer vervolgens de **in de wachtrij geplaatst & uitgevoerd** build moet letten tijdens de voortgang van de build.</span><span class="sxs-lookup"><span data-stu-id="2af9f-240">Choose your build definition, then select the **Queued & running** build to watch as the build progresses.</span></span>
9. <span data-ttu-id="2af9f-241">Wanneer de build voltooid is, wordt een nieuwe release wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2af9f-241">Once the build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="2af9f-242">Kies **bouwen & Release**, klikt u vervolgens **Releases** om te zien van het web naar uw VM IIS gepusht pakket implementeren.</span><span class="sxs-lookup"><span data-stu-id="2af9f-242">Choose **Build & Release**, then **Releases** to see the web deploy package pushed to your IIS VM.</span></span> 
    - <span data-ttu-id="2af9f-243">Selecteer de **vernieuwen** pictogram om de status te werken.</span><span class="sxs-lookup"><span data-stu-id="2af9f-243">Select the **Refresh** icon to update the status.</span></span> <span data-ttu-id="2af9f-244">Wanneer de *omgevingen* kolom ziet u een groen vinkje, de versie is geïmplementeerd naar IIS.</span><span class="sxs-lookup"><span data-stu-id="2af9f-244">When the *Environments* column shows a green check mark, the release has successfully deployed to IIS.</span></span>
11. <span data-ttu-id="2af9f-245">Overzicht van uw wijzigingen zijn toegepast, uw IIS-website in een browser te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="2af9f-245">To see your changes applied, refresh your IIS website in a browser.</span></span>

    ![ASP.NET-web-app uitgevoerd op IIS VM vanuit CI/CD-pipeline](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="2af9f-247">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2af9f-247">Next steps</span></span>

<span data-ttu-id="2af9f-248">In deze zelfstudie maakt u een ASP.NET-webtoepassing in een Team Services gemaakt en geconfigureerd build en release definities voor het implementeren van nieuwe web implementeren van pakketten naar IIS op elke doorvoer code.</span><span class="sxs-lookup"><span data-stu-id="2af9f-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions to deploy new web deploy packages to IIS on each code commit.</span></span> <span data-ttu-id="2af9f-249">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="2af9f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2af9f-250">ASP.NET-webtoepassing op een project Team Services publiceren</span><span class="sxs-lookup"><span data-stu-id="2af9f-250">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="2af9f-251">Een build-definitie die wordt geactiveerd door doorvoeracties code maken</span><span class="sxs-lookup"><span data-stu-id="2af9f-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="2af9f-252">IIS installeren en configureren op een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="2af9f-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="2af9f-253">Het IIS-exemplaar toevoegen aan een implementatiegroep in Team Services</span><span class="sxs-lookup"><span data-stu-id="2af9f-253">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="2af9f-254">Maken van een release definitie voor het publiceren van nieuwe web implementeren van pakketten naar IIS</span><span class="sxs-lookup"><span data-stu-id="2af9f-254">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="2af9f-255">De pijplijn CI/CD testen</span><span class="sxs-lookup"><span data-stu-id="2af9f-255">Test the CI/CD pipeline</span></span>

<span data-ttu-id="2af9f-256">Ga naar de volgende zelfstudie voor meer informatie over het beveiligen van een webserver met SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="2af9f-256">Advance to the next tutorial to learn how to secure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2af9f-257">Webserver met SSL beveiligde</span><span class="sxs-lookup"><span data-stu-id="2af9f-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)