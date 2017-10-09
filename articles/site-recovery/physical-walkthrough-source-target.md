---
title: aaaSet up Hallo bron en doel voor de fysieke server replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van fysieke servers tooAzure opslag Hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Stap 7: Instellen Hallo bron en doel voor de fysieke server replicatie tooAzure

Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises fysieke servers tooAzure, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en machines ontdekken.

1. Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.
2. Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.
3. In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.
5. Hallo kluisregistratiesleutel downloaden. U moet dit wanneer u Unified Setup uitvoert. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

   ![Bron instellen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Hallo configuratieserver in Hallo kluis registreren

Hallo volgende voordat u start en voer vervolgens Setup Unified tooinstall Hallo configuratieserver processerver Hallo en Hallo hoofddoelserver. Hallo video beschrijft het instellen van Hallo-onderdelen voor VMware VM tooAzure replicatie. Hallo is hetzelfde proces echter geldig voor de fysieke server tooAzure replicatie.

- Op de configuratieserver VM hello, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deze moet overeenkomen. Als het op de voorgrond 15 minuten of achter de installatie mislukken.
- Voer setup uit als lokale beheerder op Hallo configuratie server-machine.
- Zorg ervoor dat TLS 1.0 op Hallo VM is ingeschakeld.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Hallo doelomgeving instellen

Zorg voordat u de doelomgeving Hallo hebt ingesteld, hebt u een Azure-opslagaccount en een virtueel netwerk instellen.

1. Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.
2. Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.
3. Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.

   ![doel](./media/physical-walkthrough-source-target/gs-target.png)

4. Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, een Resource Manager-account of netwerk inline toocreate.

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 8: een replicatiebeleid instellen](physical-walkthrough-replication.md)
