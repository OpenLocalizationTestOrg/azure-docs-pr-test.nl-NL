---
title: De opdrachtregelinterface van Azure 2.0 gebruiken om aan de slag te gaan met Azure Data Lake Store | Microsoft Docs
description: Een Data Lake Store-account maken en basisbewerkingen uitvoeren met de platformoverschrijdende opdrachtregelinterface van Azure 2.0
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="ef943-103">Aan de slag met Azure Data Lake Store met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef943-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef943-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ef943-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ef943-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef943-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ef943-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="ef943-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ef943-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="ef943-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ef943-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ef943-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ef943-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef943-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ef943-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef943-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ef943-111">Python</span><span class="sxs-lookup"><span data-stu-id="ef943-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ef943-112">Ontdek hoe u met de Azure CLI 2.0 een Azure Data Lake Store-account maakt en basisbewerkingen uitvoert, zoals het maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ef943-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="ef943-113">De Azure CLI 2.0 is de nieuwe opdrachtregelervaring van Azure voor het beheer van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="ef943-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="ef943-114">Deze kan worden gebruikt in Mac OS, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="ef943-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="ef943-115">Zie [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Overzicht van Azure CLI 2.0) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef943-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="ef943-116">U kunt ook zoeken in de [Naslaggegevens van Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls), voor een volledige lijst met opdrachten en syntaxis.</span><span class="sxs-lookup"><span data-stu-id="ef943-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ef943-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ef943-117">Prerequisites</span></span>
<span data-ttu-id="ef943-118">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="ef943-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="ef943-119">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ef943-119">**An Azure subscription**.</span></span> <span data-ttu-id="ef943-120">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef943-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ef943-121">**Azure CLI 2.0**: zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="ef943-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="ef943-122">Verificatie</span><span class="sxs-lookup"><span data-stu-id="ef943-122">Authentication</span></span>

<span data-ttu-id="ef943-123">In dit artikel wordt een eenvoudigere verificatiemethode voor Data Lake Store gebruikt waarbij u zich als een eindgebruiker aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="ef943-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="ef943-124">Het toegangsniveau voor het account en bestandssysteem van Data Lake Store wordt vervolgens bepaald door het toegangsniveau van de aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ef943-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="ef943-125">Er zijn echter ook andere manieren om te verifiëren in Data Lake Store, zoals **verificatie door eindgebruikers** en **service-naar-serviceverificatie**.</span><span class="sxs-lookup"><span data-stu-id="ef943-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ef943-126">Zie [Eindgebruikersverificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [Service-to-serviceverificatie](data-lake-store-authenticate-using-active-directory.md) voor instructies en meer informatie over verificatie.</span><span class="sxs-lookup"><span data-stu-id="ef943-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="ef943-127">Aanmelden bij uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="ef943-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="ef943-128">Meld u aan bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef943-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="ef943-129">U ontvangt een code die u in de volgende stap nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="ef943-129">You get a code to use in the next step.</span></span> <span data-ttu-id="ef943-130">Gebruik een webbrowser om de pagina https://aka.ms/devicelogin te openen en voer de code in voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="ef943-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="ef943-131">U wordt gevraagd om u aan te melden met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="ef943-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="ef943-132">Wanneer u bent aangemeld, wordt er een venster weergegeven met alle Azure-abonnementen die aan uw account zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ef943-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="ef943-133">Gebruik de volgende opdracht als u een specifiek abonnement wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef943-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="ef943-134">Een Azure Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="ef943-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="ef943-135">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ef943-135">Create a new resource group.</span></span> <span data-ttu-id="ef943-136">Geef in de volgende opdracht de parameterwaarden op die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef943-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="ef943-137">Als de locatienaam spaties bevat, moet deze tussen dubbele aanhalingstekens worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ef943-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="ef943-138">Bijvoorbeeld “VS-oost 2”.</span><span class="sxs-lookup"><span data-stu-id="ef943-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="ef943-139">Maak de Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ef943-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ef943-140">Mappen maken in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ef943-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="ef943-141">U kunt mappen maken onder uw Azure Data Lake Store-account voor het beheren en opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ef943-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="ef943-142">Gebruik de volgende opdracht om in de hoofdmap van Data Lake Store een map te maken met de naam **mynewfolder**.</span><span class="sxs-lookup"><span data-stu-id="ef943-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="ef943-143">Met de parameter `--folder` geeft u aan dat u een map wilt maken.</span><span class="sxs-lookup"><span data-stu-id="ef943-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="ef943-144">Zonder deze parameter maakt de opdracht een leeg bestand met de naam mynewfolder in de hoofdmap van het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ef943-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="ef943-145">Gegevens uploaden naar een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ef943-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="ef943-146">U kunt gegevens direct naar het hoogste niveau in Data Lake Store uploaden of naar een map die u in het account hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef943-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="ef943-147">De codefragmenten hieronder laten zien hoe u voorbeeldgegevens uploadt naar de map (**mynewfolder**) die u in de voorgaande sectie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef943-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="ef943-148">Als u nog geen voorbeeldgegevens hebt om te uploaden, kunt u de map **Ambulance Data** uit de [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef943-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="ef943-149">Download het bestand en sla het in een lokale map op uw computer op, bijvoorbeeld C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="ef943-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="ef943-150">Als bestemming moet u het volledige pad inclusief de bestandsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="ef943-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="ef943-151">Bestanden in een Data Lake Store-account weergeven</span><span class="sxs-lookup"><span data-stu-id="ef943-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="ef943-152">Gebruik de volgende opdracht om de bestanden in een Data Lake Store-account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ef943-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="ef943-153">De uitvoer ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="ef943-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="ef943-154">Gegevens in een Data Lake Store-account een nieuwe naam geven, downloaden en verwijderen</span><span class="sxs-lookup"><span data-stu-id="ef943-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="ef943-155">**Als u de naam van een bestand wilt wijzigen**, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef943-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="ef943-156">**Als u een bestand wilt downloaden**, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef943-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="ef943-157">Zorg ervoor dat het doelpad dat u opgeeft al bestaat.</span><span class="sxs-lookup"><span data-stu-id="ef943-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="ef943-158">Met de opdracht wordt de doelmap gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ef943-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="ef943-159">**Als u een bestand wilt verwijderen**, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ef943-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="ef943-160">Als u de map **mynewfolder** en het bestand **vehicle1_09142014_copy.csv** met één opdracht wilt verwijderen, gebruikt u de parameter --recurse</span><span class="sxs-lookup"><span data-stu-id="ef943-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="ef943-161">Machtigingen en ACL's gebruiken voor een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ef943-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="ef943-162">In deze sectie vindt u informatie over het beheer van ACL's en machtigingen met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ef943-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="ef943-163">Zie [Toegangsbeheer in Azure Data Lake Store](data-lake-store-access-control.md) voor gedetailleerde informatie over de implementatie van ACL's in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ef943-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="ef943-164">Gebruik de volgende opdracht als u **de eigenaar van een bestand/map wilt bijwerken**:</span><span class="sxs-lookup"><span data-stu-id="ef943-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ef943-165">Gebruik de volgende opdracht als u **de machtigingen voor een bestand/map wilt bijwerken**:</span><span class="sxs-lookup"><span data-stu-id="ef943-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="ef943-166">Gebruik de volgende opdracht als u **de ACL's voor een gegeven pad wilt ophalen**:</span><span class="sxs-lookup"><span data-stu-id="ef943-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="ef943-167">De uitvoer moet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="ef943-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="ef943-168">Gebruik de volgende opdracht als u **een item voor een ACL wilt instellen**:</span><span class="sxs-lookup"><span data-stu-id="ef943-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="ef943-169">Gebruik de volgende opdracht als u **een item voor een ACL wilt verwijderen**:</span><span class="sxs-lookup"><span data-stu-id="ef943-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ef943-170">Gebruik de volgende opdracht als u **een complete standaard-ACL wilt verwijderen**:</span><span class="sxs-lookup"><span data-stu-id="ef943-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="ef943-171">Gebruik de volgende opdracht als u **een complete niet-standaard-ACL wilt verwijderen**:</span><span class="sxs-lookup"><span data-stu-id="ef943-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="ef943-172">Een Data Lake Store-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="ef943-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="ef943-173">Gebruik de volgende opdracht om een Data Lake Store-account te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ef943-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="ef943-174">Wanneer dit wordt gevraagd, typt u **Y** om het account te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ef943-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef943-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef943-175">Next steps</span></span>

* [<span data-ttu-id="ef943-176">Naslaggegevens van Azure Data Lake Store CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef943-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="ef943-177">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="ef943-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ef943-178">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ef943-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ef943-179">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ef943-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
