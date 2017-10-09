---
title: aaaMigrate VM's van AWS tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe toomigrate virtuele machines actief in Amazon Web Services (AWS) tooAzure met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migreren van virtuele machines in Amazon Web Services (AWS) tooAzure met Azure Site Recovery

Dit artikel wordt beschreven hoe toomigrate AWS Windows tooAzure virtuele machines met Hallo exemplaren [Azure Site Recovery](site-recovery-overview.md) service.

Migratie is in feite een failover van AWS tooAzure. U kunt geen failback machines tooAWS en er is geen lopende replicatie. In dit artikel beschrijft Hallo stappen voor migratie in hello Azure-portal en zijn gebaseerd op Hallo instructies voor het [repliceren van een fysieke machine tooAzure](site-recovery-vmware-to-azure.md).

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Ondersteunde besturingssystemen

Site Recovery kan worden gebruikt toomigrate EC2 exemplaren met een van de Hallo volgende besturingssystemen:

- Windows (alleen 64 bits)
    - Windows Server 2008 R2 SP1 + (Citrix HW-stuurprogramma's of alleen AWS HW-stuurprogramma's. **Exemplaren met RedHat HW-stuurprogramma's worden niet ondersteund**) Windows Server 2012 Windows Server 2012 R2
- Linux (alleen 64 bits)
    - Red Hat Enterprise Linux 6.7 (alleen HVM gevirtualiseerd exemplaren)

## <a name="prerequisites"></a>Vereisten

Dit is wat u nodig hebt voor deze implementatie:

* **Configuratieserver**: een Amazon EC2 VM waarop Windows Server 2012 R2 is geïmplementeerd als Hallo configuratieserver. Standaard worden hello andere Azure Site Recovery-onderdelen (processerver en hoofddoelserver) geïnstalleerd wanneer u de configuratieserver Hallo implementeert. In dit artikel beschrijft Hallo stappen voor migratie in hello Azure-portal en zijn gebaseerd op Hallo instructies voor het [meer informatie](site-recovery-components.md)

* **EC2 exemplaren**: Hallo Amazon EC2 virtuele machines exemplaren die u toomigrate wilt.

## <a name="deployment-steps"></a>Implementatiestappen

1. Maak een Recovery Services-kluis.
2. Hallo beveiligingsgroep van uw EC2-exemplaren moet zijn regels geconfigureerd tooallow communicatie tussen Hallo EC2 exemplaar dat u wilt toomigrate en Hallo-exemplaar waarop u van plan bent toodeploy Hallo configuratieserver.

3. Dezelfde Amazon virtuele Privécloud als uw exemplaren EC2 implementeren op Hallo een configuratieserver ASR. Raadpleeg Hallo VMware / fysieke tooAzure vereisten voor de implementatie van de configuratievereisten-server.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Zodra de configuratieserver is geïmplementeerd in AWS en geregistreerd met de Recovery Services-kluis, ziet u Hallo configuratieserver en de processerver onder Site Recovery-infrastructuur zoals hieronder wordt weergegeven:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Nadat u hebt geïmplementeerd Hallo configuratieserver (mogelijk het too15 minustes duren voor tooappear), kan communiceren met Hallo VM's die u toomigrate wilt valideren.

6. [Replicatie-instellingen instellen](site-recovery-setup-replication-settings-vmware.md).

7. Replicatie inschakelen: replicatie inschakelen voor virtuele machines die u wilt dat toomigrate Hallo. Hallo EC2 exemplaren Hallo privé IP-adressen, die u vanaf Hallo EC2 console krijgen kunt kunnen worden gedetecteerd.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Zodra Hallo EC2 exemplaren zijn beveiligd en Hallo replicatie tooAzure voltooid is, [een Testfailover uitvoeren](site-recovery-test-failover-to-azure.md) toovalidate de prestaties van uw toepassing in Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Voer een Failover uit vanaf AWS tooAzure voor elke virtuele machine. U kunt desgewenst een herstelplan maken en een Failover, toomigrate van meerdere virtuele machines van AWS tooAzure uitvoeren. [Meer informatie](site-recovery-create-recovery-plans.md) over plannen voor herstel.

10. Voor de migratie hoeft u geen toocommit een failover. In plaats daarvan u Hallo volledige migratie optie selecteren voor elke computer die u wilt toomigrate. Hallo volledige migratie actie is van het migratieproces Hallo is voltooid, verwijdert u de replicatie voor Hallo machine en Hiermee stopt u Site Recovery facturering voor Hallo machine.

    ![Migreren](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Volgende stappen

- [Voorbereiden van de gemigreerde machines tooenable replicatie](site-recovery-azure-to-azure-after-migration.md) tooanother regio voor herstel nodig zijn na noodgevallen.
- Beginnen met het beveiligen van uw werkbelastingen door [virtuele machines in Azure te repliceren.](site-recovery-azure-to-azure.md)
