---
title: Aan de slag met Azure Automation DSC | Microsoft Docs
description: Uitleg en voorbeelden van de meest algemene taken in Azure Automation Desired State Configuration (DSC)
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="4064a-103">Aan de slag met Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4064a-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="4064a-104">Dit onderwerp wordt uitgelegd hoe u de meest algemene taken met Azure Automation Desired State Configuration (DSC), zoals het maken, importeren, en compileren configuraties, voorbereiding-machines te beheren, en het weergeven van rapporten.</span><span class="sxs-lookup"><span data-stu-id="4064a-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="4064a-105">Zie voor een overzicht van wat Azure Automation DSC is, [overzicht van Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4064a-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="4064a-106">Zie voor documentatie DSC [Windows PowerShell Desired Configuration overzicht](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="4064a-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="4064a-107">Dit onderwerp bevat een stapsgewijze handleiding voor het gebruik van Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="4064a-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="4064a-108">Als u een Voorbeeldomgeving is al ingesteld zonder dat u de stappen in dit onderwerp beschreven wilt, kunt u [de volgende ARM-sjabloon](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="4064a-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="4064a-109">Deze sjabloon stelt u een voltooide Azure Automation DSC-omgeving, met inbegrip van een virtuele machine van Azure die wordt beheerd door Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="4064a-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4064a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4064a-110">Prerequisites</span></span>
<span data-ttu-id="4064a-111">Het volgende is vereist voor het voltooien van de voorbeelden in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="4064a-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="4064a-112">Een Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-112">An Azure Automation account.</span></span> <span data-ttu-id="4064a-113">Zie voor instructies over het maken van een Azure Automation Run As-account voor [Azure uitvoeren als-Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="4064a-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="4064a-114">Een Azure Resource Manager VM (niet-klassieke) met Windows Server 2008 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4064a-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="4064a-115">Zie voor instructies over het maken van een virtuele machine [uw eerste virtuele Windows-machine maken in de Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="4064a-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="4064a-116">Maken van een DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="4064a-116">Creating a DSC configuration</span></span>
<span data-ttu-id="4064a-117">We gaan een eenvoudige maken [DSC-configuratie](https://msdn.microsoft.com/powershell/dsc/configurations) die ervoor zorgt de aanwezigheid of afwezigheid van de **webserver** Windows functie (IIS), afhankelijk van hoe u knooppunten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="4064a-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="4064a-118">Start de Windows PowerShell ISE (of een teksteditor).</span><span class="sxs-lookup"><span data-stu-id="4064a-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="4064a-119">Typ de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4064a-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="4064a-120">Sla het bestand als `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="4064a-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="4064a-121">Deze configuratie een resource in elk blok knooppunt roept de [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), die zorgt ervoor dat de aanwezigheid of afwezigheid van de **webserver** functie.</span><span class="sxs-lookup"><span data-stu-id="4064a-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="4064a-122">Een configuratie te importeren in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4064a-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="4064a-123">We je de configuratie vervolgens importeren in het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="4064a-124">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-125">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-126">Op de **Automation-account** blade, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="4064a-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="4064a-127">Op de **DSC-configuraties** blade, klikt u op **toevoegen van een configuratie**.</span><span class="sxs-lookup"><span data-stu-id="4064a-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="4064a-128">Op de **configuratie importeren** blade, blader naar de `TestConfig.ps1` bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4064a-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Schermafbeelding van de ** importeren configuratie ** blade](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="4064a-130">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4064a-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="4064a-131">Een configuratie weergeven in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4064a-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="4064a-132">Nadat u een configuratie hebt geïmporteerd, kunt u deze bekijken in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4064a-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="4064a-133">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-134">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-135">Op de **Automation-account** blade, klikt u op **DSC-configuraties**</span><span class="sxs-lookup"><span data-stu-id="4064a-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="4064a-136">Op de **DSC-configuraties** blade, klikt u op **TestConfig** (dit is de naam van de configuratie die u hebt geïmporteerd in de vorige procedure).</span><span class="sxs-lookup"><span data-stu-id="4064a-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="4064a-137">Op de **TestConfig configuratie** blade, klikt u op **weergave configuratiebron**.</span><span class="sxs-lookup"><span data-stu-id="4064a-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Schermafbeelding van het tabblad TestConfig-configuratie](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="4064a-139">Een **TestConfig configuratiebron** blade wordt geopend, om de PowerShell-code voor de configuratie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4064a-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="4064a-140">Een Azure Automation-configuratie compileren</span><span class="sxs-lookup"><span data-stu-id="4064a-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="4064a-141">Voordat u een gewenste status op een knooppunt toepassen kunt, moet een DSC-configuratie definiëren die status worden gecompileerd naar een of meer knooppuntconfiguraties (MOF document) en op de Automation DSC-Pull-Server geplaatst.</span><span class="sxs-lookup"><span data-stu-id="4064a-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="4064a-142">Zie voor een gedetailleerdere beschrijving van het compileren van configuraties in Azure Automation DSC [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="4064a-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="4064a-143">Zie voor meer informatie over het compileren van configuraties [DSC-configuraties](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="4064a-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="4064a-144">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-145">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-146">Op de **Automation-account** blade, klikt u op **DSC-configuraties**</span><span class="sxs-lookup"><span data-stu-id="4064a-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="4064a-147">Op de **DSC-configuraties** blade, klikt u op **TestConfig** (de naam van de configuratie van de eerder geïmporteerd).</span><span class="sxs-lookup"><span data-stu-id="4064a-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="4064a-148">Op de **TestConfig configuratie** blade, klikt u op **compileren**, en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4064a-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="4064a-149">Hiermee start u een Compilatietaak.</span><span class="sxs-lookup"><span data-stu-id="4064a-149">This starts a compilation job.</span></span>
   
    ![Schermafbeelding van de TestConfig configuratie blade compileren knop markeren](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="4064a-151">Wanneer u een configuratie in Azure Automation compileert, worden automatisch alle gemaakte knooppuntconfiguratie MOF-bestanden naar de pull-server implementeert.</span><span class="sxs-lookup"><span data-stu-id="4064a-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="4064a-152">Een Compilatietaak weergeven</span><span class="sxs-lookup"><span data-stu-id="4064a-152">Viewing a compilation job</span></span>
<span data-ttu-id="4064a-153">Nadat u een compilatie start, kunt u het weergeven in de **compilatietaken** -tegel in de **configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="4064a-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="4064a-154">De **compilatietaken** tegel bevat momenteel wordt uitgevoerd, voltooid en mislukte taken.</span><span class="sxs-lookup"><span data-stu-id="4064a-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="4064a-155">Wanneer u een taak compilatie blade opent, ziet u informatie over deze taak inclusief eventuele fouten of waarschuwingen opgetreden, invoerparameters gebruikt in de configuratie en compilatie Logboeken.</span><span class="sxs-lookup"><span data-stu-id="4064a-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="4064a-156">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-157">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-158">Op de **Automation-account** blade, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="4064a-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="4064a-159">Op de **DSC-configuraties** blade, klikt u op **TestConfig** (de naam van de configuratie van de eerder geïmporteerd).</span><span class="sxs-lookup"><span data-stu-id="4064a-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="4064a-160">Op de **compilatietaken** tegel van de **TestConfig configuratie** blade, klik op een van de taken die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="4064a-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="4064a-161">Een **Compilatietaak** blade wordt geopend, gelabeld met de datum waarop de Compilatietaak is gestart.</span><span class="sxs-lookup"><span data-stu-id="4064a-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Schermafbeelding van het tabblad Compilatietaak](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="4064a-163">Klik op een tegel in de **Compilatietaak** blade om te zien om meer details over de taak.</span><span class="sxs-lookup"><span data-stu-id="4064a-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="4064a-164">Knooppuntconfiguraties weergeven</span><span class="sxs-lookup"><span data-stu-id="4064a-164">Viewing node configurations</span></span>
<span data-ttu-id="4064a-165">Voltooiing van een Compilatietaak maakt een of meer nieuwe knooppuntconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="4064a-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="4064a-166">De configuratie van een knooppunt is een MOF-document dat is geïmplementeerd naar de pull-server en klaar om te worden opgehaald en toegepast door een of meer knooppunten.</span><span class="sxs-lookup"><span data-stu-id="4064a-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="4064a-167">U kunt de knooppuntconfiguraties weergeven in uw Automation-account in de **DSC-knooppuntconfiguraties** blade.</span><span class="sxs-lookup"><span data-stu-id="4064a-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="4064a-168">De configuratie van een knooppunt heeft een naam met het formulier *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="4064a-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="4064a-169">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-170">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-171">Op de **Automation-account** blade, klikt u op **DSC-knooppuntconfiguraties**.</span><span class="sxs-lookup"><span data-stu-id="4064a-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Schermafbeelding van het tabblad DSC-knooppuntconfiguraties](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="4064a-173">Voorbereiden op een virtuele machine van Azure voor beheer met Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4064a-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="4064a-174">Azure Automation DSC kunt u virtuele Azure-machines (Classic en Resource Manager), lokale virtuele machines Linux machines, AWS virtuele machines en fysieke machines lokale beheren.</span><span class="sxs-lookup"><span data-stu-id="4064a-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="4064a-175">In dit onderwerp wordt uitgelegd hoe u kunt alleen Azure Resource Manager VM's vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="4064a-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="4064a-176">Zie voor informatie over de voorbereiding andere soorten machines, [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="4064a-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="4064a-177">Voorbereiden van een Azure Resource Manager VM voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4064a-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="4064a-178">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-179">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-180">Op de **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="4064a-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="4064a-181">In de **DSC-knooppunten** blade, klikt u op **toevoegen Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="4064a-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Schermafbeelding van het DSC-knooppunten tabblad markering van de knop toevoegen Azure VM](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="4064a-183">In de **Azure Virtual machines toevoegen** blade, klikt u op **selecteert u virtuele machines om vrij te geven**.</span><span class="sxs-lookup"><span data-stu-id="4064a-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="4064a-184">In de **Selecteer VMs** blade, selecteer de virtuele machine die u laten vrijgeven wilt en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4064a-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4064a-185">Dit moet een Azure Resource Manager-VM met Windows Server 2008 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4064a-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="4064a-186">In de **Azure Virtual machines toevoegen** blade, klikt u op **registratiegegevens configureren**.</span><span class="sxs-lookup"><span data-stu-id="4064a-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="4064a-187">In de **registratie** blade, voer de naam van de knooppuntconfiguratie die u wilt toepassen op de virtuele machine in de **knooppunt configuratienaam** vak.</span><span class="sxs-lookup"><span data-stu-id="4064a-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="4064a-188">Dit moet exact overeenkomen met de naam van de knooppuntconfiguratie van een in het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="4064a-189">Op dit moment een naam opgeven is optioneel.</span><span class="sxs-lookup"><span data-stu-id="4064a-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="4064a-190">U kunt de toegewezen knooppuntconfiguratie na het voorbereiden op het knooppunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4064a-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="4064a-191">Controleer **knooppunt opnieuw opstarten indien nodig**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4064a-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Schermafbeelding van de registratie-blade](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="4064a-193">De configuratie van het opgegeven worden toegepast op de virtuele machine met een interval dat is opgegeven door de **frequentie van de configuratiemodus**, en de virtuele machine wordt gecontroleerd op updates voor de knooppuntconfiguratie met een interval dat is opgegeven door de **vernieuwingsfrequentie**.</span><span class="sxs-lookup"><span data-stu-id="4064a-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="4064a-194">Zie voor meer informatie over het gebruik van deze waarden [configureren van de lokale Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="4064a-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="4064a-195">In de **Azure Virtual machines toevoegen** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4064a-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="4064a-196">Azure kan het proces van het voorbereiden op de virtuele machine wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4064a-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="4064a-197">Wanneer deze voltooid is, de virtuele machine wordt weergegeven in de **DSC-knooppunten** blade in de Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="4064a-198">De lijst van DSC-knooppunten</span><span class="sxs-lookup"><span data-stu-id="4064a-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="4064a-199">U kunt de lijst weergeven met alle machines die zijn vrijgegeven voor management in uw Automation-account in de **DSC-knooppunten** blade.</span><span class="sxs-lookup"><span data-stu-id="4064a-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="4064a-200">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-201">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-202">Op de **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="4064a-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="4064a-203">Weergeven van rapporten voor DSC-knooppunten</span><span class="sxs-lookup"><span data-stu-id="4064a-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="4064a-204">Elke keer dat Azure Automation DSC een consistentiecontrole uit op een beheerde knooppunt voert stuurt het knooppunt een statusrapport terug naar de pull-server.</span><span class="sxs-lookup"><span data-stu-id="4064a-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="4064a-205">U kunt deze rapporten kunt weergeven op de blade voor dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4064a-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="4064a-206">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-207">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-208">Op de **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="4064a-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="4064a-209">Op de **rapporten** tegel, klikt u op een van de rapporten in de lijst.</span><span class="sxs-lookup"><span data-stu-id="4064a-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Schermafbeelding van het tabblad rapport](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="4064a-211">Op de blade voor een afzonderlijk rapport, kunt u de volgende statusgegevens voor de bijbehorende consistentiecontrole zien:</span><span class="sxs-lookup"><span data-stu-id="4064a-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="4064a-212">De rapportstatus, of het knooppunt 'Compatibele', 'Mislukt' van de configuratie of het knooppunt is 'Niet-compatibel' (wanneer het knooppunt is in **applyandmonitor** modus en de machine zich niet in de gewenste status).</span><span class="sxs-lookup"><span data-stu-id="4064a-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="4064a-213">De begintijd voor de consistentiecontrole.</span><span class="sxs-lookup"><span data-stu-id="4064a-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="4064a-214">De totale runtime voor de consistentiecontrole.</span><span class="sxs-lookup"><span data-stu-id="4064a-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="4064a-215">Het type van een consistentiecontrole uit.</span><span class="sxs-lookup"><span data-stu-id="4064a-215">The type of consistency check.</span></span>
* <span data-ttu-id="4064a-216">Eventuele fouten, met inbegrip van de foutcode en het foutbericht.</span><span class="sxs-lookup"><span data-stu-id="4064a-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="4064a-217">Eventuele DSC-resources in de configuratie en de status van elke bron (of het knooppunt bevindt zich in de gewenste status voor die bron) gebruikt, kunt u klikken op elke bron voor meer gedetailleerde informatie voor die bron.</span><span class="sxs-lookup"><span data-stu-id="4064a-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="4064a-218">De naam, het IP-adres en de configuratiemodus van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4064a-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="4064a-219">U kunt ook klikken op **onbewerkte rapport weergeven** om te zien van de feitelijke gegevens die het knooppunt naar de server verzendt.</span><span class="sxs-lookup"><span data-stu-id="4064a-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="4064a-220">Zie voor meer informatie over het gebruik van die gegevens [met behulp van een DSC-rapportserver](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="4064a-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="4064a-221">Het kan even duren wanneer een knooppunt vrijgegeven is voordat het rapport eerste beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="4064a-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="4064a-222">U moet mogelijk wacht u tot 30 minuten voor het eerste rapport na u vrijgeven een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="4064a-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="4064a-223">Opnieuw toewijzen van een knooppunt naar een ander knooppunt-configuratie</span><span class="sxs-lookup"><span data-stu-id="4064a-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="4064a-224">U kunt een knooppunt als de configuratie van een ander knooppunt dan de die oorspronkelijk was toegewezen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4064a-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="4064a-225">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-226">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-227">Op de **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="4064a-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="4064a-228">Op de **DSC-knooppunten** blade, klik op de naam van het knooppunt dat u wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="4064a-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="4064a-229">Klik op de blade voor dat knooppunt **toewijzen knooppunt**.</span><span class="sxs-lookup"><span data-stu-id="4064a-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Schermafbeelding van het tabblad knooppunt is de knop toewijzen knooppunt markeren](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="4064a-231">Op de **knooppuntconfiguratie toewijzen** blade, selecteert u de knooppuntconfiguratie waarnaar u wilt toewijzen van het knooppunt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4064a-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Schermafbeelding van het tabblad knooppuntconfiguratie toewijzen](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="4064a-233">De registratie van een knooppunt</span><span class="sxs-lookup"><span data-stu-id="4064a-233">Unregistering a node</span></span>
<span data-ttu-id="4064a-234">Als u niet langer een knooppunt kan worden beheerd door Azure Automation DSC wilt, kunt u de registratie verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4064a-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="4064a-235">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4064a-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4064a-236">Klik in het menu Hub op **alle resources** en vervolgens de naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4064a-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="4064a-237">Op de **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="4064a-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="4064a-238">Op de **DSC-knooppunten** blade, klik op de naam van het knooppunt dat u wilt registratie.</span><span class="sxs-lookup"><span data-stu-id="4064a-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="4064a-239">Klik op de blade voor dat knooppunt **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="4064a-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Schermafbeelding van de markering van de knop Unregister knooppunt-blade](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="4064a-241">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="4064a-241">Related Articles</span></span>
* [<span data-ttu-id="4064a-242">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4064a-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="4064a-243">Computers voorbereiden voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4064a-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="4064a-244">Windows PowerShell Desired State Configuration-overzicht</span><span class="sxs-lookup"><span data-stu-id="4064a-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="4064a-245">Azure Automation DSC-cmdlets</span><span class="sxs-lookup"><span data-stu-id="4064a-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="4064a-246">Azure Automation DSC-prijzen</span><span class="sxs-lookup"><span data-stu-id="4064a-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

