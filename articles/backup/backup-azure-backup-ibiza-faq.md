---
title: aaaRecovery Services-kluis Veelgestelde vragen | Microsoft Docs
description: Deze versie van Hallo Veelgestelde vragen over ondersteunt Hallo openbare Preview-versie van hello Azure Backup-service. Toofrequently van antwoorden op veelgestelde vragen over Hallo back-upagent, back-up en retentie, herstel, beveiliging en andere veelgestelde vragen over hello Azure back-upoplossing.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-upoplossing; Backup-service
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Recovery Services-kluis - veelgestelde vragen
Dit artikel vindt u informatie specifieke tooRecovery Services-kluis en Hallo vormt een aanvulling [Veelgestelde vragen over Azure Backup](backup-azure-backup-faq.md). Hallo Veelgestelde vragen over Azure Backup biedt de volledige set Hallo van vragen en antwoorden over hello Azure Backup-service.  

U kunt vragen over Azure Backup in Hallo sectie Disqus van dit artikel of een verwant artikel. U kunt ook vragen over Azure Backup-service Hallo boeken in Hallo [discussieforum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Recovery Services-kluizen zijn op basis van Resource Manager. Worden Backup-kluizen (klassieke modus) nog steeds ondersteund? <br/>
Ja, Backup-kluizen worden nog steeds ondersteund. Maken van de Backup-kluizen in Hallo [klassieke portal](https://manage.windowsazure.com). Recovery Services-kluizen maken in Hallo [Azure-portal](https://portal.azure.com). Maar wij raden u toocreate recovery services-kluis als alle toekomstige verbeteringen worden alleen in de Recovery Services-kluis.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Kan ik een Backup-kluis tooa Recovery Services-kluis migreren? <br/>
Helaas Nee, migreren op dit moment u niet Hallo inhoud van een back-up kluis tooa die Recovery Services-kluis. We werken ernaar toe om deze functionaliteit toe te voegen, maar dit is niet beschikbaar in de openbare evaluatieversie.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Ondersteunen Recovery Services-kluizen klassieke virtuele machines of virtuele machines op basis van Resource Manager? <br/>
Recovery Services-kluizen ondersteunen beide modellen.  U kunt back-up van een VM gemaakt in Hallo klassieke portal (de klassieke modus VM's) of een virtuele machine gemaakt in Azure-portal (die Resource Manager gebaseerde) Hallo tooa Recovery Services-kluis.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Ik heb back-ups van mijn klassieke VM’s opgeslagen in de back-upkluis. Ik wil toomigrate mijn virtuele machines van de klassieke modus tooResource Manager-modus.  Hoe kan ik een back-up ervan opslaan in de Recovery Services-kluis?
Back-ups van klassieke virtuele machines in de back-upkluis won't migreren automatisch toorecovery services-kluis wanneer u Hallo virtuele machines van klassieke tooResource Manager-modus migreert. Volg deze stappen voor migratie van back-ups van VM’s:

1. Ga te in de back-upkluis**beveiligde Items** tabblad en selecteer Hallo VM. Klik op [Beveiliging stoppen](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laat de optie *Gekoppelde back-upgegevens verwijderen* **uitgeschakeld**.
2. In Hallo [Azure-portal](https://portal.azure.com), gaat u toohello **extensies** menu voor Hallo VM en Hallo verwijderen **VMSnapshot/VMSnapshotLinux** extensie.
3. Hallo virtuele machine migreren vanuit de klassieke modus tooResource Manager-modus. Zorg ervoor dat opslag en netwerk overeenkomt toovirtual machine ook gemigreerde tooResource Manager-modus.
4. Een recovery services-kluis maken en configureren op Hallo back-up met behulp van virtuele machine gemigreerd **back-** actie boven op het kluisdashboard. Meer informatie over het te[back-up in de recovery services-kluis inschakelen](backup-azure-vms-first-look-arm.md)
