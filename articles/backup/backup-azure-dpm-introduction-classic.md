---
title: aaaBack up DPM workloads tooAzure klassieke portal | Microsoft Docs
description: Een inleiding toobacking DPM-servers installeren met behulp van hello Azure Backup-service
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: System Center Data Protection Manager, data protection manager, back-up van dpm
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Tooback up werkbelastingen tooAzure met DPM wordt voorbereid
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup-Server (klassiek)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klassiek)](backup-azure-dpm-introduction-classic.md)
>
>

Dit artikel bevat een inleiding toousing Microsoft Azure Backup tooprotect uw System Center Data Protection Manager (DPM)-servers en werkbelastingen. Deze leest, moet u het volgende weten:

* De werking van Azure DPM-server back-up
* Hallo vereisten tooachieve een goede back-ervaring
* Hallo typische fouten zijn opgetreden en hoe toodeal met hen
* Ondersteunde scenario 's

System Center DPM een back-up bestand-en toepassingsgegevens. Gegevensback-ups tooDPM worden opgeslagen op tape op schijf of een back-up tooAzure bij Microsoft Azure Backup. DPM communiceert met Azure Backup als volgt:

* **DPM geïmplementeerd als een fysieke server of on-premises virtuele machine** — als DPM wordt geïmplementeerd als een fysieke server of als een lokale Hyper-V virtuele machine, u kunt back-up van gegevens tooan Azure Backup-kluis bovendien toodisk en tapeback-up.
* **DPM geïmplementeerd als een virtuele machine van Azure** : van System Center 2012 R2 met Update 3, kan DPM worden geïmplementeerd als een virtuele machine van Azure. Als DPM wordt geïmplementeerd als een virtuele machine van Azure die kunt u back-ups tooAzure gegevensschijven gekoppeld toohello DPM Azure virtuele machine of u kunt Hallo gegevensopslag offload van de door de back-up tooan Azure Backup-kluis.

## <a name="why-backup-your-dpm-servers"></a>Waarom een back-up van uw DPM-servers?
Hallo zakelijke voordelen van het gebruik van Azure Backup voor back-ups van DPM-servers zijn:

* Voor on-premises DPM-implementatie, kunt u Azure back-up als een alternatieve toolong termijn implementatie tootape.
* Voor implementaties van DPM in Azure kunt Azure Backup u toooffload opslag hello Azure-schijf, zodat u tooscale up door oudere gegevens zijn opgeslagen in Azure Backup en nieuwe gegevens op schijf.

## <a name="how-does-dpm-server-backup-work"></a>Hoe werkt de back-up van DPM-server?
tooback van een virtuele machine moet eerst een momentopname van een punt in tijd Hallo gegevens nodig is. Hello Azure Backup-service initieert Hallo back-uptaak op Hallo geplande tijd en triggers Hallo Backup-extensie tootake een momentopname. Hallo Backup-extensie coördinaten met Hallo in de Gast VSS service tooachieve consistentie en roept Hallo blob momentopname API Hallo Azure Storage-service zodra de consistentiecontrole is bereikt. Dit is gedaan tooget een consistente momentopname van het Hallo-schijven van Hallo virtuele machine, zonder tooshut deze niet actief.

Nadat de momentopname Hallo is genomen, worden Hallo gegevens worden overgedragen door hello Azure Backup-service toohello back-upkluis. Hallo service verzorgt te identificeren en dragen alleen Hallo-blokken die zijn gewijzigd van Hallo laatste back-up Hallo back-ups opslag- en netwerkstations efficiënter. Hallo-gegevensoverdracht is voltooid, Hallo momentopname wordt verwijderd als een herstelpunt wordt gemaakt. In de klassieke Azure-portal Hallo weergegeven. dit herstelpunt.

> [!NOTE]
> Voor virtuele Linux-machines is alleen bestandsconsistente back-ups het mogelijk.
>
>

## <a name="prerequisites"></a>Vereisten
Azure Backup tooback up DPM-gegevens als volgt voorbereiden:

1. **Maak een back-upkluis**. Als u een back-upkluis hebt gemaakt in uw abonnement, Zie hello Azure portal versie van dit artikel - [tooback up werkbelastingen tooAzure met DPM voorbereiden](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
  > U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
  >- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
  >- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
  >

2. **Kluisreferenties downloaden** — In Azure Backup uploaden Hallo-beheercertificaat u toohello kluis hebt gemaakt.
3. **Hello Azure Backup Agent installeren en registreren van Hallo server** : van Azure back-up, Hallo-agent installeren op elke DPM-server en Hallo DPM-server registreren in Hallo back-upkluis.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Vereisten (en beperkingen)
* DPM kan worden uitgevoerd als een fysieke server of een Hyper-V virtuele machine is geïnstalleerd op System Center 2012 SP1 of System Center 2012 R2. Kan ook worden uitgevoerd als een virtuele machine van Azure met System Center 2012 R2 met ten minste DPM 2012 R2 updatepakket 3 of een virtuele Windows-machine in VMWare uitgevoerd op System Center 2012 R2 met ten minste updatepakket 5.
* Als u DPM met System Center 2012 SP1 uitvoert, moet u de Update Rollup 2 voor System Center Data Protection Manager SP1 installeren. Dit is vereist voordat u hello Azure Backup Agent kunt installeren.
* Hallo DPM-server moet Windows PowerShell en .net Framework 4.5 geïnstalleerd.
* DPM kan back-up van de meeste werkbelastingen tooAzure back-up. Voor een volledige lijst met wat is er Zie ondersteund hello Azure Backup ondersteunt de volgende items.
* Gegevens die zijn opgeslagen in Azure Backup kunnen niet worden hersteld met 'kopiëren tootape' Hallo-optie.
* U hebt een Azure-account nodig hello Azure Backup-functie is ingeschakeld. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Meer informatie over [prijzen van Azure Backup](https://azure.microsoft.com/pricing/details/backup/).
* Hello Azure Backup Agent toobe geïnstalleerd op Hallo-servers die u tooback-up wilt maken met Azure Backup worden vereist. Elke server moet ten minste 10% van de grootte Hallo Hallo-gegevens die worden back-up, beschikbaar als lokale vrije opslagruimte hebben. Bijvoorbeeld, vereist een back-up 100 GB aan gegevens een minimum van 10 GB aan vrije ruimte op Hallo scratchruimte locatie. Hallo minimale is 10%, wordt 15% van de lokale opslag vrije ruimte toobe gebruikt voor de cachelocatie hello aanbevolen.
* Gegevens worden opgeslagen in hello Azure kluis opslag. Hallo van een gegevensbron (bijvoorbeeld een virtuele machine of een database) mag niet groter zijn dan 54,400 GB, maar er is geen limiet toohello bedrag van gegevens die u kunt back-ups tooan Azure Backup-kluis.

Deze bestandstypen worden ondersteund voor back-up tooAzure:

* Versleuteld (volledige back-ups alleen)
* Gecomprimeerd (incrementele back-ups ondersteund)
* Sparse (incrementele back-ups ondersteund)
* Gecomprimeerd en sparse (behandeld als Sparse)

En deze worden niet ondersteund:

* Servers op hoofdlettergevoelige bestandssystemen worden niet ondersteund.
* Vaste koppelingen (overgeslagen)
* Reparsepunten (overgeslagen)
* Versleuteld en gecomprimeerd (overgeslagen)
* Versleuteld en sparse (overgeslagen)
* Gecomprimeerde stream
* Sparse stream

> [!NOTE]
> Van in System Center 2012 DPM met SP1 en hoger, u kunt back-up-werkbelastingen beveiligd met DPM tooAzure met Microsoft Azure Backup.
>
>
