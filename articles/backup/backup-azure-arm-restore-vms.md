---
title: 'Azure Backup: Restore virtuele machines met de Azure portal | Microsoft Docs'
description: Azure een virtuele machine herstellen vanaf een herstelpunt met Azure portal
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: terugzetten van back-up. het herstellen van; herstelpunt;
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1fe2b94d462a30f09cb23ab905542aa121ba46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-portal-to-restore-virtual-machines"></a>Virtuele machines herstellen met Azure-portal
> [!div class="op_single_selector"]
> * [Herstellen van virtuele machines in de klassieke portal](backup-azure-restore-vms.md)
> * [Herstellen van virtuele machines in Azure-portal](backup-azure-arm-restore-vms.md)
>
>

Uw gegevens beschermen door het maken van momentopnamen van uw gegevens op de gedefinieerde intervallen. Deze momentopnamen worden aangeduid als herstelpunten en ze worden opgeslagen in de recovery services-kluizen. Als, of wanneer dit nodig is om te herstellen of opnieuw opbouwen van een virtuele machine, kunt u de virtuele machine herstellen uit een van de opgeslagen herstelpunten. Wanneer u een herstelpunt herstelt, kunt u een nieuwe virtuele machine die een punt in tijd weergave van uw VM back-up maken of herstellen van schijven en de sjabloon die wordt geleverd samen met het aanpassen van de herstelde virtuele machine of het herstel van een afzonderlijk bestand wilt gebruiken. In dit artikel wordt uitgelegd hoe u een virtuele machine naar een nieuwe virtuele machine herstellen of alle schijven van de back-up herstellen. Raadpleeg voor herstel van afzonderlijke bestanden, [bestanden herstellen vanuit back-up van virtuele machine in Azure](backup-azure-restore-files-from-vm.md)

![3-ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure heeft twee implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Dit artikel bevat de informatie en procedures voor het herstellen van virtuele machines die zijn geïmplementeerd met behulp van de Resource Manager-model.
>
>

Herstellen van een virtuele machine of alle schijven van virtuele machine back-up bestaat uit twee stappen:

1. Selecteer een herstelpunt voor herstel
2. Het herstellen te selecteren Typ - een nieuwe virtuele machine maken of herstellen van schijven en geef vereiste parameters. 

## <a name="select-restore-point-for-restore"></a>Selecteer het herstelpunt voor herstel
1. Aanmelden bij de [Azure-portal](http://portal.azure.com/)
2. Klik in het menu van Azure **Bladeren** en typt u in de lijst met services **Recovery Services**. De lijst met services wordt aangepast aan wat u typt. Wanneer er **Recovery Services-kluizen**, selecteert u deze.

    ![Recovery Services-kluis openen](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    De lijst met kluizen in het abonnement wordt weergegeven.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Selecteer de kluis die is gekoppeld aan de virtuele machine die u wilt herstellen in de lijst. Als u op de kluis, is het dashboard wordt geopend.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Nu dat u op het kluisdashboard kunt. Op de **back-Upitems** tegel, klikt u op **Azure Virtual Machines** om weer te geven van de virtuele machines die zijn gekoppeld aan de kluis.

    ![kluisdashboard](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    De **back-Upitems** blade wordt geopend en wordt de lijst met virtuele machines in Azure.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Selecteer een virtuele machine om het dashboard te openen in de lijst. Het dashboard VM geopend met het gebied bewaking, die de tegel Restore-punten bevat.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Klik op het menu dashboard VM **herstellen**

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    De Restore-blade wordt geopend.

    ![blade herstellen](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Op de **herstellen** blade, klikt u op **herstelpunt** openen de **terugbrengen Selecteer** blade.

    ![blade herstellen](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Het dialoogvenster wordt standaard weergegeven van alle herstelpunten van de laatste 30 dagen. Gebruik de **Filter** voor het wijzigen van het tijdsbereik van de herstelpunten weergegeven. Herstelpunten van alle consistentie worden standaard weergegeven. Wijzig **alle herstellen verwijst** filtert u een specifieke consistentie van herstelpunten. Zie voor meer informatie over elk type van het van herstelpunt de uitleg van [gegevensconsistentie](backup-azure-vms-introduction.md#data-consistency).  

   * **Consistentie van de punt herstellen** uit deze lijst kiezen:
     * Consistente herstelpunten crash
     * Toepassing consistente herstelpunten
     * Bestandssysteemconsistente herstelpunten
     * Alle herstelpunten.  
8. Kies een herstelpunt en klik op **OK**.

    ![herstelpunt kiezen](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    De **herstellen** blade ziet u het herstelpunt is ingesteld.

    ![herstelpunt is ingesteld](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Op de **herstellen** blade **configuratie terugzetten** automatisch geopend nadat het herstelpunt is ingesteld.

## <a name="choosing-a-vm-restore-configuration"></a>De configuratie van een virtuele machine herstellen te kiezen
Nu dat u het herstelpunt hebt geselecteerd, kiest u een configuratie voor het terugzetten van VM. Uw keuzes voor het configureren van de herstelde virtuele machine zijn om te gebruiken: Azure portal of PowerShell.

1. Als u bent niet al er, gaat u naar de **herstellen** blade. Zorg ervoor dat een [herstelpunt is geselecteerd](#select-restore-point-for-restore), en klik op **configuratie terugzetten** openen de **herstelconfiguratie** blade.

    ![configuratiewizard voor herstel is ingesteld](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Op de **configuratie terugzetten** blade hebt u twee mogelijkheden:
   * Volledige virtuele machine herstellen
   * Herstel een back-up schijven

Portal biedt een optie voor snelle invoer voor de herstelde virtuele machine. Als u wilt aanpassen van de VM-configuratie of namen van de resources die zijn gemaakt als onderdeel van de keuze van een nieuwe virtuele machine maken, gebruikt PowerShell of portal terugzetten van back-ups van schijven en gebruiken van PowerShell-opdrachten voor deze koppelt aan de keuze van de VM-configuratie of gebruik-sjabloon die wordt geleverd met re schijven voor het aanpassen van de herstelde virtuele machine opslaan. Zie [herstellen van een virtuele machine met speciale netwerkconfiguraties](#restoring-vms-with-special-network-configurations) voor meer informatie over het herstellen van de virtuele machine met meerdere NIC's of met de load balancer. Als uw virtuele machine van Windows gebruikt [HUB licentieverlening](../virtual-machines/windows/hybrid-use-benefit-licensing.md), moet u schijven herstellen en gebruiken van PowerShell/volgens onderstaande sjabloon voor de virtuele machine maken en zorg ervoor dat u LicenseType als 'Windows_Server' opgeeft tijdens het maken van virtuele machine als u wilt gebruikmaken van HUB voordelen op virtuele machine is hersteld. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Een nieuwe virtuele machine maken van herstelpunt
Als u nog geen daar [Selecteer een herstelpunt](#restoring-vms-with-special-network-configurations) voordat u een nieuwe virtuele machine maken van herstelpunt. Zodra het herstelpunt is geselecteerd, op de **configuratie terugzetten** blade invoeren of selecteren van waarden voor elk van de volgende velden:

* **Type herstellen** -virtuele machine maken.
* **Naam van virtuele machine** -Geef een naam op voor de virtuele machine. De naam moet uniek zijn voor de resourcegroep (voor een Resource Manager geïmplementeerde VM) of de cloudservice (voor een klassieke VM). U kunt de virtuele machine niet vervangen als deze al in het abonnement bestaat.
* **Resourcegroep** : gebruik een bestaande resourcegroep of maak een nieuwe. Als u een klassieke virtuele machine herstellen wilt, moet u dit veld gebruiken om op te geven van de naam van een nieuwe cloudservice. Als u een nieuwe resource-group/cloudservice maakt, is de naam moet globaal uniek zijn. Normaal gesproken de naam van de cloudservice is gekoppeld aan een openbare URL - voorbeeld: [cloudservice]. cloudapp.net. Als u probeert te gebruiken van een naam voor de cloud resource group/cloud service wordt al gebruikt, wijst Azure de bron/het cloudservice dezelfde naam als de virtuele machine. Azure weergeven resource groepen/cloudservices en virtuele machines die niet zijn gekoppeld aan een affiniteitsgroepen Zie voor meer informatie [van Affiniteitsgroepen migreren naar een regionaal virtueel netwerk (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Virtueel netwerk** -Selecteer het virtuele netwerk (VNET) bij het maken van de virtuele machine. Het veld bevat alle VNETs die zijn gekoppeld aan het abonnement. Resourcegroep van de virtuele machine wordt weergegeven tussen haakjes.
* **Subnet** -als het VNET subnetten heeft, het eerste subnet is standaard geselecteerd. Als er extra subnetten, selecteer de gewenste subnet.
* **Storage-account** -dit menu geeft een lijst van de storage-accounts op dezelfde locatie als de Recovery Services-kluis. Storage-accounts die Zoneredundant zijn worden niet ondersteund. Als er geen opslagaccounts met dezelfde locatie als de Recovery Services-kluis, moet u er een maken voordat u de herstelbewerking start. Type van de replicatie van de storage-account wordt vermeld tussen haakjes.

![configuratiewizard voor herstel is ingesteld](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Als u een Resource Manager geïmplementeerde VM terugzetten wilt, moet u een virtueel netwerk (VNET) te identificeren. Een virtueel netwerk (VNET) is optioneel voor een klassieke virtuele machine.
> 2. Als u virtuele machines met beheerde schijven herstelt, zorg ervoor dat geselecteerde opslagaccount is niet ingeschakeld voor de opslag Service Encryption(SSE) in de levensduur.
> 3. Op basis van het type van het geselecteerde opslagaccount (premium of standaard), alle schijven teruggezet worden premium of standaardschijven. Momenteel ondersteund niet gemengde modus van schijven bij het herstellen.  
>
>

Op de **configuratie terugzetten** blade, klikt u op **OK** voor het voltooien van de configuratie herstellen. Op de **herstellen** blade, klikt u op **herstellen** voor het activeren van de herstelbewerking opnieuw.

## <a name="restore-backed-up-disks"></a>Herstel een back-up schijven
Als u wilt aanpassen van de virtuele machine u wilt maken op basis van een back-up schijf dan wat aanwezig in de blade met een configuratie herstellen, selecteer is **schijven herstellen** als waarde voor **herstellen Type**. Deze keuze vraagt om een opslagaccount waarnaar de schijven van de back-ups worden gekopieerd. Selecteer een account dat u, dezelfde locatie als de Recovery Services-kluis deelt bij het kiezen van een opslagaccount. Storage-accounts die Zoneredundant zijn worden niet ondersteund. Als er geen opslagaccounts met dezelfde locatie als de Recovery Services-kluis, moet u er een maken voordat u de herstelbewerking start. Type van de replicatie van de storage-account wordt vermeld tussen haakjes.

Nadat de herstelbewerking is voltooid, kunt u:
* [De sjabloon gebruiken voor het aanpassen van de herstelde virtuele machine](#use-templates-to-customize-restore-vm)
* [De herstelde schijven gebruiken om te koppelen aan een bestaande virtuele machine](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Maak een nieuwe virtuele machine met behulp van PowerShell van herstelde schijven.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Op de **configuratie terugzetten** blade, klikt u op **OK** voor het voltooien van de configuratie herstellen. Op de **herstellen** blade, klikt u op **herstellen** voor het activeren van de herstelbewerking opnieuw.

![De herstelconfiguratie voltooid](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-the-restore-operation"></a>De herstelbewerking bijhouden
Zodra u de herstelbewerking opnieuw activeert, maakt de Backup-service een taak voor het bijhouden van de herstelbewerking opnieuw. De Backup-service maakt ook en tijdelijk de melding weergegeven in het meldingengebied van de portal. Als u de melding niet ziet, kunt u altijd het meldingspictogram om uw meldingen weer te geven.

![Herstel is geactiveerd](./media/backup-azure-arm-restore-vms/restore-notification.png)

De bewerking uit te zien wanneer het verwerken van of om weer te geven wanneer deze is voltooid, kunt u de lijst van de taken back-up openen.

1. Klik in het menu van Azure **Bladeren** en typt u in de lijst met services **Recovery Services**. De lijst met services wordt aangepast aan wat u typt. Wanneer er **Recovery Services-kluizen**, selecteert u deze.

    ![Recovery Services-kluis openen](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    De lijst met kluizen in het abonnement wordt weergegeven.

    ![Lijst met Recovery Services-kluizen](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Selecteer de kluis die is gekoppeld aan de virtuele machine die u teruggezet in de lijst. Als u op de kluis, is het dashboard wordt geopend.
3. Op het kluisdashboard op de **back-uptaken** tegel, klikt u op **Azure Virtual Machines** om weer te geven van de taken die zijn gekoppeld aan de kluis.

    ![kluisdashboard](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    De **back-uptaken** blade wordt geopend en wordt de lijst met taken.

    ![lijst met virtuele machines in de kluis](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-to-customize-restore-vm"></a>Sjablonen gebruiken voor het aanpassen van virtuele machine herstellen
Eenmaal [schijven herstelbewerking is voltooid](#Track-the-restore-operation), kunt u de sjabloon die wordt gegenereerd als onderdeel van de restore-bewerking voor het maken van een nieuwe virtuele machine met een configuratie verschilt van de back-upconfiguratie of aanpassen van de namen van bronnen die zijn gemaakt Als een nieuwe virtuele machine te maken van herstelpunt. 

> [!NOTE]
> Sjablonen worden toegevoegd als onderdeel van de schijven herstellen voor herstelpunten die zijn gemaakt na 1 maart 2017. Ze zijn van toepassing op de schijf niet-versleutelde en niet-beheerde virtuele machines. Ondersteuning voor versleutelde VM's en beheerd schijf virtuele machines wordt binnenkort in toekomstige releases. 
>
>

De sjabloon die wordt gegenereerd als onderdeel van de optie voor terugzetten schijven, ophalen

1. Ga naar de taakdetails overeenkomt met de taak te herstellen. 
2. Klik op het scherm terugzetten job details op *sjabloon implementeren* knop sjabloonimplementatie van de te starten. 

     ![taak inzoomen herstellen](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Sjabloonimplementatie te gebruiken op de blade van de sjabloon implementeren voor aangepaste implementatie [bewerken en implementeren van de sjabloon](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) of toevoeg meer aanpassingen door [ontwerpen van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md) voordat u implementeert. 

   ![bij het laden van sjabloonimplementatie](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Na het invoeren van de vereiste waarden accepteren de *voorwaarden en bepalingen* en klik op **aankoop**.

   ![sjabloonimplementatie verzenden](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Stappen na herstellen
* Als u van een cloud-init op basis van Linux-distributie zoals Ubuntu, uit veiligheidsoverwegingen gebruikmaakt, wachtwoord geblokkeerd boeken terugzetten. Gebruik VMAccess-extensie op de herstelde virtuele machine naar [wachtwoordherstel](../virtual-machines/linux/classic/reset-access.md). U wordt aangeraden met behulp van SSH-sleutels op deze verdelingen om te voorkomen dat opnieuw instellen van wachtwoord post terugzetten.
* Uitbreidingen die aanwezig zijn tijdens de back-config wordt geïnstalleerd, maar niet ingeschakeld. Installeer de extensies als er een probleem. 
* Als de back-up-VM heeft een vaste IP-adres, post herstellen, hebt teruggezette VM een dynamische IP-adres om conflicten te voorkomen wanneer de virtuele machine maken hersteld. Meer informatie over hoe u kunt [een statische IP-adres aan de herstelde virtuele machine toevoegen](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Herstelde virtuele machine geen beschikbaarheid waarde ingesteld. Aangeraden schijven-optie voor terugzetten en [toe te voegen beschikbaarheidsset](../virtual-machines/windows/tutorial-availability-sets.md) wanneer het maken van een virtuele machine van PowerShell of met behulp van sjablonen schijven teruggezet. 


## <a name="backup-for-restored-vms"></a>Back-up voor de herstelde virtuele machines
Als u VM naar dezelfde resourcegroep met dezelfde naam als het oorspronkelijk een back-up VM teruggezet hebt, blijft de back-up op de VM post terugzetten. Als u hebt hersteld van de VM naar een andere resourcegroep of een andere naam voor de herstelde virtuele machine wordt opgegeven, wordt dit beschouwd als een nieuwe virtuele machine en moet u setup back-up voor de herstelde virtuele machine.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Herstellen van een virtuele machine tijdens de Azure-dataCenter na noodgevallen
Azure Backup kunt terugzetten van back-up VM's in het gekoppelde Datacenter voor het geval waarin VM's worden uitgevoerd na noodgevallen ervaringen en u Backup-kluis geografisch redundante worden geconfigureerd voor de primaire data center. Tijdens de dergelijke scenario's, moet u een opslagaccount aanwezig in het datacenter gekoppeld is selecteren en de rest van het herstelproces blijft hetzelfde. Azure Backup gebruikt Compute-service van het gekoppelde geo voor de herstelde virtuele machine maken. Meer informatie over [Azure Data center tolerantie](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Domain Controller virtuele machines herstellen
Back-up van de domeincontroller (DC) virtuele machines is een ondersteund scenario met Azure Backup. Maar wees voorzichtig tijdens het herstelproces. Het juiste herstelproces is afhankelijk van de structuur van het domein. In het meest eenvoudige geval hebt u een enkele DC in één domein. Meer vaak voor productie-belastingen hebt u één domein met meerdere DC's, mogelijk met sommige domeincontrollers on-premises. Mogelijk hebt u ten slotte een forest met meerdere domeinen. 

Vanuit het perspectief van een Active Directory is de Azure VM zoals elke andere virtuele machine op een moderne ondersteunde hypervisor. Het belangrijkste verschil met lokale hypervisors is dat er geen VM-console beschikbaar zijn in Azure. Er is een console vereist voor bepaalde scenario's zoals herstellen met behulp van een Bare Metal Recovery (BMR) type back-up. VM-herstel van de back-upkluis is echter een volledige vervanging voor BMR. Active Directory Restore Mode (DSRM) is ook beschikbaar is, zodat alle Active Directory herstelscenario's mogelijk of gewenst zijn is. Zie voor meer achtergrondinformatie [back-up en herstellen van de overwegingen voor gevirtualiseerde domeincontrollers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) en [plannen voor herstel van Active Directory-Forest](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Enkele DC in één domein
De virtuele machine kan worden hersteld (zoals VM) van de Azure portal of met behulp van PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Meerdere domeincontrollers in één domein
Wanneer andere DC's van hetzelfde domein kunnen worden bereikt via het netwerk, kan de DC zoals een VM worden hersteld. Als dit het laatste resterende DC in het domein is of een herstel in een geïsoleerd netwerk wordt uitgevoerd, kan een herstelprocedure forest moet worden gevolgd.

### <a name="multiple-domains-in-one-forest"></a>Meerdere domeinen in een forest
Wanneer andere DC's van hetzelfde domein kunnen worden bereikt via het netwerk, kan de DC zoals een VM worden hersteld. In alle andere gevallen wordt een forestherstel echter aanbevolen.

## <a name="restoring-vms-with-special-network-configurations"></a>Herstellen van virtuele machines met speciale netwerkconfiguraties
Het is mogelijk back-up en herstellen van virtuele machines met de volgende speciale netwerkconfiguraties. Deze configuraties vereisen echter een aantal letten tijdens het doorlopen van het herstelproces.

* VM's onder de load balancer (intern en extern)
* Virtuele machines met meerdere gereserveerde IP 's
* Virtuele machines met meerdere NIC 's

> [!IMPORTANT]
> Bij het maken van de speciale configuratie voor virtuele machines, moet u PowerShell gebruiken voor het maken van virtuele machines van de schijven die zijn hersteld.
>
>

Als u volledig opnieuw de virtuele machines na het herstellen naar de schijf, wilt de volgende stappen uit:

1. De schijven herstellen vanuit een recovery services kluis met [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Maak de VM-configuratie vereist voor de load balancer-meerdere NIC/meerdere gereserveerde IP-adres met behulp van de PowerShell-cmdlets en het gebruik te maken van de virtuele machine van de gewenste configuratie.

   * Virtuele machine maken in een cloudservice met [interne Load balancer](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Verbinding maken met virtuele-machine maken [Internet gerichte load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Met virtuele machine maken [meerdere NIC's](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Met virtuele machine maken [meerdere gereserveerde IP-adressen](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Volgende stappen
Nu u uw virtuele machines kunt herstellen, gaat u naar artikel voor informatie over probleemoplossing voor veelvoorkomende problemen met virtuele machines. Controleer ook het artikel over het beheren van taken met uw virtuele machines.

* [Het oplossen van problemen](backup-azure-vms-troubleshoot.md#restore)
* [Virtuele machines beheren](backup-azure-manage-vms.md)
