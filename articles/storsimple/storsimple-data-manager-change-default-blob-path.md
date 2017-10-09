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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Wijzig het blobpad van een Hallo standaardpad (afgeschermd voorbeeld)

Dit artikel wordt beschreven hoe tooset van een Azure functioneren toorename een standaardpad voor blob. 

## <a name="prerequisites"></a>Vereisten

Zorg ervoor dat u de taakdefinitie van een die correct is geconfigureerd in de bron van een hybride gegevens binnen een resourcegroep.

## <a name="create-an-azure-function"></a>Een Azure-functie maken

een Azure-functie toocreate Hallo te volgen:

1. Ga toohello [Azure-portal](http://portal.azure.com/).

2. Hallo boven aan het linkerdeelvenster hello, klikt u op **nieuw**. 

3. In Hallo **Search** in het vak **functie-App**, en druk op Enter.

    ![Typ 'Functie-App' in het zoekvak Hallo](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. In Hallo **resultaten** lijst, klikt u op **functie-App**.

    ![Selecteer Hallo functie app resource in de lijst met resultaten Hallo](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Hallo **functie-App** venster wordt geopend.

5. Klik op **Create**.

    ![knop 'Maken' Hello functie-App-venster](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Op Hallo **functie-App** configuratie blade Hallo te volgen:

    a. In Hallo **appnaam** vak, type Hallo app-naam.
    
    b. In Hallo **abonnement** vak, type Hallo-naam van het Hallo-abonnement.

    c. Onder **resourcegroep**, klikt u op **nieuw**, en vervolgens Hallo typenaam van de resourcegroep Hallo.

    d. In Hallo **die als host fungeert van plan bent** in het vak **verbruik plannen**.

    e. In Hallo **locatie** vak type Hallo locatie.

    f. Onder **opslagaccount**, selecteer een bestaand opslagaccount of maak een nieuw opslagaccount. Een opslagaccount wordt intern gebruikt voor Hallo-functie.

    ![Voer de nieuwe functie-App-configuratiegegevens](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Klik op **Create**.  
    Hallo functie-app wordt gemaakt.

8. Klik in het linkerdeelvenster Hallo **meer services**, en vervolgens Hallo te volgen:
    
    a. In Hallo **Filter** in het vak **App services**.
    
    b. Klik op **App Services**. 

    ![De koppeling 'Meer services' in het linkerdeelvenster Hallo](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Klik op Hallo-naam van de functie-app Hallo in lijst Hallo van app-services.  
    Hallo functie app-pagina wordt geopend.

10. Klik in het linkerdeelvenster Hallo **nieuwe functie**, en vervolgens Hallo te volgen: 

    a. In Hallo **taal** selecteert **C#**.
    
    b. Selecteer in het Hallo-matrix van sjabloon tegels, **QueueTrigger CSharp**.

    c. In Hallo **naam van de functie** typt u een naam voor de functie.

    d. In Hallo **wachtrijnaam** typt u de naam van uw data transformation taak definitie.

    e. Onder **Storage-account verbinding**, klikt u op **nieuwe**, en selecteer vervolgens Hallo-account dat overeenkomt met toohello gegevenstransformatie taak.  
        Noteer de naam van de verbinding Hallo. Hallo naam is verderop in hello Azure-functie vereist.

       ![Maak een nieuwe C#-functie](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Klik op **Create**.  
    Hallo **functie** venster wordt geopend.

11. In Hallo **functie** venster uitvoeren _.csx_ -bestand en vervolgens Hallo te volgen:

    a. Plak Hallo code te volgen:

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

    b. Vervang **STORAGE_CONNECTIONNAME** op regel 11 met de storage-account verbinding (Zie punt 8 c).

    c. Klik boven Hallo links op **opslaan**.

    ![De functie opslaan](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete Hallo functie, één meer bestand toevoegen door Hallo volgende te doen:

    a. Klik op **bestanden bekijken**.

       ![Hallo 'Bestanden weergeven' koppeling](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Klik op **Add**.
    
    c. Type **project.json**, en druk op Enter.
    
    d. In Hallo **project.json** bestand, plak Hallo code te volgen:

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

    e. Klik op **Opslaan**.

U hebt een Azure-functie gemaakt. Deze functie wordt telkens wanneer die een nieuwe blob wordt gegenereerd door Hallo gegevenstransformatie taak geactiveerd.

## <a name="next-steps"></a>Volgende stappen

[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md)
