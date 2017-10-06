---
title: 'Azure Backup: Virtuele machines hello Azure-portal met Restore | Microsoft Docs'
description: Azure een virtuele machine herstellen vanaf een herstelpunt met Azure portal
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: terugzetten van back-up. hoe toorestore; herstelpunt;
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Azure portal toorestore virtuele machines gebruiken
> [!div class="op_single_selector"]
> * [Herstellen van virtuele machines in de klassieke portal](backup-azure-restore-vms.md)
> * [Herstellen van virtuele machines in Azure-portal](backup-azure-arm-restore-vms.md)
>
>

Uw gegevens beschermen door het maken van momentopnamen van uw gegevens op de gedefinieerde intervallen. Deze momentopnamen worden aangeduid als herstelpunten en ze worden opgeslagen in de recovery services-kluizen. Als, of wanneer het benodigde toorepair of opnieuw opbouwen van een virtuele machine, kunt u Hallo VM vanaf elke Hallo opgeslagen herstelpunten herstellen. Wanneer u een herstelpunt herstelt, kunt u een nieuwe virtuele machine die een punt in tijd weergave van uw VM back-up maken of herstellen schijven en gebruik Hallo-sjabloon die wordt geleverd samen met het toocustomize Hallo VM hersteld of Voer het herstel van een afzonderlijk bestand. Dit artikel wordt uitgelegd hoe een VM-tooa toorestore nieuwe virtuele machine of terugzetten van alle back-up-schijven. Raadpleeg te voor herstel van afzonderlijke bestanden,[bestanden herstellen vanuit back-up van virtuele machine in Azure](backup-azure-restore-files-from-vm.md)

![3-ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Dit artikel bevat Hallo informatie en procedures voor het herstellen van virtuele machines die zijn geïmplementeerd met behulp van Hallo Resource Manager-model.
>
>

Herstellen van een virtuele machine of alle schijven van virtuele machine back-up bestaat uit twee stappen:

1. Selecteer een herstelpunt voor herstel
2. Hallo selecteren type herstellen - Maak een nieuwe virtuele machine of schijven herstellen en geef vereiste parameters. 

## <a name="select-restore-point-for-restore"></a>Selecteer het herstelpunt voor herstel
1. Meld u aan toohello [Azure-portal](http://portal.azure.com/)
2. Klik op Hallo menu van Azure, **Bladeren** en typt u in de lijst met services Hallo **Recovery Services**. lijst met services Hallo aangepast toowhat die u typt. Wanneer er **Recovery Services-kluizen**, selecteert u deze.

    ![Recovery Services-kluis openen](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Hallo-lijst met kluizen in Hallo abonnement wordt weergegeven.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Selecteer Hallo kluis die zijn gekoppeld aan Hallo VM die u wilt dat toorestore uit Hallo-lijst. Wanneer u Hallo kluis klikt, wordt het dashboard wordt geopend.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Nu dat u Hallo kluisdashboard bent. Op Hallo **back-Upitems** tegel, klikt u op **Azure Virtual Machines** toodisplay Hallo virtuele machines die zijn gekoppeld aan Hallo kluis.

    ![kluisdashboard](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Hallo **back-Upitems** blade geopend en geeft de lijst Hallo van virtuele machines in Azure.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Selecteer een dashboard VM tooopen Hallo Hallo lijst. Hallo VM dashboard wordt toohello gebied bewaking, waarin Hallo terugzetten punten tegel geopend.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Klik op het Hallo VM dashboard menu **herstellen**

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Hallo terugzetten blade wordt geopend.

    ![blade herstellen](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Op Hallo **herstellen** blade, klikt u op **herstelpunt** tooopen hello **terugbrengen Selecteer** blade.

    ![blade herstellen](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Standaard wordt alle herstelpunten van Hallo afgelopen 30 dagen Hallo dialoogvenster weergegeven. Gebruik Hallo **Filter** tooalter Hallo tijdsbereik Hallo herstelpunten weergegeven. Herstelpunten van alle consistentie worden standaard weergegeven. Wijzig **alle herstellen verwijst** filteren tooselect een specifieke consistentie van herstelpunten. Zie voor meer informatie over elk type van het van herstelpunt Hallo uitleg van [gegevensconsistentie](backup-azure-vms-introduction.md#data-consistency).  

   * **Consistentie van de punt herstellen** uit deze lijst kiezen:
     * Consistente herstelpunten crash
     * Toepassing consistente herstelpunten
     * Bestandssysteemconsistente herstelpunten
     * Alle herstelpunten.  
8. Kies een herstelpunt en klik op **OK**.

    ![herstelpunt kiezen](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Hallo **herstellen** blade ziet u Hallo herstelpunt is ingesteld.

    ![herstelpunt is ingesteld](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Op Hallo **herstellen** blade **configuratie terugzetten** automatisch geopend nadat het herstelpunt is ingesteld.

## <a name="choosing-a-vm-restore-configuration"></a>De configuratie van een virtuele machine herstellen te kiezen
Nu dat u hebt geselecteerd herstelpunt hello, kiest u een configuratie voor het terugzetten van VM. Uw keuzes voor het configureren van Hallo hersteld VM toouse zijn: Azure portal of PowerShell.

1. Als u nog geen er, gaat u toohello **herstellen** blade. Zorg ervoor dat een [herstelpunt is geselecteerd](#select-restore-point-for-restore), en klik op **configuratie terugzetten** tooopen hello **herstelconfiguratie** blade.

    ![configuratiewizard voor herstel is ingesteld](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Op Hallo **configuratie terugzetten** blade hebt u twee mogelijkheden:
   * Volledige virtuele machine herstellen
   * Herstel een back-up schijven

Portal biedt een optie voor snelle invoer voor de herstelde virtuele machine. Als u wilt dat toocustomize Hallo VM-configuratie of namen van Hallo resources gemaakt als onderdeel van de keuze van een nieuwe virtuele machine maken, gebruikt u PowerShell of portal toorestore een back-up schijven en gebruik PowerShell-opdrachten tooattach ze toochoice van VM-configuratie of het gebruik sjabloon die wordt geleverd met het terugzetten van schijven toocustomize Hallo VM hersteld. Zie [herstellen van een virtuele machine met speciale netwerkconfiguraties](#restoring-vms-with-special-network-configurations) voor meer informatie over het toorestore VM die meerdere NIC's heeft of onder de load balancer. Als uw virtuele machine van Windows gebruikt [HUB licentieverlening](../virtual-machines/windows/hybrid-use-benefit-licensing.md), toorestore schijven nodig en gebruiken van PowerShell/sjabloon als opgegeven hieronder toocreate Hallo VM en zorg ervoor dat u LicenseType als 'Windows_Server' opgeeft tijdens het maken van VM tooavail HUB voordelen op herstelde virtuele machine. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Een nieuwe virtuele machine maken van herstelpunt
Als u nog geen daar [Selecteer een herstelpunt](#restoring-vms-with-special-network-configurations) voordat u doorgaat toocreating een nieuwe virtuele machine vanuit herstelpunt verwijzen. Zodra het herstelpunt is geselecteerd, klikt u op Hallo **configuratie terugzetten** blade invoeren of selecteren van waarden voor elk van de volgende velden Hallo:

* **Type herstellen** -virtuele machine maken.
* **Naam van virtuele machine** -Geef een naam op voor Hallo VM. Hallo-naam moet uniek toohello resourcegroep (voor een Resource Manager geïmplementeerde VM) of cloudservice (voor een klassieke VM). U kunt Hallo virtuele machine niet vervangen als deze al in het Hallo-abonnement bestaat.
* **Resourcegroep** : gebruik een bestaande resourcegroep of maak een nieuwe. Als u een klassieke virtuele machine herstellen wilt, gebruikt u deze veld toospecify Hallo-naam van een nieuwe cloudservice. Als u een nieuwe resource-group/cloudservice maakt, moet Hallo naam globaal uniek zijn. Normaal gesproken Hallo cloudservicenaam is gekoppeld aan een openbare URL - voorbeeld: [cloudservice]. cloudapp.net. Als u probeert toouse een naam op voor Hallo cloud resource group/cloudservice die is al gebruikt, worden in Azure wordt toegewezen Hallo resource group/cloudservice dezelfde naam Hallo Hallo VM. Azure weergeven resource groepen/cloudservices en virtuele machines die niet zijn gekoppeld aan een affiniteitsgroepen Zie voor meer informatie [hoe toomigrate van Affiniteitsgroepen tooa regionaal virtueel netwerk (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Virtueel netwerk** : Selecteer Hallo virtueel netwerk (VNET) bij het maken van Hallo VM. Hallo-veld bevat alle VNETs die zijn gekoppeld aan het Hallo-abonnement. Resourcegroep Hallo VM wordt weergegeven tussen haakjes.
* **Subnet** -als Hallo VNET subnetten heeft, Hallo eerste subnet is standaard geselecteerd. Als er extra subnetten, Hallo Selecteer de gewenste subnet.
* **Storage-account** -dit menu Hallo storage-accounts in Hallo bevat dezelfde locatie als Hallo Recovery Services-kluis. Storage-accounts die Zoneredundant zijn worden niet ondersteund. Als er geen opslagaccounts met hello dezelfde locatie als Hallo Recovery Services-kluis, moet u dit maken voordat u begint Hallo restore-bewerking. replicatietype Hallo van het opslagaccount wordt vermeld tussen haakjes.

![configuratiewizard voor herstel is ingesteld](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Als u een Resource Manager geïmplementeerde VM terugzetten wilt, moet u een virtueel netwerk (VNET) te identificeren. Een virtueel netwerk (VNET) is optioneel voor een klassieke virtuele machine.
> 2. Als u virtuele machines met beheerde schijven herstelt, zorg ervoor dat geselecteerde opslagaccount is niet ingeschakeld voor de opslag Service Encryption(SSE) in de levensduur.
> 3. Op basis van de opslagtype Hallo van storage-account geselecteerd (premium of standaard), alle schijven teruggezet worden premium of standaardschijven. Momenteel ondersteund niet gemengde modus van schijven bij het herstellen.  
>
>

Op Hallo **configuratie terugzetten** blade, klikt u op **OK** toofinalize Hallo terugzetten configuratie. Op Hallo **herstellen** blade, klikt u op **herstellen** tootrigger Hallo restore-bewerking.

## <a name="restore-backed-up-disks"></a>Herstel een back-up schijven
Als u toocustomize Hallo virtuele machine wilt u wilt toocreate van een back-up schijf dan wat aanwezig in de blade met een configuratie herstellen, selecteer is **schijven herstellen** als waarde voor **herstellen Type**. Deze keuze vraagt om een opslagaccount waarnaar de schijven van de back-ups worden gekopieerd. Selecteer een account dat de shares dezelfde locatie Hallo zoals Hallo Recovery Services-kluis bij het kiezen van een opslagaccount. Storage-accounts die Zoneredundant zijn worden niet ondersteund. Als er geen opslagaccounts met hello dezelfde locatie als Hallo Recovery Services-kluis, moet u dit maken voordat u begint Hallo restore-bewerking. replicatietype Hallo van het opslagaccount wordt vermeld tussen haakjes.

Nadat de herstelbewerking is voltooid, kunt u:
* [Gebruik sjabloon toocustomize Hallo hersteld VM](#use-templates-to-customize-restore-vm)
* [Gebruik Hallo hersteld schijven tooattach tooan bestaande virtuele machine](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Maak een nieuwe virtuele machine met behulp van PowerShell van herstelde schijven.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Op Hallo **configuratie terugzetten** blade, klikt u op **OK** toofinalize Hallo terugzetten configuratie. Op Hallo **herstellen** blade, klikt u op **herstellen** tootrigger Hallo restore-bewerking.

![De herstelconfiguratie voltooid](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Hallo-herstelbewerking bijhouden
Zodra u de herstelbewerking Hallo activeert, maakt Hallo Backup-service een taak voor het bijhouden van Hallo restore-bewerking. Hallo Backup-service maakt ook en tijdelijk Hallo melding weergegeven in het meldingengebied van de portal. Als u Hallo-bericht niet ziet, kunt u altijd klikken Hallo meldingen pictogram tooview uw meldingen.

![Herstel is geactiveerd](./media/backup-azure-arm-restore-vms/restore-notification.png)

tooview hello bewerking tijdens het verwerken van of tooview wanneer deze is voltooid, opent Hallo back-up takenlijst.

1. Klik op Hallo menu van Azure, **Bladeren** en typt u in de lijst met services Hallo **Recovery Services**. lijst met services Hallo aangepast toowhat die u typt. Wanneer er **Recovery Services-kluizen**, selecteert u deze.

    ![Recovery Services-kluis openen](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Hallo-lijst met kluizen in Hallo abonnement wordt weergegeven.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Selecteer Hallo kluis die zijn gekoppeld aan Hallo VM u teruggezet uit Hallo-lijst. Wanneer u Hallo kluis klikt, wordt het dashboard wordt geopend.
3. In het kluisdashboard Hallo op Hallo **back-uptaken** tegel, klikt u op **Azure Virtual Machines** toodisplay Hallo taken die zijn gekoppeld aan het Hallo-kluis.

    ![kluisdashboard](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Hallo **back-uptaken** blade wordt geopend en Hallo lijst met taken.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Gebruik sjablonen toocustomize terugzetten vm
Eenmaal [schijven herstelbewerking is voltooid](#Track-the-restore-operation), kunt u Hallo-sjabloon die wordt gegenereerd als onderdeel van de restore-bewerking toocreate een nieuwe virtuele machine met een configuratie die verschillen van de back-configuratie of toocustomize namen van bronnen Als u een nieuwe virtuele machine maken van herstelpunt gemaakt. 

> [!NOTE]
> Sjablonen worden toegevoegd als onderdeel van de schijven herstellen voor herstelpunten die zijn gemaakt na 1 maart 2017. Ze zijn van toepassing op de schijf niet-versleutelde en niet-beheerde virtuele machines. Ondersteuning voor versleutelde VM's en beheerd schijf virtuele machines wordt binnenkort in toekomstige releases. 
>
>

tooget hello sjabloon gegenereerd als onderdeel van de optie voor terugzetten schijven,

1. Ga toorestore taakdetails toohello taak overeenkomt. 
2. Klik op herstellen job details welkomstscherm, op *sjabloon implementeren* tooinitiate sjabloonimplementatie knop. 

     ![taak inzoomen herstellen](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Gebruik op Hallo implementeren sjabloon blade voor aangepaste implementatie sjabloonimplementatie te[bewerken en het Hallo-sjabloon implementeren](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) of toevoeg meer aanpassingen door [ontwerpen van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md) voordat u implementeert. 

   ![bij het laden van sjabloonimplementatie](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Na het invoeren van Hallo vereist waarden accepteren Hallo *voorwaarden en bepalingen* en klik op **aankoop**.

   ![sjabloonimplementatie verzenden](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Stappen na herstellen
* Als u van een cloud-init op basis van Linux-distributie zoals Ubuntu, uit veiligheidsoverwegingen gebruikmaakt, wachtwoord geblokkeerd boeken terugzetten. Neem hersteld gebruik VMAccess-extensie op Hallo VM te[Hallo-wachtwoord opnieuw instellen](../virtual-machines/linux/classic/reset-access.md). U wordt aangeraden met behulp van SSH-sleutels op deze distributies tooavoid opnieuw instellen van wachtwoord post terugzetten.
* Aanwezig zijn tijdens de back-config Hallo uitbreidingen worden geïnstalleerd, maar niet ingeschakeld. Installeer de extensies als er een probleem. 
* Als Hallo back-up VM heeft een vaste IP-adres, post terugzetten, herstelde virtuele machine heeft een dynamisch IP-tooavoid conflict bij het maken van VM hersteld. Meer informatie over hoe u kunt [toevoegen van een statische IP-toorestored VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Herstelde virtuele machine geen beschikbaarheid waarde ingesteld. Aangeraden schijven-optie voor terugzetten en [toe te voegen beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md) wanneer het maken van een virtuele machine van PowerShell of met behulp van sjablonen schijven teruggezet. 


## <a name="backup-for-restored-vms"></a>Back-up voor de herstelde virtuele machines
Als u VM toosame resourcegroep met dezelfde naam als het oorspronkelijk back-up VM Hallo hebt teruggezet, blijft back-up op Hallo VM post terugzetten. Als u hebt hersteld VM tooa andere resourcegroep of een andere naam voor de herstelde virtuele machine wordt opgegeven, wordt dit beschouwd als een nieuwe virtuele machine en moet u toosetup back-up voor de herstelde virtuele machine.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Herstellen van een virtuele machine tijdens de Azure-dataCenter na noodgevallen
Azure Backup kan herstellen van een back-up VMs toohello gekoppeld Datacenter geval Hallo primaire datacenters waarin VM's worden uitgevoerd na noodgevallen ervaringen en u back-up kluis toobe geografisch redundante geconfigureerd. Tijdens deze scenario's, moet u een opslagaccount aanwezig in het datacenter gekoppeld is tooselect en rest van het herstelproces Hallo blijft hetzelfde. Azure Backup maakt gebruik van Compute-service van de gekoppelde geo toocreate Hallo hersteld virtuele machine. Meer informatie over [Azure Data center tolerantie](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Domain Controller virtuele machines herstellen
Back-up van de domeincontroller (DC) virtuele machines is een ondersteund scenario met Azure Backup. Maar wees voorzichtig tijdens het terugzetten van een Hallo. de juiste herstelproces Hallo is afhankelijk van Hallo-structuur van Hallo-domein. In de meest eenvoudige geval Hallo hebt u een enkele DC in één domein. Meer vaak voor productie-belastingen hebt u één domein met meerdere DC's, mogelijk met sommige domeincontrollers on-premises. Mogelijk hebt u ten slotte een forest met meerdere domeinen. 

Vanuit een Active Directory perspectief hello is Azure VM net als elke andere virtuele machine op een moderne ondersteunde hypervisor. Hallo belangrijk verschil met lokale hypervisors is dat er geen VM-console beschikbaar in Azure is. Er is een console vereist voor bepaalde scenario's zoals herstellen met behulp van een Bare Metal Recovery (BMR) type back-up. Virtuele machine herstellen vanuit back-upkluis Hallo is echter een volledige vervanging voor BMR. Active Directory Restore Mode (DSRM) is ook beschikbaar is, zodat alle Active Directory herstelscenario's mogelijk of gewenst zijn is. Zie voor meer achtergrondinformatie [back-up en herstellen van de overwegingen voor gevirtualiseerde domeincontrollers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) en [plannen voor herstel van Active Directory-Forest](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Enkele DC in één domein
Hallo VM kan worden hersteld (zoals VM) vanuit hello Azure portal of met behulp van PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Meerdere domeincontrollers in één domein
Wanneer andere DC's van hetzelfde domein kan worden bereikt via Hallo hello netwerk, kan Hallo DC zoals een VM worden hersteld. Als het laatste resterende DC in domein Hallo hello of een herstel in een geïsoleerd netwerk wordt uitgevoerd, kan een herstelprocedure forest moet worden gevolgd.

### <a name="multiple-domains-in-one-forest"></a>Meerdere domeinen in een forest
Wanneer andere DC's van hetzelfde domein kan worden bereikt via Hallo hello netwerk, kan Hallo DC zoals een VM worden hersteld. In alle andere gevallen wordt een forestherstel echter aanbevolen.

## <a name="restoring-vms-with-special-network-configurations"></a>Herstellen van virtuele machines met speciale netwerkconfiguraties
Het is mogelijk tooback up en herstel virtuele machines met Hallo speciale netwerkconfiguraties te volgen. Deze configuraties vereisen echter bepaalde letten tijdens het herstelproces Hallo doorlopen.

* VM's onder de load balancer (intern en extern)
* Virtuele machines met meerdere gereserveerde IP 's
* Virtuele machines met meerdere NIC 's

> [!IMPORTANT]
> Bij het maken van speciale netwerkconfiguratie Hallo voor virtuele machines, moet u PowerShell toocreate virtuele machines van Hallo schijven teruggezet.
>
>

toofully Maak Hallo virtuele machines na het terugzetten van toodisk, als volgt te werk:

1. Hallo schijven herstellen vanuit een recovery services kluis met [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Hallo VM-configuratie is vereist voor de load balancer maken / meerdere NIC/meerdere gereserveerde IP-met behulp van PowerShell-cmdlets Hallo en deze toocreate Hallo VM van de gewenste configuratie gebruiken.

   * Virtuele machine maken in een cloudservice met [interne Load balancer](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Te maken van VM tooconnect[Internet gerichte load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Met virtuele machine maken [meerdere NIC's](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Met virtuele machine maken [meerdere gereserveerde IP-adressen](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Volgende stappen
Nu u uw virtuele machines kunt herstellen, gaat u naar Hallo probleemoplossing artikel voor meer informatie over veelvoorkomende problemen met virtuele machines. Controleer ook Hallo artikel over het beheren van taken met uw virtuele machines.

* [Het oplossen van problemen](backup-azure-vms-troubleshoot.md#restore)
* [Virtuele machines beheren](backup-azure-manage-vms.md)
