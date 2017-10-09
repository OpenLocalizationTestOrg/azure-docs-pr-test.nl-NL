---
title: aaaSet up Hallo bron en doel voor VMware replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van virtuele VMware-machines tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Stap 8: Instellen Hallo bron en doel voor VMware replicatie tooAzure

Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises tooAzure van VMware-virtuele machines, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en VM's detecteren.

1. Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.
2. Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.
3. In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.
5. Hallo kluisregistratiesleutel downloaden. U moet dit wanneer u Unified Setup uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

   ![Bron instellen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Hallo configuratieserver in Hallo kluis registreren

Hallo volgende voordat u start en voer vervolgens Setup Unified tooinstall Hallo configuratieserver processerver Hallo en Hallo hoofddoelserver.
    - Een video-overzicht

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Op de configuratieserver VM hello, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deze moet overeenkomen. Als het op de voorgrond 15 minuten of achter de installatie mislukken.
    - Voer de installatie als een lokale beheerder op de configuratieserver Hallo VM.
    - Zorg ervoor dat TLS 1.0 op Hallo VM is ingeschakeld.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>TooVMware servers verbinden

tooallow Azure Site Recovery toodiscover virtuele machines die worden uitgevoerd in uw on-premises-omgeving, moet u tooconnect uw VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery. Houd rekening met de volgende Hallo voordat u begint:

- Als u Hallo vCenter-server of vSphere hosts tooSite herstel met een account zonder beheerdersrechten op Hallo-server toevoegt, moet Hallo account deze bevoegdheden ingeschakeld:
    - Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine, vSphere gedistribueerde Switch.
    - Hallo vCenter-server moet opslag weergaven machtigingen.
- Wanneer u een VMware-servers tooSite herstel toevoegt, kan het 15 minuten duren of langer ze tooappear in Hallo-portal.

### <a name="add-hello-account-for-automatic-discovery"></a>Hallo-account voor automatische detectie toevoegen

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Een verbinding instellen

Verbinding maken met tooservers als volgt:

1. Selecteer **+ vCenter** toostart gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.
2. In **vCenter toevoegen**, Geef een beschrijvende naam voor Hallo vSphere-host of het vCenter-server en geef vervolgens Hallo IP-adres of FQDN-naam van het Hallo-server.
3. Behoud Hallo poort 443 tenzij uw VMware-servers geconfigureerd toolisten voor aanvragen op een andere poort zijn. Selecteer Hallo-account dat is tooconnect toohello VMware vCenter of vSphere ESXi-server. Klik op **OK**.
4. Site Recovery verbindt tooVMware servers Hallo instellingen opgegeven gebruikt en detecteert van virtuele machines.

> [!NOTE]
> Als u een server of de host met een account dat geen administrator-bevoegdheden op Hallo vCenter of host-server toevoegt, ervoor zorgen dat Hallo account deze ingeschakeld heeft: Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine en vSphere gedistribueerde Switch. Hallo VMware vCenter-server moet bovendien Hallo opslag weergaven bevoegdheid ingeschakeld.


## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Zorg voordat u de doelomgeving Hallo hebt ingesteld, hebt u een Azure-opslagaccount en een virtueel netwerk instellen.

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.
2. Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.
3. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

   ![doel](./media/vmware-walkthrough-source-target/gs-target.png)
4. Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, een Resource Manager-account of netwerk inline toocreate.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 9: een replicatiebeleid instellen](vmware-walkthrough-replication.md)
