---
title: aaaChange blobpad van de standaard Hallo | Microsoft Docs
description: Meer informatie over hoe tooset van een Azure functioneren toorename een blob-bestandspad (afgeschermd voorbeeld)
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
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="8fbf0-103">Wijzig het blobpad van een Hallo standaardpad (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="8fbf0-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="8fbf0-104">Dit artikel wordt beschreven hoe tooset van een Azure functioneren toorename een standaardpad voor blob.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8fbf0-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8fbf0-105">Prerequisites</span></span>

<span data-ttu-id="8fbf0-106">Zorg ervoor dat u de taakdefinitie van een die correct is geconfigureerd in de bron van een hybride gegevens binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="8fbf0-107">Een Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="8fbf0-107">Create an Azure function</span></span>

<span data-ttu-id="8fbf0-108">een Azure-functie toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="8fbf0-109">Ga toohello [Azure-portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8fbf0-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="8fbf0-110">Hallo boven aan het linkerdeelvenster hello, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="8fbf0-111">In Hallo **Search** in het vak **functie-App**, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Typ 'Functie-App' in het zoekvak Hallo](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="8fbf0-113">In Hallo **resultaten** lijst, klikt u op **functie-App**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-113">In hello **Results** list, click **Function App**.</span></span>

    ![Selecteer Hallo functie app resource in de lijst met resultaten Hallo](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="8fbf0-115">Hallo **functie-App** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="8fbf0-116">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-116">Click **Create**.</span></span>

    ![knop 'Maken' Hello functie-App-venster](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="8fbf0-118">Op Hallo **functie-App** configuratie blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="8fbf0-119">a.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-119">a.</span></span> <span data-ttu-id="8fbf0-120">In Hallo **appnaam** vak, type Hallo app-naam.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="8fbf0-121">b.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-121">b.</span></span> <span data-ttu-id="8fbf0-122">In Hallo **abonnement** vak, type Hallo-naam van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="8fbf0-123">c.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-123">c.</span></span> <span data-ttu-id="8fbf0-124">Onder **resourcegroep**, klikt u op **nieuw**, en vervolgens Hallo typenaam van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="8fbf0-125">d.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-125">d.</span></span> <span data-ttu-id="8fbf0-126">In Hallo **die als host fungeert van plan bent** in het vak **verbruik plannen**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="8fbf0-127">e.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-127">e.</span></span> <span data-ttu-id="8fbf0-128">In Hallo **locatie** vak type Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="8fbf0-129">f.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-129">f.</span></span> <span data-ttu-id="8fbf0-130">Onder **opslagaccount**, selecteer een bestaand opslagaccount of maak een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="8fbf0-131">Een opslagaccount wordt intern gebruikt voor Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-131">A storage account is used internally for hello function.</span></span>

    ![Voer de nieuwe functie-App-configuratiegegevens](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="8fbf0-133">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-133">Click **Create**.</span></span>  
    <span data-ttu-id="8fbf0-134">Hallo functie-app wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-134">hello function app is created.</span></span>

8. <span data-ttu-id="8fbf0-135">Klik in het linkerdeelvenster Hallo **meer services**, en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="8fbf0-136">a.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-136">a.</span></span> <span data-ttu-id="8fbf0-137">In Hallo **Filter** in het vak **App services**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="8fbf0-138">b.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-138">b.</span></span> <span data-ttu-id="8fbf0-139">Klik op **App Services**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-139">Click **App Services**.</span></span> 

    ![De koppeling 'Meer services' in het linkerdeelvenster Hallo](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="8fbf0-141">Klik op Hallo-naam van de functie-app Hallo in lijst Hallo van app-services.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="8fbf0-142">Hallo functie app-pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-142">hello function app page opens.</span></span>

10. <span data-ttu-id="8fbf0-143">Klik in het linkerdeelvenster Hallo **nieuwe functie**, en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="8fbf0-144">a.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-144">a.</span></span> <span data-ttu-id="8fbf0-145">In Hallo **taal** selecteert **C#**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="8fbf0-146">b.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-146">b.</span></span> <span data-ttu-id="8fbf0-147">Selecteer in het Hallo-matrix van sjabloon tegels, **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="8fbf0-148">c.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-148">c.</span></span> <span data-ttu-id="8fbf0-149">In Hallo **naam van de functie** typt u een naam voor de functie.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="8fbf0-150">d.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-150">d.</span></span> <span data-ttu-id="8fbf0-151">In Hallo **wachtrijnaam** typt u de naam van uw data transformation taak definitie.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="8fbf0-152">e.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-152">e.</span></span> <span data-ttu-id="8fbf0-153">Onder **Storage-account verbinding**, klikt u op **nieuwe**, en selecteer vervolgens Hallo-account dat overeenkomt met toohello gegevenstransformatie taak.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="8fbf0-154">Noteer de naam van de verbinding Hallo.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-154">Make a note of hello connection name.</span></span> <span data-ttu-id="8fbf0-155">Hallo naam is verderop in hello Azure-functie vereist.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-155">hello name is required later in hello Azure function.</span></span>

       ![Maak een nieuwe C#-functie](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="8fbf0-157">f.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-157">f.</span></span> <span data-ttu-id="8fbf0-158">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-158">Click **Create**.</span></span>  
    <span data-ttu-id="8fbf0-159">Hallo **functie** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="8fbf0-160">In Hallo **functie** venster uitvoeren _.csx_ -bestand en vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="8fbf0-161">a.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-161">a.</span></span> <span data-ttu-id="8fbf0-162">Plak Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-162">Paste hello following code:</span></span>

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

        // Create hello blob client.
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
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
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

    <span data-ttu-id="8fbf0-163">b.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-163">b.</span></span> <span data-ttu-id="8fbf0-164">Vervang **STORAGE_CONNECTIONNAME** op regel 11 met de storage-account verbinding (Zie punt 8 c).</span><span class="sxs-lookup"><span data-stu-id="8fbf0-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="8fbf0-165">c.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-165">c.</span></span> <span data-ttu-id="8fbf0-166">Klik boven Hallo links op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-166">At hello top left, click **Save**.</span></span>

    ![De functie opslaan](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="8fbf0-168">toocomplete Hallo functie, één meer bestand toevoegen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="8fbf0-169">a.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-169">a.</span></span> <span data-ttu-id="8fbf0-170">Klik op **bestanden bekijken**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-170">Click **View files**.</span></span>

       ![Hallo 'Bestanden weergeven' koppeling](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="8fbf0-172">b.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-172">b.</span></span> <span data-ttu-id="8fbf0-173">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-173">Click **Add**.</span></span>
    
    <span data-ttu-id="8fbf0-174">c.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-174">c.</span></span> <span data-ttu-id="8fbf0-175">Type **project.json**, en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="8fbf0-176">d.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-176">d.</span></span> <span data-ttu-id="8fbf0-177">In Hallo **project.json** bestand, plak Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="8fbf0-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="8fbf0-178">e.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-178">e.</span></span> <span data-ttu-id="8fbf0-179">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-179">Click **Save**.</span></span>

<span data-ttu-id="8fbf0-180">U hebt een Azure-functie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-180">You have created an Azure function.</span></span> <span data-ttu-id="8fbf0-181">Deze functie wordt telkens wanneer die een nieuwe blob wordt gegenereerd door Hallo gegevenstransformatie taak geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8fbf0-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fbf0-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fbf0-182">Next steps</span></span>

[<span data-ttu-id="8fbf0-183">Uw gegevens StorSimple Data Manager UI tootransform gebruiken</span><span class="sxs-lookup"><span data-stu-id="8fbf0-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
