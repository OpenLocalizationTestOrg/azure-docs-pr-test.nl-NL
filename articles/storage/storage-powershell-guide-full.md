---
title: Azure PowerShell gebruiken met Azure Storage | Microsoft Docs
description: Informatie over het gebruik van de Azure PowerShell-cmdlets voor Azure Storage maken en beheren van opslagaccounts; werken met blobs, tabellen, wachtrijen en bestanden. configureren en storage analytics query en handtekeningen voor gedeelde toegang maken.
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
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Azure PowerShell gebruiken met Azure Storage
## <a name="overview"></a>Overzicht
Azure PowerShell is een module die biedt voor het beheren van Azure via Windows PowerShell-cmdlets. Het is een op taken gebaseerde opdrachtregelshell en scripttaal die speciaal is ontworpen voor systeembeheer. U kunt eenvoudig beheren en het beheer van uw Azure-services en toepassingen te automatiseren met PowerShell. U kunt bijvoorbeeld de cmdlets gebruiken om uit te voeren dezelfde taken die u via uitvoeren kunt de [Azure-portal](https://portal.azure.com).

In deze handleiding wordt besproken voor het gebruik van de [Azure-opslag-Cmdlets](/powershell/module/azurerm.storage/#storage) om uit te voeren een verscheidenheid aan taken voor ontwikkeling en het beheer met Azure Storage.

Deze handleiding wordt ervan uitgegaan dat u ervaring met behulp van [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) en [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). De handleiding bevat een aantal scripts voor het demonstreren van het gebruik van PowerShell met Azure Storage. De scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd, moet u bijwerken.

De eerste sectie in deze handleiding biedt een kijkje Azure Storage en PowerShell. Voor gedetailleerde informatie en instructies starten vanuit de [vereisten voor het gebruik van Azure PowerShell met Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Aan de slag met Azure Storage en PowerShell in vijf minuten
Deze sectie wordt beschreven hoe u toegang tot Azure Storage via PowerShell in vijf minuten.

**Nieuwe naar Azure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement. Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).

Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.

**Na het maken van een Microsoft Azure-abonnement en -account:**

1. Download en installeer de meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Start Windows PowerShell Integrated Scripting Environment (ISE): In de lokale computer, gaat u naar de **Start** menu. Type **Systeembeheer** en klikt u op uit te voeren. In de **Systeembeheer** venster met de rechtermuisknop op **Windows PowerShell ISE**, klikt u op **als Administrator uitvoeren**.
3. In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** voor het maken van een script.
4. Nu geven we u een eenvoudig script waarin basic PowerShell-opdrachten voor toegang tot Azure Storage. Het script vraagt eerst uw Azure-accountreferenties voor het toevoegen van uw Azure-account aan de lokale PowerShell-omgeving. Het script wordt vervolgens de Azure-abonnement instellen en een nieuw opslagaccount maken in Azure. Het script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaand installatiekopiebestand (blob) op die container. Nadat het script geeft een lijst van alle blobs in de container, worden een nieuwe bestemming-map maken in uw lokale computer en het installatiekopiebestand te downloaden.
5. Selecteer het script tussen de opmerkingen in de volgende sectie van de code **#beginnen** en **#end**. Druk op CTRL + C om naar het Klembord kopiëren.

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. In **Windows PowerShell ISE**, druk op CTRL + V om te kopiëren van het script. Klik op **bestand** > **opslaan**. In de **OpslaanAls** dialoogvenster, typ de naam van het scriptbestand, zoals 'mystoragescript'. Klik op **Opslaan**.
7. Nu moet u de scriptvariabelen op basis van uw configuratie-instellingen bijwerken. U moet bijwerken de **$SubscriptionName** variabele met uw eigen abonnement. U kunt de andere variabelen zoals opgegeven in het script behouden of deze als u wilt bijwerken.
   
   * **$SubscriptionName:** moet u deze variabele bijwerken met de naam van uw eigen abonnement. Ga als volgt op een van de volgende drie manieren vinden van de naam van uw abonnement:
     
    a. In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** voor het maken van een script. Het volgende script kopiëren naar het nieuwe script en klik op **Debug** > **uitvoeren**. Het volgende script wordt eerst vraagt u uw Azure-accountreferenties voor het toevoegen van uw Azure account toe aan de lokale PowerShell-omgeving en alle abonnementen die zijn verbonden met de lokale PowerShell-sessie wordt weergegeven. Noteer de naam van het abonnement dat u gebruiken wilt tijdens deze zelfstudie te volgen:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. Om te zoeken en kopieert u de abonnementsnaam van uw in de [Azure-portal](https://portal.azure.com), klik in het Hub-menu aan de linkerkant op **abonnementen**. Kopieer de naam van het abonnement dat u gebruiken wilt tijdens het uitvoeren van de scripts in deze handleiding.
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. Om te zoeken en kopieert u de abonnementsnaam van uw in de [klassieke Azure-Portal](https://manage.windowsazure.com/), schuif naar beneden en klik op **instellingen** aan de linkerkant van de portal. Klik op **abonnementen** voor een overzicht van uw abonnementen. Kopieer de naam van het abonnement dat u gebruiken wilt tijdens het uitvoeren van de scripts die zijn opgegeven in deze handleiding.
     
     ![Klassieke Azure-portal](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** de voornaam in het script of geef een nieuwe naam voor uw opslagaccount. **Belangrijk:** de naam van het opslagaccount moet uniek zijn in Azure. Er moet een kleine letter, te!
   * **$Location:** gebruik van de opgegeven 'VS-West' in het script of kies andere Azure locaties, zoals VS-Oost, Noord-Europa, enzovoort.
   * **$ContainerName:** de voornaam in het script of geef een nieuwe naam voor de container.
   * **$ImageToUpload:** Voer een pad naar een afbeelding op uw lokale computer, zoals: 'C:\Images\HelloWorld.png'.
   * **$DestinationFolder:** een pad opgeven naar een lokale map voor het opslaan van bestanden die zijn gedownload van Azure Storage, zoals: 'C:\DownloadImages'.
8. Klik na het bijwerken van de scriptvariabelen in het bestand 'mystoragescript.ps1' **bestand** > **opslaan**. Klik vervolgens op **Debug** > **uitvoeren** of druk op **F5** het script uit te voeren.  

Nadat het script wordt uitgevoerd, moet u een lokale doelmap met het gedownloade bestand hebben. De volgende schermafbeelding ziet een voorbeeld van uitvoer:

![Blobs downloaden](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> De sectie 'Aan de slag met Azure Storage en PowerShell in vijf minuten' verstrekt een korte inleiding op Azure PowerShell gebruiken met Azure Storage. Voor gedetailleerde informatie en instructies raden we u aan het lezen van de volgende secties.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Vereisten voor het gebruik van Azure PowerShell met Azure Storage
U moet een Azure-abonnement en de account voor het uitvoeren van de PowerShell-cmdlets die is opgegeven in deze handleiding, zoals hierboven beschreven.

Azure PowerShell is een module die biedt voor het beheren van Azure via Windows PowerShell-cmdlets. Zie voor meer informatie over het installeren en instellen van Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview). U wordt aangeraden dat u downloaden en installeren of naar de nieuwste Azure PowerShell-module upgraden voordat u deze handleiding.

U kunt de cmdlets uitvoeren in de standaard Windows PowerShell-console of de Windows PowerShell Integrated Scripting Environment (ISE). Om bijvoorbeeld te openen **Windows PowerShell ISE**, gaat u naar het menu Start, typt u de beheerprogramma's en klikt u op uit te voeren. In het venster Systeembeheer met de rechtermuisknop op Windows PowerShell ISE, klik op uitvoeren als Administrator.

## <a name="how-to-manage-storage-accounts-in-azure"></a>Storage-accounts in Azure beheren

We gaan verdiepen in de storage-accounts in Azure met PowerShell beheren

### <a name="how-to-set-a-default-azure-subscription"></a>Het instellen van een standaard Azure-abonnement
Voor het beheren van Azure Storage met Azure PowerShell, moet u uw clientomgeving met Azure via Azure Active Directory-verificatie of verificatie op basis van certificaten verifiëren. Zie voor gedetailleerde informatie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) zelfstudie. Deze handleiding bevat de Azure Active Directory-verificatie.

1. Typ de volgende opdracht voor het toevoegen van uw Azure in Windows PowerShell ISE account toe aan de lokale PowerShell-omgeving:

    ```powershell
    Add-AzureAccount
    ```

2. Typ de e-mailadres en het wachtwoord die zijn gekoppeld aan uw account in het venster 'Aanmelding in voor Microsoft Azure'. Azure verifieert de referentiegegevens en slaat deze op. Vervolgens wordt het venster gesloten.

3. Voer de volgende opdracht om de Azure-accounts in uw lokale PowerShell-omgeving weergeven en controleer of uw account wordt vermeld:
   
    ```powershell
    Get-AzureAccount
    ```
4. Vervolgens voert u de volgende cmdlet als u wilt weergeven van alle abonnementen die zijn verbonden met de lokale PowerShell-sessie en controleert u of uw abonnement wordt weergegeven:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. Als u wilt instellen op een standaard Azure-abonnement, voer de Select-AzureSubscription-cmdlet:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Controleer de naam van het standaardabonnement door de cmdlet Get-AzureSubscription:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. Alle beschikbare PowerShell-cmdlets voor Azure Storage vindt uitvoeren:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a>Het maken van een nieuwe Azure storage-account
Voor het gebruik van Azure-opslag, moet u een opslagaccount. Nadat u uw computer verbinding maken met uw abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.

1. Voer de cmdlet Get-AzureLocation om alle beschikbare datacenterlocaties vinden:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Voer de cmdlet New-AzureStorageAccount voor het maken van een nieuw opslagaccount. Het volgende voorbeeld wordt een nieuw opslagaccount gemaakt in het datacenter 'VS-West'.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> De naam van uw opslagaccount moet uniek zijn binnen Azure en moet een kleine letter. Zie voor naamconventies en beperkingen [over Azure Storage-Accounts](storage-create-storage-account.md) en [Naming en verwijzen naar Containers, Blobs en metagegevens](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a>Het instellen van een Azure storage-standaardaccount
U kunt meerdere opslagaccounts hebben in uw abonnement. U kunt kiezen één van deze en stel dit in als het standaardopslagaccount voor alle opslag-opdrachten in dezelfde PowerShell-sessie. Hiermee kunt u de Azure PowerShell-opslag-opdrachten uitvoeren zonder expliciet opgeven van de context van de opslag.

1. Om in te stellen een standaardopslagaccount voor uw abonnement, kunt u de cmdlet Set-AzureSubscription uitvoeren.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Voer de cmdlet Get-AzureSubscription om te controleren of het opslagaccount gekoppeld aan uw abonnement standaardaccount is. Met deze opdracht retourneert de eigenschappen van het abonnement op het huidige abonnement met inbegrip van de huidige opslagaccount.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a>Hoe u alle Azure storage-accounts in een abonnement
Elk Azure-abonnement kan maximaal 100 opslagaccounts hebben. Zie voor de meest actuele informatie van limieten [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).

Voer de volgende cmdlet om erachter te komen met de naam en de status van de storage-accounts in het huidige abonnement:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a>Het maken van een Azure-opslag-context
Azure-opslag-context is een object in PowerShell inkapselen de storage-referenties. Met behulp van een context opslag terwijl alle volgende cmdlet wordt uitgevoerd, u uw aanvraag verifiëren kunt zonder het expliciet opgeven van het opslagaccount en de toegangssleutel. U kunt een context opslag maken op vele manieren, zoals het gebruik van naam en toegangssleutel van storage-account, de shared access signature (SAS)-token, de verbindingsreeks, of anonieme. Zie voor meer informatie [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Gebruik een van de volgende drie manieren voor het maken van een context opslag:

* Voer de [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet om erachter te komen de opslag van primaire toegangssleutel voor uw Azure storage-account. Daarna roept de [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet voor het maken van een context opslag:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Genereren van een shared access signature-token voor een Azure storage-container en de context van een opslagruimte maken:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Zie voor meer informatie [nieuw AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) en [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* In sommige gevallen wilt u mogelijk de service-eindpunten opgeven bij het maken van een nieuwe opslag-context. Dit kan noodzakelijk zijn wanneer u een aangepaste domeinnaam voor uw opslagaccount hebt geregistreerd met de Blob-service of u gebruiken een shared access signature wilt voor toegang tot de opslagbronnen. De service-eindpunten in een verbindingsreeks instellen en deze gebruiken voor het maken van een nieuwe opslag-context, zoals hieronder wordt weergegeven:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Zie voor meer informatie over het configureren van een verbindingsreeks voor opslag [configureren van verbindingsreeksen](storage-configure-connection-string.md).

Nu dat u hebt uw computer instellen en hebt geleerd hoe u abonnementen en opslagaccounts met Azure PowerShell beheren, gaat u naar de volgende sectie voor informatie over het beheren van Azure blobs en blob-momentopnamen.

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a>Ophalen en opnieuw genereren van sleutels voor Azure-opslag
Een Azure Storage-account wordt geleverd met twee sleutels. U kunt de volgende cmdlet gebruiken voor het ophalen van uw sleutels.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Gebruik de volgende cmdlet voor het ophalen van een specifieke sleutel. Geldige waarden zijn primair en secundair.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Gebruik de volgende cmdlet als u wilt uw sleutels genereren. Geldige waarden voor KeyType - zijn 'Primaire' en 'Secundaire'

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a>Azure BLOB's beheren
Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS. Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten van Azure Blob Storage-Service bent. Zie voor gedetailleerde informatie [aan de slag met Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-to-create-a-container"></a>Het maken van een container
Elke blob in Azure-opslag moet zich in een container. U kunt een privé-container met de cmdlet New-AzureStorageContainer maken:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**. Als u wilt voorkomen dat anonieme toegang tot blobs, stelt u de machtiging-parameter in op **uit**. Standaard worden de nieuwe container privé is en kan alleen worden geopend door de eigenaar van het account. Anonieme toegang toestaan openbare leestoegang tot blob-bronnen, maar niet aan de metagegevens van de container of aan de lijst met blobs in de container, stelt u de parameter machtiging op **Blob**. Stel de parameter machtiging op wilt toestaan volledige openbare leestoegang tot de blob-bronnen, container metagegevens en de lijst met blobs in de container, **Container**. Zie voor meer informatie [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a>Het uploaden van een blob naar een container
Azure Blob Storage ondersteunt blok-blobs en pagina-blobs. Zie voor meer informatie [blok-Blobs, toevoeg-BLobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).

Blobs in als u wilt uploaden een container, kunt u de [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. Standaard wordt met deze opdracht de lokale bestanden naar een blok-blob geüpload. Als u wilt opgeven welk type voor de blob, kunt u de parameter - BlobType.

Het volgende voorbeeld wordt uitgevoerd de [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet ophalen van alle bestanden in de opgegeven map en vervolgens doorgegeven aan de volgende cmdlet met behulp van de pijplijn-operator. De [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet wordt de lokale bestanden geüpload naar de container:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a>Blobs downloaden uit een container
Het volgende voorbeeld laat zien hoe blobs downloaden uit een container. In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de primaire toegangssleutel. Klik in het voorbeeld haalt een blob-verwijzing met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. Vervolgens in het voorbeeld wordt de [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet blobs downloaden naar de map lokale bestemming.

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a>Blobs uit een opslagcontainer naar de andere kopiëren
U kunt BLOB's tussen opslagaccounts en regio's asynchroon kopiëren. Het volgende voorbeeld laat zien hoe blobs van één opslagcontainer kopieert naar een andere in twee verschillende opslagaccounts. In het voorbeeld stelt eerst de variabelen voor de bron- en storage-accounts, en maakt vervolgens een context opslag voor elke account. Vervolgens in het voorbeeld blobs opgehaald uit de Broncontainer met de doel-container via de [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. In het voorbeeld wordt ervan uitgegaan dat de bron- en storage-accounts en containers al bestaan.

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Houd er rekening mee dat dit voorbeeld wordt een kopie van de asynchrone uitgevoerd. U kunt de status van elk exemplaar bewaken door het uitvoeren van de [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-to-copy-blobs-from-a-secondary-location"></a>Blobs kopiëren vanaf een secundaire locatie
U kunt de blobs kopiëren vanaf de secundaire locatie van een account RA-GRS-functionaliteit.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a>Het verwijderen van een blob
Als u wilt verwijderen van een blob, eerst een blobverwijzing ophalen en roept u vervolgens de cmdlet Remove-AzureStorageBlob erop. Het volgende voorbeeld verwijdert alle blobs in een bepaalde container. Het voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context. Vervolgens in het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [verwijderen AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet blobs verwijderen uit een container in Azure-opslag.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a>Het beheren van Azure blob-momentopnamen
Azure maakt u een momentopname van een blob. Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd. Wanneer een momentopname is gemaakt, kan deze worden gelezen, gekopieerd, of verwijderd, maar niet gewijzigd. Momentopnamen bieden een manier om back-up van een blob zoals deze wordt weergegeven op een moment. Zie voor meer informatie [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-to-create-a-blob-snapshot"></a>Het maken van een momentopname van een blob
Voor het maken van een snaphot van een blob, eerst een blobverwijzing ophalen en roept u vervolgens de `ICloudBlob.CreateSnapshot` methode erop. Het volgende voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context. Vervolgens in het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode om een momentopname te maken.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a>Hoe u een blob-momentopnamen
U kunt zoveel momentopnamen als u voor een blob wilt maken. U kunt de momentopnamen die zijn gekoppeld aan uw blob om bij te houden van uw huidige momentopnamen aanbieden. Het volgende voorbeeld wordt een vooraf gedefinieerde blob en aanroepen de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet voor het weergeven van de momentopnamen van de blob.  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a>Het kopiëren van een momentopname van een blob
U kunt een momentopname van een blob om te herstellen van de momentopname kopiëren. Zie voor gedetailleerde informatie en beperkingen [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Het volgende voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context. In het voorbeeld definieert vervolgens de naam van container en blob variabelen. In het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode om een momentopname te maken. Klik in het voorbeeld wordt uitgevoerd de [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet voor het kopiëren van de momentopname van een blob met behulp van het object ICloudBlob voor de bron-blob. Zorg ervoor dat de variabelen op basis van uw configuratie voordat u het voorbeeld. Houd er rekening mee dat het volgende voorbeeld wordt verondersteld dat de bron en bestemming containers en de bron-blob al bestaat.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

U hebt geleerd hoe u Azure blobs beheren en blob-momentopnamen met Azure PowerShell, gaat u naar de volgende sectie voor informatie over het beheren van tabellen, wachtrijen en -bestanden.

## <a name="how-to-manage-azure-tables-and-table-entities"></a>Azure-tabellen en tabelentiteiten beheren
Azure Table storage-service is een NoSQL-gegevensarchief, waarin u kunt opslaan en grote sets gestructureerde, niet-relationele gegevens opvragen. De belangrijkste onderdelen van de service zijn tabellen, entiteiten en eigenschappen. Een tabel is een verzameling entiteiten. Een entiteit is een set eigenschappen. Elke entiteit kan maximaal 252 eigenschappen die alle naam / waarde-paren hebben. Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten met Azure Table Storage-Service bent. Zie voor gedetailleerde informatie [inzicht in de tabel Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) en [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md).

In de volgende subsecties leert u hoe Azure Table storage-service met Azure PowerShell beheren. De scenario's worden behandeld: **maken**, **verwijderen**, en **bij het ophalen van** **tabellen**, evenals **toe te voegen**, **opvragen**, en **tabelentiteiten verwijderen**.

### <a name="how-to-create-a-table"></a>Het maken van een tabel
Elke tabel moet zich bevinden in een Azure storage-account. Het volgende voorbeeld laat zien hoe u een tabel maken in Azure Storage. In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens wordt de [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet om een tabel maken in Azure Storage.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a>Het ophalen van een tabel
U kunt een query en ophalen van een of alle tabellen in een opslagaccount. Het volgende voorbeeld toont hoe voor het ophalen van een tabel met de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Als u de cmdlet Get-AzureStorageTable zonder parameters aanroept, krijgt alle opslagtabellen voor een opslagaccount.

### <a name="how-to-delete-a-table"></a>Het verwijderen van een tabel
U kunt een tabel uit een opslagaccount verwijderen met behulp van de [verwijderen AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a>Tabelentiteiten beheren
Azure PowerShell biedt momenteel geen cmdlets voor het beheren van tabelentiteiten rechtstreeks. Om bewerkingen uitvoeren op tabelentiteiten, kunt u de klassen die zijn opgegeven in de [Azure Storage-clientbibliotheek voor .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-to-add-table-entities"></a>Het toevoegen van tabelentiteiten
Als u wilt een entiteit toevoegen aan een tabel, moet u eerst een object dat de entiteitseigenschappen van uw bepaalt maken. Een entiteit kan maximaal 255 eigenschappen, waaronder 3 eigenschappen hebben: **PartitionKey**, **RowKey**, en **tijdstempel**. U bent zelf verantwoordelijk voor het invoegen en het bijwerken van de waarden van **PartitionKey** en **RowKey**. De server beheert de waarde van **tijdstempel**, die niet worden gewijzigd. Samen de **PartitionKey** en **RowKey** unieke identificatie van elke entiteit in een tabel.

* **PartitionKey**: bepaalt de partitie die de entiteit is opgeslagen in.
* **RowKey**: een unieke identificatie van de entiteit in de partitie.

U kunt maximaal 252 aangepaste eigenschappen voor een entiteit kan definiëren. Zie voor meer informatie [inzicht in de tabel Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Het volgende voorbeeld laat zien hoe entiteiten toevoegen aan een tabel. In het voorbeeld laat zien hoe op te halen van de werknemerstabel en verschillende entiteiten in de App toevoegen. Deze maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens haalt de opgegeven tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Als de tabel niet bestaat, de [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet gebruikt voor het maken van een tabel in Azure Storage. Het voorbeeld wordt vervolgens een aangepaste functie toevoegen-entiteit entiteiten toevoegen aan de tabel door elke entiteit partitie en rijsleutel te geven. De Add-entiteit functieaanroepen de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet uit op de [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasse voor het maken van een entiteitsobject. Later in het voorbeeld wordt de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) methode voor dit entiteitsobject toe te voegen aan een tabel.

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a>Een query tabelentiteiten
Om te vragen een tabel, gebruikt u de [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasse. Het volgende voorbeeld wordt ervan uitgegaan dat u het script dat is opgegeven in de manier waarop al hebt uitgevoerd om toe te voegen entiteiten gedeelte van deze handleiding. In het voorbeeld maakt eerst een verbinding met Azure Storage met de opslag-context, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens wordt geprobeerd om op te halen van de eerder gemaakte 'werknemers' tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Het aanroepen van de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet uit op de klasse Microsoft.WindowsAzure.Storage.Table.TableQuery maakt een nieuwe query-object. In het voorbeeld wordt gezocht naar de entiteiten die een 'ID-kolom waarvan de waarde 1 zoals opgegeven in een tekenreeks-filter is. Zie voor gedetailleerde informatie [opvragen van tabellen en entiteiten](http://msdn.microsoft.com/library/azure/dd894031.aspx). Wanneer u deze query uitvoert, wordt alle entiteiten die overeenkomen met de filtercriteria.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a>Het verwijderen van de tabelentiteiten
U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen. Het volgende voorbeeld wordt ervan uitgegaan dat u het script dat is opgegeven in de manier waarop al hebt uitgevoerd om toe te voegen entiteiten gedeelte van deze handleiding. In het voorbeeld maakt eerst een verbinding met Azure Storage met de opslag-context, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens wordt geprobeerd om op te halen van de eerder gemaakte 'werknemers' tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Als de tabel bestaat, in het voorbeeld wordt de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) methode voor het ophalen van een entiteit op basis van de bijbehorende sleutelwaarden partitie en rij. Geeft u de entiteit de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) methode om te verwijderen.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a>Het beheren van Azure-wachtrijen en -berichten in wachtrij plaatsen
Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen. Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten met Azure Queue Storage-Service bent. Zie voor gedetailleerde informatie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md).

Deze sectie wordt beschreven hoe u voor het beheren van Azure Queue storage-service met Azure PowerShell. De scenario's worden behandeld: **invoegen** en **verwijderen** wachtrij berichten, evenals **maken**, **verwijderen**, en **bij het ophalen van wachtrijen**.

### <a name="how-to-create-a-queue"></a>Een wachtrij maken
Het volgende voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens roept [nieuw AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet voor het maken van een wachtrij met de naam 'wachtrijnaam'.

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Zie voor informatie over naamgevingsregels voor Azure Queue-Service, [naamgeving van wachtrijen en metagegevens](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-to-retrieve-a-queue"></a>Het ophalen van een wachtrij
U kunt een query en ophalen van een specifieke wachtrij of een lijst met alle wachtrijen in een opslagaccount. Het volgende voorbeeld toont hoe voor het ophalen van een opgegeven wachtrij met de [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Als u de [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet zonder parameters voor het ophalen van een lijst met alle wachtrijen.

### <a name="how-to-delete-a-queue"></a>Het verwijderen van een wachtrij
Roep de cmdlet Remove-AzureStorageQueue voor het verwijderen van een wachtrij en alle berichten hierin. Het volgende voorbeeld laat zien hoe een opgegeven wachtrij met de cmdlet Remove-AzureStorageQueue verwijderen.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a>Het invoegen van een bericht in een wachtrij
Als u wilt invoegen van een bericht in een bestaande wachtrij maakt een nieuw exemplaar van de [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse. Daarna roept u de methode [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) aan. Een CloudQueueMessage kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.

Het volgende voorbeeld laat zien hoe bericht toevoegen aan een wachtrij. In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel. Vervolgens haalt de opgegeven wachtrij met behulp van de [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Als de wachtrij bestaat, de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet gebruikt voor het maken van een exemplaar van de [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse. Later in het voorbeeld wordt de [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode voor dit berichtobject toe te voegen aan een wachtrij. Hier volgt een code die een wachtrij opgehaald en het bericht 'MessageInfo':

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a>Hoe u het volgende bericht uit de wachtrij
Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd. Als u aanroept de [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) methode, krijgt u het volgende bericht in een wachtrij. Een bericht dat wordt geretourneerd door **GetMessage**, wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij. Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen de [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) methode. Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen. Uw code haalt **DeleteMessage** op zodra het bericht is verwerkt.

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a>Azure-bestandsshares en bestanden beheren
Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van het standaard SMB-protocol. Microsoft Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via de API van File storage of Azure PowerShell.

Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) en [REST-API van bestand](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-to-set-and-query-storage-analytics"></a>Het instellen en query storage analytics
U kunt [Azure Storage Analytics](storage-analytics.md) voor het verzamelen van metrische gegevens voor uw Azure storage-accounts en meld u gegevens over aanvragen die worden verzonden naar uw opslagaccount. Metrische gegevens storage kunt u de status van een opslagaccount en opslag logboekregistratie voor het diagnosticeren en oplossen van problemen met uw opslagaccount. U kunt configureren met behulp van de Azure-portal of de Windows PowerShell of programmatisch met behulp van de storage-clientbibliotheek bewaking. Opslag logboekregistratie gebeurt serverzijde en kunt u de details van de records voor geslaagde en mislukte aanvragen in uw opslagaccount. Deze logboeken kunnen u de details van lezen, schrijven en verwijderen van bewerkingen op tabellen, wachtrijen en blobs, evenals de redenen voor mislukte aanvragen.

Zie voor meer informatie over het inschakelen en weergeven van metrische gegevens Storage-gegevens met behulp van PowerShell, [inschakelen met behulp van PowerShell metrische gegevens Storage](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

Zie voor meer informatie over het inschakelen en ophalen van gegevens van registratie van opslag met behulp van PowerShell, [opslag logboekregistratie met behulp van PowerShell inschakelen](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) en [zoeken naar uw logboekgegevens opslag logboekregistratie](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Zie voor gedetailleerde informatie over het gebruik van opslag metrische gegevens en opslag logboekregistratie met opslag oplossen [bewaking, diagnose en het oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a>Shared Access Signature (SAS) en opgeslagen toegangsbeleid beheren
Shared access signatures zijn een belangrijk onderdeel van het beveiligingsmodel voor elke toepassing met behulp van Azure Storage. Ze zijn nuttig voor het bieden van beperkte machtigingen naar uw opslagaccount aan clients die niet de accountsleutel moeten hebben. Standaard kan alleen de eigenaar van het storage-account toegang tot blobs, tabellen en wachtrijen in dat account. Als uw service of toepassing moet deze resources beschikbaar te maken voor andere clients zonder het delen van uw toegangssleutel, hebt u drie opties:

* Stel de machtigingen van een container toe te staan anonieme leestoegang tot de container en de blobs. Dit is niet toegestaan voor tabellen of wachtrijen.
* Gebruik een shared access signature die verleent rechten voor containers, blobs, wachtrijen en tabellen voor een bepaald tijdsinterval beperkte.
* Met een opgeslagen toegangsbeleid kunt u een extra verificatieniveau controle over handtekeningen voor gedeelde toegang voor een container of de blobs, voor een wachtrij of voor een tabel. Het opgeslagen toegangsbeleid kunt u de begintijd, de verlooptijd of de machtigingen voor een handtekening te wijzigen of om af te trekken nadat deze is uitgegeven.

Een shared access signature kan worden gebruikt in een van twee vormen:

* **Ad-hoc SAS**: wanneer u een ad-hoc SAS, de begintijd, de verlooptijd, maakt en machtigingen voor de SAS zijn opgegeven op de SAS-URI. Dit type SAS kan worden gemaakt op een container, blob, table of wachtrij en het is niet worden ingetrokken.
* **SAS met opgeslagen toegangsbeleid**: een opgeslagen-beleid is gedefinieerd in een resourcecontainer een blob-container, een tabel of een wachtrij - en u kunt deze gebruiken voor het beheren van beperkingen voor een of meer handtekeningen voor gedeelde toegang. Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, neemt de SAS de beperkingen - de begintijd, verlooptijd en machtigingen - gedefinieerd voor het opgeslagen toegangsbeleid. Dit type SAS is worden ingetrokken.

Zie voor meer informatie [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) en [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md).

In de volgende gedeelten leert u hoe u een beleid voor gedeelde toegang handtekening access token en de opslag voor Azure-tabellen maakt. Azure PowerShell biedt vergelijkbare cmdlets voor containers, blobs en wachtrijen ook. Als u wilt de scripts uitvoeren in deze sectie, downloaden de [Azure PowerShell versie 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) of hoger.

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a>Het maken van een op beleid gebaseerde Shared Access Signature-token
Gebruik de cmdlet New-AzureStorageTableStoredAccessPolicy voor het maken van een nieuw opgeslagen-beleid. Roep vervolgens de [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet voor het maken van een nieuw token van de handtekening gedeelde toegang op basis van beleid voor een Azure Storage-tabel.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Het maken van een ad-hoc (niet terughalen) Shared Access Signature-token
Gebruik de [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet voor het maken van een nieuw ad-hoc (niet terughalen) Shared Access Signature-token voor een Azure Storage-tabel:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a>Het maken van een opgeslagen-beleid
Gebruik de cmdlet New-AzureStorageTableStoredAccessPolicy voor het maken van een nieuwe opgeslagen toegangsbeleid voor een Azure Storage-tabel:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a>Het bijwerken van een opgeslagen-beleid
Gebruik de cmdlet Set-AzureStorageTableStoredAccessPolicy een bestaand opgeslagen toegangsbeleid voor een Azure Storage-tabel bijwerken:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a>Het verwijderen van een opgeslagen-beleid
Gebruik de cmdlet Remove-AzureStorageTableStoredAccessPolicy verwijderen van een opgeslagen-beleid in de tabel in een Azure Storage:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a>Azure Storage gebruiken voor de Amerikaanse overheid en Azure voor China
Een Azure-omgeving is een onafhankelijke implementatie van Microsoft Azure, zoals [Azure Government voor de overheid van de VS](https://azure.microsoft.com/features/gov/), [AzureCloud voor globale Azure](https://portal.azure.com), en [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/). U kunt nieuwe Azure-omgevingen voor Amerikaanse overheid en Azure voor China implementeren.

Voor het gebruik van Azure Storage met AzureChinaCloud, moet u een opslag-context die is gekoppeld aan AzureChinaCloud maken. Volg deze stappen om u aan de slag:

1. Voer de [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet om te controleren van de beschikbare Azure-omgevingen:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Een Azure China-account toevoegen aan Windows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Maak een context opslag voor een account AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

Azure Storage met gebruiken [VS Azure Government](https://azure.microsoft.com/features/gov/), moet u een nieuwe omgeving definiëren en vervolgens een nieuwe opslag context maken met deze omgeving:

1. Voer de [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet om te controleren van de beschikbare Azure-omgevingen:

    ```powershell
    Get-AzureEnvironment
    ```

2. Een Azure US Government-account toevoegen aan Windows PowerShell:
   
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
In deze handleiding hebt u geleerd hoe Azure Storage met Azure PowerShell beheren. Hier volgen enkele verwante artikelen en resources voor meer informatie hierover.

* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [PowerShell-Cmdlets voor Azure-opslag](/powershell/module/azurerm.storage/#storage)
* [Windows PowerShell-referentie](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
