---
title: 'Eerste blik: een back-up maken van virtuele machines van Azure met een back-upkluis | Microsoft Docs'
description: Gebruik de klassieke portal tooback Hallo van Azure Virtual machines tooa Backup-kluis. Deze zelfstudie wordt uitgelegd hoe alle fasen, inclusief Hallo Backup-kluis maken, Hallo VMs registreren, back-upbeleid maken en Hallo eerste back-uptaak wordt uitgevoerd.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Eerste blik: een back-up maken van virtuele machines van Azure
> [!div class="op_single_selector"]
> * [Virtuele machines beveiligen met een Recovery Services-kluis](backup-azure-vms-first-look-arm.md)
> * [Virtuele machines van Azure beveiligen met een back-upkluis](backup-azure-vms-first-look.md)
>
>

Deze zelfstudie leert u Hallo stappen voor het back-ups van een virtuele Azure-machine (VM) tooa back-upkluis in Azure. In dit artikel beschrijft Hallo klassieke model of de Service Manager-implementatiemodel, voor back-ups van virtuele machines. Hallo volgende stappen gelden alleen tooBackup kluizen in de klassieke portal Hallo gemaakt. Microsoft raadt het gebruik van Resource Manager-model Hallo voor nieuwe implementaties.

Als u geïnteresseerd in de back-ups van een VM tooa Recovery Services-kluis die tooa resourcegroep behoort bent, Zie [eerste kennismaking: VM's beveiligen met een recovery services-kluis](backup-azure-vms-first-look-arm.md).

toosuccessfully hello volgende voltooien zelfstudie gelden de volgende vereisten:

* U hebt een VM gemaakt in uw Azure-abonnement.
* Hallo VM heeft verbinding tooAzure openbare IP-adressen. Zie [Netwerkverbinding](backup-azure-vms-prepare.md#network-connectivity) voor meer informatie.


> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). Deze zelfstudie is bedoeld voor gebruik met virtuele machines die zijn gemaakt in de klassieke portal Hallo.
>
>

## <a name="create-a-backup-vault"></a>Een back-upkluis maken
Een back-upkluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die zijn gemaakt na verloop van tijd worden opgeslagen. Hallo back-upkluis bevat ook Hallo back-upbeleid dat toegepaste toohello virtuele machines back-up wordt gemaakt.

> [!IMPORTANT]
> Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.
> U kunt uw back-up kluizen tooRecovery Services-kluizen upgraden. Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.<br/> U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017. **Per 1 november 2017**:
>- Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.
>- U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo. In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Virtuele machines van Azure detecteren en registreren
Voordat u Hallo VM met een kluis registreert, voert u Hallo detectie proces tooidentify nieuwe VM's. Dit geeft een lijst met virtuele machines in Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloud service-naam en het Hallo-regio.

1. Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com/)
2. Klik in de klassieke Azure-portal hello, **Recovery Services** tooopen Hallo lijst met Recovery Services-kluizen.
    ![Workload selecteren](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. Selecteer in de lijst met kluizen Hallo Hallo kluis tooback van een virtuele machine.

    Wanneer u uw kluis selecteert, wordt geopend in Hallo **Quick Start** pagina
4. Hallo kluismenu en klik op **geregistreerde Items**.

    ![Workload selecteren](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. Van Hallo **Type** selecteert u **Azure virtuele Machine**.

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. Klik op **DISCOVER** Hallo Hallo pagina onderaan in.
    ![Detectieknop](./media/backup-azure-vms/discover-button-only.png)

    Hallo detectieproces kan enkele minuten duren tabelindeling van Hallo virtuele machines. Er is een melding aan de onderkant Hallo van welkomstscherm waarmee u weet dat Hallo-proces wordt uitgevoerd.

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    Hallo melding wijzigt zodra het Hallo-proces is voltooid.

    ![Detectie uitgevoerd](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Klik op **REGISTREREN** Hallo Hallo pagina onderaan in.
    ![Registratieknop](./media/backup-azure-vms-first-look/register-icon.png)
8. In Hallo **Items registreren** snelmenu, selecteer Hallo virtuele machines die u tooregister wilt.

   > [!TIP]
   > U kunt in meerdere virtuele machines tegelijkertijd registreren.
   >
   >

    Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.
9. Klik op **taak weergeven** in Hallo melding toogo toohello **taken** pagina.

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    Hallo virtuele machine wordt ook weergegeven in de lijst met geregistreerde items, inclusief Hallo status van de bewerking voor de registratie Hallo Hallo.

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    Wanneer het Hallo-bewerking is voltooid, Hallo status tooreflect Hallo gewijzigd *geregistreerd* status.

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hallo VM-Agent installeren op Hallo virtuele machine
Hello Azure VM-Agent moet worden geïnstalleerd op Hallo voor Hallo back-up extensie toowork virtuele Azure-machine. Als uw virtuele machine is gemaakt vanuit hello Azure-galerie, is Hallo VM-Agent al aanwezig op Hallo VM; u kunt te overslaan[uw VM's beveiligen](backup-azure-vms-first-look.md#create-the-backup-policy).

Als uw VM is gemigreerd uit een on-premises datacenter, Hallo VM waarschijnlijk geen Hallo die VM-Agent geïnstalleerd. U moet Hallo VM-Agent installeren op Hallo virtuele machine voordat u doorgaat tooprotect Hallo VM. Zie voor gedetailleerde stappen voor het installeren van hello VM-Agent, Hallo [VM-Agent sectie Hallo back-up VMs artikel](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Hallo back-upbeleid maken
Voordat u de eerste back-uptaak Hallo activeert, Hallo schema instellen bij het maken van momentopnamen. Hallo plannen wanneer back-momentopnamen worden genomen en Hallo tijdsduur deze momentopnamen worden is bewaard, back-upbeleid Hallo. Hallo bewaren informatie is gebaseerd op opa-vader-zoon-rotatieschema.

1. Navigeer toohello back-upkluis in **Recovery Services** Hallo klassieke Azure-portal en klikt u op **geregistreerde Items**.
2. Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. Klik op **beveiligen** Hallo Hallo pagina onderaan in.
    ![Klik op Beveiligen](./media/backup-azure-vms-first-look/protect-icon.png)

    Hallo **wizard Items beveiligen** wordt weergegeven en een lijst met *alleen* virtuele machines die zijn geregistreerd en niet beveiligd.

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)
4. Hallo virtuele machines die u tooprotect wilt selecteren.

    Als er twee of meer virtuele machines met Hallo naam dezelfde, gebruik Hallo Cloudservice toodistinguish tussen Hallo virtuele machines.
5. Op Hallo **Beveiligingsconfiguratie** menu Selecteer een bestaand beleid of maak een nieuw beleid tooprotect Hallo virtuele machines die u hebt vastgesteld.

    Nieuwe back-upkluizen hebben een standaardbeleid dat is gekoppeld aan het Hallo-kluis. Dit beleid maakt dagelijks elke avond een momentopname en Hallo dagelijkse momentopname is 30 dagen bewaard. Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld. Echter, Hallo virtuele machine kan alleen worden gekoppeld aan één beleid tegelijk.

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Een back-upbeleid bevat een bewaarschema voor Hallo geplande back-ups. Als u een bestaande back-upbeleid selecteert, kunt u zich niet kan toomodify Hallo opties in de volgende stap Hallo.
   >
   >
6. Op **bewaartermijn** definiëren dagelijkse, wekelijkse, maandelijkse en jaarlijkse bereik voor de specifieke back-uppunten Hallo Hallo.

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    Bewaarbeleid geeft Hallo tijdsduur voor het opslaan van een back-up. U kunt verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt.
7. Klik op **taken** tooview Hallo lijst met **beveiliging configureren** taken.

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

    Nu dat u Hallo beleid hebt ingesteld, gaat u de volgende stap toohello en Hallo eerste back-up uitvoeren.

## <a name="initial-backup"></a>Eerste back-up
Als een virtuele machine is beveiligd met een beleid, kunt u deze relatie bekijken op Hallo **beveiligde Items** tabblad. Totdat de eerste back-up Hallo, hello optreedt **beveiligingsstatus** wordt weergegeven als **beveiligd - (in behandeling van eerste back-up)**. Hallo eerste geplande back-up is standaard Hallo *eerste back-up*.

![Back-up in behandeling](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello eerste back-up nu:

1. Op Hallo **beveiligde Items** pagina, klikt u op **back-up nu** Hallo Hallo pagina onderaan in.
    ![Pictogram van Backup Now (Nu back-up maken)](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hello Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking Hallo.
2. Klik op Hallo **taken** tabblad tooview Hallo lijst met taken.

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Wanneer de eerste back-up is voltooid, Hallo status van Hallo virtuele machine in Hallo **beveiligde Items** tabblad *beveiligde*.

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > Het maken van back-ups van virtuele machines is een lokaal proces. Er kan geen virtuele machines Backup vanuit één regio tooa back-upkluis in een andere regio. Voor elke Azure-regio met VM's waarvan een back-up toobe moet ten minste één back-upkluis dus worden gemaakt in deze regio.
   >
   >

## <a name="next-steps"></a>Volgende stappen
Nu u een back-up hebt gemaakt van een VM, zijn er verschillende volgende stappen die van belang kunnen zijn. de meeste logische stap Hallo is toofamiliarize zelf met het herstellen van gegevens tooa VM. Er zijn echter beheertaken uitvoeren die helpen u te begrijpen hoe tookeep uw gegevens veilig en kosten te minimaliseren.

* [Uw virtuele machines beheren en controleren](backup-azure-manage-vms.md)
* [Virtuele machines herstellen](backup-azure-restore-vms.md)
* [Hulp bij het oplossen van problemen](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).
