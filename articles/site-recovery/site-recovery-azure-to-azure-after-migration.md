---
title: aaaPrepare machines tooset van herstel na noodgevallen tussen Azure-regio's na de migratie tooAzure met behulp van Site Recovery | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprepare machines tooset van herstel na noodgevallen tussen Azure-regio's na de migratie tooAzure met behulp van Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Azure Virtual machines tooanother regio na migratie tooAzure repliceren met behulp van Azure Site Recovery

>[!NOTE]
> Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.

## <a name="overview"></a>Overzicht

In dit artikel helpt u bij het voorbereiden van virtuele machines in Azure voor replicatie tussen twee Azure-regio's nadat deze machines zijn gemigreerd vanuit een lokale omgeving tooAzure met behulp van Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Herstel na noodgevallen en naleving
Vandaag de dag verplaatst meer bedrijven hun tooAzure werkbelastingen. Werkbelastingen tooAzure, instellen van herstel na noodgevallen voor deze werkbelastingen is ondernemingen bedrijfskritieke lokale productie verplaatsen verplicht voor naleving en toosafeguard tegen onderbrekingen in een Azure-regio.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Stappen voor het voorbereiden van de gemigreerde machines voor replicatie
tooprepare machines voor het instellen van replicatie tooanother Azure-regio hebt gemigreerd:

1. Voltooi de migratie.
2. Installeer hello Azure-agent indien nodig.
3. Verwijder de Mobility-service Hallo.  
4. Opnieuw opstarten Hallo VM.

Deze stappen worden in de volgende secties Hallo nader beschreven.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Stap 1: Migreren van werkbelastingen die worden uitgevoerd op Hyper-V-machines, virtuele VMware-machines en fysieke servers toorun op Azure Virtual machines

tooset van replicatie en migreren van uw lokale Hyper-V, VMware en fysieke werkbelasting tooAzure, volg Hallo de stappen in Hallo [migreren Azure IaaS virtuele machines tussen Azure-regio's met Azure Site Recovery](site-recovery-migrate-to-azure.md) artikel. 

Na de migratie niet u moet toocommit of verwijderen van een failover. In plaats daarvan selecteert Hallo **volledige migratie** optie voor elke computer die u wilt toomigrate:
1. In **gerepliceerde Items**, met de rechtermuisknop op Hallo VM en klikt u op **volledige migratie**. Klik op **OK** toocomplete Hallo stap. U kunt de voortgang in de eigenschappen van de VM Hallo volgen door de bewaking van Hallo voltooid migratietaak in **Site Recovery-taken**.
2. Hallo **volledige migratie** actie Hallo migratieproces is voltooid, verwijdert u de replicatie voor Hallo-machine en Hiermee stopt u Site Recovery facturering voor Hallo-machine.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Stap 2: Installeer hello Azure VM-agent op Hallo virtuele machine
Hello Azure [VM-agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) op Hallo virtuele machine moet worden geïnstalleerd voor Hallo Site Recovery-extensie toowork en toohelp Hallo VM beveiligen.

>[!IMPORTANT]
>Vanaf versie 9.7.0.0, op virtuele machines van Windows hello Mobility service installatieprogramma ook Hallo meest recente beschikbare Azure VM-agent geïnstalleerd. Hallo virtuele machine voldoet aan de vereisten voor het gebruik van een VM-extensie, inclusief Hallo Site Recovery-extensie de installatie van de agent op migratie. Hello Azure VM-agent behoeften toobe handmatig alleen geïnstalleerd als Hallo Mobility-service is geïnstalleerd op Hallo van de gemigreerde machines is versie 9,6 of lager.

Hallo bevat volgende tabel aanvullende informatie over het installeren van de VM-agent Hallo en valideren is geïnstalleerd:

| **Bewerking** | **Windows** | **Linux** |
| --- | --- | --- |
| Hallo VM-agent installeren |Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet administrator-bevoegdheden toocomplete Hallo installatie. |Meest recente Hallo installeren [Linux-agent](../virtual-machines/linux/agent-user-guide.md). U moet administrator-bevoegdheden toocomplete Hallo installatie. U wordt aangeraden Hallo-agent installeren uit de opslagplaats voor distributie. We *wordt niet aanbevolen* Hallo Linux VM-agent installeren rechtstreeks vanuit GitHub.  |
| Hallo VM-agent-installatie valideren |1. Blader toohello C:\WindowsAzure\Packages map in hello Azure VM. U ziet Hallo WaAppAgent.exe bestand. <br>2. Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo **productversie** veld moet 2.6.1198.718 of hoger. |N.v.t. |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Stap 3: Verwijder Hallo Mobility-service van Hallo gemigreerde virtuele machines

Als u uw lokale VMware-machines of fysieke servers op Windows of Linux hebt gemigreerd, moet u toomanually verwijderen of het verwijderen Hallo Mobility-service van Hallo gemigreerde virtuele machine.

>[!IMPORTANT]
>Deze stap is niet vereist voor de gemigreerde tooAzure Hyper-V-machines.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Verwijder de Mobility-service Hallo op een virtuele machine van Windows Server
Gebruik een van de Hallo methoden toouninstall Hallo Mobility-service op een Windows Server-computer te volgen.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Verwijder met behulp van de gebruikersinterface van Windows hello
1. Selecteer in het Configuratiescherm hello, **programma's**.
2. Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.

##### <a name="uninstall-at-a-command-prompt"></a>Bij een opdrachtprompt verwijderen
1. Open een opdrachtpromptvenster als administrator.
2. toouninstall Hallo van de Mobility-service, Hallo volgende opdracht uitvoeren:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Verwijder de Mobility-service Hallo op een Linux-computer
1. Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.
2. Ga in een terminal te/gebruiker/local/ASR.
3. toouninstall Hallo van de Mobility-service, Hallo volgende opdracht uitvoeren:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Stap 4: Hallo VM starten

Nadat u de Mobility-service Hallo verwijderd, opnieuw opstarten Hallo VM voordat u replicatie tooanother Azure-regio instellen.


## <a name="next-steps"></a>Volgende stappen
- Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md).
- Meer informatie over [richtlijnen voor het repliceren van virtuele machines van Azure toegang](site-recovery-azure-to-azure-networking-guidance.md).
