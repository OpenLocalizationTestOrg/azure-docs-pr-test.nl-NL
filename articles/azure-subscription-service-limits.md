---
title: aaaAzure abonnement limieten en quota | Microsoft Docs
description: Geeft een lijst van algemene Azure-abonnement en Servicelimieten, quota's en beperkingen. Dit omvat informatie over hoe tooincrease samen met maximale waarden beperkt.
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Azure-abonnement en servicelimieten, quota's en beperkingen
Dit document vindt u enkele van Hallo meest voorkomende Microsoft Azure-limieten, quota's soms ook wel genoemd. Dit document betrekking niet op dit moment op alle Azure-services. Na verloop van tijd Hallo lijst zal worden uitgebreid en bijgewerkt toocover meer Hallo-platform.

Ga naar [overzicht van Azure prijzen](https://azure.microsoft.com/pricing/) toolearn meer informatie over prijzen voor Azure. Daar kunt u uw kosten Hallo met schatten [Prijscalculator](https://azure.microsoft.com/pricing/calculator/) of via Hallo prijzen detailpagina voor een service (bijvoorbeeld [VM's van Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)). Uw kosten voor tips toohelp beheren, Zie [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](billing/billing-getting-started.md).

> [!NOTE]
> Als u tooraise Hallo limiet of quotum hierboven Hallo wilt **standaard limiet**, [opent u een ondersteuningsaanvraag online klant kosteloos](azure-supportability/resource-manager-core-quotas-request.md). Hallo limieten kunnen niet worden verhoogd hierboven Hallo **maximumlimiet** waarde in het Hallo-tabellen te volgen. Als er geen **maximumlimiet** kolom, klikt u vervolgens Hallo-resource heeft geen instelbare limieten. 
> 
> Gratis proefversie van abonnementen zijn niet in aanmerking komen voor limiet of quotum vergroot. Als u een gratis proefversie hebt, kunt u upgraden tooa [betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/) abonnement. Zie voor meer informatie [Upgrade gratis proefversie van Azure tooPay-als-u-Go](billing/billing-upgrade-azure-subscription.md).
> 

## <a name="limits-and-hello-azure-resource-manager"></a>Limieten en hello Azure Resource Manager
Het is nu mogelijk toocombine meerdere Azure-resources in tooa één Azure-resourcegroep. Bij gebruik van resourcegroepen limieten die eenmaal globale zijn beheerd op een regionaal niveau Hello Azure Resource Manager. Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md).

Hallo limieten onder een nieuwe tabel is toegevoegd tooreflect eventuele verschillen in limieten bij gebruik van hello Azure Resource Manager. Er is bijvoorbeeld een **abonnementen** tabel en een **abonnementen - Azure Resource Manager** tabel. Wanneer een limiet van toepassing tooboth scenario's is, is het alleen weergegeven in de eerste tabel Hallo. Tenzij anders vermeld, gelden limieten in alle regio's.

> [!NOTE]
> Belangrijke tooemphasize dat quota's voor resources in Azure-resourcegroepen per regio toegankelijk zijn voor uw abonnement zijn, en niet per abonnement is Hallo service management quota zijn. Laten we core quota gebruiken als voorbeeld. Als u een quotum verhogen met ondersteuning voor kernen toorequest nodig hebt, moet u toodecide hoe veel kernen die u wilt toouse in welke regio's en vervolgens een specifieke aanvraag maken voor Azure-resourcegroep core quota's voor Hallo bedragen en regio's die u wilt. Dus als u nodig hebt toouse 30 cores in West-Europa toorun uw toepassing. specifiek moet u 30 kernen in West-Europa aanvragen. Maar u geen een quotum voor kernen verhogen in elke andere regio--alleen West-Europa Hallo 30-kerngeheugenquotum hebben.
> <!-- -->
> Als gevolg hiervan soms is het nuttig tooconsider beslist wat uw Azure-resourcegroep quota's moeten toobe voor uw workload één regio is, en aanvragen die in elke regio waarin u implementatie overweegt bedrag. Zie [implementatieproblemen oplossen](resource-manager-common-deployment-errors.md) voor meer informatie voor het detecteren van uw huidige quota's voor specifieke regio's.
> 
> 

## <a name="service-specific-limits"></a>Servicespecifieke limieten
* [Active Directory](#active-directory-limits)
* [API Management](#api-management-limits)
* [App Service](#app-service-limits)
* [Application Gateway](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [Automatisering](#automation-limits)
* [Azure Cosmos DB](#azure-cosmos-db-limits)
* [Azure Event raster](#azure-event-grid-limits)
* [Azure Redis-cache](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [Een back-up maken](#backup-limits)
* [Batch](#batch-limits)
* [BizTalk Services](#biztalk-services-limits)
* [CDN](#cdn-limits)
* [Cloud Services](#cloud-services-limits)
* [Container Instances](#container-instances-limits)
* [Data Factory](#data-factory-limits)
* [Data Lake Analytics](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [Event Hubs](#event-hubs-limits)
* [IoT Hub](#iot-hub-limits)
* [Key Vault](#key-vault-limits)
* [Meld u Analytics / Operational Insights](#log-analytics-limits)
* [Media Services](#media-services-limits)
* [Mobile Engagement](#mobile-engagement-limits)
* [Mobile Services](#mobile-services-limits)
* [Controle](#monitor-limits)
* [Multi-Factor Authentication](#multi-factor-authentication)
* [Netwerken](#networking-limits)
* [Netwerk-Watcher](#network-watcher-limits)
* [Notification Hub-Service](#notification-hub-service-limits)
* [Resourcegroep](#resource-group-limits)
* [Scheduler](#scheduler-limits)
* [Zoeken](#search-limits)
* [Service Bus](#service-bus-limits)
* [Site Recovery](#site-recovery-limits)
* [SQL Database](#sql-database-limits)
* [Storage](#storage-limits)
* [StorSimple-systeem](#storsimple-system-limits)
* [Stream Analytics](#stream-analytics-limits)
* [Abonnement](#subscription-limits)
* [Traffic Manager](#traffic-manager-limits)
* [Virtuele machines](#virtual-machines-limits)
* [Virtuele-Machineschaalsets](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>Abonnementen
#### <a name="subscription-limits"></a>Abonnementen
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>Abonnement - limieten voor Azure Resource Manager
Hallo volgende limieten van toepassing wanneer u hello Azure Resource Manager en Azure-resourcegroepen. Limieten die niet zijn gewijzigd met hello Azure Resource Manager worden hieronder niet weergegeven. Raadpleeg de vorige tabel toohello voor deze limieten.

Zie voor meer informatie over het verwerken van limieten voor Resource Manager-verzoeken [beperking Resource Manager-aanvragen](resource-manager-request-limits.md).

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>Limieten voor resourcegroep
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>Limieten voor virtuele Machines
#### <a name="virtual-machine-limits"></a>Limieten voor de virtuele Machine
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>Limieten voor virtuele Machines - Azure Resource Manager
Hallo volgende limieten van toepassing wanneer u hello Azure Resource Manager en Azure-resourcegroepen. Limieten die niet zijn gewijzigd met hello Azure Resource Manager worden hieronder niet weergegeven. Raadpleeg de vorige tabel toohello voor deze limieten.

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>Limieten voor virtuele-Machineschaalsets
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>Container exemplaren limieten
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>Netwerklimieten
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>Netwerklimieten
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Toepassingsgateway beperkt
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>Grenzen van netwerk-Watcher
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>Traffic Manager-limieten
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>DNS-beperkingen
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>Opslaglimieten
Zie voor meer informatie over opslagaccountlimieten [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>Service opslaglimieten
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>Schijfruimtelimiet van de virtuele machine 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

Zie [grootten van virtuele machines](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

#### <a name="managed-virtual-machine-disks"></a>Beheerde virtuele-machineschijven

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>Niet-beheerde virtuele-machineschijven

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>Resource Provider opslaglimieten
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>Limieten voor cloud-Services
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>App Service-beperkingen
Hallo volgende die App Service-beperkingen zijn limieten voor Web-Apps, Mobile Apps, API-Apps en Logic Apps.

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>Scheduler-limieten
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Batch-limieten
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>Limieten voor BizTalk Services
Hallo volgende tabel toont Hallo limieten voor Azure Biztalk Services.

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Azure DB Cosmos-limieten
Azure Cosmos-database is een wereldwijde schaal-database in welke doorvoer en de opslag kan worden geschaald toohandle wat uw toepassing vereist. Als u vragen over Hallo scale Azure Cosmos DB biedt hebt, stuur e-mail tooaskcosmosdb@microsoft.com.

### <a name="mobile-engagement-limits"></a>Mobile Engagement-limieten
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>Limieten voor zoeken
Prijscategorieën bepalen Hallo capaciteit en de grenzen van uw zoekservice. Lagen zijn onder andere:

* *Gratis* multitenant-service, gedeeld met andere Azure-abonnees die zijn bestemd voor evaluatie en klein ontwikkeling projecten.
* *Basic* biedt speciale computerbronnen voor productieworkloads op kleinere schaal omhoog toothree replica's voor query maximaal beschikbare werkbelastingen.
* *Standard (S1, S2, S3, S3 high-density)* voor productieworkloads groter wordt. Meerdere niveaus bestaan binnen Hallo standaardcategorie, zodat u kunt de configuratie van een bron die het meest geschikt is voor uw profiel werkbelasting.

**Limieten per abonnement**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**Limieten per zoekservice**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

toolearn meer informatie over limieten voor een meer gedetailleerd niveau, zoals de documentgrootte van het, query's per seconde, sleutels, aanvragen en antwoorden, Zie [Servicelimieten in Azure Search](search/search-limits-quotas-capacity.md).

### <a name="media-services-limits"></a>Media Services-limieten
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>CDN-limieten
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>Limieten voor Mobile Services
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>Monitor limieten
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>Notification Hub Servicelimieten
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>Limieten voor Event Hubs
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>Service Bus-limieten
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>IoT Hub-limieten
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Hiermee beperkt u Data Factory
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Data Lake Analytics-limieten
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Data Lake Store-limieten
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>Stream Analytics-limieten
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Active Directory-limieten
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Azure Event raster limieten
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Azure RemoteApp-limieten
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>Beperkt StorSimple-systeem
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Log Analytics beperkt
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>Back-limieten
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Site Recovery-limieten
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Application Insights-limieten
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>Limieten voor API Management
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Azure Redis-Cache-limieten
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>Limieten voor Sleutelkluis
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Meervoudige verificatie
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>Limieten voor Automation
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>Limieten voor SQL-Database
Zie voor SQL-Database-limieten, [limieten voor SQL Database](sql-database/sql-database-resource-limits.md).

## <a name="see-also"></a>Zie ook
[Inzicht in de Azure-limieten en toeneemt](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Virtual Machine and Cloud Service Sizes for Azure](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Grootten voor Cloudservices](cloud-services/cloud-services-sizes-specs.md)

