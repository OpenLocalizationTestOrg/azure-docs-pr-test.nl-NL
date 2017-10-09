---
title: aaaTutorial - gebruik hello Azure Batch-clientbibliotheek voor Node.js | Microsoft Docs
description: Leer de basisconcepten Hallo van Azure Batch en bouwen van een eenvoudige oplossing met behulp van Node.js.
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Aan de slag met de Batch-SDK voor Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Leer de basisbeginselen Hallo van het bouwen van een batchclient in met behulp van Node.js [Node.js-SDK van Azure Batch](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Er wordt een stapsgewijze benadering gebruikt om inzicht te krijgen in een scenario voor een Batch-toepassing. Daarna wordt de toepassing met een Node.js-client ingesteld.  

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van Node.js en vertrouwd bent met Linux. Ook wordt ervan uitgegaan dat u een Azure-account-installatie met toegang rechten toocreate Batch- en Storage-services hebt.

Lezen wordt aangeraden [technisch overzicht van Azure Batch](batch-technical-overview.md) voordat u doorloopt Hallo stappen die worden beschreven in dit artikel.

## <a name="hello-tutorial-scenario"></a>Hallo zelfstudie scenario
Laat het ons weten Hallo batch-werkstroom scenario. We hebben een eenvoudig script geschreven in Python die downloadt alle csv-bestanden van een Azure Blob storage-container en zet deze tooJSON. tooprocess meerdere storage account containers parallel, we Hallo script als een Azure Batch-taak kunt implementeren.

## <a name="azure-batch-architecture"></a>Azure Batch-architectuur
Hallo volgende diagram illustreert hoe Hallo pythonscript met behulp van Azure Batch- en een Node.js-client kan worden geschaald.

![Azure Batch-scenario](./media/batch-nodejs-get-started/BatchScenario.png)

een batch-job implementeert Hallo node.js-client met een jobvoorbereidingstaak (uitvoerig besproken later) en een aantal taken, afhankelijk van het aantal containers in het opslagaccount Hallo Hallo. Hallo scripts kunt u downloaden van Hallo github-opslagplaats.

* [Node.js-client](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Voorbereidingstaak voor Shell-scripts](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Python csv tooJSON processor](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> Hallo Node.js-client in Hallo koppeling opgegeven bevat geen specifieke code toobe geïmplementeerd als een Azure-functie-app. U kunt de volgende koppelingen voor instructies toocreate een toohello verwijzen.
> - [Een functie-app maken](../azure-functions/functions-create-first-azure-function.md)
> - [Een timertriggerfunctie maken](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Hallo-toepassing bouwen

Laat het ons voert nu Hallo proces stap voor stap bij het bouwen van Hallo Node.js-client:

### <a name="step-1-install-azure-batch-sdk"></a>Stap 1: de Azure Batch-SDK installeren

U kunt Azure Batch-SDK voor Node.js hello npm installatieopdracht met installeren.

`npm install azure-batch`

Deze opdracht wordt de meest recente versie van azure batch-knooppunt SDK Hallo geïnstalleerd.

>[!Tip]
> In een Azure-functie-app, kunt u gaan te 'Kudu-Console' in hello Azure functie de instellingen tabblad toorun hello npm opdrachten installeren. In dit geval tooinstall Azure Batch-SDK voor Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Stap 2: een Azure Batch-account maken

U kunt het maken van Hallo [Azure-portal](batch-account-create-portal.md) of vanaf de opdrachtregel ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).

Hieronder vindt u Hallo opdrachten toocreate een via Azure CLI.

Een resourcegroep maken, deze stap overslaan als u al een waar u toocreate Hallo Batch-Account:

`az group create -n "<resource-group-name>" -l "<location>"`

Maak daarna een Azure Batch-account.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Elk Batch-account heeft bijbehorende toegangssleutels. Deze sleutels zijn benodigde toocreate meer resources in Azure batch-account. Een goede gewoonte voor productie-omgeving is toouse Azure Key Vault toostore deze sleutels. U kunt vervolgens een Service maken voor de toepassing hello principal. Met behulp van deze service-principal Hallo-toepassing, kunt een OAuth-token tooaccess-sleutels maken in Hallo sleutelkluis.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Kopiëren en Hallo sleutel toobe gebruikt bij de volgende stappen Hallo op te slaan.

### <a name="step-3-create-an-azure-batch-service-client"></a>Stap 3: een Azure Batch-serviceclient maken
Volgende codefragment eerst importeert hello azure batch Node.js-module en maakt vervolgens een Batch-Service-client. U moet toofirst een SharedKeyCredentials-object maken met Hallo Batch-accountsleutel is gekopieerd uit de vorige stap Hallo.

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

Hello Azure Batch URI vindt u in het tabblad Overzicht van Hallo Hallo Azure-portal. Het is Hallo-indeling:

`https://accountname.location.batch.azure.com`

Raadpleeg toohello schermafbeelding:

![Azure Batch-URI](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Stap 4: een Azure Batch-pool maken
Een Azure Batch-pool bestaat uit meerdere virtuele machines (ook wel Batch-knooppunten genoemd). Azure Batch-service Hallo taken op die knooppunten implementeert en beheert deze. Hallo configuratieparameters voor uw pool te volgen, kunt u definiëren.

* Type VM-installatiekopie
* Grootte van de VM-knooppunten
* Aantal VM-knooppunten

> [!Tip]
> Hallo grootte en het aantal knooppunten van de virtuele Machine afhankelijk grotendeels van het aantal gewenste taken toorun in parallel en ook Hallo taak zelf Hallo. U kunt het beste testen toodetermine Hallo ideaal aantal en de grootte.
>
>

Hallo maakt volgende codefragment Hallo configuratieobjecten van de parameter.

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> Zie voor Hallo lijst met Linux VM-installatiekopieën beschikbaar voor Azure Batch en hun SKU-id, [lijst van installatiekopieën van virtuele machines](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Zodra de configuratie van de groep Hallo is gedefinieerd, kunt u hello Azure Batch-pool maken. Hallo opdracht Batch-pool knooppunten Azure virtuele Machine maakt en bereidt ze toobe gereed tooreceive taken tooexecute. Elke pool moet een unieke id krijgen zodat er in volgende stappen naar kan worden verwezen.

Hallo volgende codefragment maakt een Azure Batch-pool.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

U kunt Hallo status controleren van Hallo-toepassingen die zijn gemaakt en zorg ervoor dat Hallo status 'actief' voordat u wilt doorgaan met het verzenden van een taak toothat pool.

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

Hier volgt een voorbeeld resultaatobject geretourneerd door Hallo pool.get functie.

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a>Stap 4: een Azure Batch-taak verzenden
Een Azure Batch-taak is een logische groep vergelijkbare taken. In ons scenario is het 'Proces csv tooJSON'. Bij elke taak worden er hier CSV-bestanden omgezet die aanwezig zijn in Azure Storage-containers.

Deze taken parallel uitgevoerd en geïmplementeerd op meerdere knooppunten, gedirigeerd door hello Azure Batch-service.

> [!Tip]
> U kunt Hallo [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) eigenschap toospecify maximum aantal taken dat tegelijk op één knooppunt kan worden uitgevoerd.
>
>

#### <a name="preparation-task"></a>Voorbereidingstaak

Hallo VM knooppunten die zijn gemaakt zijn leeg Ubuntu-knooppunten. Vaak, moet u een set programma's tooinstall als vereisten.
U kunt gewoonlijk een shell-script waarmee Hallo vereisten voordat Hallo werkelijke taken uitgevoerd worden geïnstalleerd hebben voor Linux-knooppunten. Dit kunnen echter alle programmeerbare uitvoerbare bestanden zijn.
Hallo [shell-script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in dit voorbeeld installeert u Python pip en hello Azure-opslag-SDK voor Python.

U kunt uploaden Hallo-script op basis van een Azure Storage-Account en een SAS-URI tooaccess Hallo script genereren. Dit proces kan ook worden geautomatiseerd met Hallo Node.js-SDK van Azure Storage.

> [!Tip]
> Een taak voorbereiding voor een taak wordt alleen uitgevoerd op Hallo VM knooppunten waarin specifieke taak Hallo toorun moet. Als u wilt dat vereisten toobe geïnstalleerd op alle knooppunten ongeacht Hallo-taken die erop worden uitgevoerd, kunt u Hallo [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) eigenschap tijdens het toevoegen van een groep. U kunt na de taakdefinitie voorbereiding voor verwijzing Hallo gebruiken.
>
>

Een jobvoorbereidingstaak wordt opgegeven tijdens de verzending van Hallo van Azure Batch-taak. Hieronder worden voorbereiding taak configuratieparameters Hallo:

* **ID**: een unieke id voor de jobvoorbereidingstaak Hallo
* **commandLine**: tooexecute hello opdrachtregeltaak uitvoerbare
* **resourceFiles**: matrix met objecten die Geef details op van bestanden die nodig zijn voor deze taak toorun gedownload toobe.  Hieronder vindt u de bijbehorende opties
    - blobSource: Hallo SAS-URI van Hallo-bestand
    - filePath: lokaal pad toodownload en Hallo bestand opslaan
    - fileMode: fileMode is alleen van toepassing op Linux-knooppunten en heeft een octale indeling met de standaardwaarde 0770
* **waitForSuccess**: als set tootrue, Hallo taak kan niet worden uitgevoerd op voorbereiding taakfouten
* **runElevated**: Stel deze tootrue als verhoogde bevoegdheden nodig toorun Hallo taak.

Volgende codefragment toont Hallo voorbereiding taak voorbeeldscript-configuratie:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Als er geen vereisten toobe voor uw taken toorun geïnstalleerd, kunt u Hallo systeemvoorbereidingstaken overslaan. Met de volgende code wordt een taan aangemaakt met de weergavenaam 'process csv files'.

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Stap 5: Azure Batch-taken voor een taak verzenden

Nu de taak voor het verwerken van CSV-bestanden is gemaakt, maakt u taken voor die taak. Ervan uitgaande dat er vier containers, hebben we toocreate vier taken, één voor elke container.

Als we hello bekijkt [pythonscript](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), twee parameters accepteert:

* containernaam: Hallo container toodownload opslagbestanden uit
* pattern: een optionele parameter voor een bestandsnaampatroon

Ervan uitgaande dat we hebben vier containers 'con1', 'con2', 'con3', code 'con4' volgende toont indienen voor taken toohello Azure batch-taak 'proces csv' we eerder hebben gemaakt.

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

Hallo-code wordt meerdere taken toohello groep toegevoegd. En Hallo taken worden uitgevoerd op een knooppunt in de pool Hallo van virtuele machines die zijn gemaakt. Als het aantal taken Hallo Hallo aantal virtuele machines in een groep of Hallo maxTasksPerNode-eigenschap overschrijdt, wordt Hallo taken wacht totdat een knooppunt beschikbaar wordt gesteld. Azure Batch deelt alles automatisch in.

Hallo portal heeft gedetailleerde weergaven op Hallo taken en status van een taak. U kunt ook gebruik Hallo lijst en functies in hello Azure knooppunt SDK ophalen. Details zijn beschikbaar in de documentatie van de Hallo [koppeling](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Volgende stappen

- Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.
- Zie Hallo [Batch Node.js verwijzing](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Hallo Batch-API.

