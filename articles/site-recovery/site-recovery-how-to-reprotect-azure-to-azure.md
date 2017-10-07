---
title: aaaHow tooReprotect van failover van virtuele machines in Azure back tooprimary Azure-regio | Microsoft Docs
description: "Na de failover van virtuele machines van één Azure-regio tooanother, kunt u Azure Site Recovery tooprotect Hallo-machines in omgekeerde richting. Hoe meer informatie over Hallo stappen toodo een beveiligt voordat opnieuw een failover."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Azure-regio back tooprimary regio beveiligt van failover



>[!NOTE]
>
> Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.


## <a name="overview"></a>Overzicht
Wanneer u [failover](site-recovery-failover.md) Hallo virtuele machines van één Azure-regio tooanother, Hallo virtuele machines zich in een niet-beveiligde status. Als u wilt dat toobring deze de primaire regio toohello terug te zetten, moet u toofirst Hallo virtuele machines en vervolgens failover opnieuw beveiligen. Er is geen verschil tussen het failover in één richting of andere. Inschakelen van de beveiliging van Hallo virtuele machines op dezelfde manier te posten, er is geen verschil tussen Hallo beveiligt na een failover of post failback.
tooexplain hello werkstromen van beveiligt en tooavoid verwarring, we gebruiken primaire site Hallo Hallo beveiligde machines als Oost-Azië regio en Hallo herstelsite Hallo machines als Zuidoost-Azië regio. U gaat failover Hallo virtuele machines toohello Zuidoost-Azië regio tijdens failover. Voordat u failback moet u tooreprotect Hallo virtuele machines van Zuidoost-Azië back tooEast Azië. Dit artikel Hallo stappen beschreven voor het tooreprotect.

> [!WARNING]
> Als u hebt [migratie voltooid](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), Hallo verplaatste virtuele machine tooanother resource groep of verwijderde virtuele machine van Azure Hallo, u kunt geen failback daarna.

Nadat beveiligt is voltooid en repliceren van Hallo beveiligde virtuele machines, kunt u een failover op Hallo virtuele machines toobring initiëren back ze tooEast Azië regio.

Opmerkingen of vragen plaatsen aan Hallo einde van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Vereisten
1. Hallo virtuele machines moet zijn doorgevoerd.
2. Hallo-doelsite - in dit geval Hallo Oost-Azië Azure-gebied moet beschikbaar zijn en moet kunnen tooaccess/maken van nieuwe resources in deze regio.

## <a name="steps-tooreprotect"></a>Stappen tooreprotect

Volgende zijn stappen tooreprotect Hallo Hallo standaardinstellingen met een virtuele machine.

1. In **kluis** > **gerepliceerde items**Hallo virtuele machine die de storing opgetreden met de rechtermuisknop en selecteer vervolgens **opnieuw beveiligen**. U kunt ook klikken op Hallo machine en selecteer **opnieuw beveiligen** van Hallo opdrachtknoppen.

![Klik met de rechtermuisknop tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. Hallo blade ziet die richting Hallo van beveiliging, **tooEast-Azië Zuidoost-Azië**, is al geselecteerd.

![Blade opnieuw beveiligen](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Bekijk Hallo **Resource groep, netwerk, opslag en beschikbaarheid sets** informatie en klik op OK. Als er geen bronnen gemarkeerd (nieuw), worden ze gemaakt als onderdeel van Hallo opnieuw beveiligen.

Deze trigger een taak taak die wordt eerst seed-doelsite hello (SEA in dit geval) met de meest recente gegevens Hallo beveiligt en als dat is voltooid, wordt gerepliceerd Hallo delta's voordat u de failover-back-tooSoutheast Azië.

### <a name="reprotect-customization"></a>Aanpassing beveiligt
Als u wilt dat toochoose kunt hello extract-account of Hallo opslagnetwerk tijdens beveiligt, u zodat optie opgegeven op Hallo beveiligt blade met behulp van Hallo aanpassen.

![Optie aanpassen](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Hallo volgende eigenschappen van de doel-virtuele machine tijdens beveiligt, kunt u aanpassen.

![Blade aanpassen](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Eigenschap |Opmerkingen  |
|---------|---------|
|Doelresourcegroep     | U kunt toochange hello doelresourcegroep waarin de virtuele machine wordt gemaakt. Tijdens het Hallo beveiligt, Hallo doel-virtuele machine worden verwijderd, daarom kunt u een nieuwe resourcegroep van VM-failover van post Hallo maken         |
|Doel virtueel netwerk     | Netwerk kan niet worden gewijzigd tijdens het Hallo opnieuw beveiligen. Hallo toochange netwerk, Hallo netwerktoewijzing opnieuw.         |
|Doelopslag     | U kunt Hallo toowhich Hallo virtuele machine zijn gemaakt na failover storage-account wijzigen.         |
|Cache-opslag     | U kunt opgeven dat een cache-storage-account die wordt gebruikt tijdens de replicatie. Als u de verbinding met de standaardwaarden Hallo, wordt een nieuw opslagaccount voor de cache gemaakt, als deze niet al bestaat.         |
|Beschikbaarheidsset     |Als Hallo virtuele machine in Oost-Azië deel van een beschikbaarheidsset uitmaakt, kunt u een beschikbaarheidsset voor de virtuele doelmachine Hallo in Zuidoost-Azië. Standaardwaarden wordt Hallo bestaande SEA beschikbaarheidsset vinden en probeer het toouse deze. Aangepast, kunt u een volledig nieuw AV-set.         |


### <a name="what-happens-during-reprotect"></a>Wat er gebeurt tijdens het opnieuw beveiligen?

Net zoals na Hallo eerst beveiliging inschakelt, volgen Hallo artefacten die worden gemaakt als u Hallo standaardwaarden gebruikt.
1. Een opslagaccount van de cache wordt gemaakt in Hallo Oost-Azië regio.
2. Als Hallo doel storage-account (Hallo oorspronkelijke opslagaccount Hallo Zuidoost-Azië VM) niet bestaat, wordt een nieuw gemaakt. Hallo-naam is voorafgegaan door 'asr' hello Oost-Azië van virtuele machine-opslagaccount.
3. Beveilig opnieuw taak als Hallo doel AV set niet bestaat en Hallo standaardwaarden detecteren die toocreate een nieuwe AV ingesteld, en vervolgens wordt deze als onderdeel van Hallo gemaakt nodig heeft. Als u hebt aangepast Hallo beveiligt vervolgens Hallo geselecteerd AV set wordt gebruikt.
4.

Hallo volgen Hallo lijst met stappen die ontstaan wanneer u een taak beveiligt opnieuw activeren. Dit is in Hallo case Hallo doel aan virtuele machine bestaat.

1. Hallo vereist artefacten worden gemaakt als onderdeel van het beveiligt. Als ze al aanwezig zijn, worden ze hergebruikt.
2. Hallo doel aan clientzijde (Zuidoost-Azië)-virtuele machine is eerst uitgeschakeld, als deze wordt uitgevoerd.
3. schijf Hallo doel aan clientzijde van de virtuele machine wordt door Azure Site Recovery gekopieerd naar een container als een seed-blob.
4. Hallo doel aan virtuele machine wordt vervolgens verwijderd.
5. Hallo seed blob wordt gebruikt door Hallo huidige bron kant (Oost-Azië) virtuele machine tooreplicate. Dit zorgt ervoor dat alleen de delta's worden gerepliceerd.
6. Hallo grote wijzigingen tussen Hallo bronschijf en Hallo seed blob worden gesynchroniseerd. Dit kan enige tijd toocomplete duren.
7. Nadat Hallo beveiligt taak is voltooid, deltareplicatie Hallo die u maakt een herstelpunt volgens het beleid voor Hallo begint.

> [!NOTE]
> U kunt geen op een plan herstel niveau. U kunt alleen opnieuw beveiligen op een per VM-niveau.

Nadat Hallo beveiligt slagen, Hallo virtuele machine wordt overgeschakeld naar een beveiligde status.

## <a name="next-steps"></a>Volgende stappen

Nadat Hallo virtuele machine heeft een beschermd zijn ingevoerd, kunt u een failover starten. Hallo failover Hallo virtuele machine in Azure Oost-Azië regio afsluiten en vervolgens maakt en Hallo Zuidoost-Azië regio virtuele machine worden opgestart. Daarom is er een kleine uitvaltijd voor de toepassing hello. Kies dus Hallo-tijd voor failover wanneer uw toepassing een uitvaltijd kan tolereren. Het is raadzaam eerst failover Hallo virtuele machine toomake ervoor dat dit komt goed voordat u begint een failover te testen.

-   [Stappen tooinitiate failover van Hallo virtuele machine testen](site-recovery-test-failover-to-azure.md)

-   [Stappen tooinitiate failover van Hallo virtuele machine](site-recovery-failover.md)
