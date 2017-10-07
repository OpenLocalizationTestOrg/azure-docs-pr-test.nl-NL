---
title: aaaAccess gegevenssets met Machine Learning Python-clientbibliotheek | Microsoft Docs
description: Installeren en gebruiken Hallo Python client bibliotheek tooaccess en Azure Machine Learning gegevens veilig beheren vanuit een lokale Python-omgeving.
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="5297f-103">Gegevenssets toegang met behulp van Python hello Azure Machine Learning Python-clientbibliotheek gebruiken</span><span class="sxs-lookup"><span data-stu-id="5297f-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="5297f-104">Hallo preview van Microsoft Azure Machine Learning Python-clientbibliotheek veilige toegang tooyour Azure Machine Learning gegevenssets van een lokale Python-omgeving kunt inschakelen en kunt Hallo maken en beheren van gegevenssets in een werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5297f-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="5297f-105">In dit onderwerp bevat instructies over het:</span><span class="sxs-lookup"><span data-stu-id="5297f-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="5297f-106">Hallo-clientbibliotheek voor Machine Learning Python installeren</span><span class="sxs-lookup"><span data-stu-id="5297f-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="5297f-107">toegang tot en gegevenssets heeft, inclusief aanwijzingen voor het uploaden tooget autorisatie tooaccess Azure Machine Learning gegevenssets van uw lokale omgeving voor Python</span><span class="sxs-lookup"><span data-stu-id="5297f-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="5297f-108">toegang tot tussenliggende gegevenssets van experimenten</span><span class="sxs-lookup"><span data-stu-id="5297f-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="5297f-109">Hallo Python client bibliotheek tooenumerate gegevenssets gebruiken, toegang tot metagegevens, lezen Hallo inhoud van een gegevensset, nieuwe gegevenssets maken en bijwerken van bestaande gegevenssets</span><span class="sxs-lookup"><span data-stu-id="5297f-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="5297f-110"><a name="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="5297f-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="5297f-111">Hallo Python-clientbibliotheek is getest onder Hallo volgende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="5297f-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="5297f-112">Windows, Mac en Linux</span><span class="sxs-lookup"><span data-stu-id="5297f-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="5297f-113">Python 2.7 3.3 en 3.4</span><span class="sxs-lookup"><span data-stu-id="5297f-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="5297f-114">Dit heeft een afhankelijkheid op hello-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="5297f-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="5297f-115">Aanvragen</span><span class="sxs-lookup"><span data-stu-id="5297f-115">requests</span></span>
* <span data-ttu-id="5297f-116">Python-dateutil</span><span class="sxs-lookup"><span data-stu-id="5297f-116">python-dateutil</span></span>
* <span data-ttu-id="5297f-117">pandas</span><span class="sxs-lookup"><span data-stu-id="5297f-117">pandas</span></span>

<span data-ttu-id="5297f-118">Wordt u aangeraden een Python-distributie, zoals [Anaconda](http://continuum.io/downloads#all) of [bladerdak](https://store.enthought.com/downloads/), die worden geleverd met Python, IPython en drie hello-pakketten die hierboven worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5297f-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="5297f-119">Hoewel IPython niet strikt vereist is, is een geweldige omgeving voor het werken en gegevens interactief te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="5297f-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="5297f-120"><a name="installation"></a>Hoe tooinstall Hallo clientbibliotheek van Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="5297f-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="5297f-121">Hello Azure Machine Learning Python-clientbibliotheek moet ook geïnstalleerde toocomplete Hallo taken die worden beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="5297f-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="5297f-122">Deze beschikbaar is via Hallo [Python Package Index](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="5297f-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="5297f-123">tooinstall uitvoeren in uw omgeving Python Hallo volgende opdracht uit uw lokale Python-omgeving:</span><span class="sxs-lookup"><span data-stu-id="5297f-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="5297f-124">U kunt ook downloaden en installeren vanuit Hallo bronnen op [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="5297f-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="5297f-125">Als u git op deze computer geïnstalleerd hebt, kunt u pip tooinstall rechtstreeks vanuit Hallo git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="5297f-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="5297f-126"><a name="datasetAccess"></a>Studio Code codefragmenten tooaccess gegevenssets gebruiken</span><span class="sxs-lookup"><span data-stu-id="5297f-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="5297f-127">Hallo Python-clientbibliotheek biedt u toegang op programmeerniveau tooyour bestaande gegevenssets van experimenten die zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5297f-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="5297f-128">Vanuit de Hallo Studio webinterface kunt u codefragmenten die alle Hallo benodigde informatie toodownload opnemen en gegevenssets te deserialiseren als Pandas DataFrame objecten op uw machine locatie genereren.</span><span class="sxs-lookup"><span data-stu-id="5297f-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="5297f-129"><a name="security"></a>Beveiliging voor toegang tot gegevens</span><span class="sxs-lookup"><span data-stu-id="5297f-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="5297f-130">Hallo codefragmenten geleverd door Studio voor gebruik met Hallo Python-clientbibliotheek uw werkruimte-id en -autorisatie bevat-token.</span><span class="sxs-lookup"><span data-stu-id="5297f-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="5297f-131">Deze volledige toegang tooyour werkruimte bevatten en moeten worden beveiligd, zoals een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5297f-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="5297f-132">Uit veiligheidsoverwegingen Hallo code codefragment functionaliteit is alleen beschikbaar toousers waarvoor hun rol is ingesteld als **eigenaar** voor Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5297f-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="5297f-133">Uw rol in Azure Machine Learning Studio wordt weergegeven op Hallo **gebruikers** pagina onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5297f-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Beveiliging][security]

<span data-ttu-id="5297f-135">Als uw rol niet is ingesteld als **eigenaar**, kunt u toobe reinvited als eigenaar van een aanvraag, of vraag de eigenaar van de Hallo van Hallo werkruimte tooprovide u met de Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="5297f-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="5297f-136">verificatietoken voor tooobtain hello, kunt u een van de volgende Hallo kunt doen:</span><span class="sxs-lookup"><span data-stu-id="5297f-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="5297f-137">Vragen om een token van een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="5297f-137">Ask for a token from an owner.</span></span> <span data-ttu-id="5297f-138">Eigenaars hebben toegang tot hun autorisatie-tokens van Hallo instellingenpagina van de werkruimte in Studio.</span><span class="sxs-lookup"><span data-stu-id="5297f-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="5297f-139">Selecteer **instellingen** van Hallo links deelvenster en klik op **AUTORISATIE TOKENS** toosee Hallo primaire en secundaire tokens.</span><span class="sxs-lookup"><span data-stu-id="5297f-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="5297f-140">Hoewel Hallo primaire of secundaire autorisatie-tokens Hallo kunnen worden gebruikt in het codefragment hello, wordt u aangeraden eigenaars delen alleen Hallo secundaire autorisatie-tokens.</span><span class="sxs-lookup"><span data-stu-id="5297f-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Autorisatie-tokens](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="5297f-142">Vraag toobe gepromoveerd toorole van eigenaar.</span><span class="sxs-lookup"><span data-stu-id="5297f-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="5297f-143">toodo dit, een huidige eigenaar van Hallo werkruimte behoeften toofirst worden verwijderd uit de werkruimte Hallo en vervolgens u opnieuw uit te nodigen tooit als eigenaar.</span><span class="sxs-lookup"><span data-stu-id="5297f-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="5297f-144">Als ontwikkelaars Hallo werkruimte-id en autorisatie hebt verkregen token, ze zijn kunnen tooaccess Hallo werkruimte met Hallo codefragment ongeacht hun rol.</span><span class="sxs-lookup"><span data-stu-id="5297f-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="5297f-145">Autorisatie-tokens worden beheerd op Hallo **AUTORISATIE TOKENS** pagina onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5297f-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="5297f-146">U kunt ze genereren, maar deze procedure worden de vorige toegangstoken toohello ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="5297f-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="5297f-147"><a name="accessingDatasets"></a>Gegevenssets toegang vanuit een lokale Python-toepassing</span><span class="sxs-lookup"><span data-stu-id="5297f-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="5297f-148">Klik in Machine Learning Studio **GEGEVENSSETS** Hallo navigatiebalk aan de linkerkant Hallo aan.</span><span class="sxs-lookup"><span data-stu-id="5297f-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="5297f-149">Hallo gegevensset u tooaccess wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="5297f-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="5297f-150">U kunt kiezen uit Hallo gegevenssets van Hallo **mijn GEGEVENSSETS** lijst of van Hallo **voorbeelden** lijst.</span><span class="sxs-lookup"><span data-stu-id="5297f-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="5297f-151">Hallo onderste werkbalk, klik op **toegangscode gegevens genereren**.</span><span class="sxs-lookup"><span data-stu-id="5297f-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="5297f-152">Als Hallo gegevens in een indeling die incompatibel is met de Hallo Python-clientbibliotheek is, wordt deze knop is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5297f-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![Gegevenssets][datasets]
4. <span data-ttu-id="5297f-154">Hallo codefragment selecteren in Hallo-venster dat wordt weergegeven en tooyour Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5297f-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Toegangscode][dataset-access-code]
5. <span data-ttu-id="5297f-156">Plak Hallo code in de notebook Hallo van uw lokale Python-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5297f-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Notebook][ipython-dataset]

## <span data-ttu-id="5297f-158"><a name="accessingIntermediateDatasets"></a>Tussenliggende gegevenssets van de toegang van Machine Learning-experimenten</span><span class="sxs-lookup"><span data-stu-id="5297f-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="5297f-159">Nadat een experiment in Machine Learning Studio hello wordt uitgevoerd, is het mogelijk tooaccess Hallo tussenliggende gegevenssets van Hallo uitvoerknooppunten van modules.</span><span class="sxs-lookup"><span data-stu-id="5297f-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="5297f-160">Tussenliggende gegevenssets zijn de gegevens die zijn gemaakt en gebruikt voor de tussenliggende stappen wanneer een model-hulpprogramma is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5297f-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="5297f-161">Tussenliggende gegevenssets toegankelijk zijn, zolang Hallo gegevensindeling compatibel met Hallo Python-clientbibliotheek is.</span><span class="sxs-lookup"><span data-stu-id="5297f-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="5297f-162">Hallo volgende indelingen worden ondersteund (constanten voor deze zich in Hallo `azureml.DataTypeIds` klasse):</span><span class="sxs-lookup"><span data-stu-id="5297f-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="5297f-163">Tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="5297f-163">PlainText</span></span>
* <span data-ttu-id="5297f-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="5297f-164">GenericCSV</span></span>
* <span data-ttu-id="5297f-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="5297f-165">GenericTSV</span></span>
* <span data-ttu-id="5297f-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="5297f-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="5297f-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="5297f-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="5297f-168">U kunt Hallo indeling bepalen door de muiswijzer op een knooppunt van de uitvoer module.</span><span class="sxs-lookup"><span data-stu-id="5297f-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="5297f-169">Deze wordt samen met de naam van het Hallo knooppunt, in de knopinfo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5297f-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="5297f-170">Aantal Hallo-modules, zoals Hallo [gesplitste] [ split] module met de naam de indeling van de uitvoer tooa `Dataset`, die niet wordt ondersteund door Hallo Python-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5297f-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Indeling van de gegevensset][dataset-format]

<span data-ttu-id="5297f-172">Moet u een module conversie toouse zoals [converteren tooCSV][convert-to-csv], tooget uitvoer naar een ondersteunde indeling.</span><span class="sxs-lookup"><span data-stu-id="5297f-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![GenericCSV-indeling][csv-format]

<span data-ttu-id="5297f-174">Hallo ziet volgende stappen een voorbeeld van een experiment maakt, worden uitgevoerd en heeft toegang tot de tussenliggende Hallo-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5297f-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="5297f-175">Een nieuw experiment maken.</span><span class="sxs-lookup"><span data-stu-id="5297f-175">Create a new experiment.</span></span>
2. <span data-ttu-id="5297f-176">Voeg een **volwassenen inventarisering Income binaire classificatie gegevensset** module.</span><span class="sxs-lookup"><span data-stu-id="5297f-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="5297f-177">Plaats een [gesplitste] [ split] module en verbinding maken met de invoer toohello gegevensset module uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5297f-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="5297f-178">Voeg een [tooCSV converteren] [ convert-to-csv] module en verbinding maken met de invoer tooone Hallo [gesplitste] [ split] module levert.</span><span class="sxs-lookup"><span data-stu-id="5297f-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="5297f-179">Hallo-experiment opslaan, uitvoeren en wacht totdat deze toofinish uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5297f-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="5297f-180">Klik op Hallo uitvoer knooppunt op Hallo [converteren tooCSV] [ convert-to-csv] module.</span><span class="sxs-lookup"><span data-stu-id="5297f-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="5297f-181">Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **toegangscode gegevens genereren**.</span><span class="sxs-lookup"><span data-stu-id="5297f-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Contextmenu][experiment]
8. <span data-ttu-id="5297f-183">Hallo-codefragment Selecteer en kopieer het tooyour Klembord vanuit Hallo-venster dat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5297f-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Toegangscode][intermediate-dataset-access-code]
9. <span data-ttu-id="5297f-185">Hallo-code plakken in uw laptop.</span><span class="sxs-lookup"><span data-stu-id="5297f-185">Paste hello code in your notebook.</span></span>
   
    ![Notebook][ipython-intermediate-dataset]
10. <span data-ttu-id="5297f-187">U kunt Hallo gegevens visualiseren met matplotlib.</span><span class="sxs-lookup"><span data-stu-id="5297f-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="5297f-188">Hiermee wordt in een kolom van de leeftijd Hallo histogram:</span><span class="sxs-lookup"><span data-stu-id="5297f-188">This displays in a histogram for hello age column:</span></span>
    
    ![Histogram][ipython-histogram]

## <span data-ttu-id="5297f-190"><a name="clientApis"></a>Gebruik Hallo Machine Learning Python client bibliotheek tooaccess lezen, maken en beheren van gegevenssets</span><span class="sxs-lookup"><span data-stu-id="5297f-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="5297f-191">Werkruimte</span><span class="sxs-lookup"><span data-stu-id="5297f-191">Workspace</span></span>
<span data-ttu-id="5297f-192">Hallo-werkruimte is Hallo toegangspunt voor Hallo Python-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5297f-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="5297f-193">Hallo bieden `Workspace` klasse met uw werkruimte-id en autorisatie token toocreate een exemplaar:</span><span class="sxs-lookup"><span data-stu-id="5297f-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="5297f-194">Gegevenssets opsommen</span><span class="sxs-lookup"><span data-stu-id="5297f-194">Enumerate datasets</span></span>
<span data-ttu-id="5297f-195">tooenumerate alle gegevenssets in een bepaalde werkruimte:</span><span class="sxs-lookup"><span data-stu-id="5297f-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="5297f-196">tooenumerate alleen Hallo gebruiker gemaakte gegevenssets:</span><span class="sxs-lookup"><span data-stu-id="5297f-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="5297f-197">tooenumerate alleen Hallo voorbeeld gegevenssets:</span><span class="sxs-lookup"><span data-stu-id="5297f-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="5297f-198">U kunt toegang krijgen tot een gegevensset met de naam (dit is hoofdlettergevoelig):</span><span class="sxs-lookup"><span data-stu-id="5297f-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="5297f-199">Of u toegang hebt tot het met de index:</span><span class="sxs-lookup"><span data-stu-id="5297f-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="5297f-200">Metagegevens</span><span class="sxs-lookup"><span data-stu-id="5297f-200">Metadata</span></span>
<span data-ttu-id="5297f-201">Gegevenssets hebben metagegevens, in aanvulling toocontent.</span><span class="sxs-lookup"><span data-stu-id="5297f-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="5297f-202">(Tussenliggende gegevenssets zijn een uitzonderingsregel toothis en hoeft niet alle metagegevens.)</span><span class="sxs-lookup"><span data-stu-id="5297f-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="5297f-203">Sommige metagegevenswaarden worden toegewezen door gebruiker Hallo tijdens het maken:</span><span class="sxs-lookup"><span data-stu-id="5297f-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="5297f-204">Sommige zijn toegewezen door Azure ML waarden:</span><span class="sxs-lookup"><span data-stu-id="5297f-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="5297f-205">Zie Hallo `SourceDataset` klasse voor meer op Hallo beschikbaar metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5297f-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="5297f-206">Inhoud lezen</span><span class="sxs-lookup"><span data-stu-id="5297f-206">Read contents</span></span>
<span data-ttu-id="5297f-207">Hallo codefragmenten geleverd door Machine Learning Studio automatisch downloaden en te deserialiseren Hallo gegevensset tooa Pandas DataFrame object.</span><span class="sxs-lookup"><span data-stu-id="5297f-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="5297f-208">Dit wordt gedaan met Hallo `to_dataframe` methode:</span><span class="sxs-lookup"><span data-stu-id="5297f-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="5297f-209">Als u liever toodownload Hallo onbewerkte gegevens en uitvoeren van Hallo deserialisatie, is dat een optie.</span><span class="sxs-lookup"><span data-stu-id="5297f-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="5297f-210">Momenteel Hallo is dit de enige optie Hallo voor indelingen zoals ARFF, welke Hallo Python-clientbibliotheek kan niet worden gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="5297f-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="5297f-211">tooread hello inhoud als tekst:</span><span class="sxs-lookup"><span data-stu-id="5297f-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="5297f-212">Als binair tooread Hallo-inhoud:</span><span class="sxs-lookup"><span data-stu-id="5297f-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="5297f-213">U kunt ook gewoon een stroom toohello inhoud openen:</span><span class="sxs-lookup"><span data-stu-id="5297f-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="5297f-214">Maak een nieuwe gegevensset</span><span class="sxs-lookup"><span data-stu-id="5297f-214">Create a new dataset</span></span>
<span data-ttu-id="5297f-215">Hallo Python-clientbibliotheek kunt u de gegevenssets tooupload uit een Python-programma.</span><span class="sxs-lookup"><span data-stu-id="5297f-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="5297f-216">Deze gegevenssets zijn vervolgens beschikbaar voor gebruik in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5297f-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="5297f-217">Als u uw gegevens in een DataFrame Pandas hebt, gebruikt u Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="5297f-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="5297f-218">Als u al uw gegevens geserialiseerd, kunt u het volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5297f-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="5297f-219">Hallo Python-clientbibliotheek is kunnen tooserialize een Pandas DataFrame toohello volgende indelingen (constanten voor deze zich in Hallo `azureml.DataTypeIds` klasse):</span><span class="sxs-lookup"><span data-stu-id="5297f-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="5297f-220">Tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="5297f-220">PlainText</span></span>
* <span data-ttu-id="5297f-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="5297f-221">GenericCSV</span></span>
* <span data-ttu-id="5297f-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="5297f-222">GenericTSV</span></span>
* <span data-ttu-id="5297f-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="5297f-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="5297f-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="5297f-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="5297f-225">Bijwerken van een bestaande gegevensset</span><span class="sxs-lookup"><span data-stu-id="5297f-225">Update an existing dataset</span></span>
<span data-ttu-id="5297f-226">Als u een nieuwe gegevensset met een naam die overeenkomt met een bestaande gegevensset tooupload probeert, ontvangt u een conflict opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5297f-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="5297f-227">een bestaande gegevensset tooupdate, moet u eerst een bestaande gegevensset voor verwijzing toohello tooget:</span><span class="sxs-lookup"><span data-stu-id="5297f-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="5297f-228">Gebruik vervolgens `update_from_dataframe` tooserialize en vervang Hallo-inhoud van Hallo gegevensset op Azure:</span><span class="sxs-lookup"><span data-stu-id="5297f-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="5297f-229">Als u tooserialize hello tooa verschillende gegevensindeling wilt, een waarde opgeven voor optionele Hallo `data_type_id` parameter.</span><span class="sxs-lookup"><span data-stu-id="5297f-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="5297f-230">U kunt desgewenst een nieuwe beschrijving instellen door een waarde opgeeft voor Hallo `description` parameter.</span><span class="sxs-lookup"><span data-stu-id="5297f-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="5297f-231">U kunt desgewenst een nieuwe naam instellen door een waarde opgeeft voor Hallo `name` parameter.</span><span class="sxs-lookup"><span data-stu-id="5297f-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="5297f-232">U hebt op, Hallo gegevensset met alleen de nieuwe naam Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="5297f-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="5297f-233">Hallo code na updates Hallo gegevens, naam en beschrijving.</span><span class="sxs-lookup"><span data-stu-id="5297f-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="5297f-234">Hallo `data_type_id`, `name` en `description` parameters zijn optioneel en de standaardinstellingen van de vorige waarde tootheir.</span><span class="sxs-lookup"><span data-stu-id="5297f-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="5297f-235">Hallo `dataframe` parameter is altijd vereist.</span><span class="sxs-lookup"><span data-stu-id="5297f-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="5297f-236">Als u al uw gegevens geserialiseerd, gebruikt u `update_from_raw_data` in plaats van `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="5297f-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="5297f-237">Als u alleen doorgeeft in `raw_data` in plaats van `dataframe`, het op een vergelijkbare manier werkt.</span><span class="sxs-lookup"><span data-stu-id="5297f-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

