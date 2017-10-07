---
title: aaaUsing Azure PowerShell gebruiken met Azure Storage | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure PowerShell-cmdlets voor Azure Storage toocreate en beheren van opslagaccounts; werken met blobs, tabellen, wachtrijen en bestanden. configureren en storage analytics query en handtekeningen voor gedeelde toegang maken.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Azure PowerShell gebruiken met Azure Storage
## <a name="overview"></a>Overzicht
Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt. Het is een op taken gebaseerde opdrachtregelshell en scripttaal die speciaal is ontworpen voor systeembeheer. Met PowerShell, kunt u eenvoudig beheren en automatiseren Hallo beheer van uw Azure-services en toepassingen. Bijvoorbeeld, kunt u Hallo cmdlets tooperform Hallo dezelfde taken kunt u uitvoeren via Hallo [Azure-portal](https://portal.azure.com).

In deze handleiding wordt besproken hoe toouse hello [Azure-opslag-Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform tal van ontwikkeling en het beheer van taken met Azure Storage.

Deze handleiding wordt ervan uitgegaan dat u ervaring met behulp van [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) en [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Hallo handleiding biedt een aantal scripts toodemonstrate Hallo informatie over het gebruik van PowerShell met Azure Storage. Hallo scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd, moet u bijwerken.

de eerste sectie Hallo in deze handleiding biedt een kijkje Azure Storage en PowerShell. Voor gedetailleerde informatie en instructies starten vanuit Hallo [vereisten voor het gebruik van Azure PowerShell met Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Aan de slag met Azure Storage en PowerShell in vijf minuten
Deze sectie leest u hoe tooaccess Azure Storage via PowerShell in vijf minuten.

**Nieuwe tooAzure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement. Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).

Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.

**Na het maken van een Microsoft Azure-abonnement en -account:**

1. Download en installeer Hallo nieuwste [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Start Windows PowerShell Integrated Scripting Environment (ISE): Ga In uw lokale computer toohello **Start** menu. Type **Systeembeheer** en toorun op deze. In Hallo **Systeembeheer** venster met de rechtermuisknop op **Windows PowerShell ISE**, klikt u op **als Administrator uitvoeren**.
3. In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** toocreate een nieuwe scriptbestand.
4. Nu geven we u een eenvoudig script waarin basic PowerShell-opdrachten tooaccess Azure Storage. Hallo script vraagt uw Azure-account referenties tooadd eerst uw Azure-account toohello lokale PowerShell-omgeving. Hallo-script wordt vervolgens Hallo standaard Azure-abonnement instellen en een nieuw opslagaccount maken in Azure. Hallo-script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaande installatiekopie-bestand (blob) toothat container. Nadat het Hallo-script geeft een lijst van alle blobs in de container, worden een nieuwe bestemming-map maken in uw lokale computer en Hallo installatiekopiebestand downloaden.
5. Selecteer in de Hallo volgende sectie code, Hallo script tussen Opmerking Hallo **#beginnen** en **#end**. Druk op CTRL + C toocopy het toohello Klembord.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. In **Windows PowerShell ISE**, druk op CTRL + V toocopy Hallo script. Klik op **bestand** > **opslaan**. In Hallo **OpslaanAls** dialoogvenster, Hallo-typenaam van Hallo scriptbestand, zoals 'mystoragescript'. Klik op **Opslaan**.
7. U moet nu tooupdate Hallo scriptvariabelen op basis van uw configuratie-instellingen. U moet bijwerken Hallo **$SubscriptionName** variabele met uw eigen abonnement. U kunt behouden Hallo andere variabelen zoals opgegeven in het Hallo-script of deze als u wilt bijwerken.
   
   * **$SubscriptionName:** moet u deze variabele bijwerken met de naam van uw eigen abonnement. Voer een van de Hallo drie manieren toolocate Hallo naam van uw abonnement te volgen:
     
    a. In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** toocreate een nieuwe scriptbestand. Kopiëren Hallo hieronder nieuwe scriptbestand toohello script en klik **Debug** > **uitvoeren**. Hallo volgende script wordt eerst vraagt u uw Azure-account referenties tooadd uw Azure-account toohello lokale PowerShell-omgeving en alle Hallo-abonnementen die verbonden toohello lokale PowerShell-sessie zijn wordt weergegeven. Noteer Hallo-naam van het Hallo-abonnement dat u wilt dat toouse tijdens deze zelfstudie te volgen:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate en kopieert u uw abonnement een naam in Hallo [Azure-portal](https://portal.azure.com), Hallo Hub-menu op Hallo links in, klik op **abonnementen**. Hallo-naam van het abonnement dat u tijdens het uitvoeren van scripts Hallo in deze handleiding toouse wilt kopiëren.
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate en kopieert u uw abonnement een naam in Hallo [klassieke Azure-Portal](https://manage.windowsazure.com/), schuif naar beneden en klik op **instellingen** op Hallo linkerkant van Hallo-portal. Klik op **abonnementen** toosee een lijst van uw abonnementen. Hallo-naam van het abonnement dat u toouse tijdens het uitvoeren van Hallo-scripts die zijn opgegeven in deze handleiding wilt kopiëren.
     
     ![Klassieke Azure-portal](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor uw opslagaccount. **Belangrijk:** Hallo-naam van Hallo opslagaccount moet uniek zijn in Azure. Er moet een kleine letter, te!
   * **$Location:** Hallo 'VS-West' opgegeven in Hallo script gebruiken of kies andere Azure locaties, zoals VS-Oost, Noord-Europa, enzovoort.
   * **$ContainerName:** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor de container.
   * **$ImageToUpload:** Voer een pad tooa afbeelding op uw lokale computer, zoals: 'C:\Images\HelloWorld.png'.
   * **$DestinationFolder:** Enter een pad tooa lokale directory toostore bestanden gedownload van Azure Storage, zoals: 'C:\DownloadImages'.
8. Klik na het bijwerken van Hallo scriptvariabelen in Hallo 'mystoragescript.ps1' bestand **bestand** > **opslaan**. Klik vervolgens op **Debug** > **uitvoeren** of druk op **F5** toorun Hallo script.  

Nadat het Hallo-script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben. Hallo volgende schermafbeelding ziet u een voorbeeld van uitvoer:

![Blobs downloaden](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hallo "Aan de slag met Azure Storage en PowerShell in vijf minuten" sectie opgegeven een korte inleiding voor het toouse Azure PowerShell gebruiken met Azure Storage. Voor gedetailleerde informatie en instructies raden we u tooread Hallo uit te voeren.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Vereisten voor het gebruik van Azure PowerShell met Azure Storage
U moet een Azure-abonnement en account toorun Hallo PowerShell-cmdlets die in deze handleiding, zoals hierboven is beschreven.

Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt. Zie voor meer informatie over het installeren en instellen van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). U wordt aangeraden dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello voordat u deze handleiding.

U kunt Hallo-cmdlets uitvoeren in Hallo Windows PowerShell-console of Hallo Windows PowerShell Integrated Scripting Environment (ISE). Bijvoorbeeld: tooopen **Windows PowerShell ISE**toohello startmenu gaat, typt u Systeembeheer en toorun op deze. Hallo-beheerprogramma's-venster met de rechtermuisknop op Windows PowerShell ISE, klikt u op als Administrator uitvoeren.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Hoe toomanage opslagaccounts in Azure

We gaan verdiepen in de storage-accounts in Azure met PowerShell beheren

### <a name="how-tooset-a-default-azure-subscription"></a>Hoe tooset standaard Azure-abonnement
toomanage Azure Storage met Azure PowerShell, moet u tooauthenticate uw clientomgeving met Azure via Azure Active Directory-verificatie of verificatie op basis van certificaten. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) zelfstudie. Deze handleiding gebruikt hello Azure Active Directory-verificatie.

1. Typ in Windows PowerShell ISE Hallo opdracht tooadd na uw Azure-account toohello lokale PowerShell-omgeving:

    ```powershell
    Add-AzureAccount
    ```

2. In 'tooMicrosoft Azure aanmelden' Hallo-venster, type Hallo e-mailadres en wachtwoord die zijn gekoppeld aan uw account. Azure verifieert Hallo referentie-informatie wordt opgeslagen en vervolgens Hallo-venster wordt gesloten.

3. Voer vervolgens Hallo na de opdracht tooview hello Azure accounts in uw lokale PowerShell-omgeving en controleer of uw account wordt vermeld:
   
    ```powershell
    Get-AzureAccount
    ```
4. Vervolgens Hallo cmdlet tooview na alle Hallo-abonnementen die verbonden toohello lokale PowerShell-sessie zijn uitvoeren en controleer of uw abonnement wordt vermeld:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset standaard Azure-abonnement, Hallo Select-AzureSubscription cmdlet uitvoeren:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Controleer de naam van de Hallo van Hallo standaardabonnement door Hallo Get-AzureSubscription cmdlet:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee uitvoeren voor alle Hallo beschikbare PowerShell-cmdlets voor Azure Storage:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Hoe toocreate een nieuwe Azure storage-account
toouse Azure-opslag, moet u een opslagaccount. Nadat u uw computer tooconnect tooyour-abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.

1. Hallo Get-AzureLocation cmdlet toofind alle Hallo beschikbaar datacenterlocaties uitvoeren:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Voer Hallo nieuw AzureStorageAccount cmdlet toocreate vervolgens een nieuw opslagaccount. Hallo volgende voorbeeld wordt een nieuw opslagaccount in Hallo 'VS-West' datacenter.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Hallo-naam van uw opslagaccount moet uniek zijn binnen Azure en moet een kleine letter. Zie voor naamconventies en beperkingen [over Azure Storage-Accounts](storage-create-storage-account.md) en [Naming en verwijzen naar Containers, Blobs en metagegevens](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Hoe een Azure storage-standaardaccount tooset
U kunt meerdere opslagaccounts hebben in uw abonnement. U kunt kiezen één van beide en zijn ingesteld dat deze zoals Hallo storage-standaardaccount voor alle opslag Hallo-in Hallo dezelfde opdrachten PowerShell-sessie. Hiermee kunt u toorun opslag hello Azure PowerShell-opdrachten zonder op te geven Hallo opslag context expliciet.

1. tooset een standaardopslagaccount voor uw abonnement, kunt u Hallo Set-AzureSubscription cmdlet uitvoeren.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Voer Get-AzureSubscription Hallo cmdlet tooverify of Hallo storage-account gekoppeld aan uw abonnement standaardaccount is. Deze opdracht retourneert de abonnementseigenschappen Hallo op Hallo van de huidige abonnement met inbegrip van de huidige opslagaccount.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Hoe toolist alle Azure storage-accounts in een abonnement
Elk Azure-abonnement kan up too100 storage-accounts hebben. Zie voor Hallo meest actuele informatie over limieten, [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).

Voer Hallo cmdlet toofind uit Hallo naam en status van de storage-accounts in het huidige abonnement Hallo Hallo te volgen:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Hoe toocreate de context van een Azure-opslag
Azure-opslag-context is een object in PowerShell tooencapsulate Hallo storage-referenties. Met een opslag-context tijdens het uitvoeren van een van de volgende cmdlets, kunt u tooauthenticate uw aanvraag zonder op te geven Hallo storage-account en de toegangssleutel expliciet. U kunt een context opslag maken op vele manieren, zoals het gebruik van naam en toegangssleutel van storage-account, de shared access signature (SAS)-token, de verbindingsreeks, of anonieme. Zie voor meer informatie [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Gebruik een van de volgende drie manieren toocreate Hallo een opslag-context:

* Voer Hallo [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind uit Hallo opslag primaire toegangssleutel voor uw Azure storage-account. Daarna roept Hallo [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate een context opslag:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Genereren van een shared access signature-token voor een Azure storage-container en toocreate een opslag-context worden gebruikt:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Zie voor meer informatie [nieuw AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) en [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* In sommige gevallen kunt u toospecify Hallo service-eindpunten bij het maken van een nieuwe opslag-context. Dit kan noodzakelijk zijn wanneer u een aangepaste domeinnaam voor uw opslagaccount hebt geregistreerd met Hallo Blob-service of het gewenste toouse een shared access signature voor toegang tot de opslagbronnen. Hallo-service-eindpunten in een verbindingsreeks instellen en deze toocreate een nieuwe opslag context gebruiken zoals hieronder wordt weergegeven:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Voor meer informatie over het tooconfigure een verbindingsreeks voor opslag, Zie [configureren van verbindingsreeksen](storage-configure-connection-string.md).

Nu dat u hebt uw computer instellen en hebt geleerd hoe toomanage-abonnementen en opslagaccounts met Azure PowerShell, Ga toohello volgende sectie toolearn hoe toomanage Azure blobs en blob-momentopnamen.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Hoe Azure-opslag-sleutels tooretrieve en opnieuw genereren
Een Azure Storage-account wordt geleverd met twee sleutels. U kunt uw sleutels Hallo cmdlet tooretrieve te volgen.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Hallo volgende cmdlet tooretrieve een specifieke sleutel gebruiken. Geldige waarden zijn primair en secundair.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Als u tooregenerate wilt uw sleutels Hallo volgende cmdlet gebruiken. Geldige waarden voor KeyType - zijn 'Primaire' en 'Secundaire'

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Hoe toomanage Azure blobs
Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Blob Storage-Service bent. Zie voor gedetailleerde informatie [aan de slag met Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Hoe toocreate een container
Elke blob in Azure-opslag moet zich in een container. U kunt een privé-container met de cmdlet New-AzureStorageContainer Hallo maken:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**. tooprevent anonieme toegang tot tooblobs, setparameter Hallo machtiging te**uit**. Standaard Hallo nieuwe container privé is en toegankelijk zijn alleen voor de accounteigenaar Hallo. anonieme openbare tooallow lezen toegang tot tooblob bronnen, maar niet toocontainer metagegevens of toohello lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Blob**. volledige openbare tooallow lezen toegang tot tooblob bronnen, container metagegevens en Hallo lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Container**. Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Hoe tooupload een blob naar een container
Azure Blob Storage ondersteunt blok-blobs en pagina-blobs. Zie voor meer informatie [blok-Blobs, toevoeg-BLobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload blobs in tooa container, kunt u Hallo [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. Standaard uploadt u deze opdracht Hallo lokale bestanden tooa blok-blob. Hallo-type toospecify voor Hallo blob, kunt u Hallo BlobType - parameter.

Hallo volgende voorbeeld wordt uitgevoerd Hallo [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget alle hello-bestanden in de opgegeven map Hallo en vervolgens geeft deze door de volgende cmdlet toohello met behulp van Hallo pipeline-operator. Hallo [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploadt Hallo lokale bestanden tooyour container:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Hoe toodownload blobs uit een container
Hallo volgende voorbeeld laat zien hoe toodownload blobs uit een container. Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de primaire toegangssleutel. Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. Vervolgens Hallo voorbeeld maakt gebruik van Hallo [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs in de lokale doelmap Hallo.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Hoe toocopy blobs uit één opslag container tooanother
U kunt BLOB's tussen opslagaccounts en regio's asynchroon kopiëren. Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag container tooanother in twee verschillende opslagaccounts. Hallo voorbeeld stelt eerst de variabelen voor de bron- en storage-accounts en maakt vervolgens een context opslag voor elke account. Vervolgens Hallo voorbeeld blobs kopieert van Hallo bron container toohello doelcontainer Hallo met [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. Hallo-voorbeeld wordt ervan uitgegaan dat Hallo bron- en storage-accounts en containers bestaan al.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Houd er rekening mee dat dit voorbeeld wordt een kopie van de asynchrone uitgevoerd. U kunt Hallo status van elk exemplaar bewaken door het uitvoeren van Hallo [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Hoe toocopy blobs vanaf een secundaire locatie
U kunt blobs kopiëren vanaf de secundaire locatie Hallo van een account RA-GRS-functionaliteit.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Hoe toodelete een blob
een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens Hallo verwijderen AzureStorageBlob cmdlet erop. Hallo volgende voorbeeld worden alle Hallo blobs in een bepaalde container verwijderd. Hallo voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context. Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [verwijderen AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs uit een container in Azure-opslag.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Hoe toomanage Azure blob-momentopnamen
Azure maakt u een momentopname van een blob. Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd. Wanneer een momentopname is gemaakt, kan deze worden gelezen, gekopieerd, of verwijderd, maar niet gewijzigd. Momentopnamen bieden een manier tooback van een blob, zoals deze wordt weergegeven op een moment. Zie voor meer informatie [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Hoe toocreate een momentopname van een blob
een snaphot van een blob toocreate eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo `ICloudBlob.CreateSnapshot` methode erop. Hallo volgende voorbeeld stelt eerst de variabelen voor een opslagaccount, en maakt vervolgens een opslag-context. Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode toocreate een momentopname.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Hoe toolist een blob van momentopnamen
U kunt zoveel momentopnamen als u voor een blob wilt maken. Je kunt aanbieden Hallo momentopnamen die zijn gekoppeld aan uw tootrack blob uw huidige momentopnamen. Hallo volgende voorbeeld wordt een vooraf gedefinieerde blob en aanroepen Hallo [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist Hallo momentopnamen van de blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Hoe toocopy een momentopname van een blob
U kunt een momentopname van een momentopname van een blob toorestore Hallo kopiëren. Zie voor gedetailleerde informatie en beperkingen [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Hallo volgende voorbeeld stelt eerst de variabelen voor een opslagaccount, en maakt vervolgens een opslag-context. Vervolgens definieert Hallo voorbeeld Hallo-container en blob naam variabelen. Hallo-voorbeeld wordt een blobverwijzing met Hallo opgehaald [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode toocreate een momentopname. Vervolgens Hallo-voorbeeld Hallo uitgevoerd [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy Hallo momentopname van een blob Hallo ICloudBlob-object voor de bron-blob hello gebruiken. Controleer of tooupdate Hallo variabelen gebaseerd zijn op uw configuratie voordat actieve Hallo-voorbeeld. Houd er rekening mee dat Hallo volgende voorbeeld wordt ervan uitgegaan dat Hallo bron- en doelserver containers en Hallo bron blob bestaat al.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Nu dat u hebt geleerd hoe toomanage Azure blobs en blob-momentopnamen met Azure PowerShell, gaat u toohello volgende sectie toolearn hoe toomanage tabellen, wachtrijen en bestanden.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Hoe toomanage Azure-tabellen en entiteiten tabel
Azure Table storage-service is een NoSQL-gegevensarchief kunt u toostore en query grote sets gestructureerde, niet-relationele gegevens. Hallo hoofdonderdelen van Hallo service zijn tabellen, entiteiten en eigenschappen. Een tabel is een verzameling entiteiten. Een entiteit is een set eigenschappen. Elke entiteit kan hebben too252-eigenschappen die alle naam / waarde-paren. Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Table Storage-Service bent. Zie voor gedetailleerde informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) en [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md).

In de Hallo volgende subsecties, leert u hoe toomanage Azure Table storage-service met Azure PowerShell. Hallo scenario's worden behandeld: **maken**, **verwijderen**, en **bij het ophalen van** **tabellen**, evenals **toevoegen**, **opvragen**, en **tabelentiteiten verwijderen**.

### <a name="how-toocreate-a-table"></a>Hoe toocreate een tabel
Elke tabel moet zich bevinden in een Azure storage-account. Hallo volgende voorbeeld laat zien hoe toocreate een tabel in Azure Storage. Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens wordt Hallo [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate een tabel in Azure Storage.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Hoe tooretrieve een tabel
U kunt een query en ophalen van een of alle tabellen in een opslagaccount. Hallo volgende voorbeeld laat zien hoe een tabel met tooretrieve Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Als u Hallo Get AzureStorageTable cmdlet zonder parameters aanroept, krijgt alle opslagtabellen voor een opslagaccount.

### <a name="how-toodelete-a-table"></a>Hoe toodelete een tabel
U kunt een tabel uit een opslagaccount verwijderen met behulp van Hallo [verwijderen AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Hoe toomanage tabel entiteiten
Op dit moment biedt Azure PowerShell geen tabelentiteiten voor cmdlets toomanage rechtstreeks. tooperform bewerkingen op tabelentiteiten, kunt u Hallo klassen die in het Hallo [Azure Storage-clientbibliotheek voor .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Hoe tooadd tabel entiteiten
een tabel entity tooa tooadd eerst een object dat bepaalt de entiteitseigenschappen van uw maken. Een entiteit kan hebben too255 eigenschappen, met inbegrip van de eigenschappen van 3: **PartitionKey**, **RowKey**, en **tijdstempel**. U bent zelf verantwoordelijk voor het invoegen en het bijwerken van Hallo waarden van **PartitionKey** en **RowKey**. Hallo server wordt beheerd Hallo-waarde van **tijdstempel**, die niet worden gewijzigd. Samen Hallo **PartitionKey** en **RowKey** unieke identificatie van elke entiteit in een tabel.

* **PartitionKey**: Hallo partitie die de entiteit Hallo is opgeslagen in bepaalt.
* **RowKey**: Hallo entiteit binnen Hallo partitie wordt aangeduid.

U kunt definiëren too252 aangepaste eigenschappen voor een entiteit. Zie voor meer informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hallo volgende voorbeeld laat zien hoe tooadd entiteiten tooa tabel. Hallo-voorbeeld ziet u hoe tooretrieve Hallo werknemerstabel en verschillende entiteiten in de App toevoegen. Eerst het vaststelt dat een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens wordt het ophalen van Hallo gegeven van de tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Als Hallo tabel niet bestaat, Hallo [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is gebruikte toocreate een tabel in Azure Storage. Hallo voorbeeld wordt vervolgens een aangepaste functie toevoegen entiteit tooadd entiteiten toohello tabel gedefinieerd door partitie voor elke entiteit en rijsleutel te geven. Hallo toevoegen entiteit functie aanroepen Hallo [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet op Hallo [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasse toocreate een entiteitsobject. Later Hallo voorbeeld Hallo roept [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) methode voor deze entiteit object tooadd het tooa tabel.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Hoe tooquery tabel entiteiten
een tabel tooquery gebruiken Hallo [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasse. Hallo volgende voorbeeld wordt ervan uitgegaan dat u al hoe gegeven in Hallo Hallo-script hebt uitgevoerd tooadd entiteiten gedeelte van deze handleiding. Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo opslag context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens probeert tooretrieve Hallo eerder hebt gemaakt 'werknemers' tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Aanroepen Hallo [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet op Hallo Microsoft.WindowsAzure.Storage.Table.TableQuery klasse maakt een nieuwe query-object. Hallo voorbeeld gezocht Hallo entiteiten met een 'ID-kolom waarvan de waarde 1 zoals opgegeven in een tekenreeks-filter is. Zie voor gedetailleerde informatie [opvragen van tabellen en entiteiten](http://msdn.microsoft.com/library/azure/dd894031.aspx). Wanneer u deze query uitvoert, wordt alle entiteiten die overeenkomen met de filtercriteria Hallo.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Hoe toodelete tabel entiteiten
U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen. Hallo volgende voorbeeld wordt ervan uitgegaan dat u al hoe gegeven in Hallo Hallo-script hebt uitgevoerd tooadd entiteiten gedeelte van deze handleiding. Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo opslag context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens probeert tooretrieve Hallo eerder hebt gemaakt 'werknemers' tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Als Hallo tabel bestaat, Hallo voorbeeld Hallo roept [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) methode tooretrieve een entiteit op basis van de bijbehorende sleutelwaarden partitie en rij. Vervolgens moet worden doorgegeven Hallo entiteit toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete methode.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Hoe toomanage Azure wachtrijen en berichten in een wachtrij
Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Queue Storage-Service bent. Zie voor gedetailleerde informatie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md).

Deze sectie wordt uitgelegd hoe toomanage Azure Queue storage-service met Azure PowerShell. Hallo scenario's worden behandeld: **invoegen** en **verwijderen** wachtrij berichten, evenals **maken**, **verwijderen**, en **bij het ophalen van wachtrijen**.

### <a name="how-toocreate-a-queue"></a>Hoe een wachtrij toocreate
Hallo volgende voorbeeld eerst wordt een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens roept [nieuw AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate een wachtrij met de naam 'wachtrijnaam'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Zie voor informatie over naamgevingsregels voor Azure Queue-Service, [naamgeving van wachtrijen en metagegevens](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Hoe een wachtrij tooretrieve
U kunt een query en ophalen van een specifieke wachtrij of een lijst met alle Hallo wachtrijen in een opslagaccount. Hallo volgende voorbeeld laat zien hoe een opgegeven wachtrij met tooretrieve Hallo [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Als u Hallo aanroepen [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet zonder parameters voor het ophalen van een lijst met alle Hallo wachtrijen.

### <a name="how-toodelete-a-queue"></a>Hoe een wachtrij toodelete
toodelete een wachtrij en alle Hallo-berichten opgenomen in deze aanroep Hallo verwijderen AzureStorageQueue cmdlet. Hallo volgende voorbeeld ziet u hoe toodelete een opgegeven wachtrij met de cmdlet Remove-AzureStorageQueue Hallo.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Hoe tooinsert een bericht in een wachtrij
tooinsert een bericht in een bestaande wachtrij maakt eerst een nieuw exemplaar van Hallo [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse. Daarna roept Hallo [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode. Een CloudQueueMessage kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.

Hallo volgende voorbeeld laat zien hoe tooadd tooa wachtrij bericht. Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel. Vervolgens wordt het ophalen van Hallo van de opgegeven wachtrij met Hallo [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Als Hallo wachtrij, hello bestaat [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is gebruikte toocreate een exemplaar van Hallo [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse. Later Hallo voorbeeld Hallo roept [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode voor dit bericht object tooadd het tooa wachtrij. Hier volgt een code die een wachtrij opgehaald en voegt het Hallo-bericht 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Hoe toode-wachtrij op Hallo volgend bericht
Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd. Wanneer u Hallo aanroepen [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) methode, krijgt u het volgende Hallo-bericht in een wachtrij. Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook Hallo aanroepen [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) methode. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Uw code haalt **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Hoe toomanage Azure-bestand deelt, en bestanden
Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van Hallo standaard SMB-protocol. Microsoft Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via Hallo bestands-API voor storage of Azure PowerShell.

Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) en [REST-API van bestand](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Hoe tooset en query storage analytics
U kunt [Azure Storage Analytics](storage-analytics.md) toocollect metrische gegevens voor uw Azure storage-accounts en logboekgegevens over aanvragen verzonden tooyour storage-account. U kunt opslag metrische gegevens toomonitor Hallo status van een opslagaccount en opslag logboekregistratie toodiagnose gebruiken en oplossen van problemen met uw storage-account. U kunt configureren met behulp van bewaking hello Azure-portal of met Windows PowerShell of programmatisch met Hallo storage-clientbibliotheek. Opslag logboekregistratie gebeurt serverzijde en kunt u toorecord details voor geslaagde en mislukte aanvragen in uw opslagaccount. Deze logboeken inschakelen toosee details van lees-, schrijf- en delete-bewerkingen op basis van uw tabellen, wachtrijen en blobs, evenals Hallo redenen voor mislukte aanvragen.

hoe tooenable en bekijk metrische gegevens voor opslag van gegevens met behulp van PowerShell, Zie toolearn [hoe tooenable metrische gegevens Storage met behulp van PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

hoe tooenable en ophalen logboekregistratie van opslag van gegevens met behulp van PowerShell, Zie toolearn [hoe tooenable opslag logboekregistratie met behulp van PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) en [zoeken naar uw logboekgegevens opslag logboekregistratie](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Zie voor gedetailleerde informatie over het gebruik van opslag metrische gegevens en opslag logboekregistratie opslagproblemen tootroubleshoot [bewaking, diagnose en het oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Hoe toomanage Shared Access Signature (SAS) en toegangsbeleid opgeslagen
Shared access signatures zijn een belangrijk onderdeel van het beveiligingsmodel Hallo voor elke toepassing met behulp van Azure Storage. Ze zijn nuttig voor het leveren van beperkte machtigingen tooyour storage account tooclients Hallo accountsleutel niet hebben. Standaard hebben alleen de eigenaar van het opslagaccount Hallo Hallo mogelijk toegang tot blobs, tabellen en wachtrijen in dat account. Als uw service of toepassing moet toomake deze resources beschikbaar tooother clients zonder het delen van uw toegangssleutel, hebt u drie opties:

* Een container machtigingen toopermit anonieme leestoegang toohello container en de bijbehorende blobs instellen. Dit is niet toegestaan voor tabellen of wachtrijen.
* Gebruik een shared access signature die beperkte toegang rechten toocontainers, blobs, wachtrijen en tabellen voor een bepaald tijdsinterval verleent.
* Gebruik een opgeslagen toegang beleid tooobtain een extra verificatieniveau controle over handtekeningen voor gedeelde toegang voor een container of de blobs, voor een wachtrij of voor een tabel. Hallo opgeslagen toegangsbeleid kunt u toochange Hallo begintijd, verlooptijd of machtigingen voor een handtekening of toorevoke deze nadat deze is uitgegeven.

Een shared access signature kan worden gebruikt in een van twee vormen:

* **Ad-hoc SAS**: wanneer u een ad-hoc SAS, begintijd hello, verlooptijd maken en machtigingen voor Hallo SAS zijn opgegeven op Hallo SAS-URI. Dit type SAS kan worden gemaakt op een container, blob, table of wachtrij en het is niet worden ingetrokken.
* **SAS met opgeslagen toegangsbeleid**: een opgeslagen-beleid is gedefinieerd in een resourcecontainer een blob-container, een tabel of een wachtrij - en u kunt deze gebruiken toomanage beperkingen voor een of meer handtekeningen voor gedeelde toegang. Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, Hallo SAS neemt over Hallo beperkingen - Hallo starttijd, verlooptijd en machtigingen - zijn opgegeven voor toegangsbeleid Hallo opgeslagen. Dit type SAS is worden ingetrokken.

Zie voor meer informatie [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) en [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).

In de volgende secties hello, leert u hoe toocreate een beleid voor gedeelde toegang handtekening access token en de opslag voor Azure-tabellen. Azure PowerShell biedt vergelijkbare cmdlets voor containers, blobs en wachtrijen ook. toorun hello scripts in deze sectie download Hallo [Azure PowerShell versie 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) of hoger.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Hoe een op beleid gebaseerde toocreate Shared Access Signature-token
Hallo nieuw AzureStorageTableStoredAccessPolicy cmdlet toocreate een nieuw opgeslagen-beleid gebruiken. Roep vervolgens Hallo [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate een nieuw token van de handtekening gedeelde toegang op basis van beleid voor een Azure Storage-tabel.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Hoe toocreate een ad-hoc (niet terughalen) Shared Access Signature-token
Gebruik Hallo [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate een nieuw ad-hoc (niet terughalen) Shared Access Signature-token voor een Azure Storage-tabel:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Hoe toocreate een opgeslagen-beleid
Hallo nieuw AzureStorageTableStoredAccessPolicy cmdlet toocreate een nieuw opgeslagen-beleid gebruiken voor een Azure Storage-tabel:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Hoe tooupdate een opgeslagen-beleid
Hallo Set AzureStorageTableStoredAccessPolicy cmdlet tooupdate een bestaand opgeslagen toegangsbeleid gebruiken voor een Azure Storage-tabel:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Hoe toodelete een opgeslagen-beleid
Hallo verwijderen AzureStorageTableStoredAccessPolicy cmdlet toodelete een opgeslagen-beleid gebruiken in de tabel in een Azure Storage:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Hoe toouse Azure Storage voor de Amerikaanse overheid en Azure voor China
Een Azure-omgeving is een onafhankelijke implementatie van Microsoft Azure, zoals [Azure Government voor de overheid van de VS](https://azure.microsoft.com/features/gov/), [AzureCloud voor globale Azure](https://portal.azure.com), en [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/). U kunt nieuwe Azure-omgevingen voor Amerikaanse overheid en Azure voor China implementeren.

Azure Storage met AzureChinaCloud toouse, moet u een opslag-context die is gekoppeld aan AzureChinaCloud toocreate. Volg deze stappen tooget u gestart:

1. Voer Hallo [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Hallo beschikbare Azure-omgevingen:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Een Azure China account tooWindows PowerShell toevoegen:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Maak een context opslag voor een account AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Azure Storage met [VS Azure Government](https://azure.microsoft.com/features/gov/), moet u een nieuwe omgeving definiëren en vervolgens een nieuwe opslag context maken met deze omgeving:

1. Voer Hallo [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Hallo beschikbare Azure-omgevingen:

    ```powershell
    Get-AzureEnvironment
    ```

2. Een Azure US Government account tooWindows PowerShell toevoegen:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Maak een context opslag voor een account AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Zie voor meer informatie:

* [Ontwikkelaarshandleiding voor Microsoft Azure Government](../azure-government-developer-guide.md).
* [Overzicht van verschillen bij het maken van een toepassing op China Service](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Volgende stappen
In deze handleiding hebt u geleerd hoe toomanage Azure Storage met Azure PowerShell. Hier volgen enkele verwante artikelen en resources voor meer informatie hierover.

* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [PowerShell-Cmdlets voor Azure-opslag](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell-referentie](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
