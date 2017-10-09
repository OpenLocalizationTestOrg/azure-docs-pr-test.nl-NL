---
title: aaaInstall hello Mobility-service voor replicatie van VMware tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service-agent voor VMware tooAzure replicatie met hello Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Stap 10: Hallo Mobility-service installeren


Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises tooAzure van VMware-virtuele machines, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.

Hallo Mobility-service worden vastgelegd op een machine weggeschreven en stuurt ze toohello processerver. Het moet worden geïnstalleerd op elke machine die u wilt dat tooreplicate tooAzure.

U kunt Hallo Mobility-service handmatig installeren met behulp van een push-installatie van Site Recovery-processerver Hallo wanneer replicatie is ingeschakeld, of gebruik een hulpprogramma System Center Configuration Manager. Als u push-installatie gebruikt, wordt Hallo-service is geïnstalleerd op Hallo VM wanneer replicatie is ingeschakeld.

Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>De installatie handmatig uitvoeren

1. Controleer de Hallo [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.
2. Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie met Hallo-portal.
3. Als u liever tooinstall vanaf de opdrachtregel hello, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installeren vanaf de processerver Hallo

Als u wilt dat toopush Hallo Mobility service installatie van de processerver Hallo wanneer u replicatie voor een virtuele machine inschakelen, moet u een account dat door Hallo proces server tooaccess Hallo VM kan worden gebruikt. Hallo-account wordt alleen gebruikt voor Hallo push-installatie.

1. U moet beschikken over [een account gemaakt](vmware-walkthrough-prepare-vmware.md) die kunnen worden gebruikt voor de push-installatie. Vervolgens geeft u het gewenste toouse bij het configureren van broninstellingen tijdens implementatie van Site Recovery Hallo-account.
2. Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt dat toopush Hallo Mobility-service op Windows of Linux-machines.

## <a name="other-methods"></a>Andere methoden

Meer informatie over [Hallo Mobility-service met Configuration Manager installeren](site-recovery-install-mobility-service-using-sccm.md), of met behulp van [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Volgende stappen

Ga te[stap 11: replicatie inschakelen](vmware-walkthrough-enable-replication.md)
