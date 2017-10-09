---
title: aaaUse Azure opdrachtregelprogramma 2.0 interface tooget de slag met Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure platformoverschrijdende opdrachtregel 2.0 toocreate een Data Lake Store-account en basisbewerkingen uit te voeren
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="17a4b-103">Aan de slag met Azure Data Lake Store met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17a4b-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17a4b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="17a4b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="17a4b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17a4b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="17a4b-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="17a4b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="17a4b-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="17a4b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="17a4b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="17a4b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="17a4b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17a4b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="17a4b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="17a4b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="17a4b-111">Python</span><span class="sxs-lookup"><span data-stu-id="17a4b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="17a4b-112">Meer informatie over hoe Azure CLI 2.0 toouse toocreate een Azure Data Lake opslaan account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="17a4b-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="17a4b-113">Hello Azure CLI 2.0 is een nieuwe Azure opdrachtregelprogramma ervaring voor het beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="17a4b-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="17a4b-114">Deze kan worden gebruikt in Mac OS, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="17a4b-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="17a4b-115">Zie [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Overzicht van Azure CLI 2.0) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="17a4b-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="17a4b-116">U kunt ook zoeken op Hallo [naslaginformatie over Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls) voor een volledige lijst met opdrachten en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="17a4b-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="17a4b-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="17a4b-117">Prerequisites</span></span>
<span data-ttu-id="17a4b-118">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="17a4b-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="17a4b-119">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="17a4b-119">**An Azure subscription**.</span></span> <span data-ttu-id="17a4b-120">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17a4b-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="17a4b-121">**Azure CLI 2.0**: zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="17a4b-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="17a4b-122">Verificatie</span><span class="sxs-lookup"><span data-stu-id="17a4b-122">Authentication</span></span>

<span data-ttu-id="17a4b-123">In dit artikel wordt een eenvoudigere verificatiemethode voor Data Lake Store gebruikt waarbij u zich als een eindgebruiker aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="17a4b-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="17a4b-124">Hallo toegang niveau tooData Lake Store-account en een nieuw bestandssysteem vervolgens beheerst door het toegangsniveau Hallo Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="17a4b-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="17a4b-125">Er zijn echter andere benaderingen als goed tooauthenticate met Data Lake Store, die zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="17a4b-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="17a4b-126">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="17a4b-127">Meld u bij tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="17a4b-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="17a4b-128">Meld u aan bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="17a4b-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="17a4b-129">U kunt een toouse code ophalen in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="17a4b-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="17a4b-130">Gebruik een web browser tooopen Hallo pagina https://aka.ms/devicelogin en Hallo code tooauthenticate invoeren.</span><span class="sxs-lookup"><span data-stu-id="17a4b-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="17a4b-131">U bent na vragen aan gebruiker toolog aan met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="17a4b-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="17a4b-132">Zodra u zich aanmeldt, Hallo Hallo venster een lijst met alle Azure-abonnementen die gekoppeld aan uw account zijn.</span><span class="sxs-lookup"><span data-stu-id="17a4b-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="17a4b-133">Hallo na de opdracht toouse een specifiek abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17a4b-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="17a4b-134">Een Azure Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="17a4b-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="17a4b-135">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="17a4b-135">Create a new resource group.</span></span> <span data-ttu-id="17a4b-136">In Hallo volgende opdracht, bieden Hallo parameterwaarden die u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="17a4b-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="17a4b-137">Als het Hallo-locatienaam spaties bevat, kunt u deze aanhalingstekens geplaatst.</span><span class="sxs-lookup"><span data-stu-id="17a4b-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="17a4b-138">Bijvoorbeeld “VS-oost 2”.</span><span class="sxs-lookup"><span data-stu-id="17a4b-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="17a4b-139">Hallo Data Lake Store-account maken.</span><span class="sxs-lookup"><span data-stu-id="17a4b-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="17a4b-140">Mappen maken in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="17a4b-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="17a4b-141">U kunt mappen maken onder uw Azure Data Lake Store-account toomanage en opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="17a4b-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="17a4b-142">Gebruik Hallo na de opdracht toocreate een map met de naam **mynewfolder** in de hoofdmap Hallo Hallo Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="17a4b-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="17a4b-143">Hallo `--folder` parameter zorgt ervoor dat Hallo opdracht maakt u een map.</span><span class="sxs-lookup"><span data-stu-id="17a4b-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="17a4b-144">Als deze parameter niet aanwezig is, maakt Hallo opdracht u een leeg bestand met de naam van mynewfolder in de hoofdmap Hallo Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="17a4b-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="17a4b-145">Uploaden van gegevens tooa Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="17a4b-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="17a4b-146">U kunt gegevens tooData Lake Store rechtstreeks op Hallo niveau of tooa hoofdmap die u hebt gemaakt in Hallo account uploaden.</span><span class="sxs-lookup"><span data-stu-id="17a4b-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="17a4b-147">Hallo codefragmenten hieronder laten zien hoe tooupload enkele map toohello met voorbeeldgegevens (**mynewfolder**) u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="17a4b-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="17a4b-148">Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="17a4b-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="17a4b-149">Hallo-bestand downloaden en opslaan in een lokale map op uw computer, zoals C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="17a4b-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="17a4b-150">U moet Hallo bestemming voor Hallo volledige pad inclusief Hallo-bestandsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="17a4b-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="17a4b-151">Bestanden in een Data Lake Store-account weergeven</span><span class="sxs-lookup"><span data-stu-id="17a4b-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="17a4b-152">Hallo volgende opdracht toolist Hallo bestanden in een Data Lake Store-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17a4b-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="17a4b-153">Hallo-uitvoer hiervan moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="17a4b-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="17a4b-154">Gegevens in een Data Lake Store-account een nieuwe naam geven, downloaden en verwijderen</span><span class="sxs-lookup"><span data-stu-id="17a4b-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="17a4b-155">**een bestand toorename**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="17a4b-156">**een bestand toodownload**, Hallo volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17a4b-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="17a4b-157">Zorg ervoor dat het doelpad Hallo die u al opgeeft bestaat.</span><span class="sxs-lookup"><span data-stu-id="17a4b-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="17a4b-158">Hallo opdracht maakt u de doelmap Hallo als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="17a4b-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="17a4b-159">**een bestand toodelete**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="17a4b-160">Als u toodelete Hallo map wilt **mynewfolder** en Hallo bestand **vehicle1_09142014_copy.csv** samen in één opdracht gebruik Hallo--recurse parameter</span><span class="sxs-lookup"><span data-stu-id="17a4b-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="17a4b-161">Machtigingen en ACL's gebruiken voor een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="17a4b-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="17a4b-162">In deze sectie leert u hoe u toomanage ACL's en -machtigingen met Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="17a4b-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="17a4b-163">Zie [Toegangsbeheer in Azure Data Lake Store](data-lake-store-access-control.md) voor gedetailleerde informatie over de implementatie van ACL's in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="17a4b-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="17a4b-164">**tooupdate hello eigenaar van een bestandsmap**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="17a4b-165">**tooupdate hello machtigingen voor een bestandsmap**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="17a4b-166">**tooget hello ACL's voor een opgegeven pad**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="17a4b-167">Hallo-uitvoer moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="17a4b-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="17a4b-168">**een vermelding voor een ACL tooset**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="17a4b-169">**een vermelding voor een ACL tooremove**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="17a4b-170">**de standaardwaarde van een volledige ACL tooremove**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="17a4b-171">**een hele niet-standaard ACL tooremove**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17a4b-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="17a4b-172">Een Data Lake Store-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="17a4b-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="17a4b-173">Hallo na de opdracht toodelete een Data Lake Store-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="17a4b-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="17a4b-174">Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="17a4b-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17a4b-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="17a4b-175">Next steps</span></span>

* [<span data-ttu-id="17a4b-176">Naslaggegevens van Azure Data Lake Store CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17a4b-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="17a4b-177">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="17a4b-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="17a4b-178">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="17a4b-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="17a4b-179">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="17a4b-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
