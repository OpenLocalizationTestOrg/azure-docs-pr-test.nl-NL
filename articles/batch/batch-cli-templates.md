---
title: Azure Batch aaaRun taken end-to-end-code (Preview) te schrijven | Microsoft Docs
description: Maak sjabloonbestanden hello Azure CLI toocreate Batch-pools, jobs en taken.
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="68f13-103">Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)</span><span class="sxs-lookup"><span data-stu-id="68f13-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="68f13-104">Met hello Azure CLI is het mogelijk toorun batchtaken zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="68f13-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="68f13-105">Sjabloonbestanden worden gemaakt en gebruikt met hello Azure CLI waarmee Batch-pools, jobs en taken toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68f13-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="68f13-106">Taak invoerbestanden kunnen eenvoudig worden geüpload naar Hallo storage-account gekoppeld Hallo Batch-account en taak uitvoerbestanden gedownload.</span><span class="sxs-lookup"><span data-stu-id="68f13-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="68f13-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="68f13-107">Overview</span></span>

<span data-ttu-id="68f13-108">Een uitbreiding toohello Azure CLI kunt Batch toobe gebruikt end-to-end door gebruikers die geen ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="68f13-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="68f13-109">Een groep kan worden gemaakt, invoergegevens geüpload, taken en de bijbehorende taken die zijn gemaakt, en Hallo resulterende uitvoergegevens gedownload – geen code vereist, Hallo CLI wordt geïntegreerd in scripts of rechtstreeks worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="68f13-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="68f13-110">Batch-sjablonen samenstellen op Hallo [bestaande Batch-ondersteuning in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) waarmee JSON-bestanden toospecify eigenschapswaarden voor Hallo maken van groepen, taken, taken en andere items.</span><span class="sxs-lookup"><span data-stu-id="68f13-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="68f13-111">Met Batch-sjablonen worden hello volgende mogelijkheden toegevoegd via wat is er mogelijk met Hallo JSON-bestanden:</span><span class="sxs-lookup"><span data-stu-id="68f13-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="68f13-112">Parameters kunnen worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-112">Parameters can be defined.</span></span> <span data-ttu-id="68f13-113">Wanneer het Hallo-sjabloon gebruikt, zijn alleen Hallo parameterwaarden opgegeven toocreate Hallo artikel, met andere item eigenschapswaarden worden opgegeven in de hoofdtekst van de Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="68f13-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="68f13-114">Een gebruiker die werkt met dat batch- en de toobe toepassingen worden uitgevoerd door de Batch kunt sjablonen maken pool, Jobs en taak eigenschapswaarden opgeven.</span><span class="sxs-lookup"><span data-stu-id="68f13-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="68f13-115">Een gebruiker minder bekend bent met de Batch-en/of de toepassingen hoeft slechts toospecify Hallo waarden voor parameters Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="68f13-116">Taak taak fabrieken maken van een of meer taken die zijn gekoppeld aan een taak, waardoor het Hallo voorkomen moeten voor veel taak definities toobe gemaakt en aanzienlijk vereenvoudigen verzending van de taak.</span><span class="sxs-lookup"><span data-stu-id="68f13-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="68f13-117">Invoergegevensbestanden moeten worden opgegeven voor taken toobe en uitvoerbestanden gegevens vaak worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="68f13-118">Een opslagaccount is gekoppeld, standaard, bij elke Batch-account en bestanden eenvoudig overgebrachte tooand van dit opslagaccount met behulp van de CLI met geen coderingen kunnen worden en geen referenties opslag vereist.</span><span class="sxs-lookup"><span data-stu-id="68f13-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="68f13-119">Bijvoorbeeld: [ffmpeg](http://ffmpeg.org/) is een populaire toepassing die audio en video-bestanden worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="68f13-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="68f13-120">Hello Azure Batch CLI kan gebruikte tooinvoke ffmpeg tootranscode bron videobestanden toodifferent oplossingen zijn.</span><span class="sxs-lookup"><span data-stu-id="68f13-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="68f13-121">Een pool-sjabloon is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68f13-121">A pool template is created.</span></span> <span data-ttu-id="68f13-122">Hallo-gebruiker maken Hallo sjabloon weet hoe toocall Hallo ffmpeg toepassing en de vereisten; Deze Hallo opgeven juiste OS, VM grootte, hoe ffmpeg is geïnstalleerd (van een toepassingspakket of met behulp van een Pakketbeheer bijvoorbeeld), en andere eigenschapswaarden-groep.</span><span class="sxs-lookup"><span data-stu-id="68f13-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="68f13-123">Parameters worden gemaakt wanneer het Hallo-sjabloon gebruikt, alleen Hallo verzameling-id en het aantal virtuele machines moet toobe opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68f13-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="68f13-124">Een sjabloon wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68f13-124">A job template is created.</span></span> <span data-ttu-id="68f13-125">Hallo maken Hallo gebruikerssjabloon weet hoe ffmpeg behoeften toobe aangeroepen tootranscode bron video tooa andere resolutie en geeft Hallo taak opdrachtregel; ze ook weten dat er een map met de Hallo bron videobestanden, met een taak vereist per bestand voor invoer.</span><span class="sxs-lookup"><span data-stu-id="68f13-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="68f13-126">Een eindgebruiker met een reeks videobestanden tootranscode maakt eerst een groep Hallo groep sjabloon gebruikt, geven alleen Hallo verzameling-id en het aantal virtuele machines die zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="68f13-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="68f13-127">Ze kunnen vervolgens Hallo bron bestanden tootranscode uploaden.</span><span class="sxs-lookup"><span data-stu-id="68f13-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="68f13-128">Een taak kan vervolgens worden verzonden met behulp van Hallo-taaksjabloon opgeven alleen Hallo pool-id en de locatie van bronbestanden Hallo geüpload.</span><span class="sxs-lookup"><span data-stu-id="68f13-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="68f13-129">Hallo Batch-job is gemaakt met één taak per bestand voor invoer wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="68f13-130">Ten slotte kunnen Hallo getranscodeerd uitvoerbestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="68f13-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="68f13-131">Installeren</span><span class="sxs-lookup"><span data-stu-id="68f13-131">Installation</span></span>

<span data-ttu-id="68f13-132">Hallo-sjabloon en de bestandsnaam overdrachtmogelijkheden vereisen een extensie toobe geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="68f13-133">Voor instructies over hoe tooinstall hello Azure CLI zien [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68f13-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="68f13-134">Eenmaal hello die Azure CLI is geïnstalleerd, Hallo Batch-extensie kan worden geïnstalleerd met de volgende CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="68f13-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="68f13-135">Zie voor meer informatie over Hallo Batch extensie [Microsoft Azure Batch CLI uitbreidingen voor Windows, Mac en Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="68f13-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="68f13-136">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="68f13-136">Templates</span></span>

<span data-ttu-id="68f13-137">Hello Azure Batch CLI kunt items zoals pools, jobs en taken toobe gemaakt door te geven van een JSON-bestand met de namen van eigenschappen en waarden.</span><span class="sxs-lookup"><span data-stu-id="68f13-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="68f13-138">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="68f13-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="68f13-139">Azure Batch-sjablonen zijn vergelijkbaar tooAzure Resource Manager-sjablonen, in de functionaliteit en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="68f13-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="68f13-140">Ze zijn JSON-bestanden die itemnamen en waarden bevatten, maar na de belangrijkste concepten Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="68f13-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="68f13-141">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="68f13-141">**Parameters**</span></span>

    -   <span data-ttu-id="68f13-142">Toestaan dat de eigenschap waarden toobe is opgegeven in een sectie hoofdtekst met alleen parameterwaarden hoeven toobe wanneer Hallo sjabloon wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68f13-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="68f13-143">Hallo volledige definitie voor een groep kan bijvoorbeeld worden geplaatst in Hallo-instantie en slechts één parameter gedefinieerd voor groep-id; alleen een tekenreeks in de pool-id moet daarom toobe opgegeven toocreate een pool.</span><span class="sxs-lookup"><span data-stu-id="68f13-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="68f13-144">Hallo sjabloon instantie worden geschreven door iemand met kennis van Batch en Hallo toepassingen toobe uitvoeren door de Batch; alleen waarden voor Hallo auteur gedefinieerde parameters moeten worden opgegeven als Hallo-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="68f13-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="68f13-145">Een gebruiker zonder Hallo diepgaande Batch en/of kennis van de toepassing gebruik daarom de sjablonen.</span><span class="sxs-lookup"><span data-stu-id="68f13-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="68f13-146">**Variabelen**</span><span class="sxs-lookup"><span data-stu-id="68f13-146">**Variables**</span></span>

    -   <span data-ttu-id="68f13-147">Eenvoudige of complexe parameter waarden toobe opgegeven in één locatie en gebruikt op een of meer plaatsen in de hoofdtekst van de sjabloon Hallo toestaan.</span><span class="sxs-lookup"><span data-stu-id="68f13-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="68f13-148">Variabelen kunnen vereenvoudigen en verkleinen Hallo Hallo-sjabloon, evenals meer bruikbaar maken door er één locatie toochange eigenschappen waarvan de waarde mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="68f13-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="68f13-149">**Een hoger niveau constructies**</span><span class="sxs-lookup"><span data-stu-id="68f13-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="68f13-150">Sommige op een hoger niveau constructies zijn beschikbaar in het Hallo-sjabloon die nog niet beschikbaar in Hallo Batch-API's.</span><span class="sxs-lookup"><span data-stu-id="68f13-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="68f13-151">Een taak factory kan bijvoorbeeld worden gedefinieerd in een sjabloon die wordt gemaakt van meerdere taken voor het Hallo-taak met een gemeenschappelijke taakdefinitie.</span><span class="sxs-lookup"><span data-stu-id="68f13-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="68f13-152">Deze gegevens te voorkomen dat Hallo nodig toocode om dynamisch meerdere JSON-bestanden, zoals één bestand per taak te maken, evenals een script bijvoorbeeld bestanden tooinstall toepassingen via een Pakketbeheer maken.</span><span class="sxs-lookup"><span data-stu-id="68f13-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="68f13-153">Op sommige punt, waar van toepassing, dat deze gegevens kunnen worden toegevoegd toothe Batch-service en is beschikbaar in Hallo Batch-API's, UI, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="68f13-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="68f13-154">Pool-sjablonen</span><span class="sxs-lookup"><span data-stu-id="68f13-154">Pool templates</span></span>

<span data-ttu-id="68f13-155">Bovendien worden toohello standaardsjabloon mogelijkheden van de parameters en variabelen, Hallo na een hoger niveau constructies ondersteund door Hallo groep sjabloon:</span><span class="sxs-lookup"><span data-stu-id="68f13-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="68f13-156">**Pakket met verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="68f13-156">**Package references**</span></span>

    -   <span data-ttu-id="68f13-157">Desgewenst kunnen software toobe gekopieerd toopool knooppunten met behulp van pakket managers.</span><span class="sxs-lookup"><span data-stu-id="68f13-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="68f13-158">Hallo Pakketbeheer en pakket-id worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68f13-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="68f13-159">Kan toodeclare worden een of meer pakketten voorkomt Hallo nodig toocreate een script dat vereist hello-pakketten opgehaald, Hallo script installeren en Hallo-script uitvoeren op elk knooppunt van de groep van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="68f13-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="68f13-160">Hallo Hier volgt een voorbeeld van een sjabloon die u een pool van Linux virtuele machines met ffmpeg geïnstalleerd en alleen maakt een pool-id tekenreeks en Hallo aantal virtuele machines toobe opgegeven toouse vereist:</span><span class="sxs-lookup"><span data-stu-id="68f13-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="68f13-161">Als de naam van het sjabloonbestand Hallo _groep ffmpeg.json_, en vervolgens de sjabloon Hallo zou als volgt worden aangeroepen:</span><span class="sxs-lookup"><span data-stu-id="68f13-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="68f13-162">Taaksjablonen</span><span class="sxs-lookup"><span data-stu-id="68f13-162">Job templates</span></span>

<span data-ttu-id="68f13-163">Bovendien worden toohello standaardsjabloon mogelijkheden van de parameters en variabelen, Hallo na een hoger niveau constructies ondersteund door Hallo taaksjabloon:</span><span class="sxs-lookup"><span data-stu-id="68f13-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="68f13-164">**Taak factory**</span><span class="sxs-lookup"><span data-stu-id="68f13-164">**Task factory**</span></span>

    -   <span data-ttu-id="68f13-165">Meerdere taken voor een taak maakt van de definitie van één taak.</span><span class="sxs-lookup"><span data-stu-id="68f13-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="68f13-166">Drie soorten taak factory worden ondersteund: parametrische sweep, taak per bestand, en verzameling van de taak.</span><span class="sxs-lookup"><span data-stu-id="68f13-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="68f13-167">Hallo Hieronder volgt een voorbeeld van een sjabloon die u maakt een taak die gebruikmaakt van ffmpeg te transcoderen MP4 videobestanden tooone van twee lagere resolutie, met één taak per video bronbestand gemaakt:</span><span class="sxs-lookup"><span data-stu-id="68f13-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="68f13-168">Als de naam van het sjabloonbestand Hallo _taak ffmpeg.json_, en vervolgens de sjabloon Hallo zou als volgt worden aangeroepen:</span><span class="sxs-lookup"><span data-stu-id="68f13-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="68f13-169">Bestandsgroepen en bestandsoverdracht</span><span class="sxs-lookup"><span data-stu-id="68f13-169">File groups and file transfer</span></span>

<span data-ttu-id="68f13-170">De meeste jobs en taken vereisen invoerbestanden en uitvoerbestanden wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="68f13-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="68f13-171">Beide bestanden invoer- en uitvoerbestanden moeten doorgaans toobe worden overgedragen, van Hallo client toohello knooppunt of Hallo node toohello-client.</span><span class="sxs-lookup"><span data-stu-id="68f13-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="68f13-172">Hello Azure Batch CLI extensie isoleert opslag bestandsoverdracht en maakt gebruik van Hallo storage-account dat door de standaardwaarde voor elk Batch-account wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68f13-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="68f13-173">Een bestandsgroep gelijkstaat tooa-container die in hello Azure storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68f13-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="68f13-174">Hallo-bestandsgroep misschien submappen.</span><span class="sxs-lookup"><span data-stu-id="68f13-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="68f13-175">Hallo Batch CLI-uitbreiding bevat opdrachten voor het uploaden van bestanden uit clientgroep tooa opgegeven bestand en downloaden van bestanden van Hallo opgegeven bestand groep tooa client.</span><span class="sxs-lookup"><span data-stu-id="68f13-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="68f13-176">Groep van toepassingen en -taak sjablonen kunnen bestanden die zijn opgeslagen in bestand groepen toobe opgegeven voor kopiëren naar de knooppunten van de groep van toepassingen of uit de groep knooppunten tooa bestandsgroep terug.</span><span class="sxs-lookup"><span data-stu-id="68f13-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="68f13-177">Bijvoorbeeld, in de taaksjabloon eerder hebt opgegeven, is Hallo bestand groep 'ffmpeg-invoer' opgegeven voor Hallo taak factory als Hallo locatie Hallo video van bronbestanden voor gekopieerd naar beneden op Hallo knooppunt voor transcodering; Hallo bestand groep 'ffmpeg-uitvoer' wordt gebruikt als hello locatie waar de uitvoerbestanden van Hallo getranscodeerd gekopieerd toofrom Hallo knooppunt uitgevoerd elke taak.</span><span class="sxs-lookup"><span data-stu-id="68f13-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="68f13-178">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="68f13-178">Summary</span></span>

<span data-ttu-id="68f13-179">Sjabloon en een bestand overdracht hebt op dit moment is ondersteuning toegevoegd alleen toohello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="68f13-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="68f13-180">Hallo-doel is tooexpand Hallo doelgroep die Batch toousers hoeven niet toodevelop code met Hallo Batch-API's, zoals onderzoekers en IT-gebruikers kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="68f13-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="68f13-181">Zonder codering, kunnen gebruikers met kennis van Azure Batch en Hallo toepassingen toobe uitvoeren door de Batch sjablonen voor het maken van toepassingen en -taak maken.</span><span class="sxs-lookup"><span data-stu-id="68f13-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="68f13-182">Met Sjabloonparameters, kunnen gebruikers zonder grondige kennis van de Batch- en Hallo toepassingen Hallo sjablonen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="68f13-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="68f13-183">Hallo Batch-extensie voor hello Azure CLI uitproberen en moet u alle feedback of suggesties, ofwel in Hallo opmerkingen voor dit artikel of via Hallo [Azure Batch-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="68f13-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f13-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68f13-184">Next steps</span></span>

- <span data-ttu-id="68f13-185">Zie Hallo Batch sjablonen blogbericht: [uitgevoerd op Azure Batch-taken met behulp van Azure CLI – geen code vereist Hallo](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="68f13-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="68f13-186">Gedetailleerde documentatie voor installatie en het gebruik, voorbeelden en broncode zijn beschikbaar in Hallo [Azure GitHub-opslagplaats](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="68f13-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
