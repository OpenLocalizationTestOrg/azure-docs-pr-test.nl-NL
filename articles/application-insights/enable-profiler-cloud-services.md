---
title: Azure Application Insights Profiler aaaEnable van een resource Cloud Services | Microsoft Docs
description: Meer informatie over hoe tooset up Hallo profiler op een ASP.NET-toepassing wordt gehost door een Azure Cloud Services-resource.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="d4975-103">Application Insights Profiler inschakelen op een Azure Cloud Services-bron</span><span class="sxs-lookup"><span data-stu-id="d4975-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="d4975-104">In dit scenario laat zien hoe de tooenable Azure Application Insights Profiler op een ASP.NET-toepassing wordt gehost door een Azure Cloud Services-resource.</span><span class="sxs-lookup"><span data-stu-id="d4975-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="d4975-105">Hallo-voorbeelden zijn ondersteuning voor Azure Virtual Machines, virtuele-machineschaalsets en Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d4975-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="d4975-106">alle Hallo-voorbeelden zijn afhankelijk van sjablonen die ondersteuning bieden voor hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d4975-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d4975-107">Raadpleeg voor meer informatie over het implementatiemodel Hallo [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="d4975-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="d4975-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d4975-108">Overview</span></span>

<span data-ttu-id="d4975-109">Hallo volgende diagram illustreert hoe Hallo profiler werkt voor Azure Cloud Services-bronnen.</span><span class="sxs-lookup"><span data-stu-id="d4975-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="d4975-110">Een virtuele machine van Azure wordt gebruikt als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d4975-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="d4975-111">![Overzicht](./media/enable-profiler-compute/overview.png) toocollect-informatie voor verwerking en worden weergegeven op Hallo Azure-portal, moet u Hallo Diagnostics Agent onderdeel voor hello Azure Cloud Services-bronnen installeren.</span><span class="sxs-lookup"><span data-stu-id="d4975-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="d4975-112">Hallo rest van Hallo scenario biedt richtlijnen voor het tooinstall en Hallo Diagnostics Agent tooenable Application Insights Profiler configureren.</span><span class="sxs-lookup"><span data-stu-id="d4975-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="d4975-113">Vereisten voor het Hallo-overzicht</span><span class="sxs-lookup"><span data-stu-id="d4975-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="d4975-114">Implementatie van Resource Manager-sjabloon die wordt geïnstalleerd Hallo profiler agents op Hallo VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) of sets schalen ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="d4975-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="d4975-115">Een Application Insights-exemplaar dat is ingeschakeld voor het samenstellen van profiel.</span><span class="sxs-lookup"><span data-stu-id="d4975-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="d4975-116">Zie voor instructies [Hallo profiel inschakelen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="d4975-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="d4975-117">.NET framework 4.6.1 of hoger geïnstalleerd op Hallo gericht op Azure Cloud Services-resource.</span><span class="sxs-lookup"><span data-stu-id="d4975-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="d4975-118">Een resourcegroep in uw Azure-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="d4975-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="d4975-119">Hallo volgende voorbeeld laat zien hoe een resource toocreate groeperen op basis van een PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="d4975-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="d4975-120">Een Application Insights-resource maken in de resourcegroep Hallo</span><span class="sxs-lookup"><span data-stu-id="d4975-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="d4975-121">Op Hallo **Application Insights** blade Voer Hallo-informatie voor uw resource, zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d4975-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Application Insights-blade](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="d4975-123">Een Application Insights-instrumentatiesleutel in hello Azure Resource Manager-sjabloon toepassen</span><span class="sxs-lookup"><span data-stu-id="d4975-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="d4975-124">Als u Hallo sjabloon nog niet hebt gedownload, downloaden via [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="d4975-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="d4975-125">Hallo Application Insights sleutel vinden.</span><span class="sxs-lookup"><span data-stu-id="d4975-125">Find hello Application Insights key.</span></span>
   
   ![Locatie van Hallo-sleutel](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="d4975-127">Vervang de waarde van sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4975-127">Replace hello template value.</span></span>
   
   ![Waarde vervangen in Hallo-sjabloon](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="d4975-129">Een virtuele machine van Azure toohost Hallo-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="d4975-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="d4975-130">Een beveiligde tekenreeks toosave Hallo-wachtwoord maken.</span><span class="sxs-lookup"><span data-stu-id="d4975-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="d4975-131">Hello Azure Resource Manager-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="d4975-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="d4975-132">Hallo-map in Hallo PowerShell console toohello map met Resource Manager-sjabloon wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d4975-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="d4975-133">toodeploy hello sjabloon Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d4975-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="d4975-134">Nadat Hallo script wordt uitgevoerd, vindt u een virtuele machine met de naam **MyWindowsVM** in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d4975-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="d4975-135">Web Deploy op Hallo VM configureren</span><span class="sxs-lookup"><span data-stu-id="d4975-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="d4975-136">Zorg ervoor dat Web Deploy is ingeschakeld op de virtuele machine zodat u uw webtoepassing vanuit Visual Studio kunt publiceren.</span><span class="sxs-lookup"><span data-stu-id="d4975-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="d4975-137">tooinstall Web Deploy op een virtuele machine handmatig via WebPI, Zie [installeren en configureren van Web Deploy op IIS 8.0 of Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="d4975-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="d4975-138">Voor een voorbeeld van hoe tooautomate Web Deploy installeren met behulp van een Azure Resource Manager-sjabloon, Zie [maken, configureren en implementeren van een web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="d4975-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="d4975-139">Als u een ASP.NET MVC-toepassing implementeert, gaat u tooServer Manager, selecteer **functies en onderdelen toevoegen** > **webserver (IIS)** > **webserver**  >  **Toepassingsontwikkeling**, en schakel ASP.NET 4.5 in op uw server.</span><span class="sxs-lookup"><span data-stu-id="d4975-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![ASP.NET toevoegen](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="d4975-141">Hello Azure Application Insights-SDK voor uw project installeren</span><span class="sxs-lookup"><span data-stu-id="d4975-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="d4975-142">Open uw ASP.NET-webtoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4975-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="d4975-143">Met de rechtermuisknop op het Hallo-project en selecteer **toevoegen** > **verbonden Services**.</span><span class="sxs-lookup"><span data-stu-id="d4975-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="d4975-144">Selecteer **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d4975-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="d4975-145">Hallo instructies op de pagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4975-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="d4975-146">Selecteer Hallo Application Insights-resource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4975-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="d4975-147">Selecteer Hallo **registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="d4975-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="d4975-148">Hallo project tooan virtuele machine in Azure publiceren</span><span class="sxs-lookup"><span data-stu-id="d4975-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="d4975-149">Er zijn verschillende manieren toopublish van een toepassing tooan Azure VM.</span><span class="sxs-lookup"><span data-stu-id="d4975-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="d4975-150">Een manier is toouse Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d4975-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="d4975-151">Met de rechtermuisknop op het Hallo-project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="d4975-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="d4975-152">Selecteer **Microsoft Azure Virtual Machines** als Hallo doel publiceren en Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="d4975-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publiceren FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="d4975-154">Voer een belastingtest uit op basis van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d4975-154">Run a load test against your application.</span></span> <span data-ttu-id="d4975-155">U ziet de resultaten op Hallo Application Insights exemplaar portal webpagina.</span><span class="sxs-lookup"><span data-stu-id="d4975-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="d4975-156">Hallo profiler inschakelen</span><span class="sxs-lookup"><span data-stu-id="d4975-156">Enable hello profiler</span></span>
1. <span data-ttu-id="d4975-157">Ga tooyour Application Insights **prestaties** blade en selecteer **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d4975-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Pictogram configureren](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="d4975-159">Selecteer **Profiler inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="d4975-159">Select **Enable Profiler**.</span></span>
   
   ![Pictogram Profiler inschakelen](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="d4975-161">Prestaties test tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="d4975-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="d4975-162">Volg deze stappen zodat we enkele sample data toobe weergegeven in Application Insights Profiler kunt verzamelen:</span><span class="sxs-lookup"><span data-stu-id="d4975-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="d4975-163">Blader toohello Application Insights-resource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4975-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="d4975-164">Ga toohello **beschikbaarheid** blade en voeg een prestatietest waarmee tooyour de URL van webtoepassing aanvragen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d4975-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Prestatietest toevoegen](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="d4975-166">U prestatiegegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="d4975-166">View your performance data</span></span>

1. <span data-ttu-id="d4975-167">Hallo profiler toocollect 10-15 minuten wachten tot gegevens en analyseren Hallo.</span><span class="sxs-lookup"><span data-stu-id="d4975-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="d4975-168">Ga toohello **prestaties** blade in uw Application Insights-resource en hoe uw toepassing wordt uitgevoerd wanneer deze wordt belast.</span><span class="sxs-lookup"><span data-stu-id="d4975-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Prestaties weergeven](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="d4975-170">Selecteer Hallo pictogram onder **voorbeelden** tooopen hello **Trace weergave** blade.</span><span class="sxs-lookup"><span data-stu-id="d4975-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Hallo Trace weergave blade openen](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="d4975-172">Werken met een bestaande sjabloon</span><span class="sxs-lookup"><span data-stu-id="d4975-172">Work with an existing template</span></span>

1. <span data-ttu-id="d4975-173">Hello Azure Diagnostics brondeclaratie niet vinden in de sjabloon voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="d4975-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="d4975-174">Als u een declaratie geen hebt, kunt u een dat lijkt op Hallo declaratie in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="d4975-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="d4975-175">U kunt bijwerken Hallo sjabloon van Hallo [Azure Resource Explorer website](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4975-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="d4975-176">Hallo-uitgever van wijzigingen uit `Microsoft.Azure.Diagnostics` te`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="d4975-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="d4975-177">Voor `typeHandlerVersion`, gebruik `0.0`.</span><span class="sxs-lookup"><span data-stu-id="d4975-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="d4975-178">Zorg ervoor dat `autoUpgradeMinorVersion` te is ingesteld`true`.</span><span class="sxs-lookup"><span data-stu-id="d4975-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="d4975-179">Toevoegen van nieuwe Hallo `ApplicationInsightsProfiler` sink-exemplaar in Hallo `WadCfg` instellingenobject, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="d4975-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="d4975-180">Hallo profiler op virtuele-machineschaalsets inschakelen</span><span class="sxs-lookup"><span data-stu-id="d4975-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="d4975-181">hoe tooenable Hallo profiler downloaden Hallo toosee [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="d4975-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="d4975-182">Toepassing hello dezelfde in een VM-sjabloon toohello diagnostics extensie resource voor Hallo virtuele-machineschaalset wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d4975-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="d4975-183">Zorg ervoor dat elk exemplaar in de schaalset hello toohello toegang tot internet.</span><span class="sxs-lookup"><span data-stu-id="d4975-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="d4975-184">Hallo Profiler Agent kunt vervolgens verzenden Hallo verzamelde steekproeven tooApplication Insights voor het weergeven en analyseren.</span><span class="sxs-lookup"><span data-stu-id="d4975-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="d4975-185">Hallo profiler op Service Fabric-toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="d4975-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="d4975-186">Inrichten hello Service Fabric-cluster toohave hello Azure extensie voor diagnostische gegevens die Hallo Profiler Agent installeert.</span><span class="sxs-lookup"><span data-stu-id="d4975-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="d4975-187">Hallo Application Insights-SDK in Hallo project installeren en configureren van Hallo Application Insights-sleutel.</span><span class="sxs-lookup"><span data-stu-id="d4975-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="d4975-188">Toepassingstelemetrie code tooinstrument toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d4975-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="d4975-189">Inrichten Hallo Service Fabric-cluster toohave hello Azure Diagnostics-extensie die Hallo Profiler Agent is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="d4975-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="d4975-190">Een Service Fabric-cluster kan worden beveiligd of niet-beveiligde.</span><span class="sxs-lookup"><span data-stu-id="d4975-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="d4975-191">U kunt één gateway-cluster toobe niet-beveiligde zodanig instellen een certificaat niet nodig is om toegang te krijgen.</span><span class="sxs-lookup"><span data-stu-id="d4975-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="d4975-192">Clusters die als host voor zakelijke logica en gegevens moeten worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="d4975-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="d4975-193">U kunt de profiler Hallo op zowel beveiligde als niet-beveiligde Service Fabric-clusters inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d4975-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="d4975-194">In dit scenario wordt een niet-beveiligde cluster gebruikt als een voorbeeld tooexplain welke wijzigingen zijn vereist tooenable Hallo profiler.</span><span class="sxs-lookup"><span data-stu-id="d4975-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="d4975-195">U kunt een beveiligde cluster in Hallo inrichten dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="d4975-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="d4975-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="d4975-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="d4975-197">Als u dit hebt gedaan voor virtuele machines en virtuele-machineschaalsets, vervangen `Application_Insights_Key` met uw Application Insights-sleutel:</span><span class="sxs-lookup"><span data-stu-id="d4975-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. <span data-ttu-id="d4975-198">Hallo-sjabloon implementeren met een PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="d4975-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="d4975-199">Hallo Application Insights-SDK in Hallo project installeren en configureren van Hallo Application Insights-sleutel</span><span class="sxs-lookup"><span data-stu-id="d4975-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="d4975-200">Hallo Application Insights-SDK installeren vanaf Hallo [NuGet-pakket](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="d4975-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="d4975-201">Zorg ervoor dat u een stabiele versie 2.3 of hoger installeert.</span><span class="sxs-lookup"><span data-stu-id="d4975-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="d4975-202">Zie voor meer informatie over het configureren van Application Insights in uw projecten [met behulp van Service Fabric met Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="d4975-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="d4975-203">Toepassingstelemetrie code tooinstrument toevoegen</span><span class="sxs-lookup"><span data-stu-id="d4975-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="d4975-204">Voor een stuk code dat u wilt dat tooinstrument, Voeg een met instructie omheen.</span><span class="sxs-lookup"><span data-stu-id="d4975-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="d4975-205">Hallo in Hallo voorbeeld te volgen, `RunAsync` methode is sommige werk en Hallo `telemetryClient` klasse vastgelegd Hallo telemetrie nadat deze is gestart.</span><span class="sxs-lookup"><span data-stu-id="d4975-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="d4975-206">Hallo-gebeurtenis moet een unieke naam voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d4975-206">hello event needs a unique name across hello application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. <span data-ttu-id="d4975-207">Uw toepassing toohello Service Fabric-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="d4975-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="d4975-208">Hallo app toorun wacht 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="d4975-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="d4975-209">U kunt een load-test uitvoeren op Hallo-app voor betere effect.</span><span class="sxs-lookup"><span data-stu-id="d4975-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="d4975-210">Ga toohello Application Insights-portal van **prestaties** blade, en u ziet enkele voorbeelden van profilering traceringen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d4975-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="d4975-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4975-211">Next steps</span></span>

- <span data-ttu-id="d4975-212">Hulp zoeken bij het oplossen van problemen in profiler [Profiler probleemoplossing](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="d4975-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="d4975-213">Meer informatie over de profiler Hallo in [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="d4975-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
