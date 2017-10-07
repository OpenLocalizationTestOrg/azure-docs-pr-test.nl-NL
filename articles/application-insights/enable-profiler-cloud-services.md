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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Application Insights Profiler inschakelen op een Azure Cloud Services-bron

In dit scenario laat zien hoe de tooenable Azure Application Insights Profiler op een ASP.NET-toepassing wordt gehost door een Azure Cloud Services-resource. Hallo-voorbeelden zijn ondersteuning voor Azure Virtual Machines, virtuele-machineschaalsets en Azure Service Fabric. alle Hallo-voorbeelden zijn afhankelijk van sjablonen die ondersteuning bieden voor hello Azure Resource Manager-implementatiemodel. Raadpleeg voor meer informatie over het implementatiemodel Hallo [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Overzicht

Hallo volgende diagram illustreert hoe Hallo profiler werkt voor Azure Cloud Services-bronnen. Een virtuele machine van Azure wordt gebruikt als voorbeeld.

![Overzicht](./media/enable-profiler-compute/overview.png) toocollect-informatie voor verwerking en worden weergegeven op Hallo Azure-portal, moet u Hallo Diagnostics Agent onderdeel voor hello Azure Cloud Services-bronnen installeren. Hallo rest van Hallo scenario biedt richtlijnen voor het tooinstall en Hallo Diagnostics Agent tooenable Application Insights Profiler configureren.

## <a name="prerequisites-for-hello-walkthrough"></a>Vereisten voor het Hallo-overzicht

* Implementatie van Resource Manager-sjabloon die wordt geïnstalleerd Hallo profiler agents op Hallo VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) of sets schalen ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Een Application Insights-exemplaar dat is ingeschakeld voor het samenstellen van profiel. Zie voor instructies [Hallo profiel inschakelen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 of hoger geïnstalleerd op Hallo gericht op Azure Cloud Services-resource.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Een resourcegroep in uw Azure-abonnement maken
Hallo volgende voorbeeld laat zien hoe een resource toocreate groeperen op basis van een PowerShell-script:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Een Application Insights-resource maken in de resourcegroep Hallo
Op Hallo **Application Insights** blade Voer Hallo-informatie voor uw resource, zoals in dit voorbeeld: 

![Application Insights-blade](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Een Application Insights-instrumentatiesleutel in hello Azure Resource Manager-sjabloon toepassen

1. Als u Hallo sjabloon nog niet hebt gedownload, downloaden via [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Hallo Application Insights sleutel vinden.
   
   ![Locatie van Hallo-sleutel](./media/enable-profiler-compute/copyaikey.png)

3. Vervang de waarde van sjabloon Hallo.
   
   ![Waarde vervangen in Hallo-sjabloon](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Een virtuele machine van Azure toohost Hallo-webtoepassing maken
1. Een beveiligde tekenreeks toosave Hallo-wachtwoord maken.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Hello Azure Resource Manager-sjabloon implementeren.

   Hallo-map in Hallo PowerShell console toohello map met Resource Manager-sjabloon wijzigen. toodeploy hello sjabloon Hallo volgende opdracht uitvoeren:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Nadat Hallo script wordt uitgevoerd, vindt u een virtuele machine met de naam **MyWindowsVM** in de resourcegroep.

## <a name="configure-web-deploy-on-hello-vm"></a>Web Deploy op Hallo VM configureren
Zorg ervoor dat Web Deploy is ingeschakeld op de virtuele machine zodat u uw webtoepassing vanuit Visual Studio kunt publiceren.

tooinstall Web Deploy op een virtuele machine handmatig via WebPI, Zie [installeren en configureren van Web Deploy op IIS 8.0 of Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Voor een voorbeeld van hoe tooautomate Web Deploy installeren met behulp van een Azure Resource Manager-sjabloon, Zie [maken, configureren en implementeren van een web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Als u een ASP.NET MVC-toepassing implementeert, gaat u tooServer Manager, selecteer **functies en onderdelen toevoegen** > **webserver (IIS)** > **webserver**  >  **Toepassingsontwikkeling**, en schakel ASP.NET 4.5 in op uw server.

![ASP.NET toevoegen](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Hello Azure Application Insights-SDK voor uw project installeren
1. Open uw ASP.NET-webtoepassing in Visual Studio.

2. Met de rechtermuisknop op het Hallo-project en selecteer **toevoegen** > **verbonden Services**.

3. Selecteer **Application Insights**.

4. Hallo instructies op de pagina Hallo. Selecteer Hallo Application Insights-resource die u eerder hebt gemaakt.

5. Selecteer Hallo **registreren** knop.


## <a name="publish-hello-project-tooan-azure-vm"></a>Hallo project tooan virtuele machine in Azure publiceren
Er zijn verschillende manieren toopublish van een toepassing tooan Azure VM. Een manier is toouse Visual Studio 2017.

1. Met de rechtermuisknop op het Hallo-project en selecteer **publiceren**.

2. Selecteer **Microsoft Azure Virtual Machines** als Hallo doel publiceren en Hallo stappen.

   ![Publiceren FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Voer een belastingtest uit op basis van uw toepassing. U ziet de resultaten op Hallo Application Insights exemplaar portal webpagina.


## <a name="enable-hello-profiler"></a>Hallo profiler inschakelen
1. Ga tooyour Application Insights **prestaties** blade en selecteer **configureren**.
   
   ![Pictogram configureren](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Selecteer **Profiler inschakelen**.
   
   ![Pictogram Profiler inschakelen](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Prestaties test tooyour toepassing toevoegen
Volg deze stappen zodat we enkele sample data toobe weergegeven in Application Insights Profiler kunt verzamelen:

1. Blader toohello Application Insights-resource die u eerder hebt gemaakt. 

2. Ga toohello **beschikbaarheid** blade en voeg een prestatietest waarmee tooyour de URL van webtoepassing aanvragen worden verzonden. 

   ![Prestatietest toevoegen](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>U prestatiegegevens weergeven

1. Hallo profiler toocollect 10-15 minuten wachten tot gegevens en analyseren Hallo. 

2. Ga toohello **prestaties** blade in uw Application Insights-resource en hoe uw toepassing wordt uitgevoerd wanneer deze wordt belast.

   ![Prestaties weergeven](./media/enable-profiler-compute/aiperformance.png)

3. Selecteer Hallo pictogram onder **voorbeelden** tooopen hello **Trace weergave** blade.

   ![Hallo Trace weergave blade openen](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Werken met een bestaande sjabloon

1. Hello Azure Diagnostics brondeclaratie niet vinden in de sjabloon voor uw implementatie.
   
   Als u een declaratie geen hebt, kunt u een dat lijkt op Hallo declaratie in Hallo voorbeeld te volgen. U kunt bijwerken Hallo sjabloon van Hallo [Azure Resource Explorer website](https://resources.azure.com).

2. Hallo-uitgever van wijzigingen uit `Microsoft.Azure.Diagnostics` te`AIP.Diagnostics.Test`.

3. Voor `typeHandlerVersion`, gebruik `0.0`.

4. Zorg ervoor dat `autoUpgradeMinorVersion` te is ingesteld`true`.

5. Toevoegen van nieuwe Hallo `ApplicationInsightsProfiler` sink-exemplaar in Hallo `WadCfg` instellingenobject, zoals wordt weergegeven in Hallo voorbeeld te volgen:

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Hallo profiler op virtuele-machineschaalsets inschakelen
hoe tooenable Hallo profiler downloaden Hallo toosee [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) sjabloon. Toepassing hello dezelfde in een VM-sjabloon toohello diagnostics extensie resource voor Hallo virtuele-machineschaalset wijzigingen.

Zorg ervoor dat elk exemplaar in de schaalset hello toohello toegang tot internet. Hallo Profiler Agent kunt vervolgens verzenden Hallo verzamelde steekproeven tooApplication Insights voor het weergeven en analyseren.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Hallo profiler op Service Fabric-toepassingen inschakelen
1. Inrichten hello Service Fabric-cluster toohave hello Azure extensie voor diagnostische gegevens die Hallo Profiler Agent installeert.

2. Hallo Application Insights-SDK in Hallo project installeren en configureren van Hallo Application Insights-sleutel.

3. Toepassingstelemetrie code tooinstrument toevoegen.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Inrichten Hallo Service Fabric-cluster toohave hello Azure Diagnostics-extensie die Hallo Profiler Agent is geïnstalleerd
Een Service Fabric-cluster kan worden beveiligd of niet-beveiligde. U kunt één gateway-cluster toobe niet-beveiligde zodanig instellen een certificaat niet nodig is om toegang te krijgen. Clusters die als host voor zakelijke logica en gegevens moeten worden beveiligd. U kunt de profiler Hallo op zowel beveiligde als niet-beveiligde Service Fabric-clusters inschakelen. In dit scenario wordt een niet-beveiligde cluster gebruikt als een voorbeeld tooexplain welke wijzigingen zijn vereist tooenable Hallo profiler. U kunt een beveiligde cluster in Hallo inrichten dezelfde manier.

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

2. Hallo-sjabloon implementeren met een PowerShell-script:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Hallo Application Insights-SDK in Hallo project installeren en configureren van Hallo Application Insights-sleutel
Hallo Application Insights-SDK installeren vanaf Hallo [NuGet-pakket](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Zorg ervoor dat u een stabiele versie 2.3 of hoger installeert. 

Zie voor meer informatie over het configureren van Application Insights in uw projecten [met behulp van Service Fabric met Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-tooinstrument-telemetry"></a>Toepassingstelemetrie code tooinstrument toevoegen
1. Voor een stuk code dat u wilt dat tooinstrument, Voeg een met instructie omheen. 

   Hallo in Hallo voorbeeld te volgen, `RunAsync` methode is sommige werk en Hallo `telemetryClient` klasse vastgelegd Hallo telemetrie nadat deze is gestart. Hallo-gebeurtenis moet een unieke naam voor de toepassing hello.

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

2. Uw toepassing toohello Service Fabric-cluster implementeren. Hallo app toorun wacht 10 minuten. U kunt een load-test uitvoeren op Hallo-app voor betere effect. Ga toohello Application Insights-portal van **prestaties** blade, en u ziet enkele voorbeelden van profilering traceringen worden weergegeven.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Volgende stappen

- Hulp zoeken bij het oplossen van problemen in profiler [Profiler probleemoplossing](app-insights-profiler.md#troubleshooting).

- Meer informatie over de profiler Hallo in [Application Insights Profiler](app-insights-profiler.md).
