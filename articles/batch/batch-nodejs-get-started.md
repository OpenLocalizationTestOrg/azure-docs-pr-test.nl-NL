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
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="39bc9-103">Aan de slag met de Batch-SDK voor Node.js</span><span class="sxs-lookup"><span data-stu-id="39bc9-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39bc9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="39bc9-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="39bc9-105">Python</span><span class="sxs-lookup"><span data-stu-id="39bc9-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="39bc9-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="39bc9-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="39bc9-107">Leer de basisbeginselen Hallo van het bouwen van een batchclient in met behulp van Node.js [Node.js-SDK van Azure Batch](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="39bc9-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="39bc9-108">Er wordt een stapsgewijze benadering gebruikt om inzicht te krijgen in een scenario voor een Batch-toepassing. Daarna wordt de toepassing met een Node.js-client ingesteld.</span><span class="sxs-lookup"><span data-stu-id="39bc9-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="39bc9-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="39bc9-109">Prerequisites</span></span>
<span data-ttu-id="39bc9-110">In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van Node.js en vertrouwd bent met Linux.</span><span class="sxs-lookup"><span data-stu-id="39bc9-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="39bc9-111">Ook wordt ervan uitgegaan dat u een Azure-account-installatie met toegang rechten toocreate Batch- en Storage-services hebt.</span><span class="sxs-lookup"><span data-stu-id="39bc9-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="39bc9-112">Lezen wordt aangeraden [technisch overzicht van Azure Batch](batch-technical-overview.md) voordat u doorloopt Hallo stappen die worden beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="39bc9-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="39bc9-113">Hallo zelfstudie scenario</span><span class="sxs-lookup"><span data-stu-id="39bc9-113">hello tutorial scenario</span></span>
<span data-ttu-id="39bc9-114">Laat het ons weten Hallo batch-werkstroom scenario.</span><span class="sxs-lookup"><span data-stu-id="39bc9-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="39bc9-115">We hebben een eenvoudig script geschreven in Python die downloadt alle csv-bestanden van een Azure Blob storage-container en zet deze tooJSON.</span><span class="sxs-lookup"><span data-stu-id="39bc9-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="39bc9-116">tooprocess meerdere storage account containers parallel, we Hallo script als een Azure Batch-taak kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="39bc9-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="39bc9-117">Azure Batch-architectuur</span><span class="sxs-lookup"><span data-stu-id="39bc9-117">Azure Batch Architecture</span></span>
<span data-ttu-id="39bc9-118">Hallo volgende diagram illustreert hoe Hallo pythonscript met behulp van Azure Batch- en een Node.js-client kan worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="39bc9-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch-scenario](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="39bc9-120">een batch-job implementeert Hallo node.js-client met een jobvoorbereidingstaak (uitvoerig besproken later) en een aantal taken, afhankelijk van het aantal containers in het opslagaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="39bc9-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="39bc9-121">Hallo scripts kunt u downloaden van Hallo github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="39bc9-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="39bc9-122">Node.js-client</span><span class="sxs-lookup"><span data-stu-id="39bc9-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="39bc9-123">Voorbereidingstaak voor Shell-scripts</span><span class="sxs-lookup"><span data-stu-id="39bc9-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="39bc9-124">Python csv tooJSON processor</span><span class="sxs-lookup"><span data-stu-id="39bc9-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="39bc9-125">Hallo Node.js-client in Hallo koppeling opgegeven bevat geen specifieke code toobe geïmplementeerd als een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="39bc9-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="39bc9-126">U kunt de volgende koppelingen voor instructies toocreate een toohello verwijzen.</span><span class="sxs-lookup"><span data-stu-id="39bc9-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="39bc9-127">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="39bc9-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="39bc9-128">Een timertriggerfunctie maken</span><span class="sxs-lookup"><span data-stu-id="39bc9-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="39bc9-129">Hallo-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="39bc9-129">Build hello application</span></span>

<span data-ttu-id="39bc9-130">Laat het ons voert nu Hallo proces stap voor stap bij het bouwen van Hallo Node.js-client:</span><span class="sxs-lookup"><span data-stu-id="39bc9-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="39bc9-131">Stap 1: de Azure Batch-SDK installeren</span><span class="sxs-lookup"><span data-stu-id="39bc9-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="39bc9-132">U kunt Azure Batch-SDK voor Node.js hello npm installatieopdracht met installeren.</span><span class="sxs-lookup"><span data-stu-id="39bc9-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="39bc9-133">Deze opdracht wordt de meest recente versie van azure batch-knooppunt SDK Hallo geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="39bc9-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="39bc9-134">In een Azure-functie-app, kunt u gaan te 'Kudu-Console' in hello Azure functie de instellingen tabblad toorun hello npm opdrachten installeren.</span><span class="sxs-lookup"><span data-stu-id="39bc9-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="39bc9-135">In dit geval tooinstall Azure Batch-SDK voor Node.js.</span><span class="sxs-lookup"><span data-stu-id="39bc9-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="39bc9-136">Stap 2: een Azure Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="39bc9-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="39bc9-137">U kunt het maken van Hallo [Azure-portal](batch-account-create-portal.md) of vanaf de opdrachtregel ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="39bc9-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="39bc9-138">Hieronder vindt u Hallo opdrachten toocreate een via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="39bc9-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="39bc9-139">Een resourcegroep maken, deze stap overslaan als u al een waar u toocreate Hallo Batch-Account:</span><span class="sxs-lookup"><span data-stu-id="39bc9-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="39bc9-140">Maak daarna een Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="39bc9-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="39bc9-141">Elk Batch-account heeft bijbehorende toegangssleutels.</span><span class="sxs-lookup"><span data-stu-id="39bc9-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="39bc9-142">Deze sleutels zijn benodigde toocreate meer resources in Azure batch-account.</span><span class="sxs-lookup"><span data-stu-id="39bc9-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="39bc9-143">Een goede gewoonte voor productie-omgeving is toouse Azure Key Vault toostore deze sleutels.</span><span class="sxs-lookup"><span data-stu-id="39bc9-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="39bc9-144">U kunt vervolgens een Service maken voor de toepassing hello principal.</span><span class="sxs-lookup"><span data-stu-id="39bc9-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="39bc9-145">Met behulp van deze service-principal Hallo-toepassing, kunt een OAuth-token tooaccess-sleutels maken in Hallo sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="39bc9-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="39bc9-146">Kopiëren en Hallo sleutel toobe gebruikt bij de volgende stappen Hallo op te slaan.</span><span class="sxs-lookup"><span data-stu-id="39bc9-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="39bc9-147">Stap 3: een Azure Batch-serviceclient maken</span><span class="sxs-lookup"><span data-stu-id="39bc9-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="39bc9-148">Volgende codefragment eerst importeert hello azure batch Node.js-module en maakt vervolgens een Batch-Service-client.</span><span class="sxs-lookup"><span data-stu-id="39bc9-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="39bc9-149">U moet toofirst een SharedKeyCredentials-object maken met Hallo Batch-accountsleutel is gekopieerd uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="39bc9-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

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

<span data-ttu-id="39bc9-150">Hello Azure Batch URI vindt u in het tabblad Overzicht van Hallo Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="39bc9-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="39bc9-151">Het is Hallo-indeling:</span><span class="sxs-lookup"><span data-stu-id="39bc9-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="39bc9-152">Raadpleeg toohello schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="39bc9-152">Refer toohello screenshot:</span></span>

![Azure Batch-URI](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="39bc9-154">Stap 4: een Azure Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="39bc9-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="39bc9-155">Een Azure Batch-pool bestaat uit meerdere virtuele machines (ook wel Batch-knooppunten genoemd).</span><span class="sxs-lookup"><span data-stu-id="39bc9-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="39bc9-156">Azure Batch-service Hallo taken op die knooppunten implementeert en beheert deze.</span><span class="sxs-lookup"><span data-stu-id="39bc9-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="39bc9-157">Hallo configuratieparameters voor uw pool te volgen, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="39bc9-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="39bc9-158">Type VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="39bc9-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="39bc9-159">Grootte van de VM-knooppunten</span><span class="sxs-lookup"><span data-stu-id="39bc9-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="39bc9-160">Aantal VM-knooppunten</span><span class="sxs-lookup"><span data-stu-id="39bc9-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="39bc9-161">Hallo grootte en het aantal knooppunten van de virtuele Machine afhankelijk grotendeels van het aantal gewenste taken toorun in parallel en ook Hallo taak zelf Hallo.</span><span class="sxs-lookup"><span data-stu-id="39bc9-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="39bc9-162">U kunt het beste testen toodetermine Hallo ideaal aantal en de grootte.</span><span class="sxs-lookup"><span data-stu-id="39bc9-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="39bc9-163">Hallo maakt volgende codefragment Hallo configuratieobjecten van de parameter.</span><span class="sxs-lookup"><span data-stu-id="39bc9-163">hello following code snippet creates hello configuration parameter objects.</span></span>

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
> <span data-ttu-id="39bc9-164">Zie voor Hallo lijst met Linux VM-installatiekopieën beschikbaar voor Azure Batch en hun SKU-id, [lijst van installatiekopieën van virtuele machines](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="39bc9-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="39bc9-165">Zodra de configuratie van de groep Hallo is gedefinieerd, kunt u hello Azure Batch-pool maken.</span><span class="sxs-lookup"><span data-stu-id="39bc9-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="39bc9-166">Hallo opdracht Batch-pool knooppunten Azure virtuele Machine maakt en bereidt ze toobe gereed tooreceive taken tooexecute.</span><span class="sxs-lookup"><span data-stu-id="39bc9-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="39bc9-167">Elke pool moet een unieke id krijgen zodat er in volgende stappen naar kan worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="39bc9-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="39bc9-168">Hallo volgende codefragment maakt een Azure Batch-pool.</span><span class="sxs-lookup"><span data-stu-id="39bc9-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="39bc9-169">U kunt Hallo status controleren van Hallo-toepassingen die zijn gemaakt en zorg ervoor dat Hallo status 'actief' voordat u wilt doorgaan met het verzenden van een taak toothat pool.</span><span class="sxs-lookup"><span data-stu-id="39bc9-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

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

<span data-ttu-id="39bc9-170">Hier volgt een voorbeeld resultaatobject geretourneerd door Hallo pool.get functie.</span><span class="sxs-lookup"><span data-stu-id="39bc9-170">Following is a sample result object returned by hello pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="39bc9-171">Stap 4: een Azure Batch-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="39bc9-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="39bc9-172">Een Azure Batch-taak is een logische groep vergelijkbare taken.</span><span class="sxs-lookup"><span data-stu-id="39bc9-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="39bc9-173">In ons scenario is het 'Proces csv tooJSON'.</span><span class="sxs-lookup"><span data-stu-id="39bc9-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="39bc9-174">Bij elke taak worden er hier CSV-bestanden omgezet die aanwezig zijn in Azure Storage-containers.</span><span class="sxs-lookup"><span data-stu-id="39bc9-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="39bc9-175">Deze taken parallel uitgevoerd en geïmplementeerd op meerdere knooppunten, gedirigeerd door hello Azure Batch-service.</span><span class="sxs-lookup"><span data-stu-id="39bc9-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="39bc9-176">U kunt Hallo [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) eigenschap toospecify maximum aantal taken dat tegelijk op één knooppunt kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39bc9-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="39bc9-177">Voorbereidingstaak</span><span class="sxs-lookup"><span data-stu-id="39bc9-177">Preparation task</span></span>

<span data-ttu-id="39bc9-178">Hallo VM knooppunten die zijn gemaakt zijn leeg Ubuntu-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="39bc9-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="39bc9-179">Vaak, moet u een set programma's tooinstall als vereisten.</span><span class="sxs-lookup"><span data-stu-id="39bc9-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="39bc9-180">U kunt gewoonlijk een shell-script waarmee Hallo vereisten voordat Hallo werkelijke taken uitgevoerd worden geïnstalleerd hebben voor Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="39bc9-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="39bc9-181">Dit kunnen echter alle programmeerbare uitvoerbare bestanden zijn.</span><span class="sxs-lookup"><span data-stu-id="39bc9-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="39bc9-182">Hallo [shell-script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in dit voorbeeld installeert u Python pip en hello Azure-opslag-SDK voor Python.</span><span class="sxs-lookup"><span data-stu-id="39bc9-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="39bc9-183">U kunt uploaden Hallo-script op basis van een Azure Storage-Account en een SAS-URI tooaccess Hallo script genereren.</span><span class="sxs-lookup"><span data-stu-id="39bc9-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="39bc9-184">Dit proces kan ook worden geautomatiseerd met Hallo Node.js-SDK van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="39bc9-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="39bc9-185">Een taak voorbereiding voor een taak wordt alleen uitgevoerd op Hallo VM knooppunten waarin specifieke taak Hallo toorun moet.</span><span class="sxs-lookup"><span data-stu-id="39bc9-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="39bc9-186">Als u wilt dat vereisten toobe geïnstalleerd op alle knooppunten ongeacht Hallo-taken die erop worden uitgevoerd, kunt u Hallo [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) eigenschap tijdens het toevoegen van een groep.</span><span class="sxs-lookup"><span data-stu-id="39bc9-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="39bc9-187">U kunt na de taakdefinitie voorbereiding voor verwijzing Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39bc9-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="39bc9-188">Een jobvoorbereidingstaak wordt opgegeven tijdens de verzending van Hallo van Azure Batch-taak.</span><span class="sxs-lookup"><span data-stu-id="39bc9-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="39bc9-189">Hieronder worden voorbereiding taak configuratieparameters Hallo:</span><span class="sxs-lookup"><span data-stu-id="39bc9-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="39bc9-190">**ID**: een unieke id voor de jobvoorbereidingstaak Hallo</span><span class="sxs-lookup"><span data-stu-id="39bc9-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="39bc9-191">**commandLine**: tooexecute hello opdrachtregeltaak uitvoerbare</span><span class="sxs-lookup"><span data-stu-id="39bc9-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="39bc9-192">**resourceFiles**: matrix met objecten die Geef details op van bestanden die nodig zijn voor deze taak toorun gedownload toobe.</span><span class="sxs-lookup"><span data-stu-id="39bc9-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="39bc9-193">Hieronder vindt u de bijbehorende opties</span><span class="sxs-lookup"><span data-stu-id="39bc9-193">Following are its options</span></span>
    - <span data-ttu-id="39bc9-194">blobSource: Hallo SAS-URI van Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="39bc9-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="39bc9-195">filePath: lokaal pad toodownload en Hallo bestand opslaan</span><span class="sxs-lookup"><span data-stu-id="39bc9-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="39bc9-196">fileMode: fileMode is alleen van toepassing op Linux-knooppunten en heeft een octale indeling met de standaardwaarde 0770</span><span class="sxs-lookup"><span data-stu-id="39bc9-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="39bc9-197">**waitForSuccess**: als set tootrue, Hallo taak kan niet worden uitgevoerd op voorbereiding taakfouten</span><span class="sxs-lookup"><span data-stu-id="39bc9-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="39bc9-198">**runElevated**: Stel deze tootrue als verhoogde bevoegdheden nodig toorun Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="39bc9-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="39bc9-199">Volgende codefragment toont Hallo voorbereiding taak voorbeeldscript-configuratie:</span><span class="sxs-lookup"><span data-stu-id="39bc9-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="39bc9-200">Als er geen vereisten toobe voor uw taken toorun geïnstalleerd, kunt u Hallo systeemvoorbereidingstaken overslaan.</span><span class="sxs-lookup"><span data-stu-id="39bc9-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="39bc9-201">Met de volgende code wordt een taan aangemaakt met de weergavenaam 'process csv files'.</span><span class="sxs-lookup"><span data-stu-id="39bc9-201">Following code creates a job with display name "process csv files."</span></span>

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="39bc9-202">Stap 5: Azure Batch-taken voor een taak verzenden</span><span class="sxs-lookup"><span data-stu-id="39bc9-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="39bc9-203">Nu de taak voor het verwerken van CSV-bestanden is gemaakt, maakt u taken voor die taak.</span><span class="sxs-lookup"><span data-stu-id="39bc9-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="39bc9-204">Ervan uitgaande dat er vier containers, hebben we toocreate vier taken, één voor elke container.</span><span class="sxs-lookup"><span data-stu-id="39bc9-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="39bc9-205">Als we hello bekijkt [pythonscript](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), twee parameters accepteert:</span><span class="sxs-lookup"><span data-stu-id="39bc9-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="39bc9-206">containernaam: Hallo container toodownload opslagbestanden uit</span><span class="sxs-lookup"><span data-stu-id="39bc9-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="39bc9-207">pattern: een optionele parameter voor een bestandsnaampatroon</span><span class="sxs-lookup"><span data-stu-id="39bc9-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="39bc9-208">Ervan uitgaande dat we hebben vier containers 'con1', 'con2', 'con3', code 'con4' volgende toont indienen voor taken toohello Azure batch-taak 'proces csv' we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39bc9-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="39bc9-209">Hallo-code wordt meerdere taken toohello groep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="39bc9-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="39bc9-210">En Hallo taken worden uitgevoerd op een knooppunt in de pool Hallo van virtuele machines die zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39bc9-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="39bc9-211">Als het aantal taken Hallo Hallo aantal virtuele machines in een groep of Hallo maxTasksPerNode-eigenschap overschrijdt, wordt Hallo taken wacht totdat een knooppunt beschikbaar wordt gesteld.</span><span class="sxs-lookup"><span data-stu-id="39bc9-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="39bc9-212">Azure Batch deelt alles automatisch in.</span><span class="sxs-lookup"><span data-stu-id="39bc9-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="39bc9-213">Hallo portal heeft gedetailleerde weergaven op Hallo taken en status van een taak.</span><span class="sxs-lookup"><span data-stu-id="39bc9-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="39bc9-214">U kunt ook gebruik Hallo lijst en functies in hello Azure knooppunt SDK ophalen.</span><span class="sxs-lookup"><span data-stu-id="39bc9-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="39bc9-215">Details zijn beschikbaar in de documentatie van de Hallo [koppeling](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="39bc9-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39bc9-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39bc9-216">Next steps</span></span>

- <span data-ttu-id="39bc9-217">Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.</span><span class="sxs-lookup"><span data-stu-id="39bc9-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="39bc9-218">Zie Hallo [Batch Node.js verwijzing](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Hallo Batch-API.</span><span class="sxs-lookup"><span data-stu-id="39bc9-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

