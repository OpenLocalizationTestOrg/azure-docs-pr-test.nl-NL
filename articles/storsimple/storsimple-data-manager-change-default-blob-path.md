---
title: Blob-pad van de standaardwaarde wijzigen | Microsoft Docs
description: Meer informatie over het instellen van een Azure-functie naam wijzigen van een blob-bestandspad (afgeschermd voorbeeld)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="f15c7-103">Wijzig het blobpad van een het standaardpad (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="f15c7-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="f15c7-104">In dit artikel wordt beschreven hoe een Azure-functie instellen voor het wijzigen van een standaard blob-bestandspad.</span><span class="sxs-lookup"><span data-stu-id="f15c7-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f15c7-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f15c7-105">Prerequisites</span></span>

<span data-ttu-id="f15c7-106">Zorg ervoor dat u de taakdefinitie van een die correct is geconfigureerd in de bron van een hybride gegevens binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f15c7-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="f15c7-107">Een Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="f15c7-107">Create an Azure function</span></span>

<span data-ttu-id="f15c7-108">Voor het maken van een Azure-functie, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f15c7-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="f15c7-109">Ga naar de [Azure Portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f15c7-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="f15c7-110">Klik boven in het linkerdeelvenster op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="f15c7-111">In de **Search** in het vak **functie-App**, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="f15c7-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Typ 'Functie-App' in het vak Zoeken](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="f15c7-113">In de **resultaten** lijst, klikt u op **functie-App**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-113">In the **Results** list, click **Function App**.</span></span>

    ![Selecteer een resource voor de functie-app in de lijst met resultaten](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="f15c7-115">De **functie-App** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f15c7-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="f15c7-116">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-116">Click **Create**.</span></span>

    ![De knop functie-App venster 'Maken'](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="f15c7-118">Op de **functie-App** blade van de configuratie van de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="f15c7-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="f15c7-119">a.</span><span class="sxs-lookup"><span data-stu-id="f15c7-119">a.</span></span> <span data-ttu-id="f15c7-120">In de **appnaam** typt u de appnaam.</span><span class="sxs-lookup"><span data-stu-id="f15c7-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="f15c7-121">b.</span><span class="sxs-lookup"><span data-stu-id="f15c7-121">b.</span></span> <span data-ttu-id="f15c7-122">In de **abonnement** typt u de naam van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="f15c7-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="f15c7-123">c.</span><span class="sxs-lookup"><span data-stu-id="f15c7-123">c.</span></span> <span data-ttu-id="f15c7-124">Onder **resourcegroep**, klikt u op **nieuw**, en typ vervolgens de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f15c7-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="f15c7-125">d.</span><span class="sxs-lookup"><span data-stu-id="f15c7-125">d.</span></span> <span data-ttu-id="f15c7-126">In de **die als host fungeert van plan bent** in het vak **verbruik plannen**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="f15c7-127">e.</span><span class="sxs-lookup"><span data-stu-id="f15c7-127">e.</span></span> <span data-ttu-id="f15c7-128">In de **locatie** typt u de locatie.</span><span class="sxs-lookup"><span data-stu-id="f15c7-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="f15c7-129">f.</span><span class="sxs-lookup"><span data-stu-id="f15c7-129">f.</span></span> <span data-ttu-id="f15c7-130">Onder **opslagaccount**, selecteer een bestaand opslagaccount of maak een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f15c7-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="f15c7-131">Een opslagaccount wordt intern gebruikt voor de functie.</span><span class="sxs-lookup"><span data-stu-id="f15c7-131">A storage account is used internally for the function.</span></span>

    ![Voer de nieuwe functie-App-configuratiegegevens](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="f15c7-133">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-133">Click **Create**.</span></span>  
    <span data-ttu-id="f15c7-134">De functie-app wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f15c7-134">The function app is created.</span></span>

8. <span data-ttu-id="f15c7-135">Klik in het linkerdeelvenster op **meer services**, en vervolgens de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="f15c7-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="f15c7-136">a.</span><span class="sxs-lookup"><span data-stu-id="f15c7-136">a.</span></span> <span data-ttu-id="f15c7-137">In de **Filter** in het vak **App services**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="f15c7-138">b.</span><span class="sxs-lookup"><span data-stu-id="f15c7-138">b.</span></span> <span data-ttu-id="f15c7-139">Klik op **App Services**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-139">Click **App Services**.</span></span> 

    ![De koppeling 'Meer services' in het linkerdeelvenster](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="f15c7-141">Klik op de naam van de functie-app in de lijst van app-services.</span><span class="sxs-lookup"><span data-stu-id="f15c7-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="f15c7-142">De functie app-pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f15c7-142">The function app page opens.</span></span>

10. <span data-ttu-id="f15c7-143">Klik in het linkerdeelvenster op **nieuwe functie**, en vervolgens de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="f15c7-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="f15c7-144">a.</span><span class="sxs-lookup"><span data-stu-id="f15c7-144">a.</span></span> <span data-ttu-id="f15c7-145">In de **taal** selecteert **C#**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="f15c7-146">b.</span><span class="sxs-lookup"><span data-stu-id="f15c7-146">b.</span></span> <span data-ttu-id="f15c7-147">Selecteer in de matrix van sjabloon tegels **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="f15c7-148">c.</span><span class="sxs-lookup"><span data-stu-id="f15c7-148">c.</span></span> <span data-ttu-id="f15c7-149">In de **naam van de functie** typt u een naam voor de functie.</span><span class="sxs-lookup"><span data-stu-id="f15c7-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="f15c7-150">d.</span><span class="sxs-lookup"><span data-stu-id="f15c7-150">d.</span></span> <span data-ttu-id="f15c7-151">In de **wachtrijnaam** typt u de naam van uw data transformation taak definitie.</span><span class="sxs-lookup"><span data-stu-id="f15c7-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="f15c7-152">e.</span><span class="sxs-lookup"><span data-stu-id="f15c7-152">e.</span></span> <span data-ttu-id="f15c7-153">Onder **Storage-account verbinding**, klikt u op **nieuwe**, en selecteer vervolgens het account dat overeenkomt met de taak gegevens transformatie.</span><span class="sxs-lookup"><span data-stu-id="f15c7-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="f15c7-154">Noteer de naam van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="f15c7-154">Make a note of the connection name.</span></span> <span data-ttu-id="f15c7-155">De naam van de is later in de Azure-functie vereist.</span><span class="sxs-lookup"><span data-stu-id="f15c7-155">The name is required later in the Azure function.</span></span>

       ![Maak een nieuwe C#-functie](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="f15c7-157">f.</span><span class="sxs-lookup"><span data-stu-id="f15c7-157">f.</span></span> <span data-ttu-id="f15c7-158">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-158">Click **Create**.</span></span>  
    <span data-ttu-id="f15c7-159">De **functie** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f15c7-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="f15c7-160">In de **functie** venster uitvoeren _.csx_ bestand en voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="f15c7-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="f15c7-161">a.</span><span class="sxs-lookup"><span data-stu-id="f15c7-161">a.</span></span> <span data-ttu-id="f15c7-162">Plak de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f15c7-162">Paste the following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create the blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="f15c7-163">b.</span><span class="sxs-lookup"><span data-stu-id="f15c7-163">b.</span></span> <span data-ttu-id="f15c7-164">Vervang **STORAGE_CONNECTIONNAME** op regel 11 met de storage-account verbinding (Zie punt 8 c).</span><span class="sxs-lookup"><span data-stu-id="f15c7-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="f15c7-165">c.</span><span class="sxs-lookup"><span data-stu-id="f15c7-165">c.</span></span> <span data-ttu-id="f15c7-166">Klik linksboven, **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-166">At the top left, click **Save**.</span></span>

    ![De functie opslaan](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="f15c7-168">Voor het voltooien van de functie toevoegen één meer bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="f15c7-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="f15c7-169">a.</span><span class="sxs-lookup"><span data-stu-id="f15c7-169">a.</span></span> <span data-ttu-id="f15c7-170">Klik op **bestanden bekijken**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-170">Click **View files**.</span></span>

       ![De koppeling 'Bestanden weergeven'](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="f15c7-172">b.</span><span class="sxs-lookup"><span data-stu-id="f15c7-172">b.</span></span> <span data-ttu-id="f15c7-173">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-173">Click **Add**.</span></span>
    
    <span data-ttu-id="f15c7-174">c.</span><span class="sxs-lookup"><span data-stu-id="f15c7-174">c.</span></span> <span data-ttu-id="f15c7-175">Type **project.json**, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="f15c7-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="f15c7-176">d.</span><span class="sxs-lookup"><span data-stu-id="f15c7-176">d.</span></span> <span data-ttu-id="f15c7-177">In de **project.json** bestand, plak de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f15c7-177">In the **project.json** file, paste the following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="f15c7-178">e.</span><span class="sxs-lookup"><span data-stu-id="f15c7-178">e.</span></span> <span data-ttu-id="f15c7-179">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f15c7-179">Click **Save**.</span></span>

<span data-ttu-id="f15c7-180">U hebt een Azure-functie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f15c7-180">You have created an Azure function.</span></span> <span data-ttu-id="f15c7-181">Deze functie wordt telkens wanneer die een nieuwe blob wordt gegenereerd door de taak Gegevenstransformatie geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="f15c7-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f15c7-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f15c7-182">Next steps</span></span>

[<span data-ttu-id="f15c7-183">Gebruik StorSimple Data Manager UI om uw gegevens te transformeren</span><span class="sxs-lookup"><span data-stu-id="f15c7-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
