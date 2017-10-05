---
title: Het gebruik van Azure diagnostics (.NET) met Cloudservices | Microsoft Docs
description: Met behulp van Azure diagnostics voor het verzamelen van gegevens van Azure-cloud-Services voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="cf883-103">Inschakelen van Azure Diagnostics in Azure-Cloudservices</span><span class="sxs-lookup"><span data-stu-id="cf883-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="cf883-104">Zie [overzicht van Azure Diagnostics](../azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="cf883-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="cf883-105">Het inschakelen van diagnostische gegevens in een Werkrol</span><span class="sxs-lookup"><span data-stu-id="cf883-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="cf883-106">Dit scenario wordt beschreven hoe u een Azure-werkrol die verzendt met behulp van de klasse .NET EventSource telemetriegegevens implementeert.</span><span class="sxs-lookup"><span data-stu-id="cf883-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="cf883-107">Azure Diagnostics wordt gebruikt om de telemetriegegevens verzamelen en opslaan in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="cf883-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="cf883-108">Bij het maken van een werkrol kunt Visual Studio automatisch de Diagnostics 1.0 als onderdeel van de oplossing in Azure SDK voor .NET 2.4 en eerdere versies.</span><span class="sxs-lookup"><span data-stu-id="cf883-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="cf883-109">De volgende instructies beschrijven het proces voor het maken van de werkrol Diagnostics 1.0 uitschakelen van de oplossing en het implementeren van diagnostische gegevens 1.2 of 1.3 aan uw werkrol.</span><span class="sxs-lookup"><span data-stu-id="cf883-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cf883-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cf883-110">Prerequisites</span></span>
<span data-ttu-id="cf883-111">In dit artikel wordt ervan uitgegaan dat u hebt een Azure-abonnement en gebruik van Visual Studio met de Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="cf883-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="cf883-112">Als u niet een Azure-abonnement hebt, kunt u zich aanmelden voor de [gratis proefversie][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="cf883-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="cf883-113">Zorg ervoor dat u [installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="cf883-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="cf883-114">Stap 1: Een Werkrol maken</span><span class="sxs-lookup"><span data-stu-id="cf883-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="cf883-115">Start **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="cf883-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="cf883-116">Maak een **Azure Cloud Service** project uit de **Cloud** sjabloon die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cf883-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="cf883-117">Noem het project 'WadExample' en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="cf883-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="cf883-118">Selecteer **Werkrol** en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="cf883-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="cf883-119">Het project wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf883-119">The project will be created.</span></span>
4. <span data-ttu-id="cf883-120">In **Solution Explorer**, dubbelklikt u op de **WorkerRole1** eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="cf883-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="cf883-121">In de **configuratie** tabblad un selectievakje **diagnostische gegevens inschakelen** uitschakelen Diagnostics 1.0 (Azure SDK 2.4 en eerder).</span><span class="sxs-lookup"><span data-stu-id="cf883-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="cf883-122">Het bouwen van uw oplossing om te controleren of er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="cf883-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="cf883-123">Stap 2: Uw code softwareontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="cf883-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="cf883-124">De inhoud van WorkerRole.cs vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="cf883-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="cf883-125">De klasse SampleEventSourceWriter, overgenomen van de [EventSource klasse][EventSource Class], implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod**, **SetOther** en **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="cf883-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="cf883-126">De eerste parameter voor de **WriteEvent** methode definieert u de ID voor de betreffende gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="cf883-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="cf883-127">De methode Run implementeert een oneindige lus die voor elk van de logboekregistratiemethoden geïmplementeerd aanroept in de **SampleEventSourceWriter** klasse elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="cf883-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through the loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="cf883-128">Stap 3: Uw Werkrol implementeren</span><span class="sxs-lookup"><span data-stu-id="cf883-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="cf883-129">Uw werkrol door te selecteren in Azure uit vanuit Visual Studio implementeert het **WadExample** project in Solution Explorer vervolgens **publiceren** van de **bouwen** menu.</span><span class="sxs-lookup"><span data-stu-id="cf883-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="cf883-130">Kies uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="cf883-130">Choose your subscription.</span></span>
3. <span data-ttu-id="cf883-131">In de **Microsoft Azure Publish Settings** dialoogvenster Selecteer **nieuwe maken...** .</span><span class="sxs-lookup"><span data-stu-id="cf883-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="cf883-132">In de **Cloudservice maken en Storage-Account** dialoogvenster, voer een **naam** (bijvoorbeeld ' WadExample') en selecteer een regio of affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="cf883-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="cf883-133">Stel de **omgeving** naar **fasering**.</span><span class="sxs-lookup"><span data-stu-id="cf883-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="cf883-134">Wijzigen van een andere **instellingen** als in de betreffende en klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="cf883-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="cf883-135">Wanneer implementatie is voltooid, controleert u of in de Azure portal dat uw service in de cloud zich in een **met** status.</span><span class="sxs-lookup"><span data-stu-id="cf883-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="cf883-136">Stap 4: Uw configuratiebestand diagnostische gegevens maken en de uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="cf883-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="cf883-137">De schemadefinitie van de openbare configuratie bestand downloaden door het uitvoeren van de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="cf883-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="cf883-138">Toevoegen van een XML-bestand naar uw **WorkerRole1** project door met de rechtermuisknop op de **WorkerRole1** project en selecteer **toevoegen** -> **Nieuw Item...**</span><span class="sxs-lookup"><span data-stu-id="cf883-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="cf883-139"> -> **Visual C# items** -> **gegevens** -> **XML-bestand**.</span><span class="sxs-lookup"><span data-stu-id="cf883-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="cf883-140">Noem het bestand 'WadExample.xml'.</span><span class="sxs-lookup"><span data-stu-id="cf883-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="cf883-142">De WadConfig.xsd koppelen aan het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="cf883-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="cf883-143">Zorg ervoor dat de editor voor WadExample.xml het actieve venster.</span><span class="sxs-lookup"><span data-stu-id="cf883-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="cf883-144">Druk op **F4** openen de **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="cf883-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="cf883-145">Klik op de **schema's** eigenschap in de **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="cf883-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="cf883-146">Klik op de **...**</span><span class="sxs-lookup"><span data-stu-id="cf883-146">Click the **…**</span></span> <span data-ttu-id="cf883-147">in de **schema's** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cf883-147">in the **Schemas** property.</span></span> <span data-ttu-id="cf883-148">Klik op de knop **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="cf883-148">Click the **Add…**</span></span> <span data-ttu-id="cf883-149">knop en navigeer naar de locatie waar u het XSD-bestand hebt opgeslagen en selecteert u het bestand WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="cf883-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="cf883-150">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf883-150">Click **OK**.</span></span>

4. <span data-ttu-id="cf883-151">De inhoud van het configuratiebestand WadExample.xml vervangen door de volgende XML en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="cf883-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="cf883-152">Dit configuratiebestand definieert een aantal prestatiemeteritems voor het verzamelen van: één voor CPU-gebruik en één voor geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="cf883-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="cf883-153">De configuratie definieert de vier gebeurtenissen die overeenkomt met de methoden in de klasse SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="cf883-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="cf883-154">Stap 5: Diagnostische gegevens op uw Werkrol installeren</span><span class="sxs-lookup"><span data-stu-id="cf883-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="cf883-155">De PowerShell-cmdlets voor het beheren van diagnostische gegevens op een web- of worker-rol zijn: Set-AzureServiceDiagnosticsExtension en Get-AzureServiceDiagnosticsExtension verwijderen AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="cf883-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="cf883-156">Open Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf883-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="cf883-157">Voer het script voor het installeren van diagnostische gegevens op uw werkrol (Vervang *StorageAccountKey* door de sleutel van het opslagaccount voor uw opslagaccount wadexample en *config_path* met het pad naar de *WadExample.xml* bestand):</span><span class="sxs-lookup"><span data-stu-id="cf883-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="cf883-158">Stap 6: Bekijk de telemetrische gegevens</span><span class="sxs-lookup"><span data-stu-id="cf883-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="cf883-159">In de Visual Studio **Server Explorer**, gaat u naar het opslagaccount wadexample.</span><span class="sxs-lookup"><span data-stu-id="cf883-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="cf883-160">Nadat de cloudservice actief is geweest ongeveer vijf (5) minuten, ziet u de tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** en **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="cf883-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="cf883-161">Dubbelklik op een van de tabellen om weer te geven van de telemetrie die is verzameld.</span><span class="sxs-lookup"><span data-stu-id="cf883-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="cf883-163">Schema van het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="cf883-163">Configuration File Schema</span></span>
<span data-ttu-id="cf883-164">Het configuratiebestand van de diagnostische gegevens definieert waarden die worden gebruikt voor het initialiseren van diagnostische configuratie-instellingen wanneer de diagnostics-agent wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="cf883-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="cf883-165">Zie de [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="cf883-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cf883-166">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cf883-166">Troubleshooting</span></span>
<span data-ttu-id="cf883-167">Als u problemen ondervindt, raadpleegt u [probleemoplossing Azure Diagnostics](../azure-diagnostics-troubleshooting.md) voor meer informatie over bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="cf883-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf883-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf883-168">Next Steps</span></span>
<span data-ttu-id="cf883-169">[Een overzicht van verwante Azure virtuele machines diagnostische artikelen](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) wijzigen van de gegevens die u verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="cf883-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
