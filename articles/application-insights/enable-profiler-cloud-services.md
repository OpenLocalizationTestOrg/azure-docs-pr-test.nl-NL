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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Application Insights Profiler inschakelen op een Azure Cloud Services-bron

In dit scenario laat zien hoe Azure Application Insights Profiler inschakelen op een ASP.NET-toepassing die wordt gehost door een Azure Cloud Services-resource. De voorbeelden zijn onder meer ondersteuning voor Azure Virtual Machines, virtuele-machineschaalsets en Azure Service Fabric. De voorbeelden zijn afhankelijk van sjablonen die ondersteuning bieden voor het Azure Resource Manager-implementatiemodel. Raadpleeg voor meer informatie over het implementatiemodel [Azure Resource Manager versus klassieke implementatie: begrijpen implementatiemodellen en de status van uw resources](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Overzicht

Het volgende diagram illustreert de werking van de profiler voor Azure Cloud Services-bronnen. Een virtuele machine van Azure wordt gebruikt als voorbeeld.

![Overzicht](./media/enable-profiler-compute/overview.png) om informatie te verzamelen voor verwerking en weergeven in de Azure portal, moet u het onderdeel van de Diagnostics-Agent voor de resources voor Azure Cloud Services installeren. De rest van de procedure biedt richtlijnen voor het installeren en configureren van de Agent diagnostische gegevens om in te schakelen van Application Insights Profiler.

## <a name="prerequisites-for-the-walkthrough"></a>Vereisten voor het scenario

* Implementatie van Resource Manager-sjabloon die de profiler agenten op de virtuele machines installeert ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) of sets schalen ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Een Application Insights-exemplaar dat is ingeschakeld voor het samenstellen van profiel. Zie voor instructies [inschakelen van het profiel](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 of hoger is geïnstalleerd op de doel-Azure Cloud Services-resource.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Een resourcegroep in uw Azure-abonnement maken
Het volgende voorbeeld laat zien hoe een resourcegroep maken met behulp van een PowerShell-script:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a>Een Application Insights-resource maken in de resourcegroep
Op de **Application Insights** blade, voert u de gegevens voor uw resource, zoals in dit voorbeeld: 

![Application Insights-blade](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a>Een Application Insights-instrumentatiesleutel in de Azure Resource Manager-sjabloon toepassen

1. Als u de sjabloon nog niet hebt gedownload, downloaden via [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. De Application Insights-sleutel vinden.
   
   ![Locatie van de sleutel](./media/enable-profiler-compute/copyaikey.png)

3. Vervang de waarde van sjabloon.
   
   ![Waarde vervangen in de sjabloon](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a>Een Azure-VM voor het hosten van de webtoepassing maken
1. Maak een veilige tekenreeks voor het opslaan van het wachtwoord.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. De Azure Resource Manager-sjabloon implementeren.

   Wijzig de directory in de PowerShell-console in de map waarin de Resource Manager-sjabloon. Voer de volgende opdracht voor het implementeren van de sjabloon:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Nadat het script wordt uitgevoerd, vindt u een virtuele machine met de naam **MyWindowsVM** in de resourcegroep.

## <a name="configure-web-deploy-on-the-vm"></a>Web configureren op de virtuele machine implementeren
Zorg ervoor dat Web Deploy is ingeschakeld op de virtuele machine zodat u uw webtoepassing vanuit Visual Studio kunt publiceren.

Web Deploy op een virtuele machine handmatig via WebPI Zie installeren [installeren en configureren van Web Deploy op IIS 8.0 of Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Zie voor een voorbeeld van het automatiseren van Web Deploy installeren met behulp van een Azure Resource Manager-sjabloon, [maken, configureren en implementeren van een webtoepassing naar een Azure-virtuele machine](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Als u een ASP.NET MVC-toepassing, gaat u naar Serverbeheer implementeert selecteert **functies en onderdelen toevoegen** > **webserver (IIS)** > **webserver** > **toepassingsontwikkeling**, en schakel ASP.NET 4.5 in op uw server.

![ASP.NET toevoegen](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a>Installeer de Azure Application Insights-SDK voor uw project
1. Open uw ASP.NET-webtoepassing in Visual Studio.

2. Met de rechtermuisknop op het project en selecteer **toevoegen** > **verbonden Services**.

3. Selecteer **Application Insights**.

4. Volg de instructies op de pagina. Selecteer de Application Insights-resource die u eerder hebt gemaakt.

5. Selecteer de **registreren** knop.


## <a name="publish-the-project-to-an-azure-vm"></a>Het project publiceren naar een Azure VM
Er zijn verschillende manieren voor het publiceren van een toepassing naar een Azure-virtuele machine. Een manier is het gebruik van Visual Studio 2017.

1. Met de rechtermuisknop op het project en selecteer **publiceren**.

2. Selecteer **Microsoft Azure Virtual Machines** als het publiceren als doel en volg de stappen.

   ![Publiceren FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Voer een belastingtest uit op basis van uw toepassing. U ziet de resultaten op de portal webpagina voor Application Insights-exemplaar.


## <a name="enable-the-profiler"></a>De profiler inschakelen
1. Ga naar uw Application Insights **prestaties** blade en selecteer **configureren**.
   
   ![Pictogram configureren](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Selecteer **Profiler inschakelen**.
   
   ![Pictogram Profiler inschakelen](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a>Een prestatietest aan uw toepassing toevoegen
Volg deze stappen zodat we voorbeeldgegevens moet worden weergegeven in Application Insights Profiler kunt verzamelen:

1. Blader naar de Application Insights-resource die u eerder hebt gemaakt. 

2. Ga naar de **beschikbaarheid** blade en een prestatietest die webaanvragen naar de URL van uw toepassing verzendt toevoegen. 

   ![Prestatietest toevoegen](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>U prestatiegegevens weergeven

1. Wacht 10-15 minuten tot de profiler om te verzamelen en analyseren van de gegevens. 

2. Ga naar de **prestaties** blade in uw Application Insights-resource en hoe uw toepassing wordt uitgevoerd wanneer deze wordt belast.

   ![Prestaties weergeven](./media/enable-profiler-compute/aiperformance.png)

3. Selecteer het pictogram onder **voorbeelden** openen de **Trace weergave** blade.

   ![Openen van de blade tracering weergeven](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Werken met een bestaande sjabloon

1. De declaratie van Azure Diagnostics resource niet vinden in de sjabloon voor uw implementatie.
   
   Als u een declaratie geen hebt, kunt u een bestand dat lijkt op de declaratie in het volgende voorbeeld. U kunt de sjabloon bijwerken de [Azure Resource Explorer website](https://resources.azure.com).

2. Wijzigen van de uitgever van `Microsoft.Azure.Diagnostics` naar `AIP.Diagnostics.Test`.

3. Voor `typeHandlerVersion`, gebruik `0.0`.

4. Zorg ervoor dat `autoUpgradeMinorVersion` is ingesteld op `true`.

5. Toevoegen van de nieuwe `ApplicationInsightsProfiler` sink-exemplaar in de `WadCfg` instellingenobject, zoals wordt weergegeven in het volgende voorbeeld:

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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a>Inschakelen van de profiler op virtuele-machineschaalsets
Informatie over het inschakelen van de profiler, downloaden de [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) sjabloon. De dezelfde wijzigingen in een VM-sjabloon toepassen op de bron van de extensie diagnostische gegevens voor de virtuele-machineschaalset.

Zorg ervoor dat elk exemplaar in de schaalset toegang tot internet heeft. De Profiler-Agent kan de verzamelde voorbeelden vervolgens verzenden naar Application Insights voor het weergeven en analyseren.

## <a name="enable-the-profiler-on-service-fabric-applications"></a>De profiler op Service Fabric-toepassingen inschakelen
1. De Service Fabric-cluster om de Azure Diagnostics-extensie die u de Agent Profiler installeert inrichten.

2. De Application Insights-SDK installeren in het project en configureren van de Application Insights-sleutel.

3. Toepassingscode toevoegen aan instrument telemetrie.

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a>De Service Fabric-cluster om de Azure Diagnostics-extensie die u de Agent Profiler installeert inrichten
Een Service Fabric-cluster kan worden beveiligd of niet-beveiligde. U kunt één gateway-cluster worden niet-beveiligde zodat deze niet wordt een certificaat voor toegang vereist instellen. Clusters die als host voor zakelijke logica en gegevens moeten worden beveiligd. U kunt de profiler op zowel beveiligde als niet-beveiligde Service Fabric-clusters inschakelen. In dit scenario gebruikt een niet-beveiligde cluster als een voorbeeld waarin wordt uitgelegd welke wijzigingen zijn vereist voor het inschakelen van de profiler. Op dezelfde manier kunt u een beveiligde cluster inrichten.

1. Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Als u dit hebt gedaan voor virtuele machines en virtuele-machineschaalsets, vervangen `Application_Insights_Key` met uw Application Insights-sleutel:

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

2. De sjabloon implementeren met behulp van een PowerShell-script:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a>De Application Insights-SDK installeren in het project en configureren van de Application Insights-sleutel
Installeer de Application Insights-SDK van de [NuGet-pakket](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Zorg ervoor dat u een stabiele versie 2.3 of hoger installeert. 

Zie voor meer informatie over het configureren van Application Insights in uw projecten [met behulp van Service Fabric met Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-to-instrument-telemetry"></a>Toepassingscode toevoegen aan instrument telemetrie
1. Voor elk deel van de code die u wilt softwareontwikkelaars, het toevoegen van een met instructie omheen. 

   In het volgende voorbeeld wordt de `RunAsync` methode doet werk, en de `telemetryClient` klasse bevat de telemetrie nadat deze is gestart. De gebeurtenis moet een unieke naam voor de toepassing.

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

2. Uw toepassing met het Service Fabric-cluster implementeren. Wacht tot de app voor 10 minuten worden uitgevoerd. Voor betere effect, kunt u een load-test uitvoeren op de app. Ga naar de Application Insights-portal **prestaties** blade, en u ziet enkele voorbeelden van profilering traceringen worden weergegeven.

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Volgende stappen

- Hulp zoeken bij het oplossen van problemen in profiler [Profiler probleemoplossing](app-insights-profiler.md#troubleshooting).

- Meer informatie over de profiler in [Application Insights Profiler](app-insights-profiler.md).
