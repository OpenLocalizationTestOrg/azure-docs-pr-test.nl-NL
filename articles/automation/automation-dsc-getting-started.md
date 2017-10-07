---
title: aaaGetting de slag met Azure Automation DSC | Microsoft Docs
description: Uitleg en voorbeelden van Hallo meest algemene taken in Azure Automation Desired State Configuration (DSC)
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="1b5c8-103">Aan de slag met Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="1b5c8-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="1b5c8-104">Dit onderwerp wordt uitgelegd hoe toodo Hallo meest algemene taken met Azure Automation Desired State Configuration (DSC), zoals het maken, importeren, en compileren configuraties, voorbereiding machines te beheren, en het weergeven van rapporten.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="1b5c8-105">Zie voor een overzicht van wat Azure Automation DSC is, [overzicht van Azure Automation DSC](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="1b5c8-106">Zie voor documentatie DSC [Windows PowerShell Desired Configuration overzicht](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="1b5c8-107">Dit onderwerp bevat een stapsgewijze handleiding toousing Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="1b5c8-108">Als u een Voorbeeldomgeving is al ingesteld zonder het Hallo-stappen die worden beschreven in dit onderwerp wilt, kunt u [Hallo volgende ARM-sjabloon](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="1b5c8-109">Deze sjabloon stelt u een voltooide Azure Automation DSC-omgeving, met inbegrip van een virtuele machine van Azure die wordt beheerd door Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b5c8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b5c8-110">Prerequisites</span></span>
<span data-ttu-id="1b5c8-111">toocomplete hello voorbeelden in dit onderwerp, Hallo volgende is vereist:</span><span class="sxs-lookup"><span data-stu-id="1b5c8-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="1b5c8-112">Een Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-112">An Azure Automation account.</span></span> <span data-ttu-id="1b5c8-113">Zie [Azure Uitvoeren-als-account](automation-sec-configure-azure-runas-account.md) voor instructies over het maken van een Azure Automation Uitvoeren-als-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="1b5c8-114">Een Azure Resource Manager VM (niet-klassieke) met Windows Server 2008 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="1b5c8-115">Zie voor instructies over het maken van een virtuele machine [uw eerste virtuele Windows-machine maken in hello Azure-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="1b5c8-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="1b5c8-116">Maken van een DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="1b5c8-116">Creating a DSC configuration</span></span>
<span data-ttu-id="1b5c8-117">We gaan een eenvoudige maken [DSC-configuratie](https://msdn.microsoft.com/powershell/dsc/configurations) die ervoor zorgt Hallo aanwezigheid of afwezigheid van Hallo **webserver** Windows functie (IIS), afhankelijk van hoe u knooppunten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="1b5c8-118">Start Windows PowerShell ISE hello (of een teksteditor).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="1b5c8-119">Typ na de tekst hello:</span><span class="sxs-lookup"><span data-stu-id="1b5c8-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="1b5c8-120">Hallo bestand opslaan als `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="1b5c8-121">Deze configuratie wordt één resource in elk blok knooppunt hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), die ervoor zorgt Hallo aanwezigheid of afwezigheid van Hallo **webserver** functie.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="1b5c8-122">Een configuratie te importeren in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1b5c8-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="1b5c8-123">We je vervolgens Hallo configuratie importeren in Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="1b5c8-124">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-125">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-126">Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="1b5c8-127">Op Hallo **DSC-configuraties** blade, klikt u op **toevoegen van een configuratie**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="1b5c8-128">Op Hallo **configuratie importeren** blade, bladeren toohello `TestConfig.ps1` bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Schermopname van Hallo ** importeren configuratie ** blade](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="1b5c8-130">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="1b5c8-131">Een configuratie weergeven in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1b5c8-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="1b5c8-132">Nadat u een configuratie hebt geïmporteerd, kunt u deze bekijken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="1b5c8-133">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-134">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-135">Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**</span><span class="sxs-lookup"><span data-stu-id="1b5c8-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="1b5c8-136">Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (dit is de naam Hallo van Hallo-configuratie die u hebt geïmporteerd in de vorige procedure Hallo).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="1b5c8-137">Op Hallo **TestConfig configuratie** blade, klikt u op **weergave configuratiebron**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Schermafbeelding van Hallo TestConfig configuratie tabblad](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="1b5c8-139">Een **TestConfig configuratiebron** blade geopend waarin Hallo PowerShell-code voor Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="1b5c8-140">Een Azure Automation-configuratie compileren</span><span class="sxs-lookup"><span data-stu-id="1b5c8-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="1b5c8-141">Voordat u een knooppunt van de status van de gewenste tooa toepassen kunt, moet een DSC-configuratie definiëren die status worden gecompileerd naar een of meer knooppuntconfiguraties (MOF document) en op Hallo Automation DSC-Pull-Server geplaatst.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="1b5c8-142">Zie voor een gedetailleerdere beschrijving van het compileren van configuraties in Azure Automation DSC [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="1b5c8-143">Zie voor meer informatie over het compileren van configuraties [DSC-configuraties](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="1b5c8-144">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-145">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-146">Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**</span><span class="sxs-lookup"><span data-stu-id="1b5c8-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="1b5c8-147">Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (Hallo-naam van Hallo eerder geïmporteerd configuratie).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="1b5c8-148">Op Hallo **TestConfig configuratie** blade, klikt u op **compileren**, en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="1b5c8-149">Hiermee start u een Compilatietaak.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-149">This starts a compilation job.</span></span>
   
    ![Schermafbeelding van Hallo TestConfig configuratie tabblad compileren knop markeren](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="1b5c8-151">Wanneer u een configuratie in Azure Automation compileert, wordt deze automatisch een gemaakt knooppunt configuratie MOF-bestanden toohello pull-server geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="1b5c8-152">Een Compilatietaak weergeven</span><span class="sxs-lookup"><span data-stu-id="1b5c8-152">Viewing a compilation job</span></span>
<span data-ttu-id="1b5c8-153">Nadat u een compilatie gestart, kunt u deze bekijken in Hallo **compilatietaken** -tegel in Hallo **configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="1b5c8-154">Hallo **compilatietaken** tegel bevat momenteel wordt uitgevoerd, voltooid en mislukte taken.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="1b5c8-155">Wanneer u een taak compilatie blade opent, ziet u informatie over deze taak inclusief eventuele fouten of waarschuwingen opgetreden, invoerparameters gebruikt in Hallo-configuratie en compilatie Logboeken.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="1b5c8-156">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-157">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-158">Op Hallo **Automation-account** blade, klikt u op **DSC-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="1b5c8-159">Op Hallo **DSC-configuraties** blade, klikt u op **TestConfig** (Hallo-naam van Hallo eerder geïmporteerd configuratie).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="1b5c8-160">Op Hallo **compilatietaken** tegel Hallo **TestConfig configuratie** blade, klik op een van de Hallo taken die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="1b5c8-161">Een **Compilatietaak** blade wordt geopend, gelabeld met Hallo datum op waarop Hallo Compilatietaak is gestart.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Schermafbeelding van Hallo Compilatietaak tabblad](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="1b5c8-163">Klik op een tegel in Hallo **Compilatietaak** blade toosee verdere details over Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="1b5c8-164">Knooppuntconfiguraties weergeven</span><span class="sxs-lookup"><span data-stu-id="1b5c8-164">Viewing node configurations</span></span>
<span data-ttu-id="1b5c8-165">Voltooiing van een Compilatietaak maakt een of meer nieuwe knooppuntconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="1b5c8-166">De knooppuntconfiguratie van een is een MOF-document dat is geïmplementeerd toohello pull-server en gereed toobe opgehaald en toegepast door een of meer knooppunten.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="1b5c8-167">U kunt Hallo knooppuntconfiguraties weergeven in uw Automation-account in Hallo **DSC-knooppuntconfiguraties** blade.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="1b5c8-168">De configuratie van een knooppunt heeft een naam met Hallo formulier *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="1b5c8-169">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-170">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-171">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppuntconfiguraties**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Schermafbeelding van tabblad voor Hallo DSC-knooppuntconfiguraties](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="1b5c8-173">Voorbereiden op een virtuele machine van Azure voor beheer met Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="1b5c8-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="1b5c8-174">U kunt Azure Automation DSC toomanage virtuele Azure-machines (Classic en Resource Manager), lokale VM's Linux machines, AWS virtuele machines en fysieke machines lokale gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="1b5c8-175">In dit onderwerp wordt uitgelegd hoe tooonboard alleen Azure Resource Manager virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="1b5c8-176">Zie voor informatie over de voorbereiding andere soorten machines, [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="1b5c8-177">tooonboard een Azure Resource Manager-VM voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="1b5c8-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="1b5c8-178">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-179">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-180">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="1b5c8-181">In Hallo **DSC-knooppunten** blade, klikt u op **toevoegen Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Schermafbeelding van Hallo DSC-knooppunten tabblad hello Azure VM toevoegen knop markeren](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="1b5c8-183">In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **tooonboard van virtuele machines selecteren**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="1b5c8-184">In Hallo **Selecteer VMs** blade Selecteer Hallo VM die u wilt tooonboard en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="1b5c8-185">Dit moet een Azure Resource Manager-VM met Windows Server 2008 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="1b5c8-186">In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **registratiegegevens configureren**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="1b5c8-187">In Hallo **registratie** blade Hallo naam invoeren van knooppuntconfiguratie Hallo gewenste tooapply toohello VM in Hallo **knooppunt configuratienaam** vak.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="1b5c8-188">Dit moet exact overeenkomen met de Hallo-naam van de knooppuntconfiguratie van een in Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="1b5c8-189">Op dit moment een naam opgeven is optioneel.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="1b5c8-190">U kunt Hallo toegewezen knooppuntconfiguratie na onboarding Hallo knooppunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="1b5c8-191">Controleer **knooppunt opnieuw opstarten indien nodig**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Schermafbeelding van tabblad voor Hallo-registratie](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="1b5c8-193">Hallo-knooppuntconfiguratie die u hebt opgegeven zijn toegepaste toohello VM met een interval dat is opgegeven door Hallo **frequentie van de configuratiemodus**, en Hallo VM, controleren op updates toohello knooppunt configureren met een interval dat is opgegeven door Hallo  **Vernieuwingsfrequentie**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="1b5c8-194">Zie voor meer informatie over het gebruik van deze waarden [configureren Hallo Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="1b5c8-195">In Hallo **Azure Virtual machines toevoegen** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="1b5c8-196">Azure start Hallo proces van het voorbereidingsproces Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="1b5c8-197">Wanneer deze voltooid is, Hallo VM wordt weergegeven in Hallo **DSC-knooppunten** blade in Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="1b5c8-198">Hallo-lijst van de DSC-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1b5c8-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="1b5c8-199">U kunt Hallo lijst weergeven met alle machines die vrijgegeven voor management in uw Automation-account in Hallo zijn **DSC-knooppunten** blade.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="1b5c8-200">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-201">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-202">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="1b5c8-203">Weergeven van rapporten voor DSC-knooppunten</span><span class="sxs-lookup"><span data-stu-id="1b5c8-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="1b5c8-204">Elke keer dat Azure Automation DSC een consistentiecontrole uit op een beheerde knooppunt voert verzendt Hallo knooppunt een status rapport back toohello pull-server.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="1b5c8-205">U kunt deze rapporten kunt weergeven op de blade Hallo voor dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="1b5c8-206">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-207">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-208">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="1b5c8-209">Op Hallo **rapporten** tegel, klikt u op Hallo rapporten in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Schermafbeelding van tabblad voor Hallo-rapport](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="1b5c8-211">Op Hallo blade voor een afzonderlijk rapport, kunt u zien Hallo statusinformatie voor de bijbehorende consistentie Hallo volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="1b5c8-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="1b5c8-212">statusrapportage Hallo — of Hallo knooppunt 'Compatibele', 'Mislukt' Hallo-configuratie of Hallo-knooppunt is 'Niet-compatibel' (wanneer Hallo-knooppunt is in **applyandmonitor** Hallo-modus en de machine is niet in Hallo gewenst status).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="1b5c8-213">Hallo begintijd voor Hallo consistentiecontrole uit.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="1b5c8-214">de totale runtime Hallo Hallo consistentie van controleren.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="1b5c8-215">Controleer de consistentie Hallo type.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-215">hello type of consistency check.</span></span>
* <span data-ttu-id="1b5c8-216">Eventuele fouten, met inbegrip van de fout Hallo-bericht en de fout.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="1b5c8-217">Eventuele DSC-resources in Hallo configuratie en status van elke resource (Hallo-knooppunt is of Hallo gewenst status voor die bron) Hallo gebruikt, kunt u op elke resource tooget meer gedetailleerde informatie voor die bron.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="1b5c8-218">Hallo-naam, IP-adres en configuratiemodus van Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="1b5c8-219">U kunt ook klikken op **onbewerkte rapport weergeven** toosee Hallo feitelijke gegevens die Hallo knooppunt toohello server verzendt.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="1b5c8-220">Zie voor meer informatie over het gebruik van die gegevens [met behulp van een DSC-rapportserver](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="1b5c8-221">Het kan even duren wanneer een knooppunt vrijgegeven is voordat de eerste rapport Hallo beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="1b5c8-222">Mogelijk moet u toowait up too30 minuten voor de eerste rapport Hallo nadat u vrijgeven een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="1b5c8-223">Opnieuw toewijzen van een ander knooppunt knooppuntconfiguratie van de tooa</span><span class="sxs-lookup"><span data-stu-id="1b5c8-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="1b5c8-224">U kunt een knooppunt toouse een ander knooppuntconfiguratie toewijzen dan Hallo een die oorspronkelijk was toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="1b5c8-225">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-226">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-227">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="1b5c8-228">Op Hallo **DSC-knooppunten** blade, klik op de naam van de Hallo Hallo-knooppunt dat u wilt dat tooreassign.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="1b5c8-229">Klik op de blade voor dat knooppunt Hallo **toewijzen knooppunt**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Schermafbeelding van Hallo knooppunt tabblad Hallo toewijzen knooppunt knop markeren](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="1b5c8-231">Op Hallo **knooppuntconfiguratie toewijzen** blade, selecteer Hallo knooppunt configuratie toowhich u wilt dat tooassign Hallo knooppunt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Schermafbeelding van tabblad voor Hallo knooppuntconfiguratie toewijzen](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="1b5c8-233">De registratie van een knooppunt</span><span class="sxs-lookup"><span data-stu-id="1b5c8-233">Unregistering a node</span></span>
<span data-ttu-id="1b5c8-234">Als u niet langer een knooppunt toobe beheerd door Azure Automation DSC wilt, kunt u de registratie verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="1b5c8-235">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5c8-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5c8-236">Klik op het menu Hub Hallo **alle resources** en vervolgens Hallo naam van uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="1b5c8-237">Op Hallo **Automation-account** blade, klikt u op **DSC-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="1b5c8-238">Op Hallo **DSC-knooppunten** blade, klik op de naam van de Hallo Hallo-knooppunt dat u wilt dat toounregister.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="1b5c8-239">Klik op de blade voor dat knooppunt Hallo **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="1b5c8-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Schermafbeelding van Hallo knooppunt tabblad Hallo Unregister knop markeren](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="1b5c8-241">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="1b5c8-241">Related Articles</span></span>
* [<span data-ttu-id="1b5c8-242">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="1b5c8-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="1b5c8-243">Computers voorbereiden voor beheer door Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="1b5c8-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="1b5c8-244">Windows PowerShell Desired State Configuration-overzicht</span><span class="sxs-lookup"><span data-stu-id="1b5c8-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="1b5c8-245">Azure Automation DSC-cmdlets</span><span class="sxs-lookup"><span data-stu-id="1b5c8-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="1b5c8-246">Azure Automation DSC-prijzen</span><span class="sxs-lookup"><span data-stu-id="1b5c8-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

