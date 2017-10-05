---
title: Zelfstudie - De Azure Batch-SDK voor Python gebruiken | Microsoft Docs
description: Leer de basisconcepten van Azure Batch en bouw een eenvoudige oplossing met behulp van Python.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd5a977c10d3955639beb893cd7a37581b14f7c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-batch-sdk-for-python"></a><span data-ttu-id="7f65c-103">Aan de slag met de Batch-SDK voor Python</span><span class="sxs-lookup"><span data-stu-id="7f65c-103">Get started with the Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f65c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7f65c-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="7f65c-105">Python</span><span class="sxs-lookup"><span data-stu-id="7f65c-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="7f65c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="7f65c-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="7f65c-107">Leer de basisbeginselen van [Azure Batch][azure_batch] en de [Batch Python][py_azure_sdk]-client bij de toelichting van een kleine Batch-toepassing die in Python is geschreven.</span><span class="sxs-lookup"><span data-stu-id="7f65c-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="7f65c-108">U ontdekt hier hoe twee scripts gebruikmaken van de Batch-service om een parallelle workload op virtuele Linux-machines in de cloud te verwerken, en hoe deze scripts met [Azure Storage](../storage/common/storage-introduction.md) communiceren voor het faseren en ophalen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="7f65c-108">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="7f65c-109">U maakt kennis met een gangbare werkstroom voor Batch-toepassingen en krijgt hier ook elementair inzicht in de belangrijkste onderdelen van Batch, zoals jobs, taken, pools en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7f65c-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="7f65c-110">![Werkstroom van de Batch-oplossing (basis)][11]</span><span class="sxs-lookup"><span data-stu-id="7f65c-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="7f65c-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7f65c-111">Prerequisites</span></span>
<span data-ttu-id="7f65c-112">In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van Python en vertrouwd bent met Linux.</span><span class="sxs-lookup"><span data-stu-id="7f65c-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="7f65c-113">Er wordt ook van uitgegaan dat u voldoet aan de vereisten voor het maken van een account die hieronder zijn opgegeven voor Azure en de Batch- en Storage-services.</span><span class="sxs-lookup"><span data-stu-id="7f65c-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="7f65c-114">Accounts</span><span class="sxs-lookup"><span data-stu-id="7f65c-114">Accounts</span></span>
* <span data-ttu-id="7f65c-115">**Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="7f65c-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="7f65c-116">**Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f65c-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="7f65c-117">**Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7f65c-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="7f65c-118">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="7f65c-118">Code sample</span></span>
<span data-ttu-id="7f65c-119">Het Python-[codevoorbeeld][github_article_samples] in de zelfstudie is een van de vele Batch-codevoorbeelden die beschikbaar zijn in de opslagplaats [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f65c-119">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="7f65c-120">U kunt alle voorbeelden downloaden door te klikken op **Clone or download > Download ZIP** (Klonen of downloaden > ZIP downloaden) op de introductiepagina van de opslagplaats of door te klikken op de koppeling van de directe download [azure batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="7f65c-120">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="7f65c-121">Nadat u de inhoud van het ZIP-bestand hebt uitgepakt, vindt u de twee scripts voor deze zelfstudie in de map `article_samples`:</span><span class="sxs-lookup"><span data-stu-id="7f65c-121">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="7f65c-122">Python-omgeving</span><span class="sxs-lookup"><span data-stu-id="7f65c-122">Python environment</span></span>
<span data-ttu-id="7f65c-123">Als u het voorbeeldscript *python_tutorial_client.py* op uw lokale werkstation wilt uitvoeren, hebt u een **Python-interpreter** nodig die compatibel is met versie **2.7** of **3.3+**.</span><span class="sxs-lookup"><span data-stu-id="7f65c-123">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="7f65c-124">Het script is getest op Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="7f65c-124">The script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="7f65c-125">cryptografie-afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="7f65c-125">cryptography dependencies</span></span>
<span data-ttu-id="7f65c-126">U moet de afhankelijkheden voor de [cryptografie][crypto]-bibliotheek installeren die zijn vereist door de `azure-batch`- en `azure-storage`-pakketten voor Python.</span><span class="sxs-lookup"><span data-stu-id="7f65c-126">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="7f65c-127">Voer een van de volgende bewerkingen uit die geschikt is voor uw platform of raadpleeg de [cryptografie-installatie][crypto_install]details voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="7f65c-127">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="7f65c-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7f65c-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="7f65c-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="7f65c-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="7f65c-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="7f65c-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="7f65c-131">Windows</span><span class="sxs-lookup"><span data-stu-id="7f65c-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="7f65c-132">Als u voor Python 3.3+ op Linux installeert, gebruikt u de python3-equivalenten voor de Python-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="7f65c-132">If installing for Python 3.3+ on Linux, use the python3 equivalents for the Python dependencies.</span></span> <span data-ttu-id="7f65c-133">Bijvoorbeeld op Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="7f65c-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="7f65c-134">Azure-pakketten</span><span class="sxs-lookup"><span data-stu-id="7f65c-134">Azure packages</span></span>
<span data-ttu-id="7f65c-135">Installeer daarna de **Azure Batch**- en **Azure Storage**-pakketten voor Python.</span><span class="sxs-lookup"><span data-stu-id="7f65c-135">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="7f65c-136">U kunt beide pakketten installeren met behulp van **pip** en de *requirements.txt* die u hier kunt vinden:</span><span class="sxs-lookup"><span data-stu-id="7f65c-136">You can install both packages by using **pip** and the *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="7f65c-137">Geef de volgende **pip**-opdracht om de Batch- en Storage-pakketten te installeren:</span><span class="sxs-lookup"><span data-stu-id="7f65c-137">Issue following **pip** command to install the Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="7f65c-138">U kunt de [azure batch][pypi_batch]- en [azure-opslag][pypi_storage]-pakketten voor Python ook handmatig installeren:</span><span class="sxs-lookup"><span data-stu-id="7f65c-138">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="7f65c-139">Mogelijk moet u aan uw opdrachten het voorvoegsel `sudo` toevoegen als u een niet-gemachtigd account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-139">If you are using an unprivileged account, you may need to prefix your commands with `sudo`.</span></span> <span data-ttu-id="7f65c-140">Bijvoorbeeld `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="7f65c-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="7f65c-141">Zie [Installing Packages][pypi_install] (Pakketten installeren) op python.org voor meer informatie over het installeren van Python-pakketten.</span><span class="sxs-lookup"><span data-stu-id="7f65c-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="7f65c-142">Batch-zelfstudiecodevoorbeeld voor Python</span><span class="sxs-lookup"><span data-stu-id="7f65c-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="7f65c-143">Het batch-zelfstudiecodevoorbeeld voor Python bestaat uit twee Python-scripts en enkele gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="7f65c-143">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="7f65c-144">**python_tutorial_client.py**: Communiceert met de Batch- en Storage-services voor het uitvoeren van een parallelle workload in rekenknooppunten (virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="7f65c-144">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="7f65c-145">Het script *python_tutorial_client.py* wordt uitgevoerd op uw lokale werkstation.</span><span class="sxs-lookup"><span data-stu-id="7f65c-145">The *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="7f65c-146">**python_tutorial_task.py**: Het script dat wordt uitgevoerd op rekenknooppunten in Azure om het echte werk te verrichten.</span><span class="sxs-lookup"><span data-stu-id="7f65c-146">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="7f65c-147">In het voorbeeld parseert *python_tutorial_task.py* de tekst in een bestand dat is gedownload van Azure Storage (het invoerbestand).</span><span class="sxs-lookup"><span data-stu-id="7f65c-147">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="7f65c-148">Daarna creëert het een tekstbestand (het uitvoerbestand) met daarin een lijst van de eerste drie woorden die het invoerbestand bevat.</span><span class="sxs-lookup"><span data-stu-id="7f65c-148">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="7f65c-149">Nadat het het uitvoerbestand heeft gemaakt, uploadt *python_tutorial_task.py* het bestand naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-149">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span></span> <span data-ttu-id="7f65c-150">Hierdoor kan het worden gedownload naar het clientscript dat op uw werkstation wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-150">This makes it available for download to the client script running on your workstation.</span></span> <span data-ttu-id="7f65c-151">Het script *python_tutorial_task.py* wordt parallel uitgevoerd in meerdere rekenknooppunten in de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="7f65c-151">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span></span>
* <span data-ttu-id="7f65c-152">**./data/taskdata\*.txt**: deze drie tekstbestanden leveren de invoer voor de taken die op de rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-152">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span></span>

<span data-ttu-id="7f65c-153">Het volgende diagram illustreert de primaire bewerkingen die door de client- en taakscripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-153">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span></span> <span data-ttu-id="7f65c-154">Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="7f65c-155">Hoewel het niet elke functie beschikbaar in de Batch-service aantoont, omvat vrijwel elk Batch-scenario delen van deze werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7f65c-155">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="7f65c-156">![Batch-voorbeeldwerkstroom][8]</span><span class="sxs-lookup"><span data-stu-id="7f65c-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="7f65c-157">**Stap 1.**</span><span class="sxs-lookup"><span data-stu-id="7f65c-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="7f65c-158">Maak **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="7f65c-159">
[**Stap 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="7f65c-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="7f65c-160">Upload taakscript- en invoerbestanden naar containers.</span><span class="sxs-lookup"><span data-stu-id="7f65c-160">Upload task script and input files to containers.</span></span><br/><span data-ttu-id="7f65c-161">
[**Stap 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="7f65c-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="7f65c-162">Maak een Batch-**pool**.</span><span class="sxs-lookup"><span data-stu-id="7f65c-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="7f65c-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="7f65c-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="7f65c-164">**StartTask** van de pool downloadt het taakscript (python_tutorial_task.py) naar knooppunten wanneer deze aan de pool worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-164">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span></span><br/><span data-ttu-id="7f65c-165">
[**Stap 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="7f65c-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="7f65c-166">Maak een Batch-**job**.</span><span class="sxs-lookup"><span data-stu-id="7f65c-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="7f65c-167">
[**Stap 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="7f65c-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="7f65c-168">Voeg **taken** toe aan de job.</span><span class="sxs-lookup"><span data-stu-id="7f65c-168">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="7f65c-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="7f65c-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="7f65c-170">De taken worden gepland om op knooppunten te worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-170">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="7f65c-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="7f65c-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="7f65c-172">Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="7f65c-173">
[**Stap 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="7f65c-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="7f65c-174">Controleer taken.</span><span class="sxs-lookup"><span data-stu-id="7f65c-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="7f65c-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="7f65c-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="7f65c-176">Nadat taken zijn voltooid, uploaden zij hun uitvoergegevens naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-176">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="7f65c-177">
[**Stap 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="7f65c-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="7f65c-178">Download taakuitvoer uit Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-178">Download task output from Storage.</span></span>

<span data-ttu-id="7f65c-179">Zoals vermeld voert niet elke Batch-oplossing deze exacte stappen uit en kunnen veel meer stappen nodig zijn, maar deze sjabloon toont gebruikelijke processen gevonden in een Batch-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7f65c-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="7f65c-180">Clientscripts voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7f65c-180">Prepare client script</span></span>
<span data-ttu-id="7f65c-181">Voordat u het voorbeeld uitvoert, voegt u de referenties van uw Batch- en Storage-account toe aan *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="7f65c-181">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span></span> <span data-ttu-id="7f65c-182">Als u dit nog niet hebt gedaan, opent u het bestand in uw favoriete editor en werkt u de volgende regels bij met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="7f65c-182">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span></span>

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="7f65c-183">U vindt uw Batch- en Storage-accountreferenties op de accountblade van elke service in [Azure Portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="7f65c-183">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="7f65c-184">![Batch-referenties in de portal][9]
![Storage-referenties in de portal][10]</span><span class="sxs-lookup"><span data-stu-id="7f65c-184">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="7f65c-185">In de volgende secties analyseren we de stappen die wordt gebruikt door de scripts voor het verwerken van een workload die in de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="7f65c-185">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span></span> <span data-ttu-id="7f65c-186">We raden u aan regelmatig te verwijzen naar de scripts in uw editor wanneer u zich door de rest van het artikel heen werkt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-186">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span></span>

<span data-ttu-id="7f65c-187">Navigeer naar de volgende regel in **python_tutorial_client.py** om bij stap 1 te starten:</span><span class="sxs-lookup"><span data-stu-id="7f65c-187">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="7f65c-188">Stap 1: opslagcontainers maken</span><span class="sxs-lookup"><span data-stu-id="7f65c-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="7f65c-189">![Containers maken in Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="7f65c-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="7f65c-190">Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="7f65c-191">Containers in uw opslagaccount bevatten de bestanden die nodig zijn voor de taken die in uw Batch-account worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-191">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="7f65c-192">De containers bieden ook een plaats voor de opslag van de uitvoergegevens die de taken opleveren.</span><span class="sxs-lookup"><span data-stu-id="7f65c-192">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="7f65c-193">Het eerste wat het script *python_tutorial_client.py* doet, is drie containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage) maken:</span><span class="sxs-lookup"><span data-stu-id="7f65c-193">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="7f65c-194">**application**: deze container slaat het Python-script op dat door de taken wordt uitgevoerd, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="7f65c-194">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="7f65c-195">**input**: taken downloaden de te verwerken gegevensbestanden uit de *invoer*container.</span><span class="sxs-lookup"><span data-stu-id="7f65c-195">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="7f65c-196">**output**: nadat taken de verwerking van invoerbestanden hebben voltooid, uploaden zij de resultaten naar de *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="7f65c-196">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="7f65c-197">Om te communiceren met een opslagaccount en containers te maken, gebruiken we het pakket [azure-storage][pypi_storage] om een [BlockBlobService][py_blockblobservice]-object te maken, de 'blob-client'.</span><span class="sxs-lookup"><span data-stu-id="7f65c-197">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span></span> <span data-ttu-id="7f65c-198">Daarna maken we drie containers in het opslagaccount met behulp van de blob-client.</span><span class="sxs-lookup"><span data-stu-id="7f65c-198">We then create three containers in the Storage account using the blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create the blob client, for use in obtaining references to
# blob storage containers and uploading files to containers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use the blob client to create the containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="7f65c-199">Zodra de containers zijn gemaakt, kan de toepassing nu de bestanden uploaden die door de taken worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="7f65c-200">[How to use Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) (Azure Blob Storage gebruiken met Python) biedt een uitstekend overzicht van hoe u met Azure Storage-containers en -blobs werkt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-200">[How to use Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="7f65c-201">Wanneer u met Batch begint te werken, moet dat artikel hoog in uw leeslijst zijn vermeld.</span><span class="sxs-lookup"><span data-stu-id="7f65c-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="7f65c-202">Stap 2: taakscript- en gegevensbestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="7f65c-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="7f65c-203">![Taaktoepassings- en invoer(gegevens)bestanden uploaden naar containers][2]
</span><span class="sxs-lookup"><span data-stu-id="7f65c-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="7f65c-204">In de bewerking voor het uploaden van bestanden definieert *python_tutorial_client.py* eerst verzamelingen van bestandspaden naar **toepassing**sbestanden en **invoer**bestanden op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7f65c-204">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="7f65c-205">Daarna worden deze bestanden geüpload naar de containers die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```python
# Paths to the task script. This script will be executed by the tasks that
# run on the compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# The collection of data files that are to be processed by the tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload the application script to Azure Storage. This is the script that
# will process the data files, and is executed by each of the tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload the data files. This is the data that will be processed by each of
# the tasks executed on the compute nodes in the pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="7f65c-206">Zoals dat bij lijsten gebruikelijk is, wordt de functie `upload_file_to_container` aangeroepen voor elk bestand in de verzamelingen en worden twee [ResourceFile][py_resource_file]-verzamelingen ingevuld.</span><span class="sxs-lookup"><span data-stu-id="7f65c-206">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="7f65c-207">De functie `upload_file_to_container` wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7f65c-207">The `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} to container [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="7f65c-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="7f65c-208">ResourceFiles</span></span>
<span data-ttu-id="7f65c-209">[ResourceFile][py_resource_file] levert aan taken in Batch de URL naar een bestand in Azure Storage dat naar een rekenknooppunt wordt gedownload voordat deze taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-209">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="7f65c-210">De eigenschap [ResourceFile][py_resource_file].**blob_source** geeft de volledige URL van het bestand zoals dit zich in Azure Storage bevindt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-210">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="7f65c-211">De URL kan ook een Shared Access Signature (SAS) bevatten, die veilige toegang tot het bestand biedt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-211">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="7f65c-212">De meeste typen taken in Batch bevatten een eigenschap *ResourceFiles*, waaronder:</span><span class="sxs-lookup"><span data-stu-id="7f65c-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="7f65c-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="7f65c-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="7f65c-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="7f65c-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="7f65c-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="7f65c-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="7f65c-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="7f65c-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="7f65c-217">In dit voorbeeld worden de taaktypen JobPreparationTask of JobReleaseTask niet gebruikt. Meer informatie hierover vindt u echter in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md) (Jobvoorbereidings- en jobvrijgevingstaken uitvoeren op Azure Batch-rekenknooppunten).</span><span class="sxs-lookup"><span data-stu-id="7f65c-217">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="7f65c-218">Shared Access Signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="7f65c-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="7f65c-219">Shared Access Signatures zijn tekenreeksen die beveiligde toegang bieden tot containers en blobs in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-219">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="7f65c-220">Het script *python_tutorial_client.py* gebruikt Shared Access Signatures voor blobs en containers en laat zien hoe u deze SAS-tekenreeksen uit de Storage-service verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-220">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="7f65c-221">**Shared Access Signatures voor blobs**: StartTask van de pool gebruikt Shared Access Signatures voor blobs wanneer deze het taakscript en de invoergegevensbestanden uit Storage downloadt (zie [Stap 3](#step-3-create-batch-pool) hieronder).</span><span class="sxs-lookup"><span data-stu-id="7f65c-221">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="7f65c-222">De functie `upload_file_to_container` in *python_tutorial_client.py* bevat de code die de Shared Access Signature van elke blob verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-222">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="7f65c-223">Dit gebeurt door het aanroepen van [BlockBlobService.make_blob_url][py_make_blob_url] in de Storage-module.</span><span class="sxs-lookup"><span data-stu-id="7f65c-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span></span>
* <span data-ttu-id="7f65c-224">**Shared Access Signatures voor containers**: Nadat elke taak in het rekenknooppunt zijn werk heeft verricht, uploadt elke taak zijn uitvoerbestand naar de *uitvoer*container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-224">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="7f65c-225">Hiervoor maakt *python_tutorial_task.py* gebruik van een Shared Access Signature voor containers die schrijftoegang tot de container biedt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-225">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span></span> <span data-ttu-id="7f65c-226">De functie `get_container_sas_token` in *python_tutorial_client.py* verkrijgt de Shared Access Signature van de container, die vervolgens als een opdrachtregelargument wordt doorgegeven aan de taken.</span><span class="sxs-lookup"><span data-stu-id="7f65c-226">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span></span> <span data-ttu-id="7f65c-227">In stap 5, [Taken toevoegen aan job](#step-5-add-tasks-to-job), wordt het gebruik van de Shared Access Signature voor containers besproken.</span><span class="sxs-lookup"><span data-stu-id="7f65c-227">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="7f65c-228">Bekijk de tweedelige reeks over Shared Access Signatures [Part 1: Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (Deel 1: inzicht in het Shared Access Signature (SAS)-model) en [Part 2: Create and use a SAS with the Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) (Deel 2: Een Shared Access Signature (SAS) maken en gebruiken met de Blob-service), voor meer informatie over het verstrekken van beveiligde toegang tot gegevens in uw Storage-account.</span><span class="sxs-lookup"><span data-stu-id="7f65c-228">Check out the two-part series on shared access signatures, [Part 1: Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with the Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="7f65c-229">Stap 3: Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="7f65c-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="7f65c-230">![Een Batch-pool maken][3]
</span><span class="sxs-lookup"><span data-stu-id="7f65c-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="7f65c-231">Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7f65c-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="7f65c-232">Nadat het het taakscript en gegevensbestanden naar het Storage-account heeft geüpload, start *python_tutorial_client.py* zijn interactie met de Batch-service met behulp van de Batch Python-module.</span><span class="sxs-lookup"><span data-stu-id="7f65c-232">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span></span> <span data-ttu-id="7f65c-233">Hiervoor wordt een [BatchServiceClient][py_batchserviceclient] gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7f65c-233">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with the Batch
# service in addition to Storage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="7f65c-234">Daarna wordt een pool van rekenknooppunten gemaakt in het Batch-account met een aanroep naar `create_pool`.</span><span class="sxs-lookup"><span data-stu-id="7f65c-234">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="7f65c-235">Wanneer u een pool maakt, definieert u een [PoolAddParameter][py_pooladdparam] die verschillende eigenschappen voor de pool opgeeft:</span><span class="sxs-lookup"><span data-stu-id="7f65c-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span></span>

* <span data-ttu-id="7f65c-236">**Id** van de pool (*id* - vereist)</span><span class="sxs-lookup"><span data-stu-id="7f65c-236">**ID** of the pool (*id* - required)</span></span><p/><span data-ttu-id="7f65c-237">Net als bij de meeste entiteiten in Batch, moet ook uw nieuwe pool een unieke id binnen uw Batch-account hebben.</span><span class="sxs-lookup"><span data-stu-id="7f65c-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="7f65c-238">Uw code zal naar deze pool verwijzen met de bijbehorende id. Hiermee identificeert u ook de pool in Azure [Portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="7f65c-238">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="7f65c-239">**Aantal rekenknooppunten** (*target_dedicated* - vereist)</span><span class="sxs-lookup"><span data-stu-id="7f65c-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="7f65c-240">Hiermee geeft u op hoeveel virtuele machines in de pool moeten worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-240">This property specifies how many VMs should be deployed in the pool.</span></span> <span data-ttu-id="7f65c-241">Houd er rekening mee dat alle Batch-accounts een standaard**quotum** hebben dat het aantal **kernen** (en dus rekenknooppunten) in een Batch-account beperkt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-241">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="7f65c-242">U vindt de standaardquota en instructies over het [verhogen van een quotum](batch-quota-limit.md#increase-a-quota) (zoals het maximum aantal kernen in uw Batch-account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md) (Quota en limieten voor de Azure Batch-service).</span><span class="sxs-lookup"><span data-stu-id="7f65c-242">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="7f65c-243">Rijzen er vragen zoals "Waarom kan mijn pool niet meer dan X knooppunten bevatten?",</span><span class="sxs-lookup"><span data-stu-id="7f65c-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="7f65c-244">dan is dit quotum voor kernen mogelijk de oorzaak.</span><span class="sxs-lookup"><span data-stu-id="7f65c-244">this core quota may be the cause.</span></span>
* <span data-ttu-id="7f65c-245">**Besturingssysteem** voor knooppunten (*virtual_machine_configuration* **of** *cloud_service_configuration* - vereist)</span><span class="sxs-lookup"><span data-stu-id="7f65c-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="7f65c-246">In *python_tutorial_client.py* maken we een pool met Linux-knooppunten met behulp van een [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="7f65c-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="7f65c-247">De `select_latest_verified_vm_image_with_node_agent_sku`-functie in `common.helpers` vereenvoudigt het gebruik van [Azure Virtual Machines Marketplace][vm_marketplace]-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="7f65c-247">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="7f65c-248">Zie [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie over het gebruik van Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="7f65c-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="7f65c-249">**Grootte van rekenknooppunten** (*vm_size* - vereist)</span><span class="sxs-lookup"><span data-stu-id="7f65c-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="7f65c-250">Omdat we Linux-knooppunten opgeven voor onze [VirtualMachineConfiguration][py_vm_config], geven we een VM-grootte op (in dit voorbeeld `STANDARD_A1`) uit [Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f65c-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7f65c-251">Zie opnieuw [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7f65c-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="7f65c-252">**Begintaak** (*start_task* - niet vereist)</span><span class="sxs-lookup"><span data-stu-id="7f65c-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="7f65c-253">Samen met de bovenstaande fysieke knooppunteigenschappen, kunt u ook een [StartTask][py_starttask] voor de pool opgeven (dit is niet vereist).</span><span class="sxs-lookup"><span data-stu-id="7f65c-253">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span></span> <span data-ttu-id="7f65c-254">StartTask wordt in elk knooppunt uitgevoerd wanneer dat knooppunt aan de pool wordt toegevoegd en telkens wanneer dat knooppunt opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="7f65c-254">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="7f65c-255">StartTask is vooral nuttig voor de voorbereiding van rekenknooppunten voor het uitvoeren van taken, zoals het installeren van de toepassingen die door de taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-255">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span></span><p/><span data-ttu-id="7f65c-256">In deze voorbeeldtoepassing kopieert StartTask de bestanden die het van Storage downloadt (die zijn opgegeven met behulp van de eigenschap **resource_files** van de StartTask) uit de StartTask-*werkmap* naar de *gedeelde* map waartoe alle taken die in het knooppunt worden uitgevoerd toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="7f65c-256">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span></span> <span data-ttu-id="7f65c-257">In wezen wordt hierdoor `python_tutorial_task.py` gekopieerd naar de gedeelde map in elk knooppunt wanneer het knooppunt aan de pool wordt toegevoegd, zodat alle taken die in het knooppunt worden uitgevoerd er toegang toe hebben.</span><span class="sxs-lookup"><span data-stu-id="7f65c-257">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

<span data-ttu-id="7f65c-258">Misschien merkt u de aanroep naar de Help-functie `wrap_commands_in_shell` op.</span><span class="sxs-lookup"><span data-stu-id="7f65c-258">You may notice the call to the `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="7f65c-259">Deze functie gebruikt een verzameling afzonderlijke opdrachten en maakt een enkele opdrachtregel die geschikt is voor de opdrachtregeleigenschap van een taak.</span><span class="sxs-lookup"><span data-stu-id="7f65c-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="7f65c-260">Opmerkelijk in het bovenstaande codefragment is ook het gebruik van twee omgevingsvariabelen in de eigenschap **command_line** van de StartTask: `AZ_BATCH_TASK_WORKING_DIR` en `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="7f65c-260">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="7f65c-261">Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek zijn voor Batch.</span><span class="sxs-lookup"><span data-stu-id="7f65c-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="7f65c-262">Elke proces dat door een taak wordt uitgevoerd, heeft toegang tot deze omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-262">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="7f65c-263">Zie de secties **Omgevingsinstellingen voor taken** en **Bestanden en mappen** in [Overzicht van Azure Batch-functies](batch-api-basics.md) voor meer informatie over de omgevingsvariabelen die beschikbaar zijn in rekenknooppunten in een Batch-pool en voor meer informatie over taakwerkmappen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-263">To find out more about the environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in the [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="7f65c-264">Stap 4: Batch-job maken</span><span class="sxs-lookup"><span data-stu-id="7f65c-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="7f65c-265">![Een Batch-job maken][4]</span><span class="sxs-lookup"><span data-stu-id="7f65c-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="7f65c-266">Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7f65c-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="7f65c-267">De taken in een job worden uitgevoerd op de rekenknooppunten van de gekoppelde pool.</span><span class="sxs-lookup"><span data-stu-id="7f65c-267">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="7f65c-268">U kunt een job niet alleen gebruiken om taken in gerelateerde workloads te organiseren en te volgen, maar ook om bepaalde beperkingen op te leggen, zoals de maximale runtime voor de job (en, bij uitbreiding, dus ook voor de taken ervan) en de prioriteit van de job in verhouding tot andere jobs in de Batch-account.</span><span class="sxs-lookup"><span data-stu-id="7f65c-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="7f65c-269">In dit voorbeeld wordt de job echter alleen gekoppeld aan de pool die in stap 3 is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-269">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="7f65c-270">Er worden geen aanvullende eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-270">No additional properties are configured.</span></span>

<span data-ttu-id="7f65c-271">Alle Batch-jobs worden gekoppeld aan een specifieke pool.</span><span class="sxs-lookup"><span data-stu-id="7f65c-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="7f65c-272">Deze koppeling geeft aan op welke knooppunten de taken van de job worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-272">This association indicates which nodes the job's tasks execute on.</span></span> <span data-ttu-id="7f65c-273">U geeft de pool op met behulp van de eigenschap [PoolInformation][py_poolinfo], zoals in het onderstaande codefragment wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="7f65c-273">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="7f65c-274">Nu een job is gemaakt, worden er taken aan toegevoegd die het werk verrichten.</span><span class="sxs-lookup"><span data-stu-id="7f65c-274">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="7f65c-275">Stap 5: taken toevoegen aan job</span><span class="sxs-lookup"><span data-stu-id="7f65c-275">Step 5: Add tasks to job</span></span>
<span data-ttu-id="7f65c-276">![Taken toevoegen aan job][5]</span><span class="sxs-lookup"><span data-stu-id="7f65c-276">![Add tasks to job][5]</span></span><br/><span data-ttu-id="7f65c-277">
*(1) Taken worden toegevoegd aan de job, (2) de taken worden gepland om op knooppunten te worden uitgevoerd en (3) de taken downloaden de te verwerken gegevensbestanden*</span><span class="sxs-lookup"><span data-stu-id="7f65c-277">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="7f65c-278">Batch-**taken** zijn de afzonderlijke werkeenheden die op de rekenknooppunten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-278">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="7f65c-279">Een taak heeft een opdrachtregel en voert de scripts of uitvoerbare bestanden uit die u in die opdrachtregel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="7f65c-279">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="7f65c-280">Om daadwerkelijk werk te verrichten, moeten de taken aan een job worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-280">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="7f65c-281">Elke [CloudTask][py_task] wordt geconfigureerd met een opdrachtregeleigenschap en [ResourceFiles][py_resource_file] (net als bij de StartTask van de pool) die de taak downloadt naar het knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="7f65c-282">In het voorbeeld verwerkt elke taak slechts één bestand.</span><span class="sxs-lookup"><span data-stu-id="7f65c-282">In the sample, each task processes only one file.</span></span> <span data-ttu-id="7f65c-283">Hierdoor bevat de verzameling ResourceFiles één element.</span><span class="sxs-lookup"><span data-stu-id="7f65c-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="7f65c-284">Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `$AZ_BATCH_NODE_SHARED_DIR` of een toepassing uitvoeren die niet op het `PATH` van het knooppunt wordt gevonden, moeten taakopdrachtregels de shell expliciet aanroepen, zoals bij `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="7f65c-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in the node's `PATH`, task command lines must invoke the shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="7f65c-285">Deze vereiste is niet nodig als uw taken een toepassing uitvoeren in het `PATH` van het knooppunt en verwijzen niet naar omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-285">This requirement is unnecessary if your tasks execute an application in the node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="7f65c-286">In de `for`-lus in het bovenstaande codefragment kunt u zien dat de opdrachtregel voor de taak vijf opdrachtregelargumenten bevat die worden doorgegeven aan *python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="7f65c-286">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="7f65c-287">**filepath**: Dit is het lokale pad naar het bestand, zoals zich dit in het knooppunt bevindt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-287">**filepath**: This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="7f65c-288">Toen hiervoor in stap 2 het ResourceFile-object `upload_file_to_container` werd gemaakt, werd de bestandsnaam voor deze eigenschap gebruikt (de parameter `file_path` in de constructor ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="7f65c-288">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span></span> <span data-ttu-id="7f65c-289">Dit geeft aan dat het bestand kan worden gevonden in dezelfde map in het knooppunt als *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="7f65c-289">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="7f65c-290">**numwords**: de bovenste *N* woorden moeten naar het uitvoerbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="7f65c-290">**numwords**: The top *N* words should be written to the output file.</span></span>
3. <span data-ttu-id="7f65c-291">**storageaccount**: de naam van het opslagaccount dat eigenaar is van de container waarnaar de uitvoer van de taak moet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="7f65c-291">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span></span>
4. <span data-ttu-id="7f65c-292">**storagecontainer**: de naam van de Storage-container waarnaar de uitvoerbestanden moeten worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="7f65c-292">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span></span>
5. <span data-ttu-id="7f65c-293">**sastoken**: de Shared Access Signature (SAS) die schrijftoegang biedt tot de **uitvoer**container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-293">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="7f65c-294">Het script *python_tutorial_task.py* gebruikt deze Shared Access Signature wanneer het de BlockBlobService-verwijzing maakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-294">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="7f65c-295">Dit biedt schrijftoegang tot de container zonder dat een toegangssleutel voor het opslagaccount vereist is.</span><span class="sxs-lookup"><span data-stu-id="7f65c-295">This provides write access to the container without requiring an access key for the storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="7f65c-296">Stap 6: taken controleren</span><span class="sxs-lookup"><span data-stu-id="7f65c-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="7f65c-297">![Taken controleren][6]</span><span class="sxs-lookup"><span data-stu-id="7f65c-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="7f65c-298">
*Het script (1) controleert taken op de status Voltooid en (2) de taken uploaden resultaatgegevens naar Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="7f65c-298">
*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="7f65c-299">Wanneer aan een job taken worden toegevoegd, worden deze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten binnen de pool die aan de job is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="7f65c-299">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="7f65c-300">Op basis van de instellingen die u opgeeft, zal Batch voor u alle taken in de wachtrij plaatsen, plannen en opnieuw proberen uit te voeren, evenals andere taakbeheerverrichtingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7f65c-300">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="7f65c-301">Er zijn veel manieren om de uitvoering van taken te controleren.</span><span class="sxs-lookup"><span data-stu-id="7f65c-301">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="7f65c-302">De functie `wait_for_tasks_to_complete` in *python_tutorial_client.py* biedt een eenvoudig voorbeeld van de controle van taken op een bepaalde status, in dit geval de status [completed][py_taskstate] (voltooid).</span><span class="sxs-lookup"><span data-stu-id="7f65c-302">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="7f65c-303">Stap 7: taakuitvoer downloaden</span><span class="sxs-lookup"><span data-stu-id="7f65c-303">Step 7: Download task output</span></span>
<span data-ttu-id="7f65c-304">![Taakuitvoer downloaden uit Storage][7]</span><span class="sxs-lookup"><span data-stu-id="7f65c-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="7f65c-305">Nu de taak is voltooid, kan de uitvoer van de taken worden gedownload uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f65c-305">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="7f65c-306">Dat gebeurt met een aanroep naar `download_blobs_from_container` in *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="7f65c-306">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="7f65c-307">De aanroep naar `download_blobs_from_container` in *python_tutorial_client.py* geeft aan dat de bestanden naar de basismap moeten worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="7f65c-307">The call to `download_blobs_from_container` in *python_tutorial_client.py* specifies that the files should be downloaded to your home directory.</span></span> <span data-ttu-id="7f65c-308">U kunt eventueel deze uitvoerlocatie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-308">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="7f65c-309">Stap 8: containers verwijderen</span><span class="sxs-lookup"><span data-stu-id="7f65c-309">Step 8: Delete containers</span></span>
<span data-ttu-id="7f65c-310">Omdat gegevens die zich in Azure Storage bevinden, in rekening worden gebracht, doet u er altijd goed aan alle blobs te verwijderen die niet langer nodig zijn voor uw Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="7f65c-310">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="7f65c-311">In *python_tutorial_client.py* wordt dit gedaan met drie aanroepen naar [BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="7f65c-311">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="7f65c-312">Stap 9: de job en de pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="7f65c-312">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="7f65c-313">In de laatste stap wordt u gevraagd de job en de pool te verwijderen die door het script *python_tutorial_client.py* zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-313">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span></span> <span data-ttu-id="7f65c-314">Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="7f65c-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="7f65c-315">Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="7f65c-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="7f65c-316">Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.</span><span class="sxs-lookup"><span data-stu-id="7f65c-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="7f65c-317">[JobOperations][py_job] en [PoolOperations][py_pool] van BatchServiceClient hebben beide overeenkomstige verwijderingsmethoden, die worden aangeroepen wanneer u de verwijdering bevestigt:</span><span class="sxs-lookup"><span data-stu-id="7f65c-317">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="7f65c-318">Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum.</span><span class="sxs-lookup"><span data-stu-id="7f65c-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="7f65c-319">Denk er ook aan dat een pool alle rekenknooppunten in die pool verwijdert en dat alle gegevens in de knooppunten onherstelbaar zijn nadat de pool wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-sample-script"></a><span data-ttu-id="7f65c-320">Het voorbeeldscript uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7f65c-320">Run the sample script</span></span>
<span data-ttu-id="7f65c-321">Bij het uitvoeren van het *python_tutorial_client.py*-script uit de zelfstudie [voorbeeldcode][github_article_samples], lijkt de output van de console op het volgende.</span><span class="sxs-lookup"><span data-stu-id="7f65c-321">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span></span> <span data-ttu-id="7f65c-322">Bij `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` wordt gewacht wanneer de rekenknooppunten van de pool worden gemaakt en opgestart, en wanneer de opdrachten in de begintaak van de pool worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f65c-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span></span> <span data-ttu-id="7f65c-323">Gebruik [Azure Portal][azure_portal] om uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering te controleren.</span><span class="sxs-lookup"><span data-stu-id="7f65c-323">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="7f65c-324">Gebruik [Azure Portal][azure_portal] of [Microsoft Azure Storage Explorer][storage_explorer] om de Storage-resources (containers en blobs) weer te geven die door de toepassing zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f65c-324">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

> [!TIP]
> <span data-ttu-id="7f65c-325">Voer het *python_tutorial_client.py*-script uit vanuit de `azure-batch-samples/Python/Batch/article_samples`-directory.</span><span class="sxs-lookup"><span data-stu-id="7f65c-325">Run the *python_tutorial_client.py* script from within the `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="7f65c-326">Hierbij wordt een relatief pad voor de import van de `common.helpers`-module gebruikt, dus u kunt `ImportError: No module named 'common'` tegenkomen als u het script niet uitvoert in deze directory.</span><span class="sxs-lookup"><span data-stu-id="7f65c-326">It uses a relative path for the `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run the script from within this directory.</span></span>
>
>

<span data-ttu-id="7f65c-327">Wanneer u het voorbeeld uitvoert in de standaardconfiguratie, bedraagt de uitvoeringstijd doorgaans **ongeveer 5-7 minuten**.</span><span class="sxs-lookup"><span data-stu-id="7f65c-327">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="7f65c-328">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f65c-328">Next steps</span></span>
<span data-ttu-id="7f65c-329">Breng gerust wijzigingen aan in *python_tutorial_client.py* en *python_tutorial_task.py* om met verschillende rekenscenario's te experimenteren.</span><span class="sxs-lookup"><span data-stu-id="7f65c-329">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span></span> <span data-ttu-id="7f65c-330">Probeer bijvoorbeeld een uitvoeringsvertraging toe te voegen aan *python_tutorial_task.py* om langlopende taken te simuleren en ze te controleren in de portal.</span><span class="sxs-lookup"><span data-stu-id="7f65c-330">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="7f65c-331">Probeer meer taken toe te voegen of het aantal rekenknooppunten aan te passen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-331">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="7f65c-332">Voeg logica toe om te controleren op een bestaande pool en het gebruik ervan toe te staan om de uitvoeringssnelheid te verhogen.</span><span class="sxs-lookup"><span data-stu-id="7f65c-332">Add logic to check for and allow the use of an existing pool to speed execution time.</span></span>

<span data-ttu-id="7f65c-333">Nu u vertrouwd bent met de basiswerkstroom van een Batch-oplossing, is het tijd om kennis te maken met de aanvullende functies van de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="7f65c-333">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="7f65c-334">Lees het artikel [Overzicht van Azure Batch-functies](batch-api-basics.md). Dit is raadzaam als u niet vertrouwd bent met de service.</span><span class="sxs-lookup"><span data-stu-id="7f65c-334">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="7f65c-335">Lees ook de andere artikelen over Batch-ontwikkeling die vermeld zijn onder **Ontwikkeling nader bekeken** in het [Batch-leertraject][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="7f65c-335">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="7f65c-336">Bekijk een andere implementatie van de verwerking van de workload 'eerste N woorden' met behulp van Batch in het voorbeeld [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="7f65c-336">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Containers maken in Azure Storage"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Taaktoepassings- en invoer(gegevens)bestanden uploaden naar containers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Batch-pool maken"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Batch-job maken"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Taken toevoegen aan job"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Taken controleren"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Taakuitvoer downloaden uit Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Werkstroom van de Batch-oplossing (volledige diagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Batch-referenties in Portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Storage-referenties in Portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Werkstroom van de Batch-oplossing (minimaal diagram)"
