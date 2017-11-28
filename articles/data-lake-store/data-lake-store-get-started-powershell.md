---
title: aaaUse PowerShell tooget de slag met Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure PowerShell toocreate een Data Lake Store-account en basisbewerkingen uit te voeren
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="4ec47-103">Aan de slag met Azure Data Lake Store met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ec47-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ec47-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4ec47-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="4ec47-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ec47-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="4ec47-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="4ec47-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="4ec47-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="4ec47-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="4ec47-108">REST API</span><span class="sxs-lookup"><span data-stu-id="4ec47-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="4ec47-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4ec47-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="4ec47-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="4ec47-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="4ec47-111">Python</span><span class="sxs-lookup"><span data-stu-id="4ec47-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="4ec47-112">Meer informatie over hoe toouse Azure PowerShell toocreate een Azure Data Lake opslaan account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ec47-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ec47-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4ec47-113">Prerequisites</span></span>
<span data-ttu-id="4ec47-114">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="4ec47-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="4ec47-115">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-115">**An Azure subscription**.</span></span> <span data-ttu-id="4ec47-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ec47-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4ec47-117">**Azure PowerShell 1.0 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="4ec47-118">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ec47-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="4ec47-119">Authentication</span><span class="sxs-lookup"><span data-stu-id="4ec47-119">Authentication</span></span>
<span data-ttu-id="4ec47-120">Dit artikel wordt het eenvoudiger voor verificatie met Data Lake Store waar u zich na vragen aan gebruiker tooenter de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4ec47-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="4ec47-121">Hallo toegang niveau tooData Lake Store-account en een nieuw bestandssysteem vervolgens beheerst door het toegangsniveau Hallo Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4ec47-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="4ec47-122">Er zijn echter andere benaderingen als goed tooauthenticate met Data Lake Store, die zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4ec47-123">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4ec47-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="4ec47-124">Een Azure Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="4ec47-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="4ec47-125">Op het bureaublad een nieuw Windows PowerShell-venster openen Hallo volgende codefragment toolog in tooyour Azure-account invoeren, ingesteld Hallo-abonnement en Hallo Data Lake Store-provider geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4ec47-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="4ec47-126">Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een Hallo abonnement beheerders/eigenaars:</span><span class="sxs-lookup"><span data-stu-id="4ec47-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="4ec47-127">Een Azure Data Lake Store-account is gekoppeld aan een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4ec47-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="4ec47-128">Maak daarom eerst een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4ec47-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="4ec47-129">![Een Azure-resourcegroep maken](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Een Azure-resourcegroep maken")</span><span class="sxs-lookup"><span data-stu-id="4ec47-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="4ec47-130">Maak een Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="4ec47-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="4ec47-131">Hallo-naam die u opgeeft mag alleen kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="4ec47-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="4ec47-132">![Een Azure Data Lake Store-account maken](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Een Azure Data Lake Store-account maken")</span><span class="sxs-lookup"><span data-stu-id="4ec47-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="4ec47-133">Controleer of Hallo-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ec47-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="4ec47-134">Hallo uitvoer voor dit mag **True**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="4ec47-135">Mapstructuren maken in uw Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ec47-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="4ec47-136">U kunt mappen maken onder uw Azure Data Lake Store-account toomanage en opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ec47-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="4ec47-137">Geef een hoofdmap op.</span><span class="sxs-lookup"><span data-stu-id="4ec47-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="4ec47-138">Maak een nieuwe map aangeroepen **mynewdirectory** onder Hallo opgegeven toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="4ec47-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="4ec47-139">Controleer of dat nieuwe map Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ec47-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="4ec47-140">Hallo volgende uitvoer moet worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ec47-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="4ec47-141">![Map controleren](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Map controleren")</span><span class="sxs-lookup"><span data-stu-id="4ec47-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="4ec47-142">Uploaden van gegevens tooyour Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ec47-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="4ec47-143">U kunt uw data Lake Store van de tooData rechtstreeks op Hallo niveau of tooa hoofdmap die u hebt gemaakt in Hallo account uploaden.</span><span class="sxs-lookup"><span data-stu-id="4ec47-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="4ec47-144">Hallo codefragmenten hieronder laten zien hoe tooupload enkele voorbeeld-gegevensmap toohello (**mynewdirectory**) u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ec47-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="4ec47-145">Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="4ec47-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="4ec47-146">Hallo-bestand downloaden en opslaan in een lokale map op uw computer, zoals C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="4ec47-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="4ec47-147">Gegevens in uw Data Lake Store een nieuwe naam geven, downloaden en verwijderen</span><span class="sxs-lookup"><span data-stu-id="4ec47-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="4ec47-148">toorename een bestand Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4ec47-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="4ec47-149">toodownload een bestand Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4ec47-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="4ec47-150">toodelete een bestand Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4ec47-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="4ec47-151">Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo item.</span><span class="sxs-lookup"><span data-stu-id="4ec47-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="4ec47-152">Als u meer dan één bestand toodelete hebt, kunt u opgeven dat alle Hallo paden, gescheiden door een komma.</span><span class="sxs-lookup"><span data-stu-id="4ec47-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="4ec47-153">Uw Azure Data Lake Store-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="4ec47-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="4ec47-154">Hallo opdracht toodelete na uw Data Lake Store-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ec47-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="4ec47-155">Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="4ec47-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="4ec47-156">Prestatierichtlijnen bij het gebruik van PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ec47-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="4ec47-157">Hieronder vindt Hallo meest belangrijke instellingen die afgestemd tooget Hallo optimale prestaties worden kunnen tijdens het gebruik van PowerShell toowork met Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="4ec47-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="4ec47-158">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4ec47-158">Property</span></span>            | <span data-ttu-id="4ec47-159">Standaard</span><span class="sxs-lookup"><span data-stu-id="4ec47-159">Default</span></span> | <span data-ttu-id="4ec47-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4ec47-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="4ec47-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="4ec47-161">PerFileThreadCount</span></span>  | <span data-ttu-id="4ec47-162">10</span><span class="sxs-lookup"><span data-stu-id="4ec47-162">10</span></span>      | <span data-ttu-id="4ec47-163">Deze parameter kunt u toochoose Hallo aantal parallelle threads voor uploaden of elk bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="4ec47-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="4ec47-164">Dit nummer geeft Hallo max threads dat kunnen worden verdeeld per bestand, maar krijgt u mogelijk minder threads, afhankelijk van uw scenario (bijvoorbeeld als u een 1 KB-bestand uploadt, krijgt u één thread zelfs als u voor 20 threads vragen).</span><span class="sxs-lookup"><span data-stu-id="4ec47-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="4ec47-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="4ec47-165">ConcurrentFileCount</span></span> | <span data-ttu-id="4ec47-166">10</span><span class="sxs-lookup"><span data-stu-id="4ec47-166">10</span></span>      | <span data-ttu-id="4ec47-167">Deze parameter is specifiek bedoeld voor het uploaden en downloaden van mappen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="4ec47-168">Deze parameter bepaalt het aantal gelijktijdige bestanden die kunnen worden geüpload of gedownload Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ec47-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="4ec47-169">Dit aantal geeft Hallo kunt u het maximum aantal gelijktijdige bestanden die kunnen worden geüpload of in één keer worden gedownload, maar krijgt u mogelijk minder gelijktijdigheid, afhankelijk van uw scenario (bijvoorbeeld als u twee bestanden uploaden wilt, krijgt u twee gelijktijdige bestandsuploads zelfs als u vragen 15).</span><span class="sxs-lookup"><span data-stu-id="4ec47-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="4ec47-170">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="4ec47-170">**Example**</span></span>

<span data-ttu-id="4ec47-171">Met deze opdracht downloadt bestanden van de lokale schijf van Azure Data Lake Store toohello gebruiker met 20 threads per bestand en 100 gelijktijdige bestanden.</span><span class="sxs-lookup"><span data-stu-id="4ec47-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="4ec47-172">Hoe bepaal ik Hallo waarde tooset voor deze parameters</span><span class="sxs-lookup"><span data-stu-id="4ec47-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="4ec47-173">Hier volgen een aantal richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="4ec47-174">**Stap 1: Bepalen Hallo totale aantal threads** -door berekenen Hallo thread totale aantal toouse moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="4ec47-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="4ec47-175">Een algemene richtlijn is 6 threads voor elke fysieke kern.</span><span class="sxs-lookup"><span data-stu-id="4ec47-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="4ec47-176">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="4ec47-176">**Example**</span></span>

    <span data-ttu-id="4ec47-177">Ervan uitgaande dat u uitvoert Hallo PowerShell-opdrachten van een VM D14 die 16 kernen heeft</span><span class="sxs-lookup"><span data-stu-id="4ec47-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="4ec47-178">**Stap 2: Berekenen PerFileThreadCount** -We onze PerFileThreadCount op basis van Hallo grootte van bestanden Hallo berekenen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="4ec47-179">Voor bestanden die kleiner zijn dan 2,5 GB is er geen toochange moet deze parameter omdat Hallo standaardwaarde van 10 voldoende is.</span><span class="sxs-lookup"><span data-stu-id="4ec47-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="4ec47-180">Voor bestanden groter zijn dan 2,5 GB, moet u 10 threads terwijl Hallo basis voor de eerste 2,5 GB Hallo en 1-thread voor elke extra 256 MB toename bestandsgrootte toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4ec47-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="4ec47-181">Als u een map kopieert met bestanden van zeer verschillende groottes, kunt u overwegen ze op vergelijkbare grootte te sorteren.</span><span class="sxs-lookup"><span data-stu-id="4ec47-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="4ec47-182">Grote verschillen in bestandsgroottes kunnen tot slechtere prestaties leiden.</span><span class="sxs-lookup"><span data-stu-id="4ec47-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="4ec47-183">Als dat niet mogelijk toogroup vergelijkbare bestandsgrootten, moet u PerFileThreadCount op basis van de maximale bestandsgrootte Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="4ec47-184">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="4ec47-184">**Example**</span></span>

    <span data-ttu-id="4ec47-185">Als er 100 bestanden variëren van 1GB too10GB, gebruiken we Hallo 10GB als Hallo grootste bestandsgrootte voor vergelijking, welke Hallo volgende zou lezen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="4ec47-186">**Stap 3: Berekenen ConcurrentFilecount** -gebruik Hallo totale aantal threads en PerFileThreadCount toocalculate ConcurrentFileCount op basis van Hallo volgende vergelijking.</span><span class="sxs-lookup"><span data-stu-id="4ec47-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="4ec47-187">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="4ec47-187">**Example**</span></span>

    <span data-ttu-id="4ec47-188">Op basis van voorbeeldwaarden Hallo die we hebt gebruikt</span><span class="sxs-lookup"><span data-stu-id="4ec47-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="4ec47-189">Dus **ConcurrentFileCount** is **2.4**, die we te kunnen afronden**2**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="4ec47-190">Verder afstemmen</span><span class="sxs-lookup"><span data-stu-id="4ec47-190">Further tuning</span></span>

<span data-ttu-id="4ec47-191">U wordt mogelijk verder afstemmen omdat er een bereik van het bestand grootten toowork met.</span><span class="sxs-lookup"><span data-stu-id="4ec47-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="4ec47-192">Hallo hierboven berekening werkt goed als alle of de meeste van Hallo bestanden groter en dichter toohello 10GB bereik zijn.</span><span class="sxs-lookup"><span data-stu-id="4ec47-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="4ec47-193">Als het echter bestanden van zeer uiteenlopende groottes betreft, waarbij veel bestanden kleiner zijn, kunt u de PerFileThreadCount verlagen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="4ec47-194">Hallo PerFileThreadCount verlaagt, kunnen we ConcurrentFileCount verhogen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="4ec47-195">Dus als gaan we ervan uit dat de meeste van de bestanden zijn kleiner Hallo 5GB bereik, kunnen we doen opnieuw onze berekening:</span><span class="sxs-lookup"><span data-stu-id="4ec47-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="4ec47-196">Dus **ConcurrentFileCount** wordt nu 96/20, namelijk 4.8 afgerond te**4**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="4ec47-197">U kunt tootune deze instellingen gaan door het wijzigen van Hallo **PerFileThreadCount** omhoog en omlaag afhankelijk van Hallo distributie van de bestandsgrootte.</span><span class="sxs-lookup"><span data-stu-id="4ec47-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="4ec47-198">Beperking</span><span class="sxs-lookup"><span data-stu-id="4ec47-198">Limitation</span></span>

* <span data-ttu-id="4ec47-199">**Aantal bestanden is kleiner dan ConcurrentFileCount**: als het aantal bestanden die u uploadt Hallo kleiner dan Hallo is **ConcurrentFileCount** die u hebt berekend vervolgens minder  **ConcurrentFileCount** toobe gelijk toohello aantal bestanden.</span><span class="sxs-lookup"><span data-stu-id="4ec47-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="4ec47-200">Kunt u eventuele resterende threads tooincrease **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="4ec47-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="4ec47-201">**Te veel threads**: als u thread verhogen tellen te veel zonder te verhogen van de clustergrootte van uw, loopt u verminderde prestaties Hallo risico.</span><span class="sxs-lookup"><span data-stu-id="4ec47-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="4ec47-202">Kunnen er conflicten problemen bij het context overschakelen op Hallo CPU.</span><span class="sxs-lookup"><span data-stu-id="4ec47-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="4ec47-203">**Onvoldoende gelijktijdigheid**: als Hallo gelijktijdigheid niet voldoende is, wordt het cluster is mogelijk te klein.</span><span class="sxs-lookup"><span data-stu-id="4ec47-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="4ec47-204">U kunt Hallo aantal knooppunten in uw cluster zodat u meer gelijktijdige uitvoering verhogen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="4ec47-205">**Beperkingsfouten**: er treden mogelijk beperkingsfouten op als uw gelijktijdigheid te hoog is.</span><span class="sxs-lookup"><span data-stu-id="4ec47-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="4ec47-206">Als u beperking fouten ziet, moet u beperkt Hallo of contact met ons opnemen.</span><span class="sxs-lookup"><span data-stu-id="4ec47-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec47-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ec47-207">Next steps</span></span>
* [<span data-ttu-id="4ec47-208">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="4ec47-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4ec47-209">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ec47-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4ec47-210">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ec47-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

