---
title: aaaTutorial - gebruik hello Azure Batch-SDK voor Python | Microsoft Docs
description: Leer de basisconcepten Hallo van Azure Batch en bouwen van een eenvoudige oplossing met behulp van Python.
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
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="40924-103">Aan de slag met Hallo Batch-SDK voor Python</span><span class="sxs-lookup"><span data-stu-id="40924-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="40924-104">.NET</span><span class="sxs-lookup"><span data-stu-id="40924-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="40924-105">Python</span><span class="sxs-lookup"><span data-stu-id="40924-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="40924-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="40924-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="40924-107">Leer de basisbeginselen Hallo van [Azure Batch] [ azure_batch] en Hallo [Batch Python] [ py_azure_sdk] client zoals we een kleine Batch-toepassing geschreven in Python bespreken.</span><span class="sxs-lookup"><span data-stu-id="40924-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="40924-108">We kijken hoe twee scripts gebruik Hallo Batch-service tooprocess een parallelle workload op virtuele Linux-machines in de cloud Hallo steekproeven en hoe ze communiceren met [Azure Storage](../storage/common/storage-introduction.md) voor Faseren en ophalen.</span><span class="sxs-lookup"><span data-stu-id="40924-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="40924-109">U hebt meer informatie over een algemene werkstroom voor Batch-toepassing en een elementair inzicht in Hallo belangrijkste onderdelen van Batch zoals jobs, taken, pools en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="40924-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="40924-110">![Werkstroom van de Batch-oplossing (basis)][11]</span><span class="sxs-lookup"><span data-stu-id="40924-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="40924-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="40924-111">Prerequisites</span></span>
<span data-ttu-id="40924-112">In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van Python en vertrouwd bent met Linux.</span><span class="sxs-lookup"><span data-stu-id="40924-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="40924-113">Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor de Azure- en hello Batch- en opslagservices.</span><span class="sxs-lookup"><span data-stu-id="40924-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="40924-114">Accounts</span><span class="sxs-lookup"><span data-stu-id="40924-114">Accounts</span></span>
* <span data-ttu-id="40924-115">**Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="40924-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="40924-116">**Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="40924-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="40924-117">**Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="40924-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="40924-118">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="40924-118">Code sample</span></span>
<span data-ttu-id="40924-119">Hallo Python zelfstudie [codevoorbeeld] [ github_article_samples] is een van de vele Batch-codevoorbeelden in Hallo gevonden Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="40924-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="40924-120">U kunt alle Hallo voorbeelden downloaden door te klikken op **klonen of downloaden > ZIP downloaden** op de startpagina Hallo-opslagplaats of door te klikken op Hallo [azure-batch-samples-master.zip] [ github_samples_zip]directe downloadkoppeling.</span><span class="sxs-lookup"><span data-stu-id="40924-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="40924-121">Nadat u de inhoud van het ZIP-bestand Hallo Hallo hebt uitgepakt, Hallo twee scripts voor deze zelfstudie vindt u in Hallo `article_samples` directory:</span><span class="sxs-lookup"><span data-stu-id="40924-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="40924-122">Python-omgeving</span><span class="sxs-lookup"><span data-stu-id="40924-122">Python environment</span></span>
<span data-ttu-id="40924-123">Hallo toorun *python_tutorial_client.py* voorbeeldscript op uw lokale werkstation, moet u een **Python-interpreter** compatibel is met versie **2.7** of **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="40924-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="40924-124">Hallo-script is getest op Linux- en Windows.</span><span class="sxs-lookup"><span data-stu-id="40924-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="40924-125">cryptografie-afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="40924-125">cryptography dependencies</span></span>
<span data-ttu-id="40924-126">Moet u afhankelijkheden voor Hallo Hallo installeren [cryptografie] [ crypto] bibliotheek, die vereist is door Hallo `azure-batch` en `azure-storage` Python-pakketten.</span><span class="sxs-lookup"><span data-stu-id="40924-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="40924-127">Voer een van de Hallo bewerkingen die geschikt is voor uw platform te volgen of Raadpleeg de toohello [cryptografie installatie] [ crypto_install] details voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="40924-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="40924-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="40924-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="40924-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="40924-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="40924-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="40924-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="40924-131">Windows</span><span class="sxs-lookup"><span data-stu-id="40924-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="40924-132">Als voor Python 3.3 + op Linux installeren, gebruikt u Hallo python3 equivalenten voor Hallo Python afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="40924-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="40924-133">Bijvoorbeeld op Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="40924-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="40924-134">Azure-pakketten</span><span class="sxs-lookup"><span data-stu-id="40924-134">Azure packages</span></span>
<span data-ttu-id="40924-135">Vervolgens installeert Hallo **Azure Batch** en **Azure Storage** Python-pakketten.</span><span class="sxs-lookup"><span data-stu-id="40924-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="40924-136">U kunt beide pakketten installeren met behulp van **pip** en Hallo *requirements.txt* hier vinden:</span><span class="sxs-lookup"><span data-stu-id="40924-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="40924-137">Geef de volgende **pip** opdracht tooinstall Hallo Batch- en Storage-pakketten:</span><span class="sxs-lookup"><span data-stu-id="40924-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="40924-138">Of u kunt installeren Hallo [azure batch] [ pypi_batch] en [azure-opslag] [ pypi_storage] pakketten voor Python handmatig:</span><span class="sxs-lookup"><span data-stu-id="40924-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="40924-139">Als u een niet-gemachtigd account gebruikt, moet u mogelijk tooprefix uw opdrachten `sudo`.</span><span class="sxs-lookup"><span data-stu-id="40924-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="40924-140">Bijvoorbeeld `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="40924-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="40924-141">Zie [Installing Packages][pypi_install] (Pakketten installeren) op python.org voor meer informatie over het installeren van Python-pakketten.</span><span class="sxs-lookup"><span data-stu-id="40924-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="40924-142">Batch-zelfstudiecodevoorbeeld voor Python</span><span class="sxs-lookup"><span data-stu-id="40924-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="40924-143">Hallo Batch zelfstudiecodevoorbeeld bestaat uit twee Python-scripts en enkele gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="40924-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="40924-144">**python_tutorial_client.PY**: communiceert met de Hallo Batch- en Storage services tooexecute een parallelle workload op rekenknooppunten (virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="40924-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="40924-145">Hallo *python_tutorial_client.py* script wordt uitgevoerd op uw lokale werkstation.</span><span class="sxs-lookup"><span data-stu-id="40924-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="40924-146">**python_tutorial_task.PY**: Hallo-script dat wordt uitgevoerd op rekenknooppunten in Azure tooperform Hallo echte werk.</span><span class="sxs-lookup"><span data-stu-id="40924-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="40924-147">In voorbeeld Hallo *python_tutorial_task.py* parseert Hallo tekst in een bestand gedownload van Azure Storage (Hallo-invoerbestand).</span><span class="sxs-lookup"><span data-stu-id="40924-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="40924-148">En vervolgens het genereert een tekstbestand (Hallo uitvoerbestand) die een lijst van Hallo eerste drie woorden die worden weergegeven in het invoerbestand Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="40924-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="40924-149">Na het maken van het uitvoerbestand hello, *python_tutorial_task.py* uploads Hallo bestand tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="40924-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="40924-150">Dit maakt het beschikbaar voor download toohello clientscript dat wordt uitgevoerd op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="40924-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="40924-151">Hallo *python_tutorial_task.py* script wordt parallel uitgevoerd in meerdere rekenknooppunten in Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="40924-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="40924-152">**./Data/taskdata\*.txt**: deze drie tekstbestanden leveren Hallo invoer voor Hallo-taken die worden uitgevoerd op Hallo van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="40924-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="40924-153">Hallo volgende diagram illustreert Hallo primaire bewerkingen die worden uitgevoerd door de client- en scripts Hallo.</span><span class="sxs-lookup"><span data-stu-id="40924-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="40924-154">Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="40924-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="40924-155">Hoewel hierin niet elke beschikbare functie in Hallo Batch-service, omvat vrijwel elk Batch-scenario gedeelten van deze werkstroom.</span><span class="sxs-lookup"><span data-stu-id="40924-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="40924-156">![Batch-voorbeeldwerkstroom][8]</span><span class="sxs-lookup"><span data-stu-id="40924-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="40924-157">**Stap 1.**</span><span class="sxs-lookup"><span data-stu-id="40924-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="40924-158">Maak **containers** in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="40924-159">
[**Stap 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="40924-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="40924-160">Taak script en invoer bestanden toocontainers uploaden.</span><span class="sxs-lookup"><span data-stu-id="40924-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="40924-161">
[**Stap 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="40924-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="40924-162">Maak een Batch-**pool**.</span><span class="sxs-lookup"><span data-stu-id="40924-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="40924-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="40924-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="40924-164">Hallo groep **StartTask** downloads Hallo taak script (python_tutorial_task.py) toonodes wanneer ze aan Hallo groep worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="40924-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="40924-165">
[**Stap 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="40924-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="40924-166">Maak een Batch-**job**.</span><span class="sxs-lookup"><span data-stu-id="40924-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="40924-167">
[**Stap 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="40924-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="40924-168">Voeg **taken** toohello taak.</span><span class="sxs-lookup"><span data-stu-id="40924-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="40924-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="40924-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="40924-170">Hallo-taken zijn gepland tooexecute op knooppunten.</span><span class="sxs-lookup"><span data-stu-id="40924-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="40924-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="40924-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="40924-172">Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40924-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="40924-173">
[**Stap 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="40924-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="40924-174">Controleer taken.</span><span class="sxs-lookup"><span data-stu-id="40924-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="40924-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="40924-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="40924-176">Nadat taken zijn voltooid, uploaden zij hun uitvoer gegevens tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="40924-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="40924-177">
[**Stap 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="40924-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="40924-178">Download taakuitvoer uit Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-178">Download task output from Storage.</span></span>

<span data-ttu-id="40924-179">Zoals vermeld voert niet elke Batch-oplossing deze exacte stappen uit en kunnen veel meer stappen nodig zijn, maar deze sjabloon toont gebruikelijke processen gevonden in een Batch-oplossing.</span><span class="sxs-lookup"><span data-stu-id="40924-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="40924-180">Clientscripts voorbereiden</span><span class="sxs-lookup"><span data-stu-id="40924-180">Prepare client script</span></span>
<span data-ttu-id="40924-181">Voordat u Hallo voorbeeld uitvoert, toevoegen u de referenties van uw Batch- en Storage-account te*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="40924-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="40924-182">Als u dit nog niet hebt gedaan, opent u Hallo-bestand in uw favoriete editor en update Hallo volgende regels met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="40924-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="40924-183">U vindt uw Batch- en Storage-accountreferenties op Hallo accountblade van elke service op Hallo [Azure-portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="40924-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="40924-184">![Batch-referenties in portal Hallo][9]
![Storage-referenties in portal Hallo][10]</span><span class="sxs-lookup"><span data-stu-id="40924-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="40924-185">Hallo uit te voeren, analyseren we Hallo stappen die worden gebruikt door Hallo scripts tooprocess een workload in Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="40924-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="40924-186">We raden u toorefer regelmatig toohello scripts in uw editor wanneer u zich door de rest van het artikel Hallo Hallo werken.</span><span class="sxs-lookup"><span data-stu-id="40924-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="40924-187">Navigeer toohello volgende regel in **python_tutorial_client.py** toostart bij stap 1:</span><span class="sxs-lookup"><span data-stu-id="40924-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="40924-188">Stap 1: opslagcontainers maken</span><span class="sxs-lookup"><span data-stu-id="40924-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="40924-189">![Containers maken in Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="40924-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="40924-190">Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="40924-191">Containers in uw opslagaccount biedt Hallo-bestanden die nodig zijn door Hallo-taken die worden uitgevoerd in uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="40924-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="40924-192">Hallo containers bieden ook een uitvoergegevens van plaats toostore Hallo die Hallo taken opleveren.</span><span class="sxs-lookup"><span data-stu-id="40924-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="40924-193">Hallo eerst te beginnen Hallo *python_tutorial_client.py* script doet is drie containers maken in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="40924-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="40924-194">**toepassing**: deze container slaat Hallo pythonscript uitvoeren door Hallo-taken *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="40924-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="40924-195">**invoer**: taken downloaden de Hallo gegevens bestanden tooprocess vanaf Hallo *invoer* container.</span><span class="sxs-lookup"><span data-stu-id="40924-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="40924-196">**uitvoer**: bij de verwerking van invoerbestanden taken hebt voltooid, uploaden zij Hallo resultaten toohello *uitvoer* container.</span><span class="sxs-lookup"><span data-stu-id="40924-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="40924-197">In de volgorde toointeract met een Storage-account in en containers, maken we hello gebruiken [azure-opslag] [ pypi_storage] toocreate van het pakket een [BlockBlobService] [ py_blockblobservice] object--Hallo 'blob-client'.</span><span class="sxs-lookup"><span data-stu-id="40924-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="40924-198">Vervolgens maken we drie containers in Hallo Hallo blob-client met Storage-account.</span><span class="sxs-lookup"><span data-stu-id="40924-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="40924-199">Zodra het Hallo-containers zijn gemaakt, Hallo toepassing kan nu Hallo bestanden uploaden die wordt gebruikt door Hallo taken.</span><span class="sxs-lookup"><span data-stu-id="40924-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="40924-200">[Hoe Azure Blob storage met Python toouse](../storage/blobs/storage-python-how-to-use-blob-storage.md) biedt een goed overzicht van het werken met Azure Storage-containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="40924-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="40924-201">Deze moet aan de bovenkant Hallo van uw leeslijst als u met Batch begint te werken.</span><span class="sxs-lookup"><span data-stu-id="40924-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="40924-202">Stap 2: taakscript- en gegevensbestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="40924-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="40924-203">![Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="40924-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="40924-204">In Hallo uploaden bewerking *python_tutorial_client.py* definieert eerst verzamelingen van **toepassing** en **invoer** bestandspaden die op de lokale machine Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="40924-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="40924-205">Vervolgens wordt deze bestanden toohello containers die u hebt gemaakt in de vorige stap Hallo geüpload.</span><span class="sxs-lookup"><span data-stu-id="40924-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="40924-206">Met behulp begrip van de lijst, Hallo `upload_file_to_container` functie wordt aangeroepen voor elk bestand in Hallo verzamelingen en de twee [ResourceFile] [ py_resource_file] verzamelingen ingevuld.</span><span class="sxs-lookup"><span data-stu-id="40924-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="40924-207">Hallo `upload_file_to_container` functie wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="40924-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
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

### <a name="resourcefiles"></a><span data-ttu-id="40924-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="40924-208">ResourceFiles</span></span>
<span data-ttu-id="40924-209">Een [ResourceFile] [ py_resource_file] biedt taken in Batch met Hallo URL tooa bestand in Azure Storage dat is gedownload tooa rekenknooppunt voordat deze taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40924-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="40924-210">Hallo [ResourceFile][py_resource_file]. **blob_source** eigenschap geeft u de volledige URL Hallo van Hallo-bestand zoals dit zich in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="40924-211">Hallo-URL kan ook een shared access signature (SAS) waarmee u veilige toegang tot toohello bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="40924-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="40924-212">De meeste typen taken in Batch bevatten een eigenschap *ResourceFiles*, waaronder:</span><span class="sxs-lookup"><span data-stu-id="40924-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="40924-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="40924-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="40924-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="40924-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="40924-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="40924-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="40924-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="40924-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="40924-217">Dit voorbeeld gebruikt geen Hallo JobPreparationTask of JobReleaseTask taaktypen, maar kunt u meer informatie over deze in [uitvoeren jobvoorbereidingstaken en jobvrijgevingstaken taken op Azure Batch-rekenknooppunten](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="40924-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="40924-218">Shared Access Signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="40924-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="40924-219">Shared access signatures zijn tekenreeksen die beveiligde toegang toocontainers en blobs in Azure Storage bieden.</span><span class="sxs-lookup"><span data-stu-id="40924-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="40924-220">Hallo *python_tutorial_client.py* script maakt gebruik van blobs en container gedeelde handtekeningen voor toegang en laat zien hoe deze gedeelde tooobtain vanaf toegang tot tekenreeksen Hallo Storage-service.</span><span class="sxs-lookup"><span data-stu-id="40924-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="40924-221">**Shared access signatures voor blobs**: maakt gebruik van Hallo pool-StartTask gedeelde access signatures voor blobs wanneer het Hallo-taak en de invoergegevensbestanden gegevensbestanden uit Storage downloadt (Zie [stap 3](#step-3-create-batch-pool) hieronder).</span><span class="sxs-lookup"><span data-stu-id="40924-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="40924-222">Hallo `upload_file_to_container` werken in *python_tutorial_client.py* bevat Hallo-code die shared access signature van elke blob verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="40924-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="40924-223">Dit gebeurt door het aanroepen van [BlockBlobService.make_blob_url] [ py_make_blob_url] in Hallo Storage-module.</span><span class="sxs-lookup"><span data-stu-id="40924-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="40924-224">**Shared access signature voor containers**: als elke taak zijn werk heeft verricht op Hallo rekenknooppunt, uploadt het bestand uitvoer toohello *uitvoer* container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="40924-225">toodo, *python_tutorial_task.py* maakt gebruik van een shared access signature voor containers die schrijftoegang toohello container biedt.</span><span class="sxs-lookup"><span data-stu-id="40924-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="40924-226">Hallo `get_container_sas_token` werken in *python_tutorial_client.py* Hallo-container shared access signature, die vervolgens wordt doorgegeven als een opdrachtregelargument toohello taken verkrijgt.</span><span class="sxs-lookup"><span data-stu-id="40924-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="40924-227">Stap &#5; [toevoegen taken tooa taak](#step-5-add-tasks-to-job), Hallo informatie over het gebruik van Hallo container SAS besproken.</span><span class="sxs-lookup"><span data-stu-id="40924-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="40924-228">Uitchecken Hallo tweedelige reeks over handtekeningen voor gedeelde toegang [deel 1: Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) en [deel 2: maken en gebruiken van een SAS met Hallo Blob-service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn meer informatie over veilige toegang bieden toodata in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="40924-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="40924-229">Stap 3: Batch-pool maken</span><span class="sxs-lookup"><span data-stu-id="40924-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="40924-230">![Een Batch-pool maken][3]
</span><span class="sxs-lookup"><span data-stu-id="40924-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="40924-231">Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.</span><span class="sxs-lookup"><span data-stu-id="40924-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="40924-232">Nadat het Hallo taak script en gegevens bestanden toohello Storage-account, uploadt *python_tutorial_client.py* start het zijn interactie met Hallo Batch-service met behulp van Hallo Batch Python-module.</span><span class="sxs-lookup"><span data-stu-id="40924-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="40924-233">toodo, een [BatchServiceClient] [ py_batchserviceclient] wordt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="40924-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="40924-234">Daarna wordt een pool van rekenknooppunten gemaakt in de Batch-account met een aanroep van hello te`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="40924-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
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

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
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

<span data-ttu-id="40924-235">Wanneer u een groep maakt, definieert u een [PoolAddParameter] [ py_pooladdparam] Hiermee worden verschillende eigenschappen voor Hallo van toepassingen:</span><span class="sxs-lookup"><span data-stu-id="40924-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="40924-236">**ID** van Hallo van toepassingen (*id* - vereist)</span><span class="sxs-lookup"><span data-stu-id="40924-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="40924-237">Net als bij de meeste entiteiten in Batch, moet ook uw nieuwe pool een unieke id binnen uw Batch-account hebben.</span><span class="sxs-lookup"><span data-stu-id="40924-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="40924-238">Uw code verwijst toothis groep met de bijbehorende ID, en is identificeert u Hallo van toepassingen in hello Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="40924-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="40924-239">**Aantal rekenknooppunten** (*target_dedicated* - vereist)</span><span class="sxs-lookup"><span data-stu-id="40924-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="40924-240">Deze eigenschap specificeert hoeveel virtuele machines moeten worden geïmplementeerd in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="40924-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="40924-241">Het is belangrijk toonote dat alle Batch-accounts standaard hebben **quotum** dat limieten aantal Hallo **kernen** (en dus rekenknooppunten) in een Batch-account.</span><span class="sxs-lookup"><span data-stu-id="40924-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="40924-242">U vindt Hallo standaardquota en instructies over het te[een quotum verhogen](batch-quota-limit.md#increase-a-quota) (zoals Hallo maximum aantal kernen in uw Batch-account) in [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="40924-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="40924-243">Rijzen er vragen zoals "Waarom kan mijn pool niet meer dan X knooppunten bevatten?",</span><span class="sxs-lookup"><span data-stu-id="40924-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="40924-244">Dit quotum voor kernen mogelijk Hallo oorzaak.</span><span class="sxs-lookup"><span data-stu-id="40924-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="40924-245">**Besturingssysteem** voor knooppunten (*virtual_machine_configuration* **of** *cloud_service_configuration* - vereist)</span><span class="sxs-lookup"><span data-stu-id="40924-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="40924-246">In *python_tutorial_client.py* maken we een pool met Linux-knooppunten met behulp van een [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="40924-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="40924-247">Hallo `select_latest_verified_vm_image_with_node_agent_sku` werken in `common.helpers` vereenvoudigt het werken met [Azure Virtual Machines Marketplace] [ vm_marketplace] installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="40924-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="40924-248">Zie [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie over het gebruik van Marketplace-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="40924-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="40924-249">**Grootte van rekenknooppunten** (*vm_size* - vereist)</span><span class="sxs-lookup"><span data-stu-id="40924-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="40924-250">Omdat we Linux-knooppunten opgeven voor onze [VirtualMachineConfiguration][py_vm_config], geven we een VM-grootte op (in dit voorbeeld `STANDARD_A1`) uit [Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40924-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40924-251">Zie opnieuw [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="40924-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="40924-252">**Begintaak** (*start_task* - niet vereist)</span><span class="sxs-lookup"><span data-stu-id="40924-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="40924-253">Samen met de Hallo bovenstaande fysieke knooppunteigenschappen, kunt u ook opgeven een [StartTask] [ py_starttask] voor Hallo van toepassingen (dit is niet vereist).</span><span class="sxs-lookup"><span data-stu-id="40924-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="40924-254">Hallo StartTask wordt uitgevoerd op elk knooppunt, zoals u dat knooppunt aan Hallo-pool wordt toegevoegd en telkens wanneer een knooppunt opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="40924-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="40924-255">Hallo StartTask is vooral nuttig voor het voorbereiden van rekenknooppunten voor Hallo uitvoering van taken, zoals het installeren van Hallo-toepassingen die de taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40924-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="40924-256">In deze voorbeeldtoepassing kopieert StartTask Hallo Hallo-bestanden die het van Storage downloadt (die zijn opgegeven met behulp van de StartTask hello **resource_files** eigenschap) van Hallo StartTask *werkmap* toohello *gedeelde* map waartoe alle taken die worden uitgevoerd op Hallo-knooppunt toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="40924-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="40924-257">In wezen Hiermee kopieert u `python_tutorial_task.py` toohello gedeelde map op elk knooppunt zoals Hallo knooppunt lid van groep hello, zodat alle taken die worden uitgevoerd op Hallo-knooppunt toegang kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="40924-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="40924-258">U merkt Hallo aanroep toohello `wrap_commands_in_shell` Help-functie.</span><span class="sxs-lookup"><span data-stu-id="40924-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="40924-259">Deze functie gebruikt een verzameling afzonderlijke opdrachten en maakt een enkele opdrachtregel die geschikt is voor de opdrachtregeleigenschap van een taak.</span><span class="sxs-lookup"><span data-stu-id="40924-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="40924-260">Opmerkelijk in bovenstaande Hallo codefragment is ook gebruik van twee omgevingsvariabelen in Hallo Hallo **command_line** eigenschap Hallo StartTask: `AZ_BATCH_TASK_WORKING_DIR` en `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="40924-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="40924-261">Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek tooBatch zijn.</span><span class="sxs-lookup"><span data-stu-id="40924-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="40924-262">Een proces dat wordt uitgevoerd door een taak heeft toegang tot toothese omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="40924-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="40924-263">Zie toofind voor meer informatie over Hallo omgevingsvariabelen die beschikbaar op rekenknooppunten in een Batch-pool, evenals informatie over taakwerkmappen zijn **omgevingsinstellingen voor taken** en **bestanden en mappen**  in Hallo [overzicht van Azure Batch-functies](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="40924-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="40924-264">Stap 4: Batch-job maken</span><span class="sxs-lookup"><span data-stu-id="40924-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="40924-265">![Een Batch-job maken][4]</span><span class="sxs-lookup"><span data-stu-id="40924-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="40924-266">Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="40924-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="40924-267">Hallo-taken in een taak uitgevoerd op de rekenknooppunten van de pool Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="40924-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="40924-268">U kunt een job niet alleen voor het organiseren en te volgen taken in gerelateerde workloads, maar ook voor de toepassing van bepaalde beperkingen--zoals Hallo maximale runtime voor Hallo job (en bij uitbreiding, de taken ervan) en de prioriteit van de job in relatie tooother taken in Batch-account Hallo.</span><span class="sxs-lookup"><span data-stu-id="40924-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="40924-269">In dit voorbeeld is Hallo-taak echter alleen gekoppeld aan Hallo-groep die is gemaakt in stap #3.</span><span class="sxs-lookup"><span data-stu-id="40924-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="40924-270">Er worden geen aanvullende eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="40924-270">No additional properties are configured.</span></span>

<span data-ttu-id="40924-271">Alle Batch-jobs worden gekoppeld aan een specifieke pool.</span><span class="sxs-lookup"><span data-stu-id="40924-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="40924-272">Deze koppeling geeft aan welke knooppunten Hallo taken uitvoeren op.</span><span class="sxs-lookup"><span data-stu-id="40924-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="40924-273">U Hallo groep opgeven met behulp van Hallo [PoolInformation] [ py_poolinfo] eigenschap, zoals wordt weergegeven in onderstaande Hallo codefragment.</span><span class="sxs-lookup"><span data-stu-id="40924-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
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

<span data-ttu-id="40924-274">Nu dat een taak is gemaakt, worden taken tooperform Hallo werk toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="40924-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="40924-275">Stap 5: Taken toojob toevoegen</span><span class="sxs-lookup"><span data-stu-id="40924-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="40924-276">![Taken toojob toevoegen][5]</span><span class="sxs-lookup"><span data-stu-id="40924-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="40924-277">
*(1) taken toohello taak worden toegevoegd, (2) Hallo taken zijn gepland toorun op knooppunten en (3) Hallo taken Hallo gegevens bestanden tooprocess downloaden*</span><span class="sxs-lookup"><span data-stu-id="40924-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="40924-278">Batch **taken** zijn Hallo afzonderlijke werkeenheden die worden uitgevoerd op Hallo van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="40924-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="40924-279">Een taak heeft een opdrachtregel en voert Hallo scripts of uitvoerbare bestanden die u in die opdrachtregel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="40924-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="40924-280">tooactually werk verrichten en taken tooa taak moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="40924-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="40924-281">Elke [CloudTask] [ py_task] is geconfigureerd met een opdrachtregel-eigenschap en [ResourceFiles] [ py_resource_file] (net als bij StartTask van Hallo pool) die Hallo taak downloadt toohello knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40924-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="40924-282">In Hallo voorbeeld verwerkt elke taak slechts één bestand.</span><span class="sxs-lookup"><span data-stu-id="40924-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="40924-283">Hierdoor bevat de verzameling ResourceFiles één element.</span><span class="sxs-lookup"><span data-stu-id="40924-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

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
> <span data-ttu-id="40924-284">Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `$AZ_BATCH_NODE_SHARED_DIR` of een toepassing niet gevonden in het Hallo-knooppunt uitvoeren `PATH`, taak opdrachtregels Hallo moet aanroepen shell expliciet, zoals met `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="40924-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="40924-285">Deze vereiste is niet nodig als uw taken een toepassing in Hallo-knooppunt uitvoeren `PATH` en niet verwijzen naar omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="40924-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="40924-286">Binnen Hallo `for` lus in bovenstaande Hallo codefragment, kunt u zien dat vanaf de opdrachtregel voor de taak Hallo Hallo is geconstrueerd met vijf opdrachtregelargumenten bevat die worden doorgegeven te*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="40924-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="40924-287">**FilePath**: dit is Hallo lokaal pad toohello bestand zoals dit zich op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="40924-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="40924-288">Wanneer Hallo ResourceFile-object in `upload_file_to_container` is gemaakt in stap 2 hierboven Hallo bestandsnaam voor deze eigenschap is gebruikt (Hallo `file_path` parameter in de constructor ResourceFile Hallo).</span><span class="sxs-lookup"><span data-stu-id="40924-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="40924-289">Dit geeft aan dat Hallo-bestand kan worden gevonden in Hallo dezelfde map op Hallo knooppunt als *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="40924-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="40924-290">**NUMWORDS**: Hallo boven *N* woorden moeten toohello uitvoerbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="40924-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="40924-291">**storageaccount**: naam Hallo Hallo opslagaccount dat eigenaar is van Hallo container toowhich Hallo taakuitvoer moet worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="40924-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="40924-292">**storagecontainer**: naam Hallo Hallo opslag container toowhich Hallo uitvoer bestanden moeten worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="40924-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="40924-293">**sastoken**: Hallo shared access signature (SAS) die schrijftoegang toohello biedt **uitvoer** container in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="40924-294">Hallo *python_tutorial_task.py* script gebruikt deze shared access signature wanneer de BlockBlobService-verwijzing maakt.</span><span class="sxs-lookup"><span data-stu-id="40924-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="40924-295">Dit biedt schrijftoegang toohello container zonder een toegangssleutel voor opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="40924-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="40924-296">Stap 6: taken controleren</span><span class="sxs-lookup"><span data-stu-id="40924-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="40924-297">![Taken controleren][6]</span><span class="sxs-lookup"><span data-stu-id="40924-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="40924-298">
*script (1) monitors Hallo taken voor voltooiingsstatus Hallo en (2) Hallo taken uploaden resultaat gegevens tooAzure opslag*</span><span class="sxs-lookup"><span data-stu-id="40924-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="40924-299">Wanneer taken zijn tooa taak toegevoegd, worden ze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten in die zijn gekoppeld aan taak Hallo Hallo-pool.</span><span class="sxs-lookup"><span data-stu-id="40924-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="40924-300">Batch verwerkt op basis van het Hallo-instellingen die u opgeeft, alle taak queuing, planning, opnieuw uit te voeren en andere taakbeheerverrichtingen voor u.</span><span class="sxs-lookup"><span data-stu-id="40924-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="40924-301">Er zijn veel manieren toomonitoring uitvoering van de taak.</span><span class="sxs-lookup"><span data-stu-id="40924-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="40924-302">Hallo `wait_for_tasks_to_complete` werken in *python_tutorial_client.py* biedt een eenvoudig voorbeeld van de controle van taken voor een bepaalde status, in dit geval hello [voltooid] [ py_taskstate] status.</span><span class="sxs-lookup"><span data-stu-id="40924-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
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

## <a name="step-7-download-task-output"></a><span data-ttu-id="40924-303">Stap 7: taakuitvoer downloaden</span><span class="sxs-lookup"><span data-stu-id="40924-303">Step 7: Download task output</span></span>
<span data-ttu-id="40924-304">![Taakuitvoer downloaden uit Storage][7]</span><span class="sxs-lookup"><span data-stu-id="40924-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="40924-305">Nu dat hello taak is voltooid, kan Hallo-uitvoer van Hallo taken worden gedownload uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="40924-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="40924-306">Hierbij wordt een aanroep te`download_blobs_from_container` in *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="40924-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="40924-307">Hallo aanroep te`download_blobs_from_container` in *python_tutorial_client.py* aangeeft dat de bestanden Hallo gedownloade tooyour basismap moeten worden.</span><span class="sxs-lookup"><span data-stu-id="40924-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="40924-308">Gratis toomodify van mening bent dat dit locatie uitvoer.</span><span class="sxs-lookup"><span data-stu-id="40924-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="40924-309">Stap 8: containers verwijderen</span><span class="sxs-lookup"><span data-stu-id="40924-309">Step 8: Delete containers</span></span>
<span data-ttu-id="40924-310">Omdat u in rekening voor gegevens die zich in Azure Storage bevindt gebracht, maar het is altijd een goed idee tooremove alle blobs die niet langer zijn vereist voor uw Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="40924-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="40924-311">In *python_tutorial_client.py*, dit wordt gedaan met drie aanroepen te[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="40924-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="40924-312">Stap 9: Hallo job en Hallo pool verwijderen</span><span class="sxs-lookup"><span data-stu-id="40924-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="40924-313">In de laatste stap hello, bent u na vragen aan gebruiker toodelete Hallo taak en Hallo van toepassingen die zijn gemaakt door Hallo *python_tutorial_client.py* script.</span><span class="sxs-lookup"><span data-stu-id="40924-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="40924-314">Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="40924-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="40924-315">Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="40924-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="40924-316">Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.</span><span class="sxs-lookup"><span data-stu-id="40924-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="40924-317">Hallo BatchServiceClient van [JobOperations] [ py_job] en [PoolOperations] [ py_pool] hebben beide overeenkomstige verwijderingsmethoden, die zijn met de naam als u de verwijdering bevestigt:</span><span class="sxs-lookup"><span data-stu-id="40924-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="40924-318">Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum.</span><span class="sxs-lookup"><span data-stu-id="40924-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="40924-319">Let op dat een pool verwijdert alle rekenknooppunten in die groep en dat alle gegevens op Hallo knooppunten kunnen niet worden teruggezet nadat het Hallo-pool wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="40924-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="40924-320">Hallo-voorbeeldscript uitvoeren</span><span class="sxs-lookup"><span data-stu-id="40924-320">Run hello sample script</span></span>
<span data-ttu-id="40924-321">Bij het uitvoeren van Hallo *python_tutorial_client.py* script uit Hallo zelfstudie [codevoorbeeld][github_article_samples], Hallo console-uitvoer is vergelijkbaar toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="40924-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="40924-322">Er is op een pauze `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` terwijl Hallo pool van rekenknooppunten en opgestart gemaakt, en het Hallo-opdrachten in de begintaak van Hallo pool worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="40924-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="40924-323">Gebruik Hallo [Azure-portal] [ azure_portal] toomonitor uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="40924-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="40924-324">Gebruik Hallo [Azure-portal] [ azure_portal] of Hallo [Microsoft Azure Storage Explorer] [ storage_explorer] tooview Hallo Storage-resources (containers en blobs) die zijn gemaakt door de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="40924-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="40924-325">Voer Hallo *python_tutorial_client.py* script uit binnen Hallo `azure-batch-samples/Python/Batch/article_samples` directory.</span><span class="sxs-lookup"><span data-stu-id="40924-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="40924-326">Er wordt een relatief pad voor Hallo `common.helpers` module-import, zodat u ziet mogelijk `ImportError: No module named 'common'` als u Hallo script in deze map niet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="40924-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="40924-327">Uitvoeringstijd doorgaans **ongeveer 5-7 minuten** wanneer u Hallo voorbeeld uitvoert in de standaardconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="40924-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="40924-328">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40924-328">Next steps</span></span>
<span data-ttu-id="40924-329">Gratis toomake wijzigingen te denken*python_tutorial_client.py* en *python_tutorial_task.py* tooexperiment met andere compute-scenario's.</span><span class="sxs-lookup"><span data-stu-id="40924-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="40924-330">Probeer bijvoorbeeld een uitvoeringsvertraging te toevoegen*python_tutorial_task.py* toosimulate langlopende taken en deze in de portal Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="40924-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="40924-331">Probeer meer taken toe te voegen of Hallo aantal rekenknooppunten aan te passen.</span><span class="sxs-lookup"><span data-stu-id="40924-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="40924-332">Voeg logica toocheck voor en Hallo gebruik van een bestaande groep toospeed uitvoeringstijd toestaan.</span><span class="sxs-lookup"><span data-stu-id="40924-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="40924-333">Nu u bekend bent met de basiswerkstroom Hallo van een Batch-oplossing, is het tijd toodig in toohello aanvullende functies van Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="40924-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="40924-334">Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.</span><span class="sxs-lookup"><span data-stu-id="40924-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="40924-335">Start op de andere artikelen Batch-ontwikkeling onder Hallo **Development in-depth** in Hallo [Batch-leertraject][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="40924-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="40924-336">Bekijk een andere implementatie van de verwerking van de werkbelasting Hallo 'eerste N woorden' met Batch in Hallo [TopNWords] [ github_topnwords] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="40924-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

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
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Batch-pool maken"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Batch-job maken"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Taken toojob toevoegen"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Taken controleren"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Taakuitvoer downloaden uit Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Werkstroom van de Batch-oplossing (volledige diagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Batch-referenties in Portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Storage-referenties in Portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Werkstroom van de Batch-oplossing (minimaal diagram)"
