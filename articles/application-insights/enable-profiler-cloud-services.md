---
title: Azure Application Insights Profiler van een resource Cloud Services inschakelen | Microsoft Docs
description: Informatie over het instellen van de profiler op een ASP.NET-toepassing die wordt gehost door een Azure Cloud Services-resource.
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
ms.openlocfilehash: 5ff062ac81dca9d8b205cec966d2a9c11a4005b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="ad5a6-103">Application Insights Profiler inschakelen op een Azure Cloud Services-bron</span><span class="sxs-lookup"><span data-stu-id="ad5a6-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="ad5a6-104">In dit scenario laat zien hoe Azure Application Insights Profiler inschakelen op een ASP.NET-toepassing die wordt gehost door een Azure Cloud Services-resource.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-104">This walkthrough demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="ad5a6-105">De voorbeelden zijn onder meer ondersteuning voor Azure Virtual Machines, virtuele-machineschaalsets en Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-105">The examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="ad5a6-106">De voorbeelden zijn afhankelijk van sjablonen die ondersteuning bieden voor het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-106">The examples all rely on templates that support the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ad5a6-107">Raadpleeg voor meer informatie over het implementatiemodel [Azure Resource Manager versus klassieke implementatie: begrijpen implementatiemodellen en de status van uw resources](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-107">For more information about the deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="ad5a6-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ad5a6-108">Overview</span></span>

<span data-ttu-id="ad5a6-109">Het volgende diagram illustreert de werking van de profiler voor Azure Cloud Services-bronnen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-109">The following diagram illustrates how the profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="ad5a6-110">Een virtuele machine van Azure wordt gebruikt als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="ad5a6-111">![Overzicht](./media/enable-profiler-compute/overview.png) om informatie te verzamelen voor verwerking en weergeven in de Azure portal, moet u het onderdeel van de Diagnostics-Agent voor de resources voor Azure Cloud Services installeren.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-111">![Overview](./media/enable-profiler-compute/overview.png) To collect information for processing and display on the Azure portal, you must install the Diagnostics Agent component for the Azure Cloud Services resources.</span></span> <span data-ttu-id="ad5a6-112">De rest van de procedure biedt richtlijnen voor het installeren en configureren van de Agent diagnostische gegevens om in te schakelen van Application Insights Profiler.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-112">The rest of the walkthrough provides guidance on how to install and configure the Diagnostics Agent to enable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-the-walkthrough"></a><span data-ttu-id="ad5a6-113">Vereisten voor het scenario</span><span class="sxs-lookup"><span data-stu-id="ad5a6-113">Prerequisites for the walkthrough</span></span>

* <span data-ttu-id="ad5a6-114">Implementatie van Resource Manager-sjabloon die de profiler agenten op de virtuele machines installeert ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) of sets schalen ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-114">A deployment Resource Manager template that installs the profiler agents on the VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="ad5a6-115">Een Application Insights-exemplaar dat is ingeschakeld voor het samenstellen van profiel.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="ad5a6-116">Zie voor instructies [inschakelen van het profiel](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-116">For instructions, see [Enable the profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="ad5a6-117">.NET framework 4.6.1 of hoger is geïnstalleerd op de doel-Azure Cloud Services-resource.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-117">.NET Framework 4.6.1 or later installed on the target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="ad5a6-118">Een resourcegroep in uw Azure-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="ad5a6-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="ad5a6-119">Het volgende voorbeeld laat zien hoe een resourcegroep maken met behulp van een PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-119">The following example demonstrates how to create a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a><span data-ttu-id="ad5a6-120">Een Application Insights-resource maken in de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="ad5a6-120">Create an Application Insights resource in the resource group</span></span>
<span data-ttu-id="ad5a6-121">Op de **Application Insights** blade, voert u de gegevens voor uw resource, zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-121">On the **Application Insights** blade, enter the information for your resource, as shown in this example:</span></span> 

![Application Insights-blade](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a><span data-ttu-id="ad5a6-123">Een Application Insights-instrumentatiesleutel in de Azure Resource Manager-sjabloon toepassen</span><span class="sxs-lookup"><span data-stu-id="ad5a6-123">Apply an Application Insights instrumentation key in the Azure Resource Manager template</span></span>

1. <span data-ttu-id="ad5a6-124">Als u de sjabloon nog niet hebt gedownload, downloaden via [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-124">If you haven't downloaded the template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="ad5a6-125">De Application Insights-sleutel vinden.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-125">Find the Application Insights key.</span></span>
   
   ![Locatie van de sleutel](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="ad5a6-127">Vervang de waarde van sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-127">Replace the template value.</span></span>
   
   ![Waarde vervangen in de sjabloon](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a><span data-ttu-id="ad5a6-129">Een Azure-VM voor het hosten van de webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="ad5a6-129">Create an Azure VM to host the web application</span></span>
1. <span data-ttu-id="ad5a6-130">Maak een veilige tekenreeks voor het opslaan van het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-130">Create a secure string to save the password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="ad5a6-131">De Azure Resource Manager-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-131">Deploy the Azure Resource Manager template.</span></span>

   <span data-ttu-id="ad5a6-132">Wijzig de directory in de PowerShell-console in de map waarin de Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-132">Change the directory in the PowerShell console to the folder that contains your Resource Manager template.</span></span> <span data-ttu-id="ad5a6-133">Voer de volgende opdracht voor het implementeren van de sjabloon:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-133">To deploy the template, run the following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="ad5a6-134">Nadat het script wordt uitgevoerd, vindt u een virtuele machine met de naam **MyWindowsVM** in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-134">After the script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-the-vm"></a><span data-ttu-id="ad5a6-135">Web configureren op de virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="ad5a6-135">Configure Web Deploy on the VM</span></span>
<span data-ttu-id="ad5a6-136">Zorg ervoor dat Web Deploy is ingeschakeld op de virtuele machine zodat u uw webtoepassing vanuit Visual Studio kunt publiceren.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="ad5a6-137">Web Deploy op een virtuele machine handmatig via WebPI Zie installeren [installeren en configureren van Web Deploy op IIS 8.0 of Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-137">To install Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="ad5a6-138">Zie voor een voorbeeld van het automatiseren van Web Deploy installeren met behulp van een Azure Resource Manager-sjabloon, [maken, configureren en implementeren van een webtoepassing naar een Azure-virtuele machine](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-138">For an example of how to automate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="ad5a6-139">Als u een ASP.NET MVC-toepassing, gaat u naar Serverbeheer implementeert selecteert **functies en onderdelen toevoegen** > **webserver (IIS)** > **webserver** > **toepassingsontwikkeling**, en schakel ASP.NET 4.5 in op uw server.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-139">If you are deploying an ASP.NET MVC application, go to Server Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![ASP.NET toevoegen](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="ad5a6-141">Installeer de Azure Application Insights-SDK voor uw project</span><span class="sxs-lookup"><span data-stu-id="ad5a6-141">Install the Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="ad5a6-142">Open uw ASP.NET-webtoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="ad5a6-143">Met de rechtermuisknop op het project en selecteer **toevoegen** > **verbonden Services**.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-143">Right-click the project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="ad5a6-144">Selecteer **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="ad5a6-145">Volg de instructies op de pagina.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-145">Follow the instructions on the page.</span></span> <span data-ttu-id="ad5a6-146">Selecteer de Application Insights-resource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-146">Select the Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="ad5a6-147">Selecteer de **registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-147">Select the **Register** button.</span></span>


## <a name="publish-the-project-to-an-azure-vm"></a><span data-ttu-id="ad5a6-148">Het project publiceren naar een Azure VM</span><span class="sxs-lookup"><span data-stu-id="ad5a6-148">Publish the project to an Azure VM</span></span>
<span data-ttu-id="ad5a6-149">Er zijn verschillende manieren voor het publiceren van een toepassing naar een Azure-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-149">There are several ways to publish an application to an Azure VM.</span></span> <span data-ttu-id="ad5a6-150">Een manier is het gebruik van Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-150">One way is to use Visual Studio 2017.</span></span>

1. <span data-ttu-id="ad5a6-151">Met de rechtermuisknop op het project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-151">Right-click the project and select **Publish**.</span></span>

2. <span data-ttu-id="ad5a6-152">Selecteer **Microsoft Azure Virtual Machines** als het publiceren als doel en volg de stappen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-152">Select **Microsoft Azure Virtual Machines** as the publish target and follow the steps.</span></span>

   ![Publiceren FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="ad5a6-154">Voer een belastingtest uit op basis van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-154">Run a load test against your application.</span></span> <span data-ttu-id="ad5a6-155">U ziet de resultaten op de portal webpagina voor Application Insights-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-155">You should see results on the Application Insights instance portal webpage.</span></span>


## <a name="enable-the-profiler"></a><span data-ttu-id="ad5a6-156">De profiler inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad5a6-156">Enable the profiler</span></span>
1. <span data-ttu-id="ad5a6-157">Ga naar uw Application Insights **prestaties** blade en selecteer **configureren**.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-157">Go to your Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Pictogram configureren](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="ad5a6-159">Selecteer **Profiler inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-159">Select **Enable Profiler**.</span></span>
   
   ![Pictogram Profiler inschakelen](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a><span data-ttu-id="ad5a6-161">Een prestatietest aan uw toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="ad5a6-161">Add a performance test to your application</span></span>
<span data-ttu-id="ad5a6-162">Volg deze stappen zodat we voorbeeldgegevens moet worden weergegeven in Application Insights Profiler kunt verzamelen:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-162">Follow these steps so we can collect some sample data to be displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="ad5a6-163">Blader naar de Application Insights-resource die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-163">Browse to the Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="ad5a6-164">Ga naar de **beschikbaarheid** blade en een prestatietest die webaanvragen naar de URL van uw toepassing verzendt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-164">Go to the **Availability** blade and add a performance test that sends web requests to your application URL.</span></span> 

   ![Prestatietest toevoegen](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="ad5a6-166">U prestatiegegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="ad5a6-166">View your performance data</span></span>

1. <span data-ttu-id="ad5a6-167">Wacht 10-15 minuten tot de profiler om te verzamelen en analyseren van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-167">Wait 10-15 minutes for the profiler to collect and analyze the data.</span></span> 

2. <span data-ttu-id="ad5a6-168">Ga naar de **prestaties** blade in uw Application Insights-resource en hoe uw toepassing wordt uitgevoerd wanneer deze wordt belast.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-168">Go to the **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Prestaties weergeven](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="ad5a6-170">Selecteer het pictogram onder **voorbeelden** openen de **Trace weergave** blade.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-170">Select the icon under **Examples** to open the **Trace View** blade.</span></span>

   ![Openen van de blade tracering weergeven](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="ad5a6-172">Werken met een bestaande sjabloon</span><span class="sxs-lookup"><span data-stu-id="ad5a6-172">Work with an existing template</span></span>

1. <span data-ttu-id="ad5a6-173">De declaratie van Azure Diagnostics resource niet vinden in de sjabloon voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-173">Locate the Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="ad5a6-174">Als u een declaratie geen hebt, kunt u een bestand dat lijkt op de declaratie in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-174">If you don't have a declaration, you can create one that resembles the declaration in the following example.</span></span> <span data-ttu-id="ad5a6-175">U kunt de sjabloon bijwerken de [Azure Resource Explorer website](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-175">You can update the template from the [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="ad5a6-176">Wijzigen van de uitgever van `Microsoft.Azure.Diagnostics` naar `AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-176">Change the publisher from `Microsoft.Azure.Diagnostics` to `AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="ad5a6-177">Voor `typeHandlerVersion`, gebruik `0.0`.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="ad5a6-178">Zorg ervoor dat `autoUpgradeMinorVersion` is ingesteld op `true`.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-178">Make sure that `autoUpgradeMinorVersion` is set to `true`.</span></span>

5. <span data-ttu-id="ad5a6-179">Toevoegen van de nieuwe `ApplicationInsightsProfiler` sink-exemplaar in de `WadCfg` instellingenobject, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-179">Add the new `ApplicationInsightsProfiler` sink instance in the `WadCfg` settings object, as shown in the following example:</span></span>

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
                      "ApplicationInsightsProfiler": "Enter the Application Insights instance instrumentation key guid here"
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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="ad5a6-180">Inschakelen van de profiler op virtuele-machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="ad5a6-180">Enable the profiler on virtual machine scale sets</span></span>
<span data-ttu-id="ad5a6-181">Informatie over het inschakelen van de profiler, downloaden de [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-181">To see how to enable the profiler, download the [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="ad5a6-182">De dezelfde wijzigingen in een VM-sjabloon toepassen op de bron van de extensie diagnostische gegevens voor de virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-182">Apply the same changes in a VM template to the diagnostics extension resource for the virtual machine scale set.</span></span>

<span data-ttu-id="ad5a6-183">Zorg ervoor dat elk exemplaar in de schaalset toegang tot internet heeft.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-183">Make sure that each instance in the scale set has access to the internet.</span></span> <span data-ttu-id="ad5a6-184">De Profiler-Agent kan de verzamelde voorbeelden vervolgens verzenden naar Application Insights voor het weergeven en analyseren.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-184">The Profiler Agent can then send the collected samples to Application Insights for display and analysis.</span></span>

## <a name="enable-the-profiler-on-service-fabric-applications"></a><span data-ttu-id="ad5a6-185">De profiler op Service Fabric-toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="ad5a6-185">Enable the profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="ad5a6-186">De Service Fabric-cluster om de Azure Diagnostics-extensie die u de Agent Profiler installeert inrichten.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-186">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent.</span></span>

2. <span data-ttu-id="ad5a6-187">De Application Insights-SDK installeren in het project en configureren van de Application Insights-sleutel.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-187">Install the Application Insights SDK in the project and configure the Application Insights key.</span></span>

3. <span data-ttu-id="ad5a6-188">Toepassingscode toevoegen aan instrument telemetrie.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-188">Add application code to instrument telemetry.</span></span>

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a><span data-ttu-id="ad5a6-189">De Service Fabric-cluster om de Azure Diagnostics-extensie die u de Agent Profiler installeert inrichten</span><span class="sxs-lookup"><span data-stu-id="ad5a6-189">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent</span></span>
<span data-ttu-id="ad5a6-190">Een Service Fabric-cluster kan worden beveiligd of niet-beveiligde.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="ad5a6-191">U kunt één gateway-cluster worden niet-beveiligde zodat deze niet wordt een certificaat voor toegang vereist instellen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-191">You can set one gateway cluster to be non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="ad5a6-192">Clusters die als host voor zakelijke logica en gegevens moeten worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="ad5a6-193">U kunt de profiler op zowel beveiligde als niet-beveiligde Service Fabric-clusters inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-193">You can enable the profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="ad5a6-194">In dit scenario gebruikt een niet-beveiligde cluster als een voorbeeld waarin wordt uitgelegd welke wijzigingen zijn vereist voor het inschakelen van de profiler.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-194">This walkthrough uses a non-secure cluster as an example to explain what changes are required to enable the profiler.</span></span> <span data-ttu-id="ad5a6-195">Op dezelfde manier kunt u een beveiligde cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-195">You can provision a secure cluster in the same way.</span></span>

1. <span data-ttu-id="ad5a6-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="ad5a6-197">Als u dit hebt gedaan voor virtuele machines en virtuele-machineschaalsets, vervangen `Application_Insights_Key` met uw Application Insights-sleutel:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="ad5a6-198">De sjabloon implementeren met behulp van een PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="ad5a6-198">Deploy the template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a><span data-ttu-id="ad5a6-199">De Application Insights-SDK installeren in het project en configureren van de Application Insights-sleutel</span><span class="sxs-lookup"><span data-stu-id="ad5a6-199">Install the Application Insights SDK in the project and configure the Application Insights key</span></span>
<span data-ttu-id="ad5a6-200">Installeer de Application Insights-SDK van de [NuGet-pakket](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-200">Install the Application Insights SDK from the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="ad5a6-201">Zorg ervoor dat u een stabiele versie 2.3 of hoger installeert.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="ad5a6-202">Zie voor meer informatie over het configureren van Application Insights in uw projecten [met behulp van Service Fabric met Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-to-instrument-telemetry"></a><span data-ttu-id="ad5a6-203">Toepassingscode toevoegen aan instrument telemetrie</span><span class="sxs-lookup"><span data-stu-id="ad5a6-203">Add application code to instrument telemetry</span></span>
1. <span data-ttu-id="ad5a6-204">Voor elk deel van de code die u wilt softwareontwikkelaars, het toevoegen van een met instructie omheen.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-204">For any piece of code that you want to instrument, add a using statement around it.</span></span> 

   <span data-ttu-id="ad5a6-205">In het volgende voorbeeld wordt de `RunAsync` methode doet werk, en de `telemetryClient` klasse bevat de telemetrie nadat deze is gestart.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-205">In the following  example, the `RunAsync` method is doing some work, and the `telemetryClient` class captures the telemetry after it starts.</span></span> <span data-ttu-id="ad5a6-206">De gebeurtenis moet een unieke naam voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-206">The event needs a unique name across the application.</span></span>

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace the following sample code with your own logic
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

2. <span data-ttu-id="ad5a6-207">Uw toepassing met het Service Fabric-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-207">Deploy your application to the Service Fabric cluster.</span></span> <span data-ttu-id="ad5a6-208">Wacht tot de app voor 10 minuten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-208">Wait for the app to run for 10 minutes.</span></span> <span data-ttu-id="ad5a6-209">Voor betere effect, kunt u een load-test uitvoeren op de app.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-209">For better effect, you can run a load test on the app.</span></span> <span data-ttu-id="ad5a6-210">Ga naar de Application Insights-portal **prestaties** blade, en u ziet enkele voorbeelden van profilering traceringen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ad5a6-210">Go to the Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="ad5a6-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad5a6-211">Next steps</span></span>

- <span data-ttu-id="ad5a6-212">Hulp zoeken bij het oplossen van problemen in profiler [Profiler probleemoplossing](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="ad5a6-213">Meer informatie over de profiler in [Application Insights Profiler](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="ad5a6-213">Read more about the profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
