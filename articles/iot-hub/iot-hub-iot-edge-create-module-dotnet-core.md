---
title: Een Azure IoT-Edge-Module maken met C# | Microsoft Docs
description: Deze zelfstudie gepresenteerd het schrijven van een Aanmeldingsprompt gegevens converter module met behulp van de meest recente Azure IoT rand NuGet-pakketten, Visual Studio Code en C#.
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: Azure iot, zelfstudie, module, nuget, vscode, csharp, rand
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="d6c3b-104">Een Azure IoT-Edge-Module maken met C & #x23;</span><span class="sxs-lookup"><span data-stu-id="d6c3b-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="d6c3b-105">Deze zelfstudie voor het maken van een module voor gepresenteerd `Azure IoT Edge` met `Visual Studio Code` en `C#`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="d6c3b-106">In deze zelfstudie we doorlopen omgeving instellen en het schrijven van een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) gegevens converter module met behulp van de meest recente `Azure IoT Edge NuGet` pakketten.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="d6c3b-107">Deze zelfstudie maakt gebruik van de `.NET Core SDK`, die ondersteuning biedt voor meerdere platforms compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="d6c3b-108">De volgende zelfstudie is geschreven met behulp van de `Windows 10` besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="d6c3b-109">Sommige van de opdrachten in deze zelfstudie kan afwijken afhankelijk van uw `development environment`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d6c3b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6c3b-110">Prerequisites</span></span>

<span data-ttu-id="d6c3b-111">In deze sectie we set-up uw omgeving voor `Azure IoT Edge` module ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="d6c3b-112">Van toepassing op beide **64-bits Windows** en **64-bits Linux (8 Ubuntu/Debian)** besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="d6c3b-113">De volgende software is vereist:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-113">The following software is required:</span></span>

- [<span data-ttu-id="d6c3b-114">GIT-Client</span><span class="sxs-lookup"><span data-stu-id="d6c3b-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="d6c3b-115">.NET Core-SDK</span><span class="sxs-lookup"><span data-stu-id="d6c3b-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="d6c3b-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d6c3b-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="d6c3b-117">U hoeft niet voor het klonen van de opslagplaats voor dit voorbeeld, maar alle van de voorbeeldcode besproken in deze zelfstudie bevindt zich in de volgende opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="d6c3b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="d6c3b-119">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="d6c3b-119">Getting started</span></span>

1. <span data-ttu-id="d6c3b-120">Installeer `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="d6c3b-121">Installeer `Visual Studio Code` en de `C# extension` vanuit Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="d6c3b-122">Bekijk waarvoor [snelle zelfstudie](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) over het aan de slag met `Visual Studio Code` en de `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="d6c3b-123">Maken van de rand van Azure IoT converter-module</span><span class="sxs-lookup"><span data-stu-id="d6c3b-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="d6c3b-124">Een nieuwe initialisatie `.NET Core` class library C#-project:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="d6c3b-125">Open een opdrachtprompt (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="d6c3b-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="d6c3b-126">Navigeer naar de map waarin u wilt maken van de `C#` project.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="d6c3b-127">Type **dotnet nieuwe classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="d6c3b-128">Deze opdracht maakt u een lege klasse aangeroepen `Class1.cs` in uw projectdirectory.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="d6c3b-129">Navigeer naar de map waar we zojuist hebben gemaakt de class library-project door te typen **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="d6c3b-130">Open het project in `Visual Studio Code` door **code.**.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="d6c3b-131">Nadat het project is geopend `Visual Studio Code`, klikt u op de **IoTEdgeConverterModule.csproj** het bestand te openen zoals weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Venster van Visual Studio Code bewerken](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="d6c3b-133">Plaats de `XML` blob wordt weergegeven in het volgende codefragment tussen de afsluitende `PropertyGroup` code en de afsluitcode `Project` tag; regel zes in de voorgaande afbeelding en sla het bestand door te drukken `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="d6c3b-134">Nadat u hebt opgeslagen de `.csproj` bestand `Visual Studio Code` moet worden gevraagd met een `unresolved dependencies` dialoogvenster zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Visual Studio Code terugzetten afhankelijkheden dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="d6c3b-136">een) Klik op `Restore` alle verwijzingen naar de in de projecten te herstellen `.csproj` bestand inclusief de `PackageReferences` toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="d6c3b-137">b) `Visual Studio Code` maakt automatisch het `project.assets.json` bestand in uw projecten `obj` map.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="d6c3b-138">Dit bestand bevat informatie over de afhankelijkheden van uw project om toekomstige herstelbewerkingen sneller.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="d6c3b-139">`.NET Core Tools`zijn nu MSBuild-systemen.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="d6c3b-140">Wat betekent dat een `.csproj` projectbestand is gemaakt in plaats van een `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="d6c3b-141">Als `Visual Studio Code` vraagt u die in orde is niet kunt we dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="d6c3b-142">Open de `Visual Studio Code` geïntegreerde terminalvenster door op de `Ctrl`  +  `backtick` sleutels of via de menu's `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="d6c3b-143">In de `Integrated Terminal` venstertype **dotnet terugzetten**.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="d6c3b-144">Wijzig de naam van de `Class1.cs` van het bestand in `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="d6c3b-145">a) te Wijzig de naam van het bestand eerst Klik op het bestand vervolgens drukt u op de `F2` sleutel.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="d6c3b-146">b) type in de nieuwe naam **BleConverterModule**, zoals in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Visual Studio Code naam van een klasse](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="d6c3b-148">Vervang de bestaande code in de `BleConverterModule.cs` bestand kopiëren en plakken van het volgende codefragment in uw `BleConverterModule.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. <span data-ttu-id="d6c3b-149">Sla het bestand door te drukken `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="d6c3b-150">Maak een nieuw bestand genaamd `Untitled-1` door op de `Ctrl`  +  `N` sleutels zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Visual Studio Code nieuw bestand](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="d6c3b-152">Deserialiseren van de `JSON` -object dat we van de gesimuleerde ontvangen `BLE` apparaat, Kopieer de volgende code in de `Untitled-1` venster bestand code-editor.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. <span data-ttu-id="d6c3b-153">Sla het bestand als `BleData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="d6c3b-154">In het dialoogvenster Opslaan als, in de `Save as Type` Selecteer vervolgkeuzemenu `C# (*.cs;*.csx)` zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Visual Studio Code opslaan als een dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="d6c3b-156">Maak een nieuw bestand genaamd `Untitled-1` door op de `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="d6c3b-157">Kopieer en plak het volgende codefragment in de `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="d6c3b-158">Deze klasse is een `Azure IoT Edge` module waarmee we gebruiken de gegevens ontvangen van onze `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. <span data-ttu-id="d6c3b-159">Sla het bestand als `DotNetPrinterModule.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d6c3b-160">In het dialoogvenster Opslaan als, in de `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="d6c3b-161">Maak een nieuw bestand genaamd `Untitled-1` door op de `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="d6c3b-162">Deserialiseren van de `JSON` -object dat we van ontvangen de `BleConverterModule`, kopiëren en plak de volgende code codefragment in de `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. <span data-ttu-id="d6c3b-163">Sla het bestand als `BleConverterData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d6c3b-164">In het dialoogvenster Opslaan als, in de `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="d6c3b-165">Maak een nieuw bestand genaamd `Untitled-1` door op de `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="d6c3b-166">Kopieer en plak het volgende codefragment in de `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. <span data-ttu-id="d6c3b-167">Sla het bestand als `gw-config.json` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d6c3b-168">In het dialoogvenster Opslaan als, in de `Save as Type` vervolgkeuzemenu Selecteer `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="d6c3b-169">Om in te schakelen van het configuratiebestand kopiëren naar de uitvoermap, werken de `IoTEdgeConverterModule.csproj` met de volgende XML-blob:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="d6c3b-170">De bijgewerkte `IoTEdgeConverterModule.csproj` moet eruitzien als in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Visual Studio Code bijgewerkt .csproj-bestand](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="d6c3b-172">Maak een nieuw bestand genaamd `Untitled-1` door op de `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="d6c3b-173">Kopieer en plak het volgende codefragment in de `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="d6c3b-174">Sla het bestand als `binplace.ps1` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="d6c3b-175">In het dialoogvenster Opslaan als, in de `Save as Type` vervolgkeuzemenu Selecteer `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="d6c3b-176">Bouw het project door op de `Ctrl`  +  `Shift`  +  `B` sleutels.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="d6c3b-177">Als u het project voor het eerst bouwen `Visual Studio Code` vraagt u met de `No build task defined.` dialoogvenster zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Dialoogvenster voor Visual Studio Code build-taak](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="d6c3b-179">een) Klik op de `Configure Build Task` knop.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="d6c3b-180">b) in de `Select a Task Runner` vervolgkeuzemenu in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="d6c3b-181">Selecteer `.NET Core` zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Visual Studio Code selecteren een dialoogvenster taak](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="d6c3b-183">c) op de `.NET Core` artikel maakt de `tasks.json` bestand uw `.vscode` directory en opent u het bestand in de `code editor` venster.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="d6c3b-184">Er is niet nodig om te wijzigen van dit bestand, het tabblad sluit.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="d6c3b-185">Open de `Visual Studio Code` geïntegreerde terminalvenster door op de `Ctrl`  +  `backtick` sleutels of via de menu's `View`  ->  `Integrated Terminal` en het type **.\binplace.ps1** in de `PowerShell` opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="d6c3b-186">Met deze opdracht wordt alle afhankelijkheden van onze gekopieerd naar de uitvoermap.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="d6c3b-187">Navigeer naar de uitvoermap projecten in de `Integrated Terminal` venster door op te geven **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="d6c3b-188">Het voorbeeldproject uitvoeren door te typen **. \gw.exe gw-config.json** in de `Integrated Terminal` venster prompt.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="d6c3b-189">Als u nauw de stappen in deze zelfstudie hebt gevolgd, u moet nu worden uitgevoerd de `Azure IoT Edge BLE Data Converter Module` voorbeeldproject zoals te zien is in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d6c3b-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Voorbeeld van het gesimuleerde apparaat uitgevoerd in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="d6c3b-191">Als u wilt dat de toepassing beëindigt, drukt u op de `<Enter>` sleutel.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="d6c3b-192">Het wordt niet aangeraden om te gebruiken `Ctrl`  +  `C` worden beëindigd of dat de `IoT Edge` application gateway (dat wil zeggen, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="d6c3b-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="d6c3b-193">Als u deze actie kan ertoe leiden dat het proces abnormaal beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d6c3b-193">As this action may cause the process to terminate abnormally.</span></span>

