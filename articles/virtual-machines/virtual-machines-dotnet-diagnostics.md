---
title: aaaHow toouse Azure diagnostics in virtuele Machines | Microsoft Docs
description: Met behulp van Azure diagnostics toogather-gegevens van virtuele Machines van Azure voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="72b9a-103">Diagnostische gegevens in Azure Virtual Machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="72b9a-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="72b9a-104">Zie [overzicht van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="72b9a-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="72b9a-105">Hoe tooEnable diagnostische gegevens in een virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="72b9a-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="72b9a-106">Deze doorloop wordt beschreven hoe tooremotely Diagnostics tooan virtuele machine van Azure installeren vanaf een ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="72b9a-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="72b9a-107">U leert ook hoe een toepassing die wordt uitgevoerd op deze virtuele machine van Azure en verzendt telemetrie gegevens met tooimplement .NET Hallo [EventSource klasse][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="72b9a-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="72b9a-108">Azure Diagnostics is gebruikte toocollect Hallo Telemetrie en opslaan in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="72b9a-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="72b9a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="72b9a-109">Pre-requisites</span></span>
<span data-ttu-id="72b9a-110">Deze doorloop wordt ervan uitgegaan dat u hebt een Azure-abonnement en Visual Studio 2017 Hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="72b9a-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="72b9a-111">Als u niet een Azure-abonnement hebt, kunt u zich aanmeldt voor Hallo [gratis proefversie][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="72b9a-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="72b9a-112">Zorg ervoor dat te[installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="72b9a-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="72b9a-113">Stap 1: Een virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="72b9a-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="72b9a-114">Start Visual Studio 2017 op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="72b9a-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="72b9a-115">In Visual Studio Hallo **Server Explorer** Vouw **Azure**, met de rechtermuisknop op **virtuele Machines** Selecteer **virtuele Machine maken**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="72b9a-116">Selecteer uw Azure-abonnement in Hallo **Kies een abonnement** dialoogvenster en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="72b9a-117">Selecteer **Windows Server 2012 R2 Datacenter, juni 2017** in Hallo **selecteert u de installatiekopie van een virtuele Machine** dialoogvenster en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="72b9a-118">In Hallo **basisinstellingen van de virtuele Machine**, stel de naam van de virtuele machine Hallo te 'wadexample'.</span><span class="sxs-lookup"><span data-stu-id="72b9a-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="72b9a-119">Stel uw gebruikersnaam en wachtwoord en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="72b9a-120">In Hallo **Cloud Service-instellingen** dialoogvenster Maak een nieuwe cloudservice met de naam 'wadexampleVM'.</span><span class="sxs-lookup"><span data-stu-id="72b9a-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="72b9a-121">Maken van een nieuw opslagaccount met de naam 'wadexample' en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="72b9a-122">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="72b9a-123">Stap 2: Uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="72b9a-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="72b9a-124">Start Visual Studio 2017 op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="72b9a-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="72b9a-125">Maak een nieuwe Visual C#-consoletoepassing die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="72b9a-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="72b9a-126">Naam Hallo project 'WadExampleVM'.</span><span class="sxs-lookup"><span data-stu-id="72b9a-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="72b9a-128">Hallo inhoud van Program.cs met de volgende code Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="72b9a-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="72b9a-129">Hallo klasse **SampleEventSourceWriter** implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod**, **SetOther** en  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="72b9a-130">Hallo eerste parameter toohello WriteEvent-methode definieert Hallo-ID voor de betreffende gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="72b9a-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="72b9a-131">Hallo Run-methode implementeert een oneindige lus die elk Hallo logboekregistratiemethoden die worden geïmplementeerd in Hallo aanroept **SampleEventSourceWriter** klasse elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="72b9a-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="72b9a-132">Hallo-bestand opslaan en selecteer **Build Solution** van Hallo **bouwen** menu toobuild uw code.</span><span class="sxs-lookup"><span data-stu-id="72b9a-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="72b9a-133">Stap 3: Uw toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="72b9a-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="72b9a-134">Met de rechtermuisknop op Hallo **WadExampleVM** project in **Solution Explorer** en kies **map in Verkenner openen**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="72b9a-135">Navigeer toohello *bin\Debug* map en kopieer alle Hallo-bestanden (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="72b9a-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="72b9a-136">In **Server Explorer** met de rechtermuisknop op Hallo virtuele machine en kies **verbinding maken met behulp van extern bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="72b9a-137">Eenmaal zijn verbonden toohello VM maakt u een map met de naam WadExampleVM en plak de toepassingsbestanden van uw in Hallo map.</span><span class="sxs-lookup"><span data-stu-id="72b9a-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="72b9a-138">Hallo toepassing WadExampleVM.exe starten.</span><span class="sxs-lookup"><span data-stu-id="72b9a-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="72b9a-139">Hier ziet u een lege consolevenster.</span><span class="sxs-lookup"><span data-stu-id="72b9a-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="72b9a-140">Stap 4: Maken van uw configuratie van diagnostische en Hallo uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="72b9a-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="72b9a-141">Hallo openbare configuratie bestand schema definitie tooyour ontwikkelingscomputer door het uitvoeren van de volgende PowerShell-opdracht Hallo downloaden:</span><span class="sxs-lookup"><span data-stu-id="72b9a-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="72b9a-142">(Get-AzureServiceAvailableExtension - Extensienaam 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-codering utf8 - FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="72b9a-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="72b9a-143">Open een nieuw XML-bestand in Visual Studio, hetzij in een project dat u al hebt geopend of in een Visual Studio-instantie met geen openstaande projecten.</span><span class="sxs-lookup"><span data-stu-id="72b9a-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="72b9a-144">Selecteer in Visual Studio **toevoegen** -> **Nieuw Item...**</span><span class="sxs-lookup"><span data-stu-id="72b9a-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="72b9a-145"> -> **Visual C# items** -> **gegevens** -> **XML-bestand**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="72b9a-146">Bestand met de Hallo 'WadExample.xml'</span><span class="sxs-lookup"><span data-stu-id="72b9a-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="72b9a-147">Hallo WadConfig.xsd koppelen aan Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="72b9a-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="72b9a-148">Zorg ervoor dat Hallo WadExample.xml editorvenster Hallo actieve venster.</span><span class="sxs-lookup"><span data-stu-id="72b9a-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="72b9a-149">Druk op **F4** tooopen hello **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="72b9a-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="72b9a-150">Klik op Hallo **schema's** eigenschap in Hallo **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="72b9a-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="72b9a-151">Klik op Hallo **...**</span><span class="sxs-lookup"><span data-stu-id="72b9a-151">Click hello **…**</span></span> <span data-ttu-id="72b9a-152">in Hallo **schema's** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="72b9a-152">in hello **Schemas** property.</span></span> <span data-ttu-id="72b9a-153">Klik op Hallo **toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="72b9a-153">Click hello **Add…**</span></span> <span data-ttu-id="72b9a-154">knop en navigeer toohello locatie waar u Hallo XSD-bestand en selecteer Hallo bestand WadConfig.xsd opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="72b9a-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="72b9a-155">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-155">Click **OK**.</span></span>
4. <span data-ttu-id="72b9a-156">Hallo-inhoud van Hallo WadExample.xml configuratiebestand vervangen Hello na XML en sla het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="72b9a-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="72b9a-157">Dit configuratiebestand definieert een aantal prestaties tellers toocollect: één voor CPU-gebruik en één voor geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="72b9a-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="72b9a-158">Vervolgens definieert Hallo configuratie Hallo vier gebeurtenissen toohello methoden in Hallo SampleEventSourceWriter klasse overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="72b9a-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="72b9a-159">Stap 5: Extern installeren diagnostische gegevens op uw virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="72b9a-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="72b9a-160">Hallo PowerShell-cmdlets voor het beheren van diagnostische gegevens op een virtuele machine zijn: Set-AzureVMDiagnosticsExtension en Get-AzureVMDiagnosticsExtension verwijderen AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="72b9a-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="72b9a-161">Open op uw computer developer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72b9a-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="72b9a-162">Hallo script tooremotely installeren diagnostische gegevens niet uitvoeren op uw virtuele machine (vervangen `<user>` door uw gebruikersnaam van de directory.</span><span class="sxs-lookup"><span data-stu-id="72b9a-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="72b9a-163">Vervang `<StorageAccountKey>` met Hallo-toegangssleutel voor uw opslagaccount wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="72b9a-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="72b9a-164">Stap 6: Bekijk de telemetrische gegevens</span><span class="sxs-lookup"><span data-stu-id="72b9a-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="72b9a-165">In Visual Studio Hallo **Server Explorer** navigeren toohello wadexample storage-account.</span><span class="sxs-lookup"><span data-stu-id="72b9a-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="72b9a-166">Na het Hallo-virtuele machine actief is geweest ongeveer 5 minuten ziet u Hallo tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** en **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="72b9a-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="72b9a-167">Dubbelklik op een van de Hallo tabellen tooview Hallo telemetrie die is verzameld.</span><span class="sxs-lookup"><span data-stu-id="72b9a-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="72b9a-169">Schema van het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="72b9a-169">Configuration file schema</span></span>
<span data-ttu-id="72b9a-170">Hallo Diagnostics configuratiebestand definieert waarden die gebruikt tooinitialize diagnostische configuratie-instellingen zijn wanneer Hallo diagnostics agent wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="72b9a-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="72b9a-171">Zie Hallo [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="72b9a-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="72b9a-172">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="72b9a-172">Troubleshooting</span></span>
<span data-ttu-id="72b9a-173">Zie [probleemoplossing Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72b9a-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b9a-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72b9a-174">Next steps</span></span>
<span data-ttu-id="72b9a-175">[Zie een lijst met virtuele machine verwante artikelen van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange Hallo gegevens verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="72b9a-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
