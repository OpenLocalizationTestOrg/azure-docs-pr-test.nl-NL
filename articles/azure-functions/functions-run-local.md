---
title: aaaDevelop en voer Azure functions lokaal | Microsoft Docs
description: Meer informatie over hoe toocode en test Azure functioneert op de lokale computer voordat u deze uitvoeren op Azure Functions.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Code en Azure functions lokaal testen

Tijdens het Hallo [Azure-portal] biedt een volledige set hulpprogramma's voor het ontwikkelen en testen Azure Functions, veel ontwikkelaars de voorkeur aan een lokale ontwikkeling biedt. Azure Functions maakt het eenvoudig toouse uw favoriete editor en lokale development tools toodevelop code en testen van uw functies op uw lokale computer. Uw functies kunnen activeren van gebeurtenissen in Azure en u kunt fouten opsporen in uw C#- en JavaScript-functies op uw lokale computer. 

Als u een Azure-functies van Visual Studio C# ontwikkelaar, ook bent [kan worden geïntegreerd met Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Hello Azure Functions Core hulpprogramma's installeren

Kernonderdelen van Azure Functions is een lokale versie van Azure Functions-runtime voor Hallo die kunnen worden uitgevoerd op de lokale Windows-computer. Het is niet een emulator of simulator. Deze heeft dezelfde runtime Hallo die bevoegdheden functies in Azure.

Hallo [kernonderdelen van Azure Functions] is opgegeven als een pakket npm. U moet eerst [installeren NodeJS](https://docs.npmjs.com/getting-started/installing-node), waaronder npm.  

>[!NOTE]
>Op dit moment worden Hallo kernonderdelen van Azure Functions pakket alleen geïnstalleerd op Windows-computers. Deze beperking is vanwege tijdelijke beperking tooa in Hallo functies host.

[kernonderdelen van Azure Functions] voegt Hallo opdracht aliassen te volgen:
* **func**
* **azfun**
* **azurefunctions**

Alle deze alias kan worden gebruikt in plaats van `func` wordt weergegeven in het Hallo-voorbeelden in dit onderwerp.

## <a name="create-a-local-functions-project"></a>Een lokale functies-project maken

Wanneer lokaal wordt uitgevoerd, is een project functies in een map met Hallo bestanden host.json en local.settings.json. Deze map is Hallo equivalent van een functie-app in Azure. toolearn meer informatie over hello Azure Functions-mapstructuur, Zie Hallo [handleiding voor ontwikkelaars voor Azure Functions voor](functions-reference.md#folder-structure).

Voer bij een opdrachtprompt Hallo volgende opdracht:

```
func init MyFunctionProj
```

Hallo-uitvoer ziet er Hallo voorbeeld te volgen:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt buiten het maken van een Git-opslagplaats, gebruik de optie Hallo `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Lokale instellingenbestand

Hallo bestand local.settings.json slaat app-instellingen, verbindingsreeksen en instellingen voor Azure Functions Core hulpprogramma's. Er Hallo structuur te volgen:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Instelling      | Beschrijving                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Als de waarde te**true**, alle waarden zijn versleuteld met een sleutel van de lokale computer. Gebruikt met `func settings` opdrachten. Standaardwaarde is **false**. |
| **Waarden** | Verzameling toepassingsinstellingen gebruikt bij lokale uitvoering. Uw toepassing instellingen toothis object toevoegen.  |
| **AzureWebJobsStorage** | Sets Hallo connection string toohello Azure Storage-account intern door hello Azure Functions-runtime gebruikt wordt. Hallo storage-account biedt ondersteuning voor de functie-triggers. Deze instelling van de storage-account is vereist voor alle functies, met uitzondering van HTTP-geactiveerde functies.  |
| **AzureWebJobsDashboard** | Hiermee stelt u Hallo verbinding tekenreeks toohello Azure Storage-account dat is gebruikt toostore Hallo functie Logboeken. Deze optionele waarde toegankelijk Hallo Logboeken in Hallo-portal.|
| **Host** | Instellingen in deze sectie aanpassen Hallo functies hostproces bij lokale uitvoering. | 
| **LocalHttpPort** | Sets Hallo standaardpoort gebruikt bij het uitvoeren van de lokale functies host hello (`func host start` en `func run`). Hallo `--port` opdrachtregeloptie heeft voorrang op deze waarde. |
| **CORS** | Hallo oorsprongen toegestaan voor definieert [cross-origin-resource delen (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Oorsprongen zijn opgegeven als een door komma's gescheiden lijst zonder spaties. Hallo jokerteken (**\***) wordt ondersteund, waarmee aanvragen van een oorsprong. |
| **ConnectionStrings** | Hallo tekenreeksen voor databaseverbindingen voor uw functies bevat. Verbindingsreeksen in dit object toohello omgeving met Hallo providertype worden toegevoegd **System.Data.SqlClient**.  | 

De meeste triggers en bindingen hebben een **verbinding** eigenschap die de naam van een variabele of een app omgevingsinstelling toohello toegewezen. Voor elke verbindingseigenschap moet worden gedefinieerd in local.settings.json-bestand van app-instelling. 

Deze instellingen kunnen ook worden gelezen in uw code als omgevingsvariabelen. Gebruik in C#, [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) of [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). Gebruik in JavaScript, `process.env`. Instellingen die zijn opgegeven als een systeemomgevingsvariabele hebben voorrang op de waarden in Hallo local.settings.json bestand. 

Instellingen in Hallo local.settings.json bestand worden alleen gebruikt door extra functies bij lokale uitvoering. Standaard worden deze instellingen niet automatisch gemigreerd als Hallo project gepubliceerde tooAzure is. Gebruik Hallo `--publish-local-settings` overschakelen [bij het publiceren van](#publish) toomake zeker van te zijn dat deze instellingen toohello functie-app in Azure worden toegevoegd.

Als er geen geldige opslagverbindingsreeks is ingesteld voor **AzureWebJobsStorage**, Hallo volgende foutbericht wordt weergegeven:  

>Ontbrekende waarde voor AzureWebJobsStorage in local.settings.json. Dit is vereist voor alle triggers dan HTTP. U kunt uitvoeren ' azure functionary ophalen-app-instellingen van de func <functionAppName>' of een verbindingsreeks in local.settings.json opgeven.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>App-instellingen configureren

een waarde voor verbindingsreeksen tooset, kunt u een van de volgende Hallo kunt doen:
* Geef de verbindingsreeks Hallo van [Azure Opslagverkenner](http://storageexplorer.com/).
* Gebruik een van de volgende opdrachten Hallo:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Beide opdrachten moeten u toofirst aanmelden tooAzure.

## <a name="create-a-function"></a>Een functie maken

toocreate een functie Hallo volgende opdracht uitvoeren:

```
func new
``` 
`func new`ondersteunt de volgende optionele argumenten Hallo:

| Argument     | Beschrijving                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | Hallo sjabloon programmeertaal, zoals C#, F # of JavaScript. |
| **`--template -t`** | Hallo sjabloonnaam. |
| **`--name -n`** | Hallo functienaam. |

Bijvoorbeeld, toocreate een JavaScript-HTTP-trigger uitvoeren:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

een functie wachtrij geactiveerd toocreate uitvoeren:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Functies lokaal uitvoeren

toorun een project functies Hallo functies host uitvoeren. Hallo host kunt triggers voor alle functies in Hallo project:

```
func host start
```

`func host start`ondersteunt Hallo volgende opties:

| Optie     | Beschrijving                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Hallo toolisten van de lokale poort op. Standaardwaarde: 7071. |
| **`--debug <type>`** | Hallo-opties zijn `VSCode` en `VS`. |
| **`--cors`** | Een door komma's gescheiden lijst van CORS-oorsprong, zonder spaties. |
| **`--nodeDebugPort -n`** | Hallo-poort voor Hallo knooppunt foutopsporingsprogramma toouse. Standaard: Een waarde van launch.json of 5858. |
| **`--debugLevel -d`** | Hallo console traceerniveau (uit verbose,-info, waarschuwing of fout). Standaard: Info.|
| **`--timeout -t`** | Hallo time-out voor Hallo functies host t o beginnen, in seconden. Standaardwaarde: 20 seconden.|
| **`--useHttps`** | Toohttps://localhost binden: {poort} in plaats van toohttp://localhost: {poort}. Deze optie maakt standaard een vertrouwd certificaat op uw computer.|
| **`--pause-on-error`** | Onderbreken om extra gegevens voordat u afsluit Hallo-proces. Dit is handig bij het starten van Azure Functions kernonderdelen van een integrated development environment (IDE).|

Wanneer Hallo functies host wordt gestart, levert het Hallo-URL van de HTTP-geactiveerde functies:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Fouten opsporen in VS-Code of Visual Studio

een foutopsporingsprogramma tooattach doorgeven Hallo `--debug` argument. toodebug JavaScript-functies, gebruikt u Visual Studio Code. Voor C#, Visual Studio te gebruiken.

toodebug C#-functies gebruiken `--debug vs`. U kunt ook [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

toolaunch hello host en stelt u de JavaScript-foutopsporing uitvoeren:

```
func host start --debug vscode
```

Klik in Visual Studio Code op Hallo **Debug** weergave, selecteer **tooAzure functies koppelen**. U kunt onderbrekingspunten koppelen, variabelen inspecteren en analyseer code.

![JavaScript foutopsporing met Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Doorgeven test gegevens tooa functie

U kunt ook een functie aanroepen via `func run <FunctionName>` en geef de invoergegevens voor Hallo-functie. Met deze opdracht is vergelijkbaar toorunning functie Hallo met **Test** tabblad in hello Azure-portal. Met deze opdracht wordt het hele functies host Hallo gestart.

`func run`ondersteunt Hallo volgende opties:

| Optie     | Beschrijving                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Inline-inhoud. |
| **`--debug -d`** | Koppel het hostproces van een foutopsporingsprogramma toohello voordat het Hallo-functie uit te voeren.|
| **`--timeout -t`** | Toowait tijd (in seconden) tot en met het lokale functies host Hallo is gereed.|
| **`--file -f`** | Hallo bestand naam toouse als inhoud.|
| **`--no-interactive`** | Wordt niet gevraagd om invoer. Dit is handig voor automatiseringsscenario's.|

Toocall een functie HTTP wordt geactiveerd en de tekstinhoud op te geven, Hallo volgende opdracht uitvoeren:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>TooAzure publiceren

een functies project tooa functie-app in Azure, gebruik Hallo toopublish `publish` opdracht:

```
func azure functionapp publish <FunctionAppName>
```

U kunt Hallo volgende opties gebruiken:

| Optie     | Beschrijving                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Publicatie-instellingen in local.settings.json tooAzure, toooverwrite vragen als Hallo instelt, al bestaat.|
| **`--overwrite-settings -y`** | Moet worden gebruikt met `-i`. Overschrijft AppSettings in Azure met lokale waarde als deze verschilt. De standaardwaarde is vragen.|

Hallo `publish` opdracht uploadt Hallo inhoud van de projectmap Hallo-functies. Als u bestanden lokaal verwijdert, Hallo `publish` opdracht ze niet verwijdert uit Azure. U kunt bestanden in Azure verwijderen met behulp van Hallo [Kudu hulpprogramma](functions-how-to-use-azure-function-app-settings.md#kudu) in Hallo [Azure-portal].

## <a name="next-steps"></a>Volgende stappen

Azure Functions Core Tools [open source en wordt gehost op GitHub](https://github.com/azure/azure-functions-cli).  
een aanvraag bug of functie toofile [opent u een probleem met de GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[kernonderdelen van Azure Functions]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure-portal]: https://portal.azure.com 
