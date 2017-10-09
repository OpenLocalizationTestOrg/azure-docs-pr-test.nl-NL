---
title: aaaHow toocreate, beheren of verwijderen van een opslagaccount in hello Azure-portal | Microsoft Docs
description: Een nieuw opslagaccount maken, de toegangssleutels van uw account te beheren of verwijderen van een opslagaccount in hello Azure-portal. Meer informatie over Standard en Premium Storage-accounts.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Over Azure-opslagaccounts
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Overzicht
Een Azure-opslagaccount biedt een unieke naamruimte toostore en toegang tot uw Azure Storage-gegevensobjecten. Alle objecten in een opslagaccount worden samen gefactureerd als een groep. Hallo-gegevens in uw account is standaard beschikbaar alleen tooyou Hallo accounteigenaar.

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Facturering voor opslagaccounts
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Bij het maken van een virtuele machine van Azure wordt storage-account u automatisch gemaakt op Hallo implementatielocatie als u nog geen storage-account op die locatie. Het is daarom niet nodig toofollow Hallo stappen hieronder toocreate een opslagaccount voor uw virtuele machine-schijven. Hallo opslagaccountnaam wordt gebaseerd op de naam van de virtuele machine Hallo. Zie Hallo [documentatie bij Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/) voor meer informatie.
> 
> 

## <a name="storage-account-endpoints"></a>Eindpunten van opslagaccount
Elk object dat u in Azure Storage opslaat, heeft een uniek URL-adres. Hallo storage account name formulieren Hallo subdomein van dat adres. Hallo combinatie van subdomein- en domeinnaam, die specifieke tooeach service, vormt een *eindpunt* voor uw opslagaccount.

Bijvoorbeeld, als de naam van uw opslagaccount *mystorageaccount*, Hallo Standaardeindpunten voor uw opslagaccount:

* Blob service: http://*mystorageaccount*.blob.core.windows.net
* Tabelservice: http://*mystorageaccount*.table.core.windows.net
* Queue-service: http://*mystorageaccount*.queue.core.windows.net
* File-service: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Een Blob storage-account toont alleen Hallo eindpunt voor Blob-service.
> 
> 

Hallo-URL voor het openen van een object in een opslagaccount wordt samengesteld door de locatie van Hallo object in Hallo storage account toohello eindpunt toe te voegen. Een blobadres kan bijvoorbeeld de volgende indeling hebben: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

U kunt ook een aangepast domein naam toouse configureren met uw opslagaccount. Zie [Een aangepaste domeinnaam configureren voor het eindpunt voor Blob Storage](../blobs/storage-custom-domain-name.md) voor meer informatie. U kunt dit ook configureren met PowerShell. Zie voor meer informatie, Hallo [Set AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.  


## <a name="create-a-storage-account"></a>Een opslagaccount maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer op de Hub-menu Hallo **nieuw** -> **opslag** -> **opslagaccount**.
3. Voer een naam in voor het opslagaccount. Zie [eindpunten van Opslagaccounts](#storage-account-endpoints) voor details over hoe de opslagaccountnaam Hallo gebruikte tooaddress, worden uw objecten in Azure Storage.
   
   > [!NOTE]
   > Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten.
   > 
   > De naam van uw opslagaccount moet uniek zijn binnen Azure. Hello Azure-portal wordt aangegeven of Hallo opslagaccountnaam u zich al in gebruik.
   > 
   > 
4. Geef Hallo deployment model toobe gebruikt: **Resource Manager** of **klassieke**. **Resource Manager** hello wordt aanbevolen implementatiemodel. Zie [Resource Manager-implementatie en klassieke implementatie begrijpen](../../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie.
   
   > [!NOTE]
   > BLOB storage-accounts kunnen alleen worden gemaakt met behulp van Hallo Resource Manager-implementatiemodel.

5. Selecteer Hallo type opslagaccount: **algemeen** of **Blob storage**. **Algemeen** Hallo standaard is.
   
    Als **algemeen** is geselecteerd, geeft u vervolgens de prestatielaag Hallo: **standaard** of **Premium**. Hallo standaardwaarde is **standaard**. Zie voor meer informatie over standard en premium storage-accounts, [tooMicrosoft inleiding Azure Storage](storage-introduction.md) en [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md).
   
    Als **Blob Storage** is geselecteerd, geeft u vervolgens de toegangslaag Hallo: **Hot** of **Cool**. Hallo standaardwaarde is **Hot**. Zie [Azure Blob Storage: Hot Storage-laag en Cool Storage-laag](../blobs/storage-blob-storage-tiers.md) voor meer informatie.
6. Selecteer de replicatieoptie Hallo voor Hallo storage-account: **LRS**, **GRS**, **RA-GRS**, of **ZRS**. Hallo standaardwaarde is **RA-GRS**. Zie [Azure Storage-replicatie](storage-redundancy.md) voor meer informatie over Azure Storage-replicatieopties.
7. Hallo-abonnement waaraan u toocreate Hallo nieuw opslagaccount wilt selecteren.
8. Geef een nieuwe resourcegroep op of selecteer een bestaande resourcegroep. Zie [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
9. Selecteer Hallo geografische locatie voor uw opslagaccount. Zie [Azure-regio’s](https://azure.microsoft.com/regions/#services) voor meer informatie over welke services beschikbaar zijn in welke regio.
10. Klik op **maken** toocreate Hallo storage-account.

## <a name="manage-your-storage-account"></a>Uw opslagaccount beheren
### <a name="change-your-account-configuration"></a>De configuratie van uw account wijzigen
Nadat u uw storage-account maakt, kunt u de configuratie, zoals het wijzigen van Hallo replicatie-optie gebruikt voor het Hallo-account of veranderende Hallo toegangslaag voor een Blob storage-account wijzigen. In Hallo [Azure-portal](https://portal.azure.com), navigeer tooyour storage-account, zoeken en klik op **configuratie** onder **instellingen** Hallo-accountconfiguratie tooview en/of wijzigen.

> [!NOTE]
> Afhankelijk van Hallo prestatielaag die u hebt gekozen bij het maken van Hallo storage-account, sommige replicatieopties mogelijk niet beschikbaar.
> 
> 

Hallo replicatie-optie wijzigen wordt uw prijscategorie wijzigen. Zie de pagina [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor meer informatie.

Voor Blob storage-accounts wijzigen van de toegangslaag Hallo mogelijk kosten wijzigen voor Hallo bovendien toochanging uw prijscategorie. Zie Hallo [Blob storage-accounts: prijzen en facturering](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) voor meer informatie.

### <a name="manage-your-storage-access-keys"></a>De toegangssleutels van uw opslagaccount beheren
Wanneer u een opslagaccount maakt, genereert Azure twee 512-bits opslagtoegangssleutels, die worden gebruikt voor verificatie bij Hallo opslagaccount wordt geopend. Dankzij de twee opslagtoegangssleutels, kunt Azure u tooregenerate Hallo sleutels zonder onderbreking tooyour storage-service of toothat-access-service.

> [!NOTE]
> We raden u aan uw opslagtoegangssleutels met niemand anders te delen. toopermit toegang tot bronnen toostorage zonder opgave van uw toegangssleutels, kunt u een *shared access signature voor*. Een shared access signature biedt toegang tot tooa resource in uw account voor een interval dat u definieert en met Hallo machtigingen die u opgeeft. Zie [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Shared Access Signatures (SAS) gebruiken) voor meer informatie.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Opslagtoegangssleutels bekijken en kopiëren
In Hallo [Azure-portal](https://portal.azure.com), navigeer tooyour storage-account, klikt u op **alle instellingen** en klik vervolgens op **toegangssleutels** tooview, kopiëren en opnieuw genereren van de toegangssleutels van uw account. Hallo **toegangstoetsen** blade bevat ook vooraf geconfigureerde verbindingsreeksen die gebruikmaken van uw primaire en secundaire sleutels die u kunt toouse in uw toepassingen te kopiëren.

#### <a name="regenerate-storage-access-keys"></a>Opslagtoegangssleutels opnieuw genereren
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
2. Genereer Hallo primaire toegangssleutel voor uw opslagaccount opnieuw. Op Hallo **toegangssleutels** blade, klikt u op **sleutel 1 opnieuw genereren**, en klik vervolgens op **Ja** tooconfirm dat u wilt dat een nieuwe sleutel toogenerate.
3. Werk de verbindingsreeksen Hallo in uw code tooreference Hallo nieuwe primaire toegangssleutel.
4. Sleutel opnieuw genereren Hallo secundaire toegang in Hallo dezelfde manier.

## <a name="delete-a-storage-account"></a>Een opslagaccount verwijderen
tooremove een opslagaccount dat u niet langer gebruikt, gaat u toohello storage-account in Hallo [Azure-portal](https://portal.azure.com), en klik op **verwijderen**. Een opslagaccount verwijdert, worden Hallo hele account, inclusief alle gegevens in het Hallo-account.

> [!WARNING]
> Het is niet mogelijk toorestore een verwijderd opslagaccount of Hallo-inhoud die het vóór verwijdering bevatte te halen. Ervoor tooback niets worden u toosave voordat u Hallo account verwijdert. Dit geldt ook voor alle resources in Hallo-account: als u een blob, table, wachtrij of bestand verwijdert, wordt deze blijvend verwijderd.
> 

Als u een opslagaccount die is gekoppeld aan een virtuele machine van Azure toodelete probeert, krijgt u mogelijk een foutbericht over Hallo opslagaccount nog wordt gebruikt. Zie [Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md) (Fouten oplossen met het verwijderen van Azure-opslagaccounts, containers of VHD's) voor informatie over het oplossen van deze fout.

## <a name="next-steps"></a>Volgende stappen
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Azure Blob Storage: Cool Storage-laag en Hot Storage-laag](../blobs/storage-blob-storage-tiers.md)
* [Azure Storage-replicatie](storage-redundancy.md)
* [Azure Storage-verbindingsreeksen configureren](../storage-configure-connection-string.md)
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)
* Ga naar Hallo [Blog van Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/).

