---
title: aaaFailback in Azure Site Recovery voor Hyper-v virtuele machines | Microsoft Docs
description: "Azure Site Recovery coördineert Hallo replicatie, failovers en herstel van virtuele machines en fysieke servers. Meer informatie over failback vanuit Azure tooon-premises datacenter."
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
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Failback in Site Recovery voor Hyper-V virtuele machines

Dit artikel wordt beschreven hoe toofailback virtuele machines beveiligd door Site Recovery.

## <a name="prerequisites"></a>Vereisten
1. Zorg ervoor dat Hallo primaire site VMM-server/Hyper-V-server is verbonden.
2. U moet hebben uitgevoerd **doorvoeren** op Hallo virtuele machine.

## <a name="why-is-there-no-button-called-failback"></a>Waarom is er geen knop failback aangeroepen?
Op Hallo-portal, er is geen expliciete gebaar van de failback wordt aangeroepen. Failback is een stap waar u terugkomen toohello primaire site. Failover is wanneer u een failover Hallo virtuele machines van primary(on-premises) site toorecovery (Azure) en failback is wanneer u failover Hallo virtuele machines van herstel een back-tooprimary per definitie.

Wanneer u een failover initieert, informeert het Hallo-blade u over Hallo richting van het Hallo-taak. Als Hallo richting van Azure tooOn-premises is, is een failback.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Waarom ligt er alleen een geplande failover gebaar toofailback?
Azure is een maximaal beschikbare omgeving en uw virtuele machines altijd beschikbaar. Failback is een geplande activiteit waarin u een kleine uitvaltijd tootake kiest zodat Hallo werkbelastingen kunnen starten lokale nogmaals uit te voeren. Dit verwacht geen gegevens verloren gaan. Daarom alleen een gebaar van de geplande failover beschikbaar is, wordt die uitschakelen Hallo virtuele machines in Azure, download de meest recente wijzigingen Hallo en zorg dat er geen gegevens verloren gaan.

## <a name="initiate-failback"></a>Failback initiëren
Na een failover van Hallo primaire toosecondary locatie gerepliceerde virtuele machines niet worden beveiligd door Site Recovery en de secundaire locatie Hallo nu fungeert als Hallo active-locatie. Volg deze procedures toofail back toohello originele primaire site. Deze procedure wordt beschreven hoe toorun een geplande failover voor een herstel van plan bent. U kunt ook Hallo failover voor een enkele virtuele machine uitvoeren op Hallo **virtuele Machines** tabblad.

1. Selecteer **herstelplannen** > *recoveryplan_name*. Klik op **Failover** > **geplande Failover**.
2. Op Hallo ** geplande Failover bevestigen ** pagina, kiest u de bron- en doellocaties Hallo. Houd er rekening mee Hallo failoverrichting. Als Hallo failover van primaire gewerkt als verwacht en alle virtuele machines zich in de secundaire locatie Hallo die dit alleen ter informatie is.
3. Als u failback vanuit Azure mislukken bent instellingen in selecteren **gegevenssynchronisatie**:

   * **Synchroniseren van gegevens voordat failover wordt uitgevoerd (alleen synchroniseren deltawijzigingen)**— deze optie uitvaltijd voor virtuele machines wordt geminimaliseerd omdat het synchroniseert zonder dat deze wordt afgesloten. Het Hallo te volgen:
     * Fase 1: Duurt momentopname van Hallo virtuele machine in Azure en kopieert deze toohello lokale Hyper-V-host. Hallo machine blijft worden uitgevoerd in Azure.
     * Fase 2: Afgesloten Hallo virtuele machine in Azure, zodat er geen nieuwe wijzigingen worden uitgevoerd. Hallo uiteindelijke set deltawijzigingen zijn overgedragen toohello lokale server en Hallo on-premises virtuele machine is opgestart.

    - **Synchroniseren van gegevens tijdens de failover alleen (volledige download)**: Gebruik deze optie als u gedurende een lange periode hebt is uitgevoerd op Azure. Deze optie is sneller, omdat we verwachten dat de meeste Hallo schijf is gewijzigd en we willen toospend tijd in de berekening van de controlesom niet. Een download van Hallo schijf wordt uitgevoerd. Het is ook handig wanneer Hallo on-premises virtuele machine is verwijderd.

    >[!NOTE]
    >Het is raadzaam het gebruik van deze optie als u hebt al actief Azure een tijdje (een maand of langer) of Hallo on-premises virtuele machine is verwijderd. Deze optie niet controlesom berekeningen uit te voeren.
    >
    >




4. Als gegevensversleuteling is ingeschakeld voor Hallo-cloud in **versleutelingssleutel** Selecteer Hallo-certificaat dat was uitgegeven wanneer u de versleuteling van gegevens tijdens de installatie van de Provider op Hallo VMM-server ingeschakeld.
5. Start Hallo failover. U kunt Hallo failover voortgang volgen op Hallo **taken** tabblad.
6. Als u hebt geselecteerd Hallo optie toosynchronize Hallo gegevens voordat Hallo failover wordt uitgevoerd, eenmaal Hallo initiële synchronisatie van gegevens is voltooid en u bent klaar tooshut omlaag Hallo virtuele machines in Azure, klikt u op **taken** taaknaam geplande failover **Failover voltooien**. Dit wordt afgesloten hello Azure machine en begint Hallo VM lokale overdrachten Hallo meest recente wijzigingen toohello on-premises virtuele machine.
7. U kunt nu aanmelden op Hallo virtuele machine toovalidate is beschikbaar zoals verwacht.
8. Hallo virtuele machine is in behandeling status. Klik op **doorvoeren** toocommit Hallo failover.
9. Nu in volgorde toocomplete Hallo failback klikt u op **omgekeerde replicatie** toostart Hallo virtuele machine in de primaire site Hallo beveiligen.

## <a name="failback-tooan-alternate-location"></a>Failback tooan alternatieve locatie
Als u de beveiliging tussen hebt geïmplementeerd een [Hyper-V-site en Azure](site-recovery-hyper-v-site-to-azure.md) u tooability toofailback uit Azure tooan alternatieve on-premises locatie hebt. Dit is handig als u tooset van nieuwe lokale hardware nodig. Hier ziet u hoe u dit doet.

1. Als u nieuwe hardware instelt Installeer Windows Server 2012 R2 en Hyper-V-rol op Hallo server Hallo.
2. Een virtuele netwerkswitch met dezelfde naam moest u op de oorspronkelijke server Hallo Hallo maken.
3. Selecteer **beveiligde Items** -> **beveiligingsgroep**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> u wilt toofail terug en selecteer **gepland Failover**.
4. In **geplande Failover bevestigen** Selecteer **maken lokale virtuele machine als deze niet bestaat**.
5. In **hostnaam** Selecteer Hallo nieuwe Hyper-V-hostserver waarop tooplace Hallo virtuele machine.
6. In de gegevenssynchronisatie raden wij u Hallo optie **synchroniseren van gegevens voordat de failover Hallo Hallo**. Hierdoor minimaliseert uitvaltijd voor virtuele machines als het synchroniseert zonder dat deze wordt afgesloten. Het Hallo te volgen:

   * Fase 1: Duurt momentopname van Hallo virtuele machine in Azure en kopieert deze toohello lokale Hyper-V-host. Hallo machine blijft worden uitgevoerd in Azure.
   * Fase 2: Afgesloten Hallo virtuele machine in Azure, zodat er geen nieuwe wijzigingen worden uitgevoerd. Hallo definitieve wijzigingen worden overgebracht toohello lokale server en Hallo on-premises virtuele machine is opgestart.
7. Klik op Hallo vinkje toobegin Hallo failover (failback).
8. Nadat de initiële synchronisatie Hallo is voltooid en u klaar tooshut omlaag Hallo virtuele machine in Azure bent, klikt u op **taken** > <planned failover job> > **volledige Failover**. Dit wordt afgesloten hello Azure machine, overdrachten Hallo meest recente wijzigingen toohello on-premises virtuele machine en deze wordt gestart.
9. U kunt zich aanmelden op Hallo lokale virtuele machine tooverify die alles werkt zoals verwacht. Klik vervolgens op **doorvoeren** toofinish Hallo failover.
10. Klik op **omgekeerde replicatie** toostart Hallo on-premises virtuele machine te beveiligen.

    > [!NOTE]
    > Als u Hallo failbacktaak annuleert terwijl het gegevenssynchronisatie stap, Hallo lokale virtuele machine zich in een beschadigde status. Dit komt doordat gegevenssynchronisatie Hallo meest recente gegevens opgehaald uit Azure VM schijven toohello on-premises gegevensschijven en totdat het Hallo-synchronisatie is voltooid, Hallo schijfgegevens mogelijk niet in een consistente status. Als Hallo On-premises VM wordt opgestart nadat de synchronisatie van gegevens is geannuleerd, kan deze niet opgestart. Failover toocomplete Hallo gegevenssynchronisatie opnieuw worden geactiveerd.
    >
    >



## <a name="next-steps"></a>Volgende stappen

Als u klaar bent Hallo failbacktaak, **doorvoeren** Hallo virtuele machine. Commit hello Azure virtuele machine en de schijven ervan worden verwijderd en wordt voorbereid Hallo VM toobe opnieuw beveiligd.

Na **doorvoeren**, kunt u Hallo initiëren *omgekeerde replicatie*. Hiermee start u Hallo virtuele machine worden beschermd tegen lokale back-tooAzure. Houd er rekening mee dat dit alleen repliceren Hallo wijzigingen wordt omdat Hallo virtuele machine in Azure is uitgeschakeld en daarom verzendt differentiële alleen wijzigingen.
