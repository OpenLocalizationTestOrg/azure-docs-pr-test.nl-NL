---
title: Het gebruik van Azure diagnostics in virtuele Machines | Microsoft Docs
description: Met behulp van Azure diagnostics voor het verzamelen van gegevens van virtuele Machines van Azure voor foutopsporing, prestaties, bewaking, analyse van het netwerkverkeer en meer meten.
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="a05c3-103">Diagnostische gegevens in Azure Virtual Machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="a05c3-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="a05c3-104">Zie [overzicht van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) voor de achtergrond op Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a05c3-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="a05c3-105">Diagnostische gegevens in een virtuele Machine inschakelen</span><span class="sxs-lookup"><span data-stu-id="a05c3-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="a05c3-106">Deze doorloop wordt beschreven hoe extern diagnostische gegevens naar een virtuele machine van Azure installeren vanaf een ontwikkelingscomputer.</span><span class="sxs-lookup"><span data-stu-id="a05c3-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="a05c3-107">U leert ook hoe voor het implementeren van een toepassing die wordt uitgevoerd op deze virtuele machine van Azure en verzendt met behulp van de .NET-telemetriegegevens [EventSource klasse][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="a05c3-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="a05c3-108">Azure Diagnostics wordt gebruikt voor het verzamelen van de Telemetrie en opslaan in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="a05c3-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="a05c3-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a05c3-109">Pre-requisites</span></span>
<span data-ttu-id="a05c3-110">Deze doorloop wordt ervan uitgegaan dat u hebt een Azure-abonnement en Visual Studio 2017 gebruikt met de Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="a05c3-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="a05c3-111">Als u niet een Azure-abonnement hebt, kunt u zich aanmelden voor de [gratis proefversie][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="a05c3-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="a05c3-112">Zorg ervoor dat u [installeren en configureren van Azure PowerShell versie 0.8.7 of hoger][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="a05c3-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="a05c3-113">Stap 1: Een virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="a05c3-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="a05c3-114">Start Visual Studio 2017 op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a05c3-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="a05c3-115">In de Visual Studio **Server Explorer** Vouw **Azure**, met de rechtermuisknop op **virtuele Machines** Selecteer **virtuele Machine maken**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="a05c3-116">Selecteer uw Azure-abonnement in de **Kies een abonnement** dialoogvenster en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="a05c3-117">Selecteer **Windows Server 2012 R2 Datacenter, juni 2017** in de **selecteert u de installatiekopie van een virtuele Machine** dialoogvenster en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="a05c3-118">In de **basisinstellingen van de virtuele Machine**, de naam van virtuele machine 'wadexample' ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a05c3-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="a05c3-119">Stel uw gebruikersnaam en wachtwoord en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="a05c3-120">In de **Cloud Service-instellingen** dialoogvenster Maak een nieuwe cloudservice met de naam 'wadexampleVM'.</span><span class="sxs-lookup"><span data-stu-id="a05c3-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="a05c3-121">Maken van een nieuw opslagaccount met de naam 'wadexample' en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="a05c3-122">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="a05c3-123">Stap 2: Uw toepassing maken</span><span class="sxs-lookup"><span data-stu-id="a05c3-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="a05c3-124">Start Visual Studio 2017 op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a05c3-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="a05c3-125">Maak een nieuwe Visual C#-consoletoepassing die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="a05c3-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="a05c3-126">Noem het project 'WadExampleVM'.</span><span class="sxs-lookup"><span data-stu-id="a05c3-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="a05c3-128">Vervang de inhoud van Program.cs met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="a05c3-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="a05c3-129">De klasse **SampleEventSourceWriter** implementeert vier logboekregistratiemethoden: **SendEnums**, **MessageMethod**, **SetOther** en **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="a05c3-130">De eerste parameter voor de WriteEvent-methode definieert de ID voor de betreffende gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="a05c3-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="a05c3-131">De methode Run implementeert een oneindige lus die voor elk van de logboekregistratiemethoden geïmplementeerd aanroept in de **SampleEventSourceWriter** klasse elke 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="a05c3-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="a05c3-132">Sla het bestand en selecteer **Build Solution** van de **bouwen** menu voor het bouwen van uw code.</span><span class="sxs-lookup"><span data-stu-id="a05c3-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="a05c3-133">Stap 3: Uw toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="a05c3-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="a05c3-134">Met de rechtermuisknop op de **WadExampleVM** project in **Solution Explorer** en kies **map in Verkenner openen**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="a05c3-135">Navigeer naar de *bin\Debug* map en kopieer alle bestanden (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="a05c3-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="a05c3-136">In **Server Explorer** met de rechtermuisknop op de virtuele machine en kies **verbinding maken met behulp van extern bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="a05c3-137">Maak een map met de naam WadExampleVM en uw toepassing naar de map bestanden plakken eenmaal zijn verbonden met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a05c3-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="a05c3-138">Start de toepassing WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="a05c3-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="a05c3-139">Hier ziet u een lege consolevenster.</span><span class="sxs-lookup"><span data-stu-id="a05c3-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="a05c3-140">Stap 4: De configuratie van diagnostische gegevens maakt en de uitbreiding te installeren</span><span class="sxs-lookup"><span data-stu-id="a05c3-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="a05c3-141">De schemadefinitie van de openbare configuratie voor bestand naar uw ontwikkelcomputer downloaden door het uitvoeren van de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="a05c3-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="a05c3-142">(Get-AzureServiceAvailableExtension - Extensienaam 'PaaSDiagnostics' - ProviderNamespace 'Microsoft.Azure.Diagnostics'). PublicConfigurationSchema | Out-File-codering utf8 - FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="a05c3-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="a05c3-143">Open een nieuw XML-bestand in Visual Studio, hetzij in een project dat u al hebt geopend of in een Visual Studio-instantie met geen openstaande projecten.</span><span class="sxs-lookup"><span data-stu-id="a05c3-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="a05c3-144">Selecteer in Visual Studio **toevoegen** -> **Nieuw Item...**</span><span class="sxs-lookup"><span data-stu-id="a05c3-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="a05c3-145"> -> **Visual C# items** -> **gegevens** -> **XML-bestand**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="a05c3-146">Noem het bestand 'WadExample.xml'</span><span class="sxs-lookup"><span data-stu-id="a05c3-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="a05c3-147">De WadConfig.xsd koppelen aan het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="a05c3-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="a05c3-148">Zorg ervoor dat de editor voor WadExample.xml het actieve venster.</span><span class="sxs-lookup"><span data-stu-id="a05c3-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="a05c3-149">Druk op **F4** openen de **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="a05c3-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="a05c3-150">Klik op de **schema's** eigenschap in de **eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="a05c3-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="a05c3-151">Klik op de **...**</span><span class="sxs-lookup"><span data-stu-id="a05c3-151">Click the **…**</span></span> <span data-ttu-id="a05c3-152">in de **schema's** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a05c3-152">in the **Schemas** property.</span></span> <span data-ttu-id="a05c3-153">Klik op de knop **Toevoegen...**</span><span class="sxs-lookup"><span data-stu-id="a05c3-153">Click the **Add…**</span></span> <span data-ttu-id="a05c3-154">knop en navigeer naar de locatie waar u het XSD-bestand hebt opgeslagen en selecteert u het bestand WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="a05c3-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="a05c3-155">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-155">Click **OK**.</span></span>
4. <span data-ttu-id="a05c3-156">De inhoud van het configuratiebestand WadExample.xml vervangen door de volgende XML en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="a05c3-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="a05c3-157">Dit configuratiebestand definieert een aantal prestatiemeteritems voor het verzamelen van: één voor CPU-gebruik en één voor geheugengebruik.</span><span class="sxs-lookup"><span data-stu-id="a05c3-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="a05c3-158">De configuratie definieert de vier gebeurtenissen die overeenkomt met de methoden in de klasse SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="a05c3-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="a05c3-159">Stap 5: Extern installeren diagnostische gegevens op uw virtuele Machine van Azure</span><span class="sxs-lookup"><span data-stu-id="a05c3-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="a05c3-160">De PowerShell-cmdlets voor het beheren van diagnostische gegevens op een virtuele machine zijn: Set-AzureVMDiagnosticsExtension en Get-AzureVMDiagnosticsExtension verwijderen AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="a05c3-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="a05c3-161">Open op uw computer developer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a05c3-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="a05c3-162">Voer het script op afstand te installeren diagnostische gegevens op de virtuele machine (vervangen `<user>` door uw gebruikersnaam van de directory.</span><span class="sxs-lookup"><span data-stu-id="a05c3-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="a05c3-163">Vervang `<StorageAccountKey>` door de sleutel van het opslagaccount voor uw opslagaccount wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="a05c3-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="a05c3-164">Stap 6: Bekijk de telemetrische gegevens</span><span class="sxs-lookup"><span data-stu-id="a05c3-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="a05c3-165">In de Visual Studio **Server Explorer** gaat u naar het opslagaccount wadexample.</span><span class="sxs-lookup"><span data-stu-id="a05c3-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="a05c3-166">Nadat de virtuele machine actief is geweest ongeveer 5 minuten ziet u de tabellen **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** en **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="a05c3-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="a05c3-167">Dubbelklik op een van de tabellen om weer te geven van de telemetrie die is verzameld.</span><span class="sxs-lookup"><span data-stu-id="a05c3-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="a05c3-169">Schema van het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="a05c3-169">Configuration file schema</span></span>
<span data-ttu-id="a05c3-170">Het configuratiebestand van de diagnostische gegevens definieert waarden die worden gebruikt voor het initialiseren van diagnostische configuratie-instellingen wanneer de diagnostics-agent wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a05c3-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="a05c3-171">Zie de [nieuwste schemaverwijzing](https://msdn.microsoft.com/library/azure/mt634524.aspx) voor geldige waarden en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a05c3-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a05c3-172">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="a05c3-172">Troubleshooting</span></span>
<span data-ttu-id="a05c3-173">Zie [probleemoplossing Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a05c3-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a05c3-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a05c3-174">Next steps</span></span>
<span data-ttu-id="a05c3-175">[Zie een lijst met virtuele machine verwante artikelen van Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) wijzigen van de gegevens die u verzamelt, oplossen van problemen of meer informatie over diagnostische gegevens over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="a05c3-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
