---
title: Back-up en herstel versleuteld VM's met Azure Backup
description: In dit artikel wordt gesproken over de back-up en herstel ervaring voor virtuele machines versleuteld met Azure Disk Encryption.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89492cda8eff23509bee7693bb5f7e6ab5eb10d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Het back-up en herstellen van versleuteld virtuele machines met Azure Backup
In dit artikel wordt gesproken over de stappen voor de back-up en herstel van virtuele machines met Azure Backup. Het bevat ook informatie over ondersteunde scenario's, vereisten en stappen voor probleemoplossing voor foutgevallen.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
> [!NOTE]
> * Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor Resource Manager geïmplementeerde virtuele machines. Dit wordt niet ondersteund voor klassieke virtuele machines. <br>
> * Voor Windows- en Linux virtuele machines met behulp van Azure Disk Encryption toe die gebruikmaakt van de branche standaard BitLocker-functie van Windows en DM-Crypt functie van Linux voor versleuteling van schijven wordt ondersteund. <br>
> * Dit wordt alleen ondersteund voor virtuele machines die zijn versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key. Dit wordt niet ondersteund voor virtuele machines die zijn versleuteld met BitLocker-versleutelingssleutel alleen. <br>
>
>

## <a name="prerequisites"></a>Vereisten
1. Virtuele machine is versleuteld met [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Deze moet worden versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key.
2. Recovery services-kluis is gemaakt en storage-replicatie is ingesteld met de stappen vermeld in het artikel [uw omgeving voorbereiden voor back-up](backup-azure-arm-vms-prepare.md).
3. Azure Backup heeft gekregen [machtigingen voor toegang tot de sleutelkluis](#provide-permissions-to-azure-backup) met sleutels, geheimen voor virtuele machines versleuteld.

## <a name="backup-encrypted-vm"></a>Back-up versleuteld VM
Gebruik de volgende stappen uit back-updoel instellen, beleid definiëren, artikelen en trigger back-up configureren.

### <a name="configure-backup"></a>Back-up configureren
1. Als u al een Recovery Services-kluis opent, kunt u doorgaan naar volgende stap. Als er nog geen Recovery Services-kluis is geopend, maar Azure Portal wordt weergeven, klikt u in het menu Hub op **Bladeren**.

   * Typ in de lijst met resources **Recovery Services**.
   * Als u begint te typen, wordt de lijst gefilterd op basis van uw invoer. Wanneer **Recovery Services-kluizen** wordt weergegeven, klikt u erop.

      ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     De lijst met Recovery Services-kluizen wordt weergegeven. Selecteer in de lijst met Recovery Services-kluizen een kluis.

     Het geselecteerde kluisdashboard wordt geopend.
2. In de lijst met items die onder de kluis wordt weergegeven, klikt u op **back-up** om de blade back-up te openen.

      ![Blade Back-up openen](./media/backup-azure-vms-encryption/select-backup.png)
3. Klik op de blade Back-up op **Back-updoel** om de blade Back-updoel openen.

      ![Blade Scenario openen](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Stel op de blade back-updoel **waar wordt uw workload uitgevoerd** naar Azure en **wat wilt u back-up maken** aan de virtuele machine, klik vervolgens op **OK**.

   De blade Back-updoel wordt gesloten en de blade Back-upbeleid wordt geopend.

   ![Blade Scenario openen](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Selecteer op de blade Back-upbeleid het back-upbeleid dat u wilt toepassen op de kluis en klik op **OK**.

      ![Back-upbeleid selecteren](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    De details van het standaardbeleid worden in de details weergegeven. Als u een beleid wilt maken, selecteert u **Nieuw maken** in de vervolgkeuzelijst. Nadat u op **OK** hebt geklikt, is het back-upbeleid gekoppeld aan de kluis.

    Kies vervolgens de VM's die u aan de kluis wilt koppelen.
6. Kies de versleutelde virtuele machines wilt koppelen aan het opgegeven beleid en klik op **OK**.

      ![Selecteer versleutelde virtuele machines](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Deze pagina bevat een bericht over sleutelkluis die is gekoppeld aan de versleutelde virtuele machines zijn geselecteerd. Backup-service vereist alleen-lezen toegang tot de sleutels en geheimen in de sleutelkluis. Deze machtigingen voor het back-sleutel en geheime, samen met de bijbehorende virtuele machines wordt gebruikt. **U moet machtigingen met Backup-service voor toegang tot de sleutelkluis voor back-ups werken geven**. U kunt opgeven dat deze machtigingen met [stappen die worden vermeld in de onderstaande sectie](#provide-permissions-to-azure-backup).

      ![Versleutelde VMs bericht](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Nu dat u hebt gedefinieerd op alle instellingen voor de kluis, in de blade back-up back-up inschakelen aan de onderkant van de pagina. Back-up wordt het beleid geïmplementeerd voor de kluis en de virtuele machines.
8. De volgende fase in de voorbereiding van de VM-Agent wordt geïnstalleerd of alleen voor zorgen dat de VM-Agent is geïnstalleerd. Dezelfde gebruikt u de stappen die zijn vermeld in het artikel [uw omgeving voorbereiden voor back-up](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Activering van de back-uptaak
Gebruik de stappen die zijn vermeld in het artikel [back-Azure-machines naar een recovery services-kluis](backup-azure-arm-vms.md) naar de back-uptaak trigger.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Back-ups van blijven al een back-up virtuele machines met versleuteling ingeschakeld  
Als u virtuele machines die al worden back-up in de recovery services-kluis en zijn ingeschakeld voor versleuteling op een later tijdstip, geeft u de machtigingen met Backup-service voor toegang tot de sleutelkluis voor back-ups om door te gaan. U kunt opgeven dat deze machtigingen met [stappen in de onderstaande sectie](#provide-permissions-to-azure-backup) of met behulp van PowerShell stappen vermeld in **back-up inschakelen** sectie van [PowerShell documentatie](backup-azure-vms-automation.md). 

## <a name="provide-permissions-to-azure-backup"></a>Machtigingen verlenen voor Azure Backup
Gebruik de volgende stappen uit om relevante machtigingen met Azure Backup voor toegangssleutel-kluis en back-up van versleutelde virtuele machines te bieden:
1. Selecteer **meer Services** en zoek naar **kluizen sleutel**.

    ![De sleutelkluis zoeken](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Selecteer in de lijst van sleutelkluizen, de sleutelkluis die zijn gekoppeld aan de versleutelde VM die worden back moet-up.

     ![Selecteer de sleutelkluis](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Klik op **toegangsbeleid** en vervolgens **nieuwe toevoegen**.

    ![-Beleid toevoegen](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Klik op **Selecteer principal** en het type **back-up-beheerservice** in de zoekbalk. 

    ![Back-service voor zoeken](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Selecteer **back-up-beheerservice** en klik op de knop selecteren.

    ![Selecteer de Backup-service](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Selecteer **Azure Backup** vervolgkeuzelijst in het configureren van de sjabloon. De vereiste machtigingen in de machtigingen van de sleutel wordt vooraf ingevuld en geheime machtigingen vervolgkeuzelijst. 

    ![Selecteer Azure back-up](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Klik op **OK**. U ziet dat back-up Management-Service op de blade toegangsbeleid opgehaald toegevoegd. 

    ![Beleid voor Backup-service toegang](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Klik op **Opslaan**. Hierdoor krijgt de vereiste machtigingen op Azure Backup.

    ![Beleid voor Backup-service toegang](./media/backup-azure-vms-encryption/save-access-policy.png)

Zodra de machtigingen zijn is opgegeven, kunt u doorgaan met het inschakelen van back-up voor versleutelde virtuele machines.

## <a name="restore-encrypted-vm"></a>Versleutelde VM herstellen
Voor het herstellen van versleutelde VM vermeld in sectie met behulp van eerste schijven herstellen stappen **terugzetten een back-up schijven** in [kiezen VM restore-configuratie](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Daarna kunt u een van de volgende opties:
* Gebruik de PowerShell-stappen die worden vermeld [een virtuele machine maken van herstelde schijven](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) volledige virtuele machine maken van herstelde schijven.
* OR [sjabloon gegenereerd als onderdeel van de schijven herstellen](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) voor het maken van virtuele machines van herstelde schijven. Sjablonen kunnen alleen worden gebruikt voor herstelpunten die zijn gemaakt na 26 April 2017.

## <a name="troubleshooting-errors"></a>Het oplossen van problemen
| Bewerking | Details van fouten | Oplossing |
| --- | --- | --- |
| Back-up |Validatie is mislukt, omdat virtuele machine is versleuteld met BEK alleen. Back-ups kunnen alleen worden ingeschakeld voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel. |Virtuele machine moet worden versleuteld met BEK en KEK-sleutel. Eerst ontsleutelen van de virtuele machine en versleutelen met behulp van zowel BEK en KEK-sleutel. Back-up inschakelen zodra de VM is versleuteld met behulp van zowel BEK en KEK-sleutel. Meer informatie over hoe u kunt [ontsleutelen en de virtuele machine versleutelen](../security/azure-security-disk-encryption.md)  |
| Herstellen |U kunt deze versleutelde virtuele machine niet herstellen omdat sleutelkluis die zijn gekoppeld aan deze virtuele machine niet bestaat. |Maakt met behulp van sleutelkluis [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md). Raadpleeg het artikel [sleutelkluis-sleutel en geheime met Azure Backup herstellen](backup-azure-restore-key-secret.md) voor het herstellen van sleutel en geheime als ze niet aanwezig zijn. |
| Herstellen |U kunt deze versleutelde virtuele machine niet herstellen omdat sleutel en het geheim die is gekoppeld aan deze virtuele machine niet bestaat. |Raadpleeg het artikel [sleutelkluis-sleutel en geheime met Azure Backup herstellen](backup-azure-restore-key-secret.md) voor het herstellen van sleutel en geheime als ze niet aanwezig zijn. |
| Herstellen |De Backup-service heeft geen toegang tot resources in uw abonnement. |Zoals eerder vermeld, schijven herstellen eerst met stappen die worden vermeld in de sectie **terugzetten een back-up schijven** in [kiezen VM restore-configuratie](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Na die, gebruiker PowerShell naar [een virtuele machine maken van herstelde schijven](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Back-up | Azure Backup-Service beschikt niet over voldoende machtigingen voor Sleutelkluis voor back-up van versleuteld Virtual Machines | Virtuele machine moeten worden versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key. Daarna wordt de back-up moet worden ingeschakeld.  Backup-service moet worden opgegeven met behulp van machtigingen [stappen die worden vermeld in de bovenstaande sectie](#provide-permissions-to-azure-backup) of met behulp van PowerShell-stappen die worden vermeld de **beveiliging inschakelen** sectie van de PowerShell documentatie bij [gebruik AzureRM.RecoveryServices.Backup-cmdlets voor back-up van virtuele machines](backup-azure-vms-automation.md#back-up-azure-vms). |  
