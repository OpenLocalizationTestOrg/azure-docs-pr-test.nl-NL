---
title: aanbevelingen voor hoge beschikbaarheid van Advisor aaaAzure | Microsoft Docs
description: Gebruik Azure Advisor tooimprove hoge beschikbaarheid van uw Azure-implementaties.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Hoge beschikbaarheid aanbevelingen Advisor te ontvangen

Azure Advisor kunt u ervoor te zorgen en Hallo continuïteit van uw bedrijfskritieke toepassingen te verbeteren. Hallo kunt u hoge beschikbaarheid aanbevelingen door Advisor downloaden **hoge beschikbaarheid** van Hallo Advisor dashboard.

![Hoge beschikbaarheid knop op Hallo Advisor dashboard](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Zorg ervoor dat de virtuele machine fouttolerantie

Advisor identificeert virtuele machines die geen deel uitmaken van een beschikbaarheidsset en raadt in een beschikbaarheidsset. Als u redundantie tooyour toepassing, is het raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de virtuele machine van Azure SLA Hallo. U kunt beide toocreate beschikbaarheidsset voor Hallo virtuele machine of tooadd Hallo virtuele machine tooan bestaande beschikbaarheidsset.

> [!NOTE]
> Als u een beschikbaarheidsset toocreate kiest ingesteld, moet u ten minste één meer virtuele machine in de App toevoegen. Het is raadzaam dat u twee groeperen of meer virtuele machines in een beschikbaarheidsset ingesteld tooensure ten minste één machine is beschikbaar tijdens een storing.

![Advisor aanbeveling: voor de redundantie van de virtuele machine, gebruik beschikbaarheidssets](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Zorg ervoor dat de beschikbaarheidsset fouttolerantie 

Advisor identificeert beschikbaarheidssets met een enkele virtuele machine en aan een of meer virtuele machines tooit toe te voegen. Als u redundantie tooyour toepassing, is het raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de virtuele machine van Azure SLA Hallo. U kunt beide toocreate op een virtuele machine of een bestaande virtuele machine toouse en tooadd deze beschikbaarheidsset toohello.  

![Advisor aanbeveling: Voeg een of meer virtuele machines toothis beschikbaarheidsset weergeven](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Zorg ervoor dat fouttolerantie voor application gateway
tooensure hello zakelijke continuïteit van bedrijfskritieke toepassingen die gemaakt, via Toepassingsgateways aangeboden zijn Advisor identificeert toepassingsexemplaren gateway die niet zijn geconfigureerd voor fouttolerantie en er wordt verwezen naar herstelacties die u kunt ondernemen . Advisor identificeert grote of middelgrote single instance Toepassingsgateways en raadt aan om ten minste één meer exemplaar toe te voegen. Ook één of meerdere instance kleine Toepassingsgateways identificeert en raadt aan om te migreren toomedium of groot SKU's. Advisor raadt aan om deze acties tooensure dat uw gateway toepassingsexemplaren geconfigureerde toosatisfy Hallo huidige SLA-vereisten voor deze resources zijn.

![Advisor aanbeveling: twee of meer grote of middelgrote grootte gatewayexemplaren van een toepassing implementeren](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Hallo prestaties en betrouwbaarheid van de virtuele-machineschijven verbeteren

Advisor identificeert virtuele machines met standaardschijven en raadt toopremium schijven.
 
Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines die I/O-intensieve werkbelastingen worden uitgevoerd. Virtuele machine-schijven die gebruikmaken van premium storage-accounts opslaan gegevens op de SSD-schijven (SSD's). Voor de beste prestaties voor uw toepassing hello wordt u aangeraden een hoge IOPS toopremium opslag vereisen schijven op virtuele machine te migreren. 

Als uw schijven geen hoge IOPS vereisen, kunt u de kosten beperken door het onderhoud ervan in standard-opslag. Standard-opslag slaat schijfgegevens voor virtuele machine op de harde schijven (HDD's) in plaats van SSD's. U kunt uw virtuele machine schijven toopremium schijven toomigrate. Premium-schijven worden op de meeste virtuele machine SKU's ondersteund. In sommige gevallen, als u wilt dat toouse premium-schijven, hoeft u wellicht tooupgrade uw virtuele machine SKU's ook.

![Advisor aanbeveling: Hallo betrouwbaarheid van uw virtuele-machineschijven verbeteren door het upgraden van toopremium schijven](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>De gegevens van uw virtuele machines te beschermen tegen onopzettelijk verwijderen
Advisor identificeert virtuele machines waar back-up is niet ingeschakeld en het beveelt back-up inschakelen. Instellen van de virtuele machine back-up zorgt voor de beschikbaarheid van uw bedrijfskritieke gegevens Hallo en biedt bescherming tegen onbedoeld worden verwijderd of beschadigd.

![Advisor aanbeveling: uw bedrijfskritieke gegevens van virtuele machine back-tooprotect configureren](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Toegang tot hoge beschikbaarheid aanbevelingen in Advisor

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Klik in het linkerdeelvenster Hallo **meer services**.

3. Service in Hallo menu deelvenster onder **bewaking en beheer**, klikt u op **Azure Advisor**.  
 Hallo Advisor dashboard wordt weergegeven.

4. Klik op Hallo Advisor dashboard Hallo **hoge beschikbaarheid** tabblad en selecteer vervolgens Hallo-abonnement waarvoor u tooreceive aanbevelingen wilt.

> [!NOTE]
> tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor. Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop. Dit is een *eenmalige bewerking*. Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Advisor aanbevelingen:
* [Inleiding tooAzure Advisor](advisor-overview.md)
* [Aan de slag met Advisor](advisor-get-started.md)
* [Advisor kosten aanbevelingen](advisor-performance-recommendations.md)
* [Aanbevelingen van Advisor-prestaties](advisor-performance-recommendations.md)
* [Aanbevelingen voor beveiliging van Advisor](advisor-security-recommendations.md)

