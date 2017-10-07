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
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Aan de slag met Hallo Batch-SDK voor Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Leer de basisbeginselen Hallo van [Azure Batch] [ azure_batch] en Hallo [Batch Python] [ py_azure_sdk] client zoals we een kleine Batch-toepassing geschreven in Python bespreken. We kijken hoe twee scripts gebruik Hallo Batch-service tooprocess een parallelle workload op virtuele Linux-machines in de cloud Hallo steekproeven en hoe ze communiceren met [Azure Storage](../storage/common/storage-introduction.md) voor Faseren en ophalen. U hebt meer informatie over een algemene werkstroom voor Batch-toepassing en een elementair inzicht in Hallo belangrijkste onderdelen van Batch zoals jobs, taken, pools en rekenknooppunten.

![Werkstroom van de Batch-oplossing (basis)][11]<br/>

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u praktische kennis hebt van Python en vertrouwd bent met Linux. Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor de Azure- en hello Batch- en opslagservices.

### <a name="accounts"></a>Accounts
* **Azure-account**: als u nog geen Azure-abonnement hebt, [maakt u een gratis Azure-account][azure_free_account].
* **Batch-account**: als u al een Azure-abonnement hebt, [maakt u een Azure Batch-account](batch-account-create-portal.md).
* **Opslagaccount**: zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Codevoorbeeld
Hallo Python zelfstudie [codevoorbeeld] [ github_article_samples] is een van de vele Batch-codevoorbeelden in Hallo gevonden Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub. U kunt alle Hallo voorbeelden downloaden door te klikken op **klonen of downloaden > ZIP downloaden** op de startpagina Hallo-opslagplaats of door te klikken op Hallo [azure-batch-samples-master.zip] [ github_samples_zip]directe downloadkoppeling. Nadat u de inhoud van het ZIP-bestand Hallo Hallo hebt uitgepakt, Hallo twee scripts voor deze zelfstudie vindt u in Hallo `article_samples` directory:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Python-omgeving
Hallo toorun *python_tutorial_client.py* voorbeeldscript op uw lokale werkstation, moet u een **Python-interpreter** compatibel is met versie **2.7** of **3.3 +**. Hallo-script is getest op Linux- en Windows.

### <a name="cryptography-dependencies"></a>cryptografie-afhankelijkheden
Moet u afhankelijkheden voor Hallo Hallo installeren [cryptografie] [ crypto] bibliotheek, die vereist is door Hallo `azure-batch` en `azure-storage` Python-pakketten. Voer een van de Hallo bewerkingen die geschikt is voor uw platform te volgen of Raadpleeg de toohello [cryptografie installatie] [ crypto_install] details voor meer informatie:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Als voor Python 3.3 + op Linux installeren, gebruikt u Hallo python3 equivalenten voor Hallo Python afhankelijkheden. Bijvoorbeeld op Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Azure-pakketten
Vervolgens installeert Hallo **Azure Batch** en **Azure Storage** Python-pakketten. U kunt beide pakketten installeren met behulp van **pip** en Hallo *requirements.txt* hier vinden:

`/azure-batch-samples/Python/Batch/requirements.txt`

Geef de volgende **pip** opdracht tooinstall Hallo Batch- en Storage-pakketten:

`pip install -r requirements.txt`

Of u kunt installeren Hallo [azure batch] [ pypi_batch] en [azure-opslag] [ pypi_storage] pakketten voor Python handmatig:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Als u een niet-gemachtigd account gebruikt, moet u mogelijk tooprefix uw opdrachten `sudo`. Bijvoorbeeld `sudo pip install -r requirements.txt`. Zie [Installing Packages][pypi_install] (Pakketten installeren) op python.org voor meer informatie over het installeren van Python-pakketten.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Batch-zelfstudiecodevoorbeeld voor Python
Hallo Batch zelfstudiecodevoorbeeld bestaat uit twee Python-scripts en enkele gegevensbestanden.

* **python_tutorial_client.PY**: communiceert met de Hallo Batch- en Storage services tooexecute een parallelle workload op rekenknooppunten (virtuele machines). Hallo *python_tutorial_client.py* script wordt uitgevoerd op uw lokale werkstation.
* **python_tutorial_task.PY**: Hallo-script dat wordt uitgevoerd op rekenknooppunten in Azure tooperform Hallo echte werk. In voorbeeld Hallo *python_tutorial_task.py* parseert Hallo tekst in een bestand gedownload van Azure Storage (Hallo-invoerbestand). En vervolgens het genereert een tekstbestand (Hallo uitvoerbestand) die een lijst van Hallo eerste drie woorden die worden weergegeven in het invoerbestand Hallo bevat. Na het maken van het uitvoerbestand hello, *python_tutorial_task.py* uploads Hallo bestand tooAzure opslag. Dit maakt het beschikbaar voor download toohello clientscript dat wordt uitgevoerd op uw werkstation. Hallo *python_tutorial_task.py* script wordt parallel uitgevoerd in meerdere rekenknooppunten in Hallo Batch-service.
* **./Data/taskdata\*.txt**: deze drie tekstbestanden leveren Hallo invoer voor Hallo-taken die worden uitgevoerd op Hallo van rekenknooppunten.

Hallo volgende diagram illustreert Hallo primaire bewerkingen die worden uitgevoerd door de client- en scripts Hallo. Deze basiswerkstroom is typerend voor vele rekenoplossingen die met Batch worden gemaakt. Hoewel hierin niet elke beschikbare functie in Hallo Batch-service, omvat vrijwel elk Batch-scenario gedeelten van deze werkstroom.

![Batch-voorbeeldwerkstroom][8]<br/>

[**Stap 1.**](#step-1-create-storage-containers) Maak **containers** in Azure Blob Storage.<br/>
[**Stap 2.**](#step-2-upload-task-script-and-data-files) Taak script en invoer bestanden toocontainers uploaden.<br/>
[**Stap 3.**](#step-3-create-batch-pool) Maak een Batch-**pool**.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hallo groep **StartTask** downloads Hallo taak script (python_tutorial_task.py) toonodes wanneer ze aan Hallo groep worden toegevoegd.<br/>
[**Stap 4.**](#step-4-create-batch-job) Maak een Batch-**job**.<br/>
[**Stap 5.**](#step-5-add-tasks-to-job) Voeg **taken** toohello taak.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Hallo-taken zijn gepland tooexecute op knooppunten.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Elke taak downloadt de bijbehorende invoergegevens uit Azure Storage en wordt daarna uitgevoerd.<br/>
[**Stap 6.**](#step-6-monitor-tasks) Controleer taken.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Nadat taken zijn voltooid, uploaden zij hun uitvoer gegevens tooAzure opslag.<br/>
[**Stap 7.**](#step-7-download-task-output) Download taakuitvoer uit Storage.

Zoals vermeld voert niet elke Batch-oplossing deze exacte stappen uit en kunnen veel meer stappen nodig zijn, maar deze sjabloon toont gebruikelijke processen gevonden in een Batch-oplossing.

## <a name="prepare-client-script"></a>Clientscripts voorbereiden
Voordat u Hallo voorbeeld uitvoert, toevoegen u de referenties van uw Batch- en Storage-account te*python_tutorial_client.py*. Als u dit nog niet hebt gedaan, opent u Hallo-bestand in uw favoriete editor en update Hallo volgende regels met uw referenties.

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

U vindt uw Batch- en Storage-accountreferenties op Hallo accountblade van elke service op Hallo [Azure-portal][azure_portal]:

![Batch-referenties in portal Hallo][9]
![Storage-referenties in portal Hallo][10]<br/>

Hallo uit te voeren, analyseren we Hallo stappen die worden gebruikt door Hallo scripts tooprocess een workload in Hallo Batch-service. We raden u toorefer regelmatig toohello scripts in uw editor wanneer u zich door de rest van het artikel Hallo Hallo werken.

Navigeer toohello volgende regel in **python_tutorial_client.py** toostart bij stap 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Stap 1: opslagcontainers maken
![Containers maken in Azure Storage][1]
<br/>

Batch bevat ingebouwde ondersteuning voor interactie met Azure Storage. Containers in uw opslagaccount biedt Hallo-bestanden die nodig zijn door Hallo-taken die worden uitgevoerd in uw Batch-account. Hallo containers bieden ook een uitvoergegevens van plaats toostore Hallo die Hallo taken opleveren. Hallo eerst te beginnen Hallo *python_tutorial_client.py* script doet is drie containers maken in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):

* **toepassing**: deze container slaat Hallo pythonscript uitvoeren door Hallo-taken *python_tutorial_task.py*.
* **invoer**: taken downloaden de Hallo gegevens bestanden tooprocess vanaf Hallo *invoer* container.
* **uitvoer**: bij de verwerking van invoerbestanden taken hebt voltooid, uploaden zij Hallo resultaten toohello *uitvoer* container.

In de volgorde toointeract met een Storage-account in en containers, maken we hello gebruiken [azure-opslag] [ pypi_storage] toocreate van het pakket een [BlockBlobService] [ py_blockblobservice] object--Hallo 'blob-client'. Vervolgens maken we drie containers in Hallo Hallo blob-client met Storage-account.

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

Zodra het Hallo-containers zijn gemaakt, Hallo toepassing kan nu Hallo bestanden uploaden die wordt gebruikt door Hallo taken.

> [!TIP]
> [Hoe Azure Blob storage met Python toouse](../storage/blobs/storage-python-how-to-use-blob-storage.md) biedt een goed overzicht van het werken met Azure Storage-containers en blobs. Deze moet aan de bovenkant Hallo van uw leeslijst als u met Batch begint te werken.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Stap 2: taakscript- en gegevensbestanden uploaden
![Het uploaden van taak toepassing en invoer (gegevens) bestanden toocontainers][2]
<br/>

In Hallo uploaden bewerking *python_tutorial_client.py* definieert eerst verzamelingen van **toepassing** en **invoer** bestandspaden die op de lokale machine Hallo zijn. Vervolgens wordt deze bestanden toohello containers die u hebt gemaakt in de vorige stap Hallo geüpload.

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

Met behulp begrip van de lijst, Hallo `upload_file_to_container` functie wordt aangeroepen voor elk bestand in Hallo verzamelingen en de twee [ResourceFile] [ py_resource_file] verzamelingen ingevuld. Hallo `upload_file_to_container` functie wordt hieronder weergegeven:

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

### <a name="resourcefiles"></a>ResourceFiles
Een [ResourceFile] [ py_resource_file] biedt taken in Batch met Hallo URL tooa bestand in Azure Storage dat is gedownload tooa rekenknooppunt voordat deze taak wordt uitgevoerd. Hallo [ResourceFile][py_resource_file]. **blob_source** eigenschap geeft u de volledige URL Hallo van Hallo-bestand zoals dit zich in Azure Storage. Hallo-URL kan ook een shared access signature (SAS) waarmee u veilige toegang tot toohello bestand bevatten. De meeste typen taken in Batch bevatten een eigenschap *ResourceFiles*, waaronder:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Dit voorbeeld gebruikt geen Hallo JobPreparationTask of JobReleaseTask taaktypen, maar kunt u meer informatie over deze in [uitvoeren jobvoorbereidingstaken en jobvrijgevingstaken taken op Azure Batch-rekenknooppunten](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Shared Access Signature (SAS)
Shared access signatures zijn tekenreeksen die beveiligde toegang toocontainers en blobs in Azure Storage bieden. Hallo *python_tutorial_client.py* script maakt gebruik van blobs en container gedeelde handtekeningen voor toegang en laat zien hoe deze gedeelde tooobtain vanaf toegang tot tekenreeksen Hallo Storage-service.

* **Shared access signatures voor blobs**: maakt gebruik van Hallo pool-StartTask gedeelde access signatures voor blobs wanneer het Hallo-taak en de invoergegevensbestanden gegevensbestanden uit Storage downloadt (Zie [stap 3](#step-3-create-batch-pool) hieronder). Hallo `upload_file_to_container` werken in *python_tutorial_client.py* bevat Hallo-code die shared access signature van elke blob verkrijgt. Dit gebeurt door het aanroepen van [BlockBlobService.make_blob_url] [ py_make_blob_url] in Hallo Storage-module.
* **Shared access signature voor containers**: als elke taak zijn werk heeft verricht op Hallo rekenknooppunt, uploadt het bestand uitvoer toohello *uitvoer* container in Azure Storage. toodo, *python_tutorial_task.py* maakt gebruik van een shared access signature voor containers die schrijftoegang toohello container biedt. Hallo `get_container_sas_token` werken in *python_tutorial_client.py* Hallo-container shared access signature, die vervolgens wordt doorgegeven als een opdrachtregelargument toohello taken verkrijgt. Stap &#5; [toevoegen taken tooa taak](#step-5-add-tasks-to-job), Hallo informatie over het gebruik van Hallo container SAS besproken.

> [!TIP]
> Uitchecken Hallo tweedelige reeks over handtekeningen voor gedeelde toegang [deel 1: Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) en [deel 2: maken en gebruiken van een SAS met Hallo Blob-service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn meer informatie over veilige toegang bieden toodata in uw opslagaccount.
>
>

## <a name="step-3-create-batch-pool"></a>Stap 3: Batch-pool maken
![Een Batch-pool maken][3]
<br/>

Een Batch-**pool** is een verzameling rekenknooppunten (virtuele machines) waarop Batch de taken van een job uitvoert.

Nadat het Hallo taak script en gegevens bestanden toohello Storage-account, uploadt *python_tutorial_client.py* start het zijn interactie met Hallo Batch-service met behulp van Hallo Batch Python-module. toodo, een [BatchServiceClient] [ py_batchserviceclient] wordt gemaakt:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Daarna wordt een pool van rekenknooppunten gemaakt in de Batch-account met een aanroep van hello te`create_pool`.

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

Wanneer u een groep maakt, definieert u een [PoolAddParameter] [ py_pooladdparam] Hiermee worden verschillende eigenschappen voor Hallo van toepassingen:

* **ID** van Hallo van toepassingen (*id* - vereist)<p/>Net als bij de meeste entiteiten in Batch, moet ook uw nieuwe pool een unieke id binnen uw Batch-account hebben. Uw code verwijst toothis groep met de bijbehorende ID, en is identificeert u Hallo van toepassingen in hello Azure [portal][azure_portal].
* **Aantal rekenknooppunten** (*target_dedicated* - vereist)<p/>Deze eigenschap specificeert hoeveel virtuele machines moeten worden geïmplementeerd in Hallo van toepassingen. Het is belangrijk toonote dat alle Batch-accounts standaard hebben **quotum** dat limieten aantal Hallo **kernen** (en dus rekenknooppunten) in een Batch-account. U vindt Hallo standaardquota en instructies over het te[een quotum verhogen](batch-quota-limit.md#increase-a-quota) (zoals Hallo maximum aantal kernen in uw Batch-account) in [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md). Rijzen er vragen zoals "Waarom kan mijn pool niet meer dan X knooppunten bevatten?", Dit quotum voor kernen mogelijk Hallo oorzaak.
* **Besturingssysteem** voor knooppunten (*virtual_machine_configuration* **of** *cloud_service_configuration* - vereist)<p/>In *python_tutorial_client.py* maken we een pool met Linux-knooppunten met behulp van een [VirtualMachineConfiguration][py_vm_config]. Hallo `select_latest_verified_vm_image_with_node_agent_sku` werken in `common.helpers` vereenvoudigt het werken met [Azure Virtual Machines Marketplace] [ vm_marketplace] installatiekopieën. Zie [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie over het gebruik van Marketplace-installatiekopieën.
* **Grootte van rekenknooppunten** (*vm_size* - vereist)<p/>Omdat we Linux-knooppunten opgeven voor onze [VirtualMachineConfiguration][py_vm_config], geven we een VM-grootte op (in dit voorbeeld `STANDARD_A1`) uit [Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Zie opnieuw [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Linux-rekenknooppunten in Azure Batch-pools inrichten) voor meer informatie.
* **Begintaak** (*start_task* - niet vereist)<p/>Samen met de Hallo bovenstaande fysieke knooppunteigenschappen, kunt u ook opgeven een [StartTask] [ py_starttask] voor Hallo van toepassingen (dit is niet vereist). Hallo StartTask wordt uitgevoerd op elk knooppunt, zoals u dat knooppunt aan Hallo-pool wordt toegevoegd en telkens wanneer een knooppunt opnieuw wordt gestart. Hallo StartTask is vooral nuttig voor het voorbereiden van rekenknooppunten voor Hallo uitvoering van taken, zoals het installeren van Hallo-toepassingen die de taken worden uitgevoerd.<p/>In deze voorbeeldtoepassing kopieert StartTask Hallo Hallo-bestanden die het van Storage downloadt (die zijn opgegeven met behulp van de StartTask hello **resource_files** eigenschap) van Hallo StartTask *werkmap* toohello *gedeelde* map waartoe alle taken die worden uitgevoerd op Hallo-knooppunt toegang heeft. In wezen Hiermee kopieert u `python_tutorial_task.py` toohello gedeelde map op elk knooppunt zoals Hallo knooppunt lid van groep hello, zodat alle taken die worden uitgevoerd op Hallo-knooppunt toegang kunnen hebben.

U merkt Hallo aanroep toohello `wrap_commands_in_shell` Help-functie. Deze functie gebruikt een verzameling afzonderlijke opdrachten en maakt een enkele opdrachtregel die geschikt is voor de opdrachtregeleigenschap van een taak.

Opmerkelijk in bovenstaande Hallo codefragment is ook gebruik van twee omgevingsvariabelen in Hallo Hallo **command_line** eigenschap Hallo StartTask: `AZ_BATCH_TASK_WORKING_DIR` en `AZ_BATCH_NODE_SHARED_DIR`. Elk rekenknooppunt in een Batch-pool wordt automatisch geconfigureerd met meerdere omgevingsvariabelen die specifiek tooBatch zijn. Een proces dat wordt uitgevoerd door een taak heeft toegang tot toothese omgevingsvariabelen.

> [!TIP]
> Zie toofind voor meer informatie over Hallo omgevingsvariabelen die beschikbaar op rekenknooppunten in een Batch-pool, evenals informatie over taakwerkmappen zijn **omgevingsinstellingen voor taken** en **bestanden en mappen**  in Hallo [overzicht van Azure Batch-functies](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Stap 4: Batch-job maken
![Een Batch-job maken][4]<br/>

Een Batch-**job** is een verzameling taken en is gekoppeld aan een pool van rekenknooppunten. Hallo-taken in een taak uitgevoerd op de rekenknooppunten van de pool Hallo die zijn gekoppeld.

U kunt een job niet alleen voor het organiseren en te volgen taken in gerelateerde workloads, maar ook voor de toepassing van bepaalde beperkingen--zoals Hallo maximale runtime voor Hallo job (en bij uitbreiding, de taken ervan) en de prioriteit van de job in relatie tooother taken in Batch-account Hallo. In dit voorbeeld is Hallo-taak echter alleen gekoppeld aan Hallo-groep die is gemaakt in stap #3. Er worden geen aanvullende eigenschappen geconfigureerd.

Alle Batch-jobs worden gekoppeld aan een specifieke pool. Deze koppeling geeft aan welke knooppunten Hallo taken uitvoeren op. U Hallo groep opgeven met behulp van Hallo [PoolInformation] [ py_poolinfo] eigenschap, zoals wordt weergegeven in onderstaande Hallo codefragment.

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

Nu dat een taak is gemaakt, worden taken tooperform Hallo werk toegevoegd.

## <a name="step-5-add-tasks-toojob"></a>Stap 5: Taken toojob toevoegen
![Taken toojob toevoegen][5]<br/>
*(1) taken toohello taak worden toegevoegd, (2) Hallo taken zijn gepland toorun op knooppunten en (3) Hallo taken Hallo gegevens bestanden tooprocess downloaden*

Batch **taken** zijn Hallo afzonderlijke werkeenheden die worden uitgevoerd op Hallo van rekenknooppunten. Een taak heeft een opdrachtregel en voert Hallo scripts of uitvoerbare bestanden die u in die opdrachtregel opgeeft.

tooactually werk verrichten en taken tooa taak moeten worden toegevoegd. Elke [CloudTask] [ py_task] is geconfigureerd met een opdrachtregel-eigenschap en [ResourceFiles] [ py_resource_file] (net als bij StartTask van Hallo pool) die Hallo taak downloadt toohello knooppunt voordat de opdrachtregel ervan automatisch wordt uitgevoerd. In Hallo voorbeeld verwerkt elke taak slechts één bestand. Hierdoor bevat de verzameling ResourceFiles één element.

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
> Wanneer ze toegang krijgen tot omgevingsvariabelen zoals `$AZ_BATCH_NODE_SHARED_DIR` of een toepassing niet gevonden in het Hallo-knooppunt uitvoeren `PATH`, taak opdrachtregels Hallo moet aanroepen shell expliciet, zoals met `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Deze vereiste is niet nodig als uw taken een toepassing in Hallo-knooppunt uitvoeren `PATH` en niet verwijzen naar omgevingsvariabelen.
>
>

Binnen Hallo `for` lus in bovenstaande Hallo codefragment, kunt u zien dat vanaf de opdrachtregel voor de taak Hallo Hallo is geconstrueerd met vijf opdrachtregelargumenten bevat die worden doorgegeven te*python_tutorial_task.py*:

1. **FilePath**: dit is Hallo lokaal pad toohello bestand zoals dit zich op Hallo-knooppunt. Wanneer Hallo ResourceFile-object in `upload_file_to_container` is gemaakt in stap 2 hierboven Hallo bestandsnaam voor deze eigenschap is gebruikt (Hallo `file_path` parameter in de constructor ResourceFile Hallo). Dit geeft aan dat Hallo-bestand kan worden gevonden in Hallo dezelfde map op Hallo knooppunt als *python_tutorial_task.py*.
2. **NUMWORDS**: Hallo boven *N* woorden moeten toohello uitvoerbestand worden geschreven.
3. **storageaccount**: naam Hallo Hallo opslagaccount dat eigenaar is van Hallo container toowhich Hallo taakuitvoer moet worden geüpload.
4. **storagecontainer**: naam Hallo Hallo opslag container toowhich Hallo uitvoer bestanden moeten worden geüpload.
5. **sastoken**: Hallo shared access signature (SAS) die schrijftoegang toohello biedt **uitvoer** container in Azure Storage. Hallo *python_tutorial_task.py* script gebruikt deze shared access signature wanneer de BlockBlobService-verwijzing maakt. Dit biedt schrijftoegang toohello container zonder een toegangssleutel voor opslagaccount Hallo.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Stap 6: taken controleren
![Taken controleren][6]<br/>
*script (1) monitors Hallo taken voor voltooiingsstatus Hallo en (2) Hallo taken uploaden resultaat gegevens tooAzure opslag*

Wanneer taken zijn tooa taak toegevoegd, worden ze automatisch in de wachtrij geplaatst en gepland voor uitvoering op rekenknooppunten in die zijn gekoppeld aan taak Hallo Hallo-pool. Batch verwerkt op basis van het Hallo-instellingen die u opgeeft, alle taak queuing, planning, opnieuw uit te voeren en andere taakbeheerverrichtingen voor u.

Er zijn veel manieren toomonitoring uitvoering van de taak. Hallo `wait_for_tasks_to_complete` werken in *python_tutorial_client.py* biedt een eenvoudig voorbeeld van de controle van taken voor een bepaalde status, in dit geval hello [voltooid] [ py_taskstate] status.

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

## <a name="step-7-download-task-output"></a>Stap 7: taakuitvoer downloaden
![Taakuitvoer downloaden uit Storage][7]<br/>

Nu dat hello taak is voltooid, kan Hallo-uitvoer van Hallo taken worden gedownload uit Azure Storage. Hierbij wordt een aanroep te`download_blobs_from_container` in *python_tutorial_client.py*:

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
> Hallo aanroep te`download_blobs_from_container` in *python_tutorial_client.py* aangeeft dat de bestanden Hallo gedownloade tooyour basismap moeten worden. Gratis toomodify van mening bent dat dit locatie uitvoer.
>
>

## <a name="step-8-delete-containers"></a>Stap 8: containers verwijderen
Omdat u in rekening voor gegevens die zich in Azure Storage bevindt gebracht, maar het is altijd een goed idee tooremove alle blobs die niet langer zijn vereist voor uw Batch-taken. In *python_tutorial_client.py*, dit wordt gedaan met drie aanroepen te[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Stap 9: Hallo job en Hallo pool verwijderen
In de laatste stap hello, bent u na vragen aan gebruiker toodelete Hallo taak en Hallo van toepassingen die zijn gemaakt door Hallo *python_tutorial_client.py* script. Hoewel jobs en taken zelf niet in rekening worden gebracht, worden rekenknooppunten *wel* in rekening gebracht. Daarom is het raadzaam om knooppunten alleen toe te wijzen als dat nodig is. Het verwijderen van ongebruikte pools kan een onderdeel zijn van uw onderhoudsprocedure.

Hallo BatchServiceClient van [JobOperations] [ py_job] en [PoolOperations] [ py_pool] hebben beide overeenkomstige verwijderingsmethoden, die zijn met de naam als u de verwijdering bevestigt:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Houd er rekening mee dat rekenresources in rekening worden gebracht. Door ongebruikte pools te verwijderen, beperkt u uw kosten tot een minimum. Let op dat een pool verwijdert alle rekenknooppunten in die groep en dat alle gegevens op Hallo knooppunten kunnen niet worden teruggezet nadat het Hallo-pool wordt verwijderd.
>
>

## <a name="run-hello-sample-script"></a>Hallo-voorbeeldscript uitvoeren
Bij het uitvoeren van Hallo *python_tutorial_client.py* script uit Hallo zelfstudie [codevoorbeeld][github_article_samples], Hallo console-uitvoer is vergelijkbaar toohello volgende. Er is op een pauze `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` terwijl Hallo pool van rekenknooppunten en opgestart gemaakt, en het Hallo-opdrachten in de begintaak van Hallo pool worden uitgevoerd. Gebruik Hallo [Azure-portal] [ azure_portal] toomonitor uw pool, rekenknooppunten, job en taken tijdens en na de uitvoering. Gebruik Hallo [Azure-portal] [ azure_portal] of Hallo [Microsoft Azure Storage Explorer] [ storage_explorer] tooview Hallo Storage-resources (containers en blobs) die zijn gemaakt door de toepassing hello.

> [!TIP]
> Voer Hallo *python_tutorial_client.py* script uit binnen Hallo `azure-batch-samples/Python/Batch/article_samples` directory. Er wordt een relatief pad voor Hallo `common.helpers` module-import, zodat u ziet mogelijk `ImportError: No module named 'common'` als u Hallo script in deze map niet uitvoert.
>
>

Uitvoeringstijd doorgaans **ongeveer 5-7 minuten** wanneer u Hallo voorbeeld uitvoert in de standaardconfiguratie.

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

## <a name="next-steps"></a>Volgende stappen
Gratis toomake wijzigingen te denken*python_tutorial_client.py* en *python_tutorial_task.py* tooexperiment met andere compute-scenario's. Probeer bijvoorbeeld een uitvoeringsvertraging te toevoegen*python_tutorial_task.py* toosimulate langlopende taken en deze in de portal Hallo controleren. Probeer meer taken toe te voegen of Hallo aantal rekenknooppunten aan te passen. Voeg logica toocheck voor en Hallo gebruik van een bestaande groep toospeed uitvoeringstijd toestaan.

Nu u bekend bent met de basiswerkstroom Hallo van een Batch-oplossing, is het tijd toodig in toohello aanvullende functies van Hallo Batch-service.

* Bekijk Hallo [overzicht van Azure Batch-functies](batch-api-basics.md) artikel, waarin het is raadzaam als je nieuwe toohello-service.
* Start op de andere artikelen Batch-ontwikkeling onder Hallo **Development in-depth** in Hallo [Batch-leertraject][batch_learning_path].
* Bekijk een andere implementatie van de verwerking van de werkbelasting Hallo 'eerste N woorden' met Batch in Hallo [TopNWords] [ github_topnwords] voorbeeld.

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
