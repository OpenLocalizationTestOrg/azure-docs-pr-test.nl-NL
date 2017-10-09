---
title: aaaCreate een Azure IoT Edge-Module met C# | Microsoft Docs
description: Deze zelfstudie wordt gepresenteerd hoe toowrite een Aanmeldingsprompt gegevens converter module met de meest recente Azure IoT rand NuGet-pakketten, Visual Studio Code en C# Hallo.
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
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="713a7-104">Een Azure IoT-Edge-Module maken met C & #x23;</span><span class="sxs-lookup"><span data-stu-id="713a7-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="713a7-105">Deze zelfstudie gepresenteerd hoe toocreate een module voor `Azure IoT Edge` met `Visual Studio Code` en `C#`.</span><span class="sxs-lookup"><span data-stu-id="713a7-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="713a7-106">In deze zelfstudie we omgeving opzet hebt doorlopen en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) meest recente gegevens converter module met Hallo `Azure IoT Edge NuGet` pakketten.</span><span class="sxs-lookup"><span data-stu-id="713a7-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="713a7-107">Deze zelfstudie maakt gebruik van Hallo `.NET Core SDK`, die ondersteuning biedt voor meerdere platforms compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="713a7-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="713a7-108">Hallo volgende zelfstudie is geschreven met behulp van Hallo `Windows 10` besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="713a7-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="713a7-109">Bepaalde Hallo-opdrachten in deze zelfstudie kan afwijken afhankelijk van uw `development environment`.</span><span class="sxs-lookup"><span data-stu-id="713a7-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="713a7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="713a7-110">Prerequisites</span></span>

<span data-ttu-id="713a7-111">In deze sectie we set-up uw omgeving voor `Azure IoT Edge` module ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="713a7-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="713a7-112">Toepassing tooboth **64-bits Windows** en **64-bits Linux (8 Ubuntu/Debian)** besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="713a7-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="713a7-113">Hallo volgende software is vereist:</span><span class="sxs-lookup"><span data-stu-id="713a7-113">hello following software is required:</span></span>

- [<span data-ttu-id="713a7-114">GIT-Client</span><span class="sxs-lookup"><span data-stu-id="713a7-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="713a7-115">.NET Core-SDK</span><span class="sxs-lookup"><span data-stu-id="713a7-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="713a7-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="713a7-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="713a7-117">U hoeft geen tooclone Hallo opslagplaats voor dit voorbeeld, maar alle Hallo voorbeeldcode besproken in deze zelfstudie bevindt zich in Hallo opslagplaats te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="713a7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="713a7-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="713a7-119">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="713a7-119">Getting started</span></span>

1. <span data-ttu-id="713a7-120">Installeer `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="713a7-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="713a7-121">Installeer `Visual Studio Code` en Hallo `C# extension` van Hallo Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="713a7-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="713a7-122">Bekijk waarvoor [snelle zelfstudie](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) over hoe tooget met behulp van gestart `Visual Studio Code` en Hallo `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="713a7-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="713a7-123">Hello Azure IoT rand converter module maken</span><span class="sxs-lookup"><span data-stu-id="713a7-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="713a7-124">Een nieuwe initialisatie `.NET Core` class library C#-project:</span><span class="sxs-lookup"><span data-stu-id="713a7-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="713a7-125">Open een opdrachtprompt (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="713a7-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="713a7-126">Navigeer toohello map waar u toocreate hello wilt `C#` project.</span><span class="sxs-lookup"><span data-stu-id="713a7-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="713a7-127">Type **dotnet nieuwe classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="713a7-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="713a7-128">Deze opdracht maakt u een lege klasse aangeroepen `Class1.cs` in uw projectdirectory.</span><span class="sxs-lookup"><span data-stu-id="713a7-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="713a7-129">Navigeer toohello map waar we zojuist hebben gemaakt Hallo class library-project door te typen **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="713a7-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="713a7-130">Open Hallo-project in `Visual Studio Code` door **code.**.</span><span class="sxs-lookup"><span data-stu-id="713a7-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="713a7-131">Zodra het Hallo-project wordt geopend in `Visual Studio Code`, klikt u op Hallo **IoTEdgeConverterModule.csproj** tooopen Hallo bestand, zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Venster van Visual Studio Code bewerken](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="713a7-133">Hallo invoegen `XML` blob wordt weergegeven in het codefragment na tussen Hallo sluiten Hallo `PropertyGroup` labelen en Hallo sluiten `Project` tag; regel zes in Hallo voorafgaand aan de installatiekopie van bestand en sla Hallo door te drukken `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="713a7-134">Nadat u hebt opgeslagen Hallo `.csproj` bestand `Visual Studio Code` moet worden gevraagd met een `unresolved dependencies` dialoogvenster zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Visual Studio Code terugzetten afhankelijkheden dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="713a7-136">een) Klik op `Restore` toorestore alle Hallo verwijzingen in Hallo projecten `.csproj` bestand inclusief Hallo `PackageReferences` toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="713a7-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="713a7-137">b) `Visual Studio Code` maakt automatisch Hallo `project.assets.json` bestand in uw projecten `obj` map.</span><span class="sxs-lookup"><span data-stu-id="713a7-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="713a7-138">Dit bestand bevat informatie over uw project afhankelijkheden toomake daaropvolgende herstelacties sneller.</span><span class="sxs-lookup"><span data-stu-id="713a7-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="713a7-139">`.NET Core Tools`zijn nu MSBuild-systemen.</span><span class="sxs-lookup"><span data-stu-id="713a7-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="713a7-140">Wat betekent dat een `.csproj` projectbestand is gemaakt in plaats van een `project.json`.</span><span class="sxs-lookup"><span data-stu-id="713a7-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="713a7-141">Als `Visual Studio Code` vraagt u die in orde is niet kunt we dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="713a7-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="713a7-142">Open Hallo `Visual Studio Code` geïntegreerde terminalvenster door Hallo drukken `Ctrl`  +  `backtick` sleutels of met behulp van menu's Hallo `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="713a7-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="713a7-143">In Hallo `Integrated Terminal` venstertype **dotnet terugzetten**.</span><span class="sxs-lookup"><span data-stu-id="713a7-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="713a7-144">Wijzig de naam van Hallo `Class1.cs` bestand te`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="713a7-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="713a7-145">een) toorename Hallo bestand eerst klikt u op Hallo-bestand en druk op Hallo `F2` sleutel.</span><span class="sxs-lookup"><span data-stu-id="713a7-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="713a7-146">b) type in de nieuwe naam Hallo **BleConverterModule**, zoals in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Visual Studio Code naam van een klasse](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="713a7-148">Vervang de bestaande code Hallo in Hallo `BleConverterModule.cs` bestand door te kopiëren en plakken Hallo volgende codefragment in uw `BleConverterModule.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="713a7-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="713a7-149">Hallo-bestand opslaan door te drukken `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="713a7-150">Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Visual Studio Code nieuw bestand](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="713a7-152">toodeserialize hello `JSON` -object dat we van Hallo gesimuleerde ontvangen `BLE` apparaat, kopie Hallo na de code in Hallo `Untitled-1` venster bestand code-editor.</span><span class="sxs-lookup"><span data-stu-id="713a7-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="713a7-153">Hallo bestand opslaan als `BleData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="713a7-154">Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` Selecteer vervolgkeuzemenu `C# (*.cs;*.csx)` zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Visual Studio Code opslaan als een dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="713a7-156">Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="713a7-157">Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="713a7-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="713a7-158">Deze klasse is een `Azure IoT Edge` module waarmee we toooutput Hallo gegevens ontvangen gebruiken van onze `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="713a7-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="713a7-159">Hallo bestand opslaan als `DotNetPrinterModule.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="713a7-160">Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="713a7-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="713a7-161">Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="713a7-162">Hallo toodeserialize `JSON` -object dat we van Hallo ontvangen `BleConverterModule`, kopiëren en plakken Hallo volgende codefragment in Hallo `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="713a7-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="713a7-163">Hallo bestand opslaan als `BleConverterData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="713a7-164">Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="713a7-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="713a7-165">Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="713a7-166">Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="713a7-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="713a7-167">Hallo bestand opslaan als `gw-config.json` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="713a7-168">Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="713a7-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="713a7-169">directory, update Hallo tooenable kopiëren van Hallo configuration file toohello uitvoer `IoTEdgeConverterModule.csproj` Hello XML-blob te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="713a7-170">Hallo bijgewerkt `IoTEdgeConverterModule.csproj` moet eruit Hallo de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="713a7-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Visual Studio Code bijgewerkt .csproj-bestand](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="713a7-172">Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="713a7-173">Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand.</span><span class="sxs-lookup"><span data-stu-id="713a7-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="713a7-174">Hallo bestand opslaan als `binplace.ps1` door te drukken `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="713a7-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="713a7-175">Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="713a7-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="713a7-176">Hallo-project te bouwen door Hallo drukken `Ctrl`  +  `Shift`  +  `B` sleutels.</span><span class="sxs-lookup"><span data-stu-id="713a7-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="713a7-177">Als u de eerste keer voor Hallo-project voor Hallo bouwen `Visual Studio Code` vraagt u Hello `No build task defined.` dialoogvenster zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Dialoogvenster voor Visual Studio Code build-taak](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="713a7-179">een) Klik op Hallo `Configure Build Task` knop.</span><span class="sxs-lookup"><span data-stu-id="713a7-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="713a7-180">b) in Hallo `Select a Task Runner` vervolgkeuzemenu in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="713a7-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="713a7-181">Selecteer `.NET Core` zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Visual Studio Code selecteren een dialoogvenster taak](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="713a7-183">c) op Hallo `.NET Core` artikel maakt Hallo `tasks.json` bestand uw `.vscode` directory en wordt geopend bestand in Hallo Hallo `code editor` venster.</span><span class="sxs-lookup"><span data-stu-id="713a7-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="713a7-184">Er is geen toomodify moet dit bestand, sluiten Hallo tabblad.</span><span class="sxs-lookup"><span data-stu-id="713a7-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="713a7-185">Open Hallo `Visual Studio Code` geïntegreerde terminalvenster door Hallo drukken `Ctrl`  +  `backtick` sleutels of met behulp van menu's Hallo `View`  ->  `Integrated Terminal` en het type **.\binplace.ps1**in Hallo `PowerShell` opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="713a7-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="713a7-186">Met deze opdracht worden alle onze afhankelijkheden toohello uitvoermap gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="713a7-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="713a7-187">Navigeer toohello projecten uitvoermap in Hallo `Integrated Terminal` venster door op te geven **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="713a7-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="713a7-188">Hallo-voorbeeldproject uitvoeren door te typen **. \gw.exe gw-config.json** in Hallo `Integrated Terminal` venster prompt.</span><span class="sxs-lookup"><span data-stu-id="713a7-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="713a7-189">Als u nauw Hallo stappen in deze zelfstudie hebt gevolgd, u moet nu worden uitgevoerd Hallo `Azure IoT Edge BLE Data Converter Module` voorbeeldproject zoals gezien in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="713a7-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Voorbeeld van het gesimuleerde apparaat uitgevoerd in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="713a7-191">Als u tooterminate Hallo toepassing wilt, drukt u op Hallo `<Enter>` sleutel.</span><span class="sxs-lookup"><span data-stu-id="713a7-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="713a7-192">Het wordt niet aangeraden toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` application gateway (dat wil zeggen, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="713a7-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="713a7-193">Als u deze actie kan Hallo proces tooterminate abnormaal veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="713a7-193">As this action may cause hello process tooterminate abnormally.</span></span>

