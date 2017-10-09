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
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="f95b5-103">Code en Azure functions lokaal testen</span><span class="sxs-lookup"><span data-stu-id="f95b5-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="f95b5-104">Tijdens het Hallo [Azure-portal] biedt een volledige set hulpprogramma's voor het ontwikkelen en testen Azure Functions, veel ontwikkelaars de voorkeur aan een lokale ontwikkeling biedt.</span><span class="sxs-lookup"><span data-stu-id="f95b5-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="f95b5-105">Azure Functions maakt het eenvoudig toouse uw favoriete editor en lokale development tools toodevelop code en testen van uw functies op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="f95b5-106">Uw functies kunnen activeren van gebeurtenissen in Azure en u kunt fouten opsporen in uw C#- en JavaScript-functies op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="f95b5-107">Als u een Azure-functies van Visual Studio C# ontwikkelaar, ook bent [kan worden geïntegreerd met Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="f95b5-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="f95b5-108">Hello Azure Functions Core hulpprogramma's installeren</span><span class="sxs-lookup"><span data-stu-id="f95b5-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="f95b5-109">Kernonderdelen van Azure Functions is een lokale versie van Azure Functions-runtime voor Hallo die kunnen worden uitgevoerd op de lokale Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="f95b5-110">Het is niet een emulator of simulator.</span><span class="sxs-lookup"><span data-stu-id="f95b5-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="f95b5-111">Deze heeft dezelfde runtime Hallo die bevoegdheden functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="f95b5-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="f95b5-112">Hallo [kernonderdelen van Azure Functions] is opgegeven als een pakket npm.</span><span class="sxs-lookup"><span data-stu-id="f95b5-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="f95b5-113">U moet eerst [installeren NodeJS](https://docs.npmjs.com/getting-started/installing-node), waaronder npm.</span><span class="sxs-lookup"><span data-stu-id="f95b5-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="f95b5-114">Op dit moment worden Hallo kernonderdelen van Azure Functions pakket alleen geïnstalleerd op Windows-computers.</span><span class="sxs-lookup"><span data-stu-id="f95b5-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="f95b5-115">Deze beperking is vanwege tijdelijke beperking tooa in Hallo functies host.</span><span class="sxs-lookup"><span data-stu-id="f95b5-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="f95b5-116">[kernonderdelen van Azure Functions] voegt Hallo opdracht aliassen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f95b5-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="f95b5-117">**func**</span><span class="sxs-lookup"><span data-stu-id="f95b5-117">**func**</span></span>
* <span data-ttu-id="f95b5-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="f95b5-118">**azfun**</span></span>
* <span data-ttu-id="f95b5-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="f95b5-119">**azurefunctions**</span></span>

<span data-ttu-id="f95b5-120">Alle deze alias kan worden gebruikt in plaats van `func` wordt weergegeven in het Hallo-voorbeelden in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f95b5-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="f95b5-121">Een lokale functies-project maken</span><span class="sxs-lookup"><span data-stu-id="f95b5-121">Create a local Functions project</span></span>

<span data-ttu-id="f95b5-122">Wanneer lokaal wordt uitgevoerd, is een project functies in een map met Hallo bestanden host.json en local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f95b5-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="f95b5-123">Deze map is Hallo equivalent van een functie-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f95b5-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="f95b5-124">toolearn meer informatie over hello Azure Functions-mapstructuur, Zie Hallo [handleiding voor ontwikkelaars voor Azure Functions voor](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="f95b5-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="f95b5-125">Voer bij een opdrachtprompt Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f95b5-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="f95b5-126">Hallo-uitvoer ziet er Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="f95b5-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="f95b5-127">tooopt buiten het maken van een Git-opslagplaats, gebruik de optie Hallo `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="f95b5-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="f95b5-128">Lokale instellingenbestand</span><span class="sxs-lookup"><span data-stu-id="f95b5-128">Local settings file</span></span>

<span data-ttu-id="f95b5-129">Hallo bestand local.settings.json slaat app-instellingen, verbindingsreeksen en instellingen voor Azure Functions Core hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="f95b5-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="f95b5-130">Er Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="f95b5-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="f95b5-131">Instelling</span><span class="sxs-lookup"><span data-stu-id="f95b5-131">Setting</span></span>      | <span data-ttu-id="f95b5-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f95b5-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="f95b5-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="f95b5-133">**IsEncrypted**</span></span> | <span data-ttu-id="f95b5-134">Als de waarde te**true**, alle waarden zijn versleuteld met een sleutel van de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="f95b5-135">Gebruikt met `func settings` opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f95b5-135">Used with `func settings` commands.</span></span> <span data-ttu-id="f95b5-136">Standaardwaarde is **false**.</span><span class="sxs-lookup"><span data-stu-id="f95b5-136">Default value is **false**.</span></span> |
| <span data-ttu-id="f95b5-137">**Waarden**</span><span class="sxs-lookup"><span data-stu-id="f95b5-137">**Values**</span></span> | <span data-ttu-id="f95b5-138">Verzameling toepassingsinstellingen gebruikt bij lokale uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f95b5-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="f95b5-139">Uw toepassing instellingen toothis object toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f95b5-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="f95b5-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="f95b5-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="f95b5-141">Sets Hallo connection string toohello Azure Storage-account intern door hello Azure Functions-runtime gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="f95b5-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="f95b5-142">Hallo storage-account biedt ondersteuning voor de functie-triggers.</span><span class="sxs-lookup"><span data-stu-id="f95b5-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="f95b5-143">Deze instelling van de storage-account is vereist voor alle functies, met uitzondering van HTTP-geactiveerde functies.</span><span class="sxs-lookup"><span data-stu-id="f95b5-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="f95b5-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="f95b5-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="f95b5-145">Hiermee stelt u Hallo verbinding tekenreeks toohello Azure Storage-account dat is gebruikt toostore Hallo functie Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f95b5-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="f95b5-146">Deze optionele waarde toegankelijk Hallo Logboeken in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f95b5-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="f95b5-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="f95b5-147">**Host**</span></span> | <span data-ttu-id="f95b5-148">Instellingen in deze sectie aanpassen Hallo functies hostproces bij lokale uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f95b5-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="f95b5-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="f95b5-149">**LocalHttpPort**</span></span> | <span data-ttu-id="f95b5-150">Sets Hallo standaardpoort gebruikt bij het uitvoeren van de lokale functies host hello (`func host start` en `func run`).</span><span class="sxs-lookup"><span data-stu-id="f95b5-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="f95b5-151">Hallo `--port` opdrachtregeloptie heeft voorrang op deze waarde.</span><span class="sxs-lookup"><span data-stu-id="f95b5-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="f95b5-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="f95b5-152">**CORS**</span></span> | <span data-ttu-id="f95b5-153">Hallo oorsprongen toegestaan voor definieert [cross-origin-resource delen (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="f95b5-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="f95b5-154">Oorsprongen zijn opgegeven als een door komma's gescheiden lijst zonder spaties.</span><span class="sxs-lookup"><span data-stu-id="f95b5-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="f95b5-155">Hallo jokerteken (**\***) wordt ondersteund, waarmee aanvragen van een oorsprong.</span><span class="sxs-lookup"><span data-stu-id="f95b5-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="f95b5-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="f95b5-156">**ConnectionStrings**</span></span> | <span data-ttu-id="f95b5-157">Hallo tekenreeksen voor databaseverbindingen voor uw functies bevat.</span><span class="sxs-lookup"><span data-stu-id="f95b5-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="f95b5-158">Verbindingsreeksen in dit object toohello omgeving met Hallo providertype worden toegevoegd **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="f95b5-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="f95b5-159">De meeste triggers en bindingen hebben een **verbinding** eigenschap die de naam van een variabele of een app omgevingsinstelling toohello toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f95b5-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="f95b5-160">Voor elke verbindingseigenschap moet worden gedefinieerd in local.settings.json-bestand van app-instelling.</span><span class="sxs-lookup"><span data-stu-id="f95b5-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="f95b5-161">Deze instellingen kunnen ook worden gelezen in uw code als omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="f95b5-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="f95b5-162">Gebruik in C#, [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) of [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f95b5-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="f95b5-163">Gebruik in JavaScript, `process.env`.</span><span class="sxs-lookup"><span data-stu-id="f95b5-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="f95b5-164">Instellingen die zijn opgegeven als een systeemomgevingsvariabele hebben voorrang op de waarden in Hallo local.settings.json bestand.</span><span class="sxs-lookup"><span data-stu-id="f95b5-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="f95b5-165">Instellingen in Hallo local.settings.json bestand worden alleen gebruikt door extra functies bij lokale uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f95b5-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="f95b5-166">Standaard worden deze instellingen niet automatisch gemigreerd als Hallo project gepubliceerde tooAzure is.</span><span class="sxs-lookup"><span data-stu-id="f95b5-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="f95b5-167">Gebruik Hallo `--publish-local-settings` overschakelen [bij het publiceren van](#publish) toomake zeker van te zijn dat deze instellingen toohello functie-app in Azure worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f95b5-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="f95b5-168">Als er geen geldige opslagverbindingsreeks is ingesteld voor **AzureWebJobsStorage**, Hallo volgende foutbericht wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f95b5-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="f95b5-169">Ontbrekende waarde voor AzureWebJobsStorage in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f95b5-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="f95b5-170">Dit is vereist voor alle triggers dan HTTP.</span><span class="sxs-lookup"><span data-stu-id="f95b5-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="f95b5-171">U kunt uitvoeren ' azure functionary ophalen-app-instellingen van de func <functionAppName>' of een verbindingsreeks in local.settings.json opgeven.</span><span class="sxs-lookup"><span data-stu-id="f95b5-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="f95b5-172">App-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="f95b5-172">Configure app settings</span></span>

<span data-ttu-id="f95b5-173">een waarde voor verbindingsreeksen tooset, kunt u een van de volgende Hallo kunt doen:</span><span class="sxs-lookup"><span data-stu-id="f95b5-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="f95b5-174">Geef de verbindingsreeks Hallo van [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f95b5-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="f95b5-175">Gebruik een van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="f95b5-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="f95b5-176">Beide opdrachten moeten u toofirst aanmelden tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f95b5-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="f95b5-177">Een functie maken</span><span class="sxs-lookup"><span data-stu-id="f95b5-177">Create a function</span></span>

<span data-ttu-id="f95b5-178">toocreate een functie Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f95b5-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="f95b5-179">`func new`ondersteunt de volgende optionele argumenten Hallo:</span><span class="sxs-lookup"><span data-stu-id="f95b5-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="f95b5-180">Argument</span><span class="sxs-lookup"><span data-stu-id="f95b5-180">Argument</span></span>     | <span data-ttu-id="f95b5-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f95b5-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="f95b5-182">Hallo sjabloon programmeertaal, zoals C#, F # of JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f95b5-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="f95b5-183">Hallo sjabloonnaam.</span><span class="sxs-lookup"><span data-stu-id="f95b5-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="f95b5-184">Hallo functienaam.</span><span class="sxs-lookup"><span data-stu-id="f95b5-184">hello function name.</span></span> |

<span data-ttu-id="f95b5-185">Bijvoorbeeld, toocreate een JavaScript-HTTP-trigger uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f95b5-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="f95b5-186">een functie wachtrij geactiveerd toocreate uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f95b5-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="f95b5-187">Functies lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f95b5-187">Run functions locally</span></span>

<span data-ttu-id="f95b5-188">toorun een project functies Hallo functies host uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f95b5-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="f95b5-189">Hallo host kunt triggers voor alle functies in Hallo project:</span><span class="sxs-lookup"><span data-stu-id="f95b5-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="f95b5-190">`func host start`ondersteunt Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f95b5-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="f95b5-191">Optie</span><span class="sxs-lookup"><span data-stu-id="f95b5-191">Option</span></span>     | <span data-ttu-id="f95b5-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f95b5-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="f95b5-193">Hallo toolisten van de lokale poort op.</span><span class="sxs-lookup"><span data-stu-id="f95b5-193">hello local port toolisten on.</span></span> <span data-ttu-id="f95b5-194">Standaardwaarde: 7071.</span><span class="sxs-lookup"><span data-stu-id="f95b5-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="f95b5-195">Hallo-opties zijn `VSCode` en `VS`.</span><span class="sxs-lookup"><span data-stu-id="f95b5-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="f95b5-196">Een door komma's gescheiden lijst van CORS-oorsprong, zonder spaties.</span><span class="sxs-lookup"><span data-stu-id="f95b5-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="f95b5-197">Hallo-poort voor Hallo knooppunt foutopsporingsprogramma toouse.</span><span class="sxs-lookup"><span data-stu-id="f95b5-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="f95b5-198">Standaard: Een waarde van launch.json of 5858.</span><span class="sxs-lookup"><span data-stu-id="f95b5-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="f95b5-199">Hallo console traceerniveau (uit verbose,-info, waarschuwing of fout).</span><span class="sxs-lookup"><span data-stu-id="f95b5-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="f95b5-200">Standaard: Info.</span><span class="sxs-lookup"><span data-stu-id="f95b5-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f95b5-201">Hallo time-out voor Hallo functies host t o beginnen, in seconden.</span><span class="sxs-lookup"><span data-stu-id="f95b5-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="f95b5-202">Standaardwaarde: 20 seconden.</span><span class="sxs-lookup"><span data-stu-id="f95b5-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="f95b5-203">Toohttps://localhost binden: {poort} in plaats van toohttp://localhost: {poort}.</span><span class="sxs-lookup"><span data-stu-id="f95b5-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="f95b5-204">Deze optie maakt standaard een vertrouwd certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="f95b5-205">Onderbreken om extra gegevens voordat u afsluit Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="f95b5-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="f95b5-206">Dit is handig bij het starten van Azure Functions kernonderdelen van een integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="f95b5-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="f95b5-207">Wanneer Hallo functies host wordt gestart, levert het Hallo-URL van de HTTP-geactiveerde functies:</span><span class="sxs-lookup"><span data-stu-id="f95b5-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="f95b5-208">Fouten opsporen in VS-Code of Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f95b5-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="f95b5-209">een foutopsporingsprogramma tooattach doorgeven Hallo `--debug` argument.</span><span class="sxs-lookup"><span data-stu-id="f95b5-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="f95b5-210">toodebug JavaScript-functies, gebruikt u Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f95b5-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="f95b5-211">Voor C#, Visual Studio te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f95b5-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="f95b5-212">toodebug C#-functies gebruiken `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="f95b5-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="f95b5-213">U kunt ook [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="f95b5-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="f95b5-214">toolaunch hello host en stelt u de JavaScript-foutopsporing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f95b5-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="f95b5-215">Klik in Visual Studio Code op Hallo **Debug** weergave, selecteer **tooAzure functies koppelen**.</span><span class="sxs-lookup"><span data-stu-id="f95b5-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="f95b5-216">U kunt onderbrekingspunten koppelen, variabelen inspecteren en analyseer code.</span><span class="sxs-lookup"><span data-stu-id="f95b5-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![JavaScript foutopsporing met Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="f95b5-218">Doorgeven test gegevens tooa functie</span><span class="sxs-lookup"><span data-stu-id="f95b5-218">Passing test data tooa function</span></span>

<span data-ttu-id="f95b5-219">U kunt ook een functie aanroepen via `func run <FunctionName>` en geef de invoergegevens voor Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="f95b5-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="f95b5-220">Met deze opdracht is vergelijkbaar toorunning functie Hallo met **Test** tabblad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f95b5-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="f95b5-221">Met deze opdracht wordt het hele functies host Hallo gestart.</span><span class="sxs-lookup"><span data-stu-id="f95b5-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="f95b5-222">`func run`ondersteunt Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f95b5-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="f95b5-223">Optie</span><span class="sxs-lookup"><span data-stu-id="f95b5-223">Option</span></span>     | <span data-ttu-id="f95b5-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f95b5-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="f95b5-225">Inline-inhoud.</span><span class="sxs-lookup"><span data-stu-id="f95b5-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="f95b5-226">Koppel het hostproces van een foutopsporingsprogramma toohello voordat het Hallo-functie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f95b5-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f95b5-227">Toowait tijd (in seconden) tot en met het lokale functies host Hallo is gereed.</span><span class="sxs-lookup"><span data-stu-id="f95b5-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="f95b5-228">Hallo bestand naam toouse als inhoud.</span><span class="sxs-lookup"><span data-stu-id="f95b5-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="f95b5-229">Wordt niet gevraagd om invoer.</span><span class="sxs-lookup"><span data-stu-id="f95b5-229">Does not prompt for input.</span></span> <span data-ttu-id="f95b5-230">Dit is handig voor automatiseringsscenario's.</span><span class="sxs-lookup"><span data-stu-id="f95b5-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="f95b5-231">Toocall een functie HTTP wordt geactiveerd en de tekstinhoud op te geven, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f95b5-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="f95b5-232"><a name="publish"></a>TooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="f95b5-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="f95b5-233">een functies project tooa functie-app in Azure, gebruik Hallo toopublish `publish` opdracht:</span><span class="sxs-lookup"><span data-stu-id="f95b5-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="f95b5-234">U kunt Hallo volgende opties gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f95b5-234">You can use hello following options:</span></span>

| <span data-ttu-id="f95b5-235">Optie</span><span class="sxs-lookup"><span data-stu-id="f95b5-235">Option</span></span>     | <span data-ttu-id="f95b5-236">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f95b5-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="f95b5-237">Publicatie-instellingen in local.settings.json tooAzure, toooverwrite vragen als Hallo instelt, al bestaat.</span><span class="sxs-lookup"><span data-stu-id="f95b5-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="f95b5-238">Moet worden gebruikt met `-i`.</span><span class="sxs-lookup"><span data-stu-id="f95b5-238">Must be used with `-i`.</span></span> <span data-ttu-id="f95b5-239">Overschrijft AppSettings in Azure met lokale waarde als deze verschilt.</span><span class="sxs-lookup"><span data-stu-id="f95b5-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="f95b5-240">De standaardwaarde is vragen.</span><span class="sxs-lookup"><span data-stu-id="f95b5-240">Default is prompt.</span></span>|

<span data-ttu-id="f95b5-241">Hallo `publish` opdracht uploadt Hallo inhoud van de projectmap Hallo-functies.</span><span class="sxs-lookup"><span data-stu-id="f95b5-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="f95b5-242">Als u bestanden lokaal verwijdert, Hallo `publish` opdracht ze niet verwijdert uit Azure.</span><span class="sxs-lookup"><span data-stu-id="f95b5-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="f95b5-243">U kunt bestanden in Azure verwijderen met behulp van Hallo [Kudu hulpprogramma](functions-how-to-use-azure-function-app-settings.md#kudu) in Hallo [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f95b5-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f95b5-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f95b5-244">Next steps</span></span>

<span data-ttu-id="f95b5-245">Azure Functions Core Tools [open source en wordt gehost op GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="f95b5-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="f95b5-246">een aanvraag bug of functie toofile [opent u een probleem met de GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="f95b5-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[kernonderdelen van Azure Functions]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure-portal]: https://portal.azure.com 
