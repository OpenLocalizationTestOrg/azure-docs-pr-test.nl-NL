---
title: aaaMoving grote hoeveelheden gegevens van/naar de cloudopslag in Azure | Microsoft Docs
description: Een overzicht van Hallo verschillende methoden voor het verplaatsen tooand van gegevens uit Azure Storage.
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Verplaatsen van gegevens tooand van Azure Storage
Als u wilt dat toomove lokale gegevens tooAzure opslag (of andersom), er zijn tal van manieren toodo dit. Hallo-benadering die het meest geschikt voor u is afhankelijk van uw scenario. In dit artikel biedt een snel overzicht van verschillende scenario's en de juiste aanbiedingen voor elk criterium.

## <a name="building-applications"></a>Toepassingen maken
Als u een toepassing maakt, is het ontwikkelen van toepassingen met Hallo REST-API of een van onze veel clientbibliotheken een uitstekende manier toomove gegevens tooand uit Azure Storage.

Azure Storage biedt uitgebreide clientbibliotheken voor .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby en Python. Hallo-clientbibliotheken bieden geavanceerde mogelijkheden, zoals Pogingslogica, logboekregistratie en parallelle uploads. U kunt ook rechtstreeks met de REST-API kan worden aangeroepen door elke taal waarin HTTP/HTTPS-aanvragen Hallo ontwikkelen.

Zie [aan de slag met Azure Blob Storage](../blobs/storage-dotnet-how-to-use-blobs.md) toolearn meer.

Bovendien bieden wij ook Hallo [Azure Storage-bibliotheek voor gegevensverplaatsing](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) dit is een bibliotheek is ontworpen voor high-performance kopiëren van gegevens tooand van Azure. Raadpleeg de tooour-bibliotheek voor gegevensverplaatsing [documentatie](https://github.com/Azure/azure-storage-net-data-movement) toolearn meer. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Snel weergeven van/interactie met uw gegevens
Als u wilt dat uw Azure Storage-gegevens een eenvoudige manier tooview terwijl hiervoor ook Hallo mogelijkheid tooupload en uw gegevens te downloaden, klikt u vervolgens kunt u overwegen een Azure Storage Explorer.

Bekijk onze lijst met [Azure Storage Explorers](../storage-explorers.md) toolearn meer.

## <a name="system-administration"></a>Systeembeheer
Als u vereisen of meer vertrouwd met een opdrachtregelprogramma (bijvoorbeeld systeembeheerders bent), moet u hier een aantal opties voor u tooconsider zijn:

### <a name="azcopy"></a>AzCopy
AzCopy is een Windows-opdrachtregelprogramma ontworpen voor high-performance kopiëren van gegevens tooand uit Azure Storage. U kunt ook gegevens binnen een opslagaccount of tussen verschillende opslagaccounts kopiëren.

Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) toolearn meer.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell is een module die cmdlets biedt voor het beheren van services op Azure. Het is een op taken gebaseerde opdrachtregelshell en scripttaal die speciaal is ontworpen voor systeembeheer.

Zie [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md) toolearn meer.

### <a name="azure-cli"></a>Azure CLI
Azure CLI biedt een set van open-source platformoverschrijdende opdrachten voor het werken met Azure-services. Azure CLI is beschikbaar op Windows, OSX en Linux.

Zie [Using hello Azure CLI met Azure Storage](../storage-azure-cli.md) toolearn meer.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Het verplaatsen van grote hoeveelheden gegevens met een langzaam netwerk
Een van de grootste uitdagingen Hallo die zijn gekoppeld aan het verplaatsen van grote hoeveelheden gegevens is Hallo overdrachtstijd. Als u gegevens uit Azure Storage tooget zonder zorgen te hoeven maken over de kosten van netwerken of code te schrijven, is Azure Import/Export een passende oplossing.

Zie [Azure Import/Export](../storage-import-export-service.md) toolearn meer.

## <a name="backing-up-your-data"></a>Back-ups van uw gegevens
Als u hoeft alleen toobackup uw gegevens tooAzure opslag, is Azure Backup Hallo manier toogo. Dit is een krachtige oplossing voor back-up on-premises gegevens en virtuele Azure-machines.

Zie [Azure Backup](../../backup/backup-introduction-to-azure-backup.md) toolearn meer.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Toegang tot uw gegevens on-premises als vanuit de cloud Hallo
Als u een oplossing nodig voor toegang tot uw gegevens on-premises en vanuit de cloud hello, moet vervolgens u met behulp van Azure hybride cloud opslagoplossing, StorSimple. Deze oplossing bestaat uit een fysiek StorSimple-apparaat dat op intelligente wijze winkels vaak gebruikte gegevens op SSD's en van tijd tot tijd gebruikt gegevens op HDD's en niet-actief/back-up/archivering van gegevens op Azure Storage.

Zie [StorSimple](../../storsimple/storsimple-overview.md) toolearn meer.

## <a name="recovering-your-data"></a>Uw gegevens herstellen
Wanneer u lokale werkbelastingen en toepassingen hebt, moet u een oplossing waarmee u uw zakelijke toocontinue uitgevoerd in de gebeurtenis Hallo van een noodgeval. Azure Site Recovery verwerkt replicatie, failovers en herstel van virtuele machines en fysieke servers. Gerepliceerde gegevens worden opgeslagen in Azure Storage, zodat u een secundair datacenter ter plaatse tooeliminate Hallo nodig.

Zie [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn meer.
### <a name="moving-data-faq"></a>Veelgestelde vragen over gegevens te verplaatsen:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>Kan ik VHD's migreren van één regio tooanother zonder te kopiëren?
Hallo is alleen manier toocopy VHD's tussen regio toocopy Hallo gegevens tussen de storage-accounts op elke regio. U kunt AZCopy gebruiken voor deze. Overdracht van gegevens met het AzCopy-opdrachtregelprogramma toolearn Hallo meer zien. Voor zeer grote hoeveelheden gegevens kunt u ook Azure Import/Export. Zie [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn meer.
