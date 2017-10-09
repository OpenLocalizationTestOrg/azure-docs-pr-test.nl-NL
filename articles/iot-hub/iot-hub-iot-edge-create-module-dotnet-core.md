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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Een Azure IoT-Edge-Module maken met C & #x23;

Deze zelfstudie gepresenteerd hoe toocreate een module voor `Azure IoT Edge` met `Visual Studio Code` en `C#`.

In deze zelfstudie we omgeving opzet hebt doorlopen en hoe toowrite een [uitschakelen](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) meest recente gegevens converter module met Hallo `Azure IoT Edge NuGet` pakketten. 

>[!NOTE]
Deze zelfstudie maakt gebruik van Hallo `.NET Core SDK`, die ondersteuning biedt voor meerdere platforms compatibiliteit. Hallo volgende zelfstudie is geschreven met behulp van Hallo `Windows 10` besturingssysteem. Bepaalde Hallo-opdrachten in deze zelfstudie kan afwijken afhankelijk van uw `development environment`. 

## <a name="prerequisites"></a>Vereisten

In deze sectie we set-up uw omgeving voor `Azure IoT Edge` module ontwikkeling. Toepassing tooboth **64-bits Windows** en **64-bits Linux (8 Ubuntu/Debian)** besturingssystemen.

Hallo volgende software is vereist:

- [GIT-Client](https://git-scm.com/downloads)
- [.NET Core-SDK](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

U hoeft geen tooclone Hallo opslagplaats voor dit voorbeeld, maar alle Hallo voorbeeldcode besproken in deze zelfstudie bevindt zich in Hallo opslagplaats te volgen:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Aan de slag

1. Installeer `.NET Core SDK`.
2. Installeer `Visual Studio Code` en Hallo `C# extension` van Hallo Visual Studio Code Marketplace.

Bekijk waarvoor [snelle zelfstudie](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) over hoe tooget met behulp van gestart `Visual Studio Code` en Hallo `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Hello Azure IoT rand converter module maken

1. Een nieuwe initialisatie `.NET Core` class library C#-project:
    - Open een opdrachtprompt (`Windows + R` -> `cmd` -> `enter`).
    - Navigeer toohello map waar u toocreate hello wilt `C#` project.
    - Type **dotnet nieuwe classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Deze opdracht maakt u een lege klasse aangeroepen `Class1.cs` in uw projectdirectory.
2. Navigeer toohello map waar we zojuist hebben gemaakt Hallo class library-project door te typen **cd IoTEdgeConverterModule**.
3. Open Hallo-project in `Visual Studio Code` door **code.**.
4. Zodra het Hallo-project wordt geopend in `Visual Studio Code`, klikt u op Hallo **IoTEdgeConverterModule.csproj** tooopen Hallo bestand, zoals weergegeven in Hallo installatiekopie te volgen:

    ![Venster van Visual Studio Code bewerken](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Hallo invoegen `XML` blob wordt weergegeven in het codefragment na tussen Hallo sluiten Hallo `PropertyGroup` labelen en Hallo sluiten `Project` tag; regel zes in Hallo voorafgaand aan de installatiekopie van bestand en sla Hallo door te drukken `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Nadat u hebt opgeslagen Hallo `.csproj` bestand `Visual Studio Code` moet worden gevraagd met een `unresolved dependencies` dialoogvenster zoals gezien in Hallo installatiekopie te volgen: 

    ![Visual Studio Code terugzetten afhankelijkheden dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    een) Klik op `Restore` toorestore alle Hallo verwijzingen in Hallo projecten `.csproj` bestand inclusief Hallo `PackageReferences` toegevoegd. 

    b) `Visual Studio Code` maakt automatisch Hallo `project.assets.json` bestand in uw projecten `obj` map. Dit bestand bevat informatie over uw project afhankelijkheden toomake daaropvolgende herstelacties sneller.
 
    >[!NOTE]
    `.NET Core Tools`zijn nu MSBuild-systemen. Wat betekent dat een `.csproj` projectbestand is gemaakt in plaats van een `project.json`.

    - Als `Visual Studio Code` vraagt u die in orde is niet kunt we dit handmatig doen. Open Hallo `Visual Studio Code` geïntegreerde terminalvenster door Hallo drukken `Ctrl`  +  `backtick` sleutels of met behulp van menu's Hallo `View`  ->  `Integrated Terminal`.
    - In Hallo `Integrated Terminal` venstertype **dotnet terugzetten**.
    
7. Wijzig de naam van Hallo `Class1.cs` bestand te`BleConverterModule.cs`. 

    een) toorename Hallo bestand eerst klikt u op Hallo-bestand en druk op Hallo `F2` sleutel.
    
    b) type in de nieuwe naam Hallo **BleConverterModule**, zoals in Hallo installatiekopie te volgen:

    ![Visual Studio Code naam van een klasse](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Vervang de bestaande code Hallo in Hallo `BleConverterModule.cs` bestand door te kopiëren en plakken Hallo volgende codefragment in uw `BleConverterModule.cs` bestand.

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

9. Hallo-bestand opslaan door te drukken `Ctrl`  +  `S`.

10. Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels zoals gezien in Hallo installatiekopie te volgen:

    ![Visual Studio Code nieuw bestand](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello `JSON` -object dat we van Hallo gesimuleerde ontvangen `BLE` apparaat, kopie Hallo na de code in Hallo `Untitled-1` venster bestand code-editor. 

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

12. Hallo bestand opslaan als `BleData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S` sleutels.
    - Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` Selecteer vervolgkeuzemenu `C# (*.cs;*.csx)` zoals gezien in Hallo installatiekopie te volgen:

    ![Visual Studio Code opslaan als een dialoogvenster](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.

14. Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand. Deze klasse is een `Azure IoT Edge` module waarmee we toooutput Hallo gegevens ontvangen gebruiken van onze `BleConverterModule`.

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

15. Hallo bestand opslaan als `DotNetPrinterModule.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.
    - Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.

16. Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.

17. Hallo toodeserialize `JSON` -object dat we van Hallo ontvangen `BleConverterModule`, kopiëren en plakken Hallo volgende codefragment in Hallo `Untitled-1` bestand. 

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

18. Hallo bestand opslaan als `BleConverterData.cs` door te drukken `Ctrl`  +  `Shift`  +  `S`.
    - Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `C# (*.cs;*.csx)`.

19. Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.

20. Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand.

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

21. Hallo bestand opslaan als `gw-config.json` door te drukken `Ctrl`  +  `Shift`  +  `S`.
    - Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. directory, update Hallo tooenable kopiëren van Hallo configuration file toohello uitvoer `IoTEdgeConverterModule.csproj` Hello XML-blob te volgen:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Hallo bijgewerkt `IoTEdgeConverterModule.csproj` moet eruit Hallo de volgende afbeelding:

    ![Visual Studio Code bijgewerkt .csproj-bestand](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Maak een nieuw bestand genaamd `Untitled-1` door Hallo drukken `Ctrl`  +  `N` sleutels.

24. Kopieer en plak de volgende codefragment in Hallo Hallo `Untitled-1` bestand.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Hallo bestand opslaan als `binplace.ps1` door te drukken `Ctrl`  +  `Shift`  +  `S`.
    - Op Hallo opslaan als in het dialoogvenster in Hallo `Save as Type` vervolgkeuzemenu Selecteer `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Hallo-project te bouwen door Hallo drukken `Ctrl`  +  `Shift`  +  `B` sleutels. Als u de eerste keer voor Hallo-project voor Hallo bouwen `Visual Studio Code` vraagt u Hello `No build task defined.` dialoogvenster zoals gezien in Hallo installatiekopie te volgen:

    ![Dialoogvenster voor Visual Studio Code build-taak](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    een) Klik op Hallo `Configure Build Task` knop.

    b) in Hallo `Select a Task Runner` vervolgkeuzemenu in het dialoogvenster. Selecteer `.NET Core` zoals gezien in Hallo installatiekopie te volgen: 

    ![Visual Studio Code selecteren een dialoogvenster taak](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c) op Hallo `.NET Core` artikel maakt Hallo `tasks.json` bestand uw `.vscode` directory en wordt geopend bestand in Hallo Hallo `code editor` venster. Er is geen toomodify moet dit bestand, sluiten Hallo tabblad.

27.  Open Hallo `Visual Studio Code` geïntegreerde terminalvenster door Hallo drukken `Ctrl`  +  `backtick` sleutels of met behulp van menu's Hallo `View`  ->  `Integrated Terminal` en het type **.\binplace.ps1**in Hallo `PowerShell` opdrachtprompt. Met deze opdracht worden alle onze afhankelijkheden toohello uitvoermap gekopieerd.

28. Navigeer toohello projecten uitvoermap in Hallo `Integrated Terminal` venster door op te geven **cd.\bin\Debug\netstandard1.3**.

29. Hallo-voorbeeldproject uitvoeren door te typen **. \gw.exe gw-config.json** in Hallo `Integrated Terminal` venster prompt. 
    - Als u nauw Hallo stappen in deze zelfstudie hebt gevolgd, u moet nu worden uitgevoerd Hallo `Azure IoT Edge BLE Data Converter Module` voorbeeldproject zoals gezien in Hallo installatiekopie te volgen:
    
        ![Voorbeeld van het gesimuleerde apparaat uitgevoerd in Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Als u tooterminate Hallo toepassing wilt, drukt u op Hallo `<Enter>` sleutel.

>[!IMPORTANT]
Het wordt niet aangeraden toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` application gateway (dat wil zeggen, **gw.exe**). Als u deze actie kan Hallo proces tooterminate abnormaal veroorzaken.

