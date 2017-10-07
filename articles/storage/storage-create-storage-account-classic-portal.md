---
title: aaaHow toocreate, beheren of verwijderen van een opslagaccount in de klassieke Azure-portal Hallo | Microsoft Docs
description: Een nieuw opslagaccount maken, de toegangssleutels van uw account te beheren of verwijderen van een opslagaccount in hello Azure-portal. Meer informatie over Standard en Premium Storage-accounts.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Over Azure-opslagaccounts
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Overzicht
Een Azure-opslag biedt u toegang tot Azure Blob, Queue, Table en bestand services toohello in Azure Storage. Uw opslagaccount biedt Hallo unieke naamruimte voor uw Azure Storage-gegevensobjecten. Hallo-gegevens in uw account is standaard beschikbaar alleen tooyou Hallo accounteigenaar.

Er zijn twee typen opslagaccounts:

* Een Standard-opslagaccount omvat Blob Storage, Table Storage, Queue Storage en File Storage.
* Een Premium Storage-account biedt momenteel alleen ondersteuning voor schijven van virtuele Azure-machines. Zie [Premium Storage: krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md) voor een gedetailleerd overzicht van Premium Storage.

## <a name="storage-account-billing"></a>Facturering voor opslagaccounts
U wordt gefactureerd voor het gebruik van Azure Storage op basis van uw opslagaccount. De opslagkosten worden gebaseerd op vier factoren: opslagcapaciteit, replicatieschema, opslagtransacties en uitgaande gegevens.

* Opslagcapaciteit verwijst toohow veel aandeel van uw opslag u toostore gegevens gebruikt. Hallo kosten van het opslaan van uw gegevens wordt bepaald door hoeveel gegevens u opslaat en hoe deze worden gerepliceerd.
* Replicatie staat voor hoeveel kopieën van uw gegevens gelijktijdig worden bewaard en op welke locaties.
* Transacties verwijzen tooall lezen en schrijven operations tooAzure opslag.
* Uitgaande gegevens verwijst toodata overgebracht buiten een Azure-regio. Wanneer Hallo-gegevens in uw opslagaccount worden geopend door een toepassing die niet wordt uitgevoerd in Hallo dezelfde regio, of die van toepassing is een cloudservice of een ander type van de toepassing, vervolgens worden in rekening gebracht voor uitgaande gegevens. (Voor Azure-services, kunt u stappen toogroup nemen uw gegevens en services in Hallo dezelfde gegevens tooreduce gecentreerd of kosten voor uitgaande gegevens elimineren.)  

Hallo [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage) pagina bevat gedetailleerde informatie over de prijzen voor opslagcapaciteit, replicatie en transacties. Hallo [prijsinformatie over gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/) pagina bevat gedetailleerde informatie over de prijzen voor uitgaande gegevens.

Zie [Schaalbaarheids- en prestatiedoelen in Azure Storage](storage-scalability-targets.md) voor meer informatie over opslagaccountcapaciteit en prestatiedoelen.

> [!NOTE]
> Bij het maken van een virtuele machine van Azure wordt storage-account u automatisch gemaakt op Hallo implementatielocatie als u nog geen storage-account op die locatie. Het is daarom niet nodig toofollow Hallo stappen hieronder toocreate een opslagaccount voor uw virtuele machine-schijven. Hallo opslagaccountnaam wordt gebaseerd op de naam van de virtuele machine Hallo. Zie Hallo [documentatie bij Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/) voor meer informatie.
> 
> 

## <a name="create-a-storage-account"></a>Een opslagaccount maken
1. Meld u aan toohello [klassieke Azure-Portal](https://manage.windowsazure.com).
2. Klik op **nieuw** in de taakbalk Hallo HALLO hallo pagina onderaan in. Kies **Data Services** | **Opslag** en klik vervolgens op **Snelle invoer**.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. Voer in **URL** een naam in voor het opslagaccount.
   
   > [!NOTE]
   > Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.
   > 
   > De naam van uw opslagaccount moet uniek zijn binnen Azure. Hallo klassieke Azure-Portal wordt aangegeven als Hallo opslagaccountnaam die u selecteert al in gebruik.
   > 
   > 
   
    Zie [eindpunten van Opslagaccounts](#storage-account-endpoints) hieronder voor details over hoe de opslagaccountnaam Hallo gebruikte tooaddress, worden uw objecten in Azure Storage.
4. In **locatie/Affiniteitsgroep**, selecteer een locatie voor uw opslagaccount, dat wil zeggen sluiten tooyou of tooyour klanten. Als gegevens in uw storage-account kan worden bereikt vanaf een andere Azure-service, zoals een virtuele machine van Azure of een cloudservice, kunt u een affiniteitsgroep uit Hallo lijst toogroup tooselect uw opslagaccount in Hallo hetzelfde datacentrum als andere Azure-services Gebruik tooimprove prestaties en kosten te verlagen.
   
    U moet een affiniteitsgroep selecteren bij het aanmaken van een opslagaccount. U kunt een bestaande account tooan affiniteitsgroep niet verplaatsen. Voor meer informatie over affiniteitsgroepen ziet u [Serviceco-locatie met een affiniteitsgroep](#service-co-location-with-an-affinity-group) hieronder.
   
   > [!IMPORTANT]
   > toodetermine welke locaties beschikbaar voor uw abonnement zijn, kunt u Hallo aanroepen [alle resourceproviders vermelden](https://msdn.microsoft.com/library/azure/dn790524.aspx) bewerking. toolist providers via PowerShell, roepen [Get-AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). Gebruik in .NET Hallo [lijst](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) methode Hallo klasse provideroperationsextensions.
   > 
   > Zie ook [Azure-gebieden](https://azure.microsoft.com/regions/#services) voor meer informatie over welke services beschikbaar zijn in welke regio.
   > 
   > 
5. Als u meer dan één Azure-abonnement hebt, Hallo **abonnement** veld wordt weergegeven. In **abonnement**, hello Azure-abonnement dat u wilt dat toouse Hallo storage-account met invoeren.
6. In **replicatie**, selecteer Hallo gewenste replicatieniveau voor uw opslagaccount. Hallo aanbevolen replicatieoptie is geografisch redundante replicatie, waarbij maximale duurzaamheid voor uw gegevens biedt. Zie [Azure Storage-replicatie](storage-redundancy.md) voor meer informatie over Azure Storage-replicatieopties.
7. Klik op **Opslagaccount maken**.
   
    Het duurt enkele minuten toocreate uw storage-account. status van de toocheck Hallo Hallo meldingen onderin Hallo Hallo klassieke Azure-Portal kunt bewaken. Nadat het Hallo-storage-account is gemaakt, wordt uw nieuwe opslagaccount heeft **Online** status en is klaar voor gebruik.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Eindpunten van opslagaccount
Elk object dat u in Azure Storage opslaat, heeft een uniek URL-adres. Hallo storage account name formulieren Hallo subdomein van dat adres. Hallo combinatie van subdomein- en domeinnaam, die specifieke tooeach service, vormt een *eindpunt* voor uw opslagaccount.

Bijvoorbeeld, als de naam van uw opslagaccount *mystorageaccount*, Hallo Standaardeindpunten voor uw opslagaccount:

* Blob service: http://*mystorageaccount*.blob.core.windows.net
* Tabelservice: http://*mystorageaccount*.table.core.windows.net
* Queue-service: http://*mystorageaccount*.queue.core.windows.net
* File-service: http://*mystorageaccount*.file.core.windows.net

U ziet Hallo eindpunten voor uw opslagaccount op Hallo opslagdashboard in Hallo [klassieke Azure-Portal](https://manage.windowsazure.com) zodra Hallo-account is gemaakt.

Hallo-URL voor het openen van een object in een opslagaccount wordt samengesteld door de locatie van Hallo object in Hallo storage account toohello eindpunt toe te voegen. Een blobadres kan bijvoorbeeld de volgende indeling hebben: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

U kunt ook een aangepast domein naam toouse configureren met uw opslagaccount. Zie [Een aangepaste domeinnaam configureren voor het eindpunt voor Blob Storage](storage-custom-domain-name.md) voor meer informatie.

### <a name="service-co-location-with-an-affinity-group"></a>Serviceco-locatie met een affiniteitsgroep
Een *affiniteitsgroep* is een geografische groepering van uw Azure-services en virtuele machines met uw Azure-opslagaccount. Een affiniteitsgroep kunt serviceprestaties verbeteren door computerwerkbelastingen in Hallo dezelfde gegevens centreren of in de buurt van Hallo gebruikersdoelgroep. Bovendien geen kosten worden gebracht voor uitgaande gegevens wanneer gegevens in een opslagaccount worden geopend via een andere service die deel uitmaakt van Hallo dezelfde affiniteitsgroep.

> [!NOTE]
> toocreate een affiniteitsgroep open Hallo <b>instellingen</b> gebied Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), klikt u op <b>Affiniteitsgroepen</b>, en klikt u ofwel <b>toevoegen een affiniteitsgroep</b> of Hallo <b>toevoegen</b> knop. U kunt ook maken en beheren van affiniteitsgroepen via hello Azure Service Management-API. Zie <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Bewerkingen voor affiniteitsgroepen</a> voor meer informatie.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren
Wanneer u een opslagaccount maakt, genereert Azure twee 512-bits opslagtoegangssleutels, die worden gebruikt voor verificatie bij Hallo opslagaccount wordt geopend. Dankzij de twee opslagtoegangssleutels, kunt Azure u tooregenerate Hallo sleutels zonder onderbreking tooyour storage-service of toothat-access-service.

> [!NOTE]
> We raden u aan uw opslagtoegangssleutels met niemand anders te delen. toopermit toegang tot bronnen toostorage zonder opgave van uw toegangssleutels, kunt u een *shared access signature voor*. Een shared access signature biedt toegang tot tooa resource in uw account voor een interval dat u definieert en met Hallo machtigingen die u opgeeft. Zie [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) voor meer informatie.
> 
> 

In Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), gebruik **sleutels beheren** op Hallo dashboard of Hallo **opslag** pagina tooview, kopiëren en opnieuw genereren Hallo opslagtoegangssleutels die worden gebruikt tooaccess hello Blob, Table en Queue-services.

### <a name="copy-a-storage-access-key"></a>Een toegangssleutel voor opslag kopiëren
U kunt **sleutels beheren** toocopy een toegang tot opslag toouse sleutel in een verbindingsreeks. Hallo-verbindingsreeks moet Hallo opslagaccountnaam en een sleutel toouse bij de verificatie. Zie voor informatie over het configureren van connection strings tooaccess Azure storage-services, [Azure Storage-verbindingsreeksen configureren](storage-configure-connection-string.md).

1. In Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), klikt u op **opslag**, en klik vervolgens op Hallo-naam van Hallo storage account tooopen Hallo dashboard.
2. Klik op **Sleutels beheren**.
   
     **Toegangssleutels beheren** wordt geopend.
   
    ![Sleutels beheren](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy een toegangssleutel voor opslag, selecteer Hallo Sleuteltekst. Klik met de rechtermuisknop en klik op **Kopiëren**.

### <a name="regenerate-storage-access-keys"></a>Opslagtoegangssleutels opnieuw genereren
We raden u Hallo toegangstoetsen tooyour storage account periodiek toohelp ervoor dat uw Opslagverbindingen veilig te wijzigen. Twee toegangssleutels toegewezen zodat u verbindingen toohello storage-account onderhouden kunt met behulp van één toegangssleutel tijdens het genereren van Hallo andere toegangssleutel.

> [!WARNING]
> Opnieuw genereren van uw toegangssleutels kan invloed hebben op services in Azure en uw eigen toepassingen die afhankelijk van Hallo storage-account zijn. Alle clients die gebruikmaken van Hallo toegang sleutel tooaccess Hallo storage-account moet bijgewerkte toouse Hallo nieuwe sleutel.
> 
> 

**Mediaservices** -als u mediaservices die afhankelijk van uw storage-account zijn hebt, moet u opnieuw synchroniseren Hallo toegangstoetsen met uw mediaservice nadat u Hallo sleutels opnieuw genereert.

**Toepassingen** : als u webtoepassingen of cloud services-die gebruik Hallo storage-account, wordt Hallo verbinding verbroken als u opnieuw sleutels genereert, tenzij u uw sleutels rouleert. 

**Storage Explorers** : als u werkt met [opslagverkennertoepassingen](storage-explorers.md), moet u waarschijnlijk tooupdate Hallo-opslagsleutel is gebruikt in deze toepassingen.

Hier volgt Hallo-proces voor roulatie van uw toegangssleutels voor opslag:

1. Werk de verbindingsreeksen Hallo in uw toepassing code tooreference Hallo secundaire toegangssleutel van Hallo storage-account.
2. Genereer Hallo primaire toegangssleutel voor uw opslagaccount opnieuw. In Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), vanuit het Hallo-dashboard of Hallo **configureren** pagina, klikt u op **sleutels beheren**. Klik op **genereren** onder Hallo primaire toegangssleutel en klik vervolgens op **Ja** tooconfirm dat u wilt dat een nieuwe sleutel toogenerate.
3. Werk de verbindingsreeksen Hallo in uw code tooreference Hallo nieuwe primaire toegangssleutel.
4. Genereer de secundaire toegangssleutel Hallo opnieuw.

## <a name="delete-a-storage-account"></a>Een opslagaccount verwijderen
een opslagaccount dat u niet langer gebruikt, gebruik tooremove **verwijderen** op Hallo dashboard of Hallo **configureren** pagina. **Verwijder** verwijderingen Hallo hele opslagaccount, inclusief alle Hallo blobs, tabellen en wachtrijen in Hallo-account.

> [!WARNING]
> Het is niet mogelijk toorestore een verwijderd opslagaccount of Hallo-inhoud die het vóór verwijdering bevatte te halen. Ervoor tooback niets worden u toosave voordat u Hallo account verwijdert. Dit geldt ook voor alle resources in Hallo-account: als u een blob, table, wachtrij of bestand verwijdert, wordt deze blijvend verwijderd.
> 
> Als uw opslagaccount bevat de VHD-bestanden voor een virtuele machine van Azure, moet vervolgens u alle installatiekopieën en schijven die worden gebruikt die VHD-bestanden voordat u Hallo opslagaccount kunt verwijderen. Stop eerst Hallo virtuele machine als deze wordt uitgevoerd en vervolgens te verwijderen. toodelete schijven, navigeer toohello **schijven** tabblad en verwijdert u alle schijven. toodelete afbeeldingen, navigeer toohello **installatiekopieën** tabblad en verwijdert u alle installatiekopieën die zijn opgeslagen in het Hallo-account.
> 
> 

1. In Hallo [klassieke Azure-Portal](https://manage.windowsazure.com), klikt u op **opslag**.
2. Klik ergens in de opslagaccountvermelding Hallo behalve Hallo naam en klik vervolgens op **verwijderen**.
   
     - Of -
   
    Klik op de naam Hallo van Hallo storage account tooopen Hallo dashboard en klik vervolgens op **verwijderen**.
3. Klik op **Ja** tooconfirm gewenste toodelete Hallo storage-account.

## <a name="next-steps"></a>Volgende stappen
* toolearn meer informatie over Azure Storage, Zie Hallo [documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/).
* Ga naar Hallo [Blog van Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/).
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)

