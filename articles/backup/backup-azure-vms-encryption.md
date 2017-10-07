---
title: aaaBackup en herstel de VM's met Azure Backup versleuteld
description: In dit artikel wordt gesproken over Hallo back-up en herstel ervaring voor virtuele machines versleuteld met Azure Disk Encryption.
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
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Hoe tooback up en herstel virtuele machines met Azure Backup versleuteld
In dit artikel wordt gesproken over stappen toobackup en terugzetten van virtuele machines maken met Azure Backup. Het bevat ook informatie over ondersteunde scenario's, vereisten en stappen voor probleemoplossing voor foutgevallen.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
> [!NOTE]
> * Back-up en herstel van versleutelde virtuele machines wordt alleen ondersteund voor Resource Manager geïmplementeerde virtuele machines. Dit wordt niet ondersteund voor klassieke virtuele machines. <br>
> * Voor Windows- en Linux virtuele machines met behulp van Azure Disk Encryption toe die gebruikmaakt van Hallo bedrijfstak standaard BitLocker-functies van Windows en DM-Crypt Linux tooprovide versleuteling van schijven wordt ondersteund. <br>
> * Dit wordt alleen ondersteund voor virtuele machines die zijn versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key. Dit wordt niet ondersteund voor virtuele machines die zijn versleuteld met BitLocker-versleutelingssleutel alleen. <br>
>
>

## <a name="prerequisites"></a>Vereisten
1. Virtuele machine is versleuteld met [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Deze moet worden versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key.
2. Recovery services-kluis is gemaakt en storage-replicatie is ingesteld met de stappen beschreven in artikel Hallo [uw omgeving voorbereiden voor back-up](backup-azure-arm-vms-prepare.md).
3. Azure Backup heeft gekregen [machtigingen tooaccess sleutelkluis](#provide-permissions-to-azure-backup) met sleutels, geheimen voor virtuele machines versleuteld.

## <a name="backup-encrypted-vm"></a>Back-up versleuteld VM
Volgende stappen tooset back-updoel hello gebruiken, beleid definiëren, het configureren van items en -trigger back-up.

### <a name="configure-backup"></a>Back-up configureren
1. Als u al een Recovery Services-kluis openen, gaat u verder toonext stap. Als u geen een Recovery Services-kluis is geopend hebt, maar in hello Azure-portal op Hallo Hub-menu zijn, klikt u op **Bladeren**.

   * Typ in de lijst met resources Hallo **Recovery Services**.
   * Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Wanneer **Recovery Services-kluizen** wordt weergegeven, klikt u erop.

      ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     Hallo-lijst met Recovery Services-kluizen wordt weergegeven. Selecteer in Hallo lijst met Recovery Services-kluizen een kluis.

     Hallo geselecteerde kluisdashboard wordt geopend.
2. Uit Hallo lijst met items die onder de kluis wordt weergegeven, klikt u op **back-up** blade tooopen Hallo-back-up.

      ![Blade Back-up openen](./media/backup-azure-vms-encryption/select-backup.png)
3. Klik op de blade back-Hallo **back-updoel** tooopen Hallo back-updoel blade.

      ![Blade Scenario openen](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Stel op de blade back-updoel hello, **waar wordt uw workload uitgevoerd** tooAzure en **wat wilt u wilt toobackup** tooVirtual machine en klik vervolgens op **OK**.

   blade Hallo-back-updoel wordt gesloten en blade Hallo back-upbeleid wordt geopend.

   ![Blade Scenario openen](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Selecteer op de blade van Hallo back-up Hallo back-upbeleid tooapply toohello kluis en klik op **OK**.

      ![Back-upbeleid selecteren](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    Hallo-details van het standaardbeleid Hallo worden vermeld in Hallo details. Als u wilt dat een beleid toocreate, selecteert u **nieuw** uit de vervolgkeuzelijst Hallo. Nadat u op **OK**, back-upbeleid Hallo is gekoppeld aan het Hallo-kluis.

    Kies vervolgens Hallo VMs tooassociate met Hallo kluis.
6. Kies Hallo versleuteld virtuele machines tooassociate Hello opgegeven beleid en klik op **OK**.

      ![Selecteer versleutelde virtuele machines](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Deze pagina bevat een bericht over sleutelkluis die gekoppeld toohello versleuteld virtuele machines is geselecteerd. Backup-service is alleen-lezentoegang toohello sleutels en geheimen in de sleutelkluis Hallo vereist. Deze machtigingen toobackup sleutel wordt gebruikt en geheim, samen met de Hallo bijbehorende virtuele machines. **U moet machtigingen toobackup service tooaccess sleutelkluis voor back-ups toowork geeft**. U kunt opgeven dat deze machtigingen met [stappen die worden vermeld in de onderstaande sectie voor Hallo](#provide-permissions-to-azure-backup).

      ![Versleutelde VMs bericht](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Nu dat u hebt gedefinieerd op alle instellingen voor Hallo kluis, in de blade back-up Hallo back-up inschakelen Hallo Hallo pagina onderaan in. Schakel back-up Hallo beleid toohello kluis en Hallo VM's geïmplementeerd.
8. Hallo volgende fase in voorbereiding installeert Hallo VM-Agent of waardoor ervoor Hallo VM-Agent is geïnstalleerd. toodo Hallo dezelfde, gebruik Hallo stappen vermeld in artikel Hallo [uw omgeving voorbereiden voor back-up](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Activering van de back-uptaak
Gebruik Hallo stappen vermeld in artikel Hallo [back-up Azure Virtual machines toorecovery services-kluis](backup-azure-arm-vms.md) tootrigger back-uptaak.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Back-ups van blijven al een back-up virtuele machines met versleuteling ingeschakeld  
Als u virtuele machines die al worden back-up in de recovery services-kluis en zijn ingeschakeld voor versleuteling op een later tijdstip, moet u machtigingen toobackup service tooaccess sleutelkluis voor back-ups toocontinue geven. Kunt u deze met behulp van machtigingen bieden [stappen in onderstaande sectie voor Hallo](#provide-permissions-to-azure-backup) of met behulp van PowerShell stappen vermeld in **back-up inschakelen** sectie van [PowerShell documentatie](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Machtigingen tooAzure back-up bieden
Volgende stappen tooprovide relevante machtigingen tooAzure back-up tooaccess sleutelkluis hello gebruiken en back-up van versleutelde virtuele machines:
1. Selecteer **meer Services** en zoek naar **kluizen sleutel**.

    ![De sleutelkluis zoeken](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Hallo-lijst van sleutelkluizen, selecteer Hallo sleutelkluis die zijn gekoppeld aan de versleutelde VM die toobe back moet-up gemaakt.

     ![Selecteer de sleutelkluis](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Klik op **toegangsbeleid** en vervolgens **nieuwe toevoegen**.

    ![-Beleid toevoegen](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Klik op **Selecteer principal** en het type **back-up-beheerservice** in de zoekbalk Hallo. 

    ![Back-service voor zoeken](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Selecteer **back-up-beheerservice** en klik op de knop selecteren.

    ![Selecteer de Backup-service](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Selecteer **Azure Backup** vervolgkeuzelijst in het configureren van de sjabloon. Vooraf wordt ingevuld Hallo vereist machtigingen in de machtigingen van de sleutel en geheime machtigingen vervolgkeuzelijst. 

    ![Selecteer Azure back-up](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Klik op **OK**. U ziet dat back-up Management-Service op de blade toegangsbeleid opgehaald toegevoegd. 

    ![Beleid voor Backup-service toegang](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Klik op **Opslaan**. Hierdoor krijgt Hallo vereist machtigingen tooAzure back-up.

    ![Beleid voor Backup-service toegang](./media/backup-azure-vms-encryption/save-access-policy.png)

Zodra de machtigingen zijn is opgegeven, kunt u doorgaan met het inschakelen van back-up voor versleutelde virtuele machines.

## <a name="restore-encrypted-vm"></a>Versleutelde VM herstellen
toorestore VM versleuteld, met behulp van eerste schijven herstellen stappen vermeld in sectie **terugzetten een back-up schijven** in [kiezen VM restore-configuratie](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Daarna kunt u een Hallo volgende opties:
* Gebruik Hallo PowerShell stappen vermeld in [een virtuele machine maken van herstelde schijven](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate volledige VM van herstelde schijven.
* OR [sjabloon gegenereerd als onderdeel van de schijven herstellen](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate VM's van herstelde schijven. Sjablonen kunnen alleen worden gebruikt voor herstelpunten die zijn gemaakt na 26 April 2017.

## <a name="troubleshooting-errors"></a>Het oplossen van problemen
| Bewerking | Details van fouten | Oplossing |
| --- | --- | --- |
| Back-up |Validatie is mislukt, omdat virtuele machine is versleuteld met BEK alleen. Back-ups kunnen alleen worden ingeschakeld voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel. |Virtuele machine moet worden versleuteld met BEK en KEK-sleutel. Eerst ontsleutelen Hallo VM en versleutelen met behulp van zowel BEK en KEK-sleutel. Back-up inschakelen zodra de VM is versleuteld met behulp van zowel BEK en KEK-sleutel. Meer informatie over hoe u kunt [ontsleutelen en te coderen Hallo VM](../security/azure-security-disk-encryption.md)  |
| Herstellen |U kunt deze versleutelde virtuele machine niet herstellen omdat sleutelkluis die zijn gekoppeld aan deze virtuele machine niet bestaat. |Maakt met behulp van sleutelkluis [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md). Raadpleeg Hallo artikel [sleutelkluis-sleutel en geheime met Azure Backup herstellen](backup-azure-restore-key-secret.md) toorestore sleutel en geheime als ze zijn niet aanwezig. |
| Herstellen |U kunt deze versleutelde virtuele machine niet herstellen omdat sleutel en het geheim die is gekoppeld aan deze virtuele machine niet bestaat. |Raadpleeg Hallo artikel [sleutelkluis-sleutel en geheime met Azure Backup herstellen](backup-azure-restore-key-secret.md) toorestore sleutel en geheime als ze zijn niet aanwezig. |
| Herstellen |Backup-Service heeft geen autorisatie tooaccess resources in uw abonnement. |Zoals eerder vermeld, schijven herstellen eerst met stappen die worden vermeld in de sectie **terugzetten een back-up schijven** in [kiezen VM restore-configuratie](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Na die, gebruiker PowerShell te[een virtuele machine maken van herstelde schijven](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Back-up | Azure Backup-Service heeft geen voldoende machtigingen tooKey kluis voor back-up van versleuteld Virtual Machines | Virtuele machine moeten worden versleuteld met BitLocker-versleutelingssleutel en coderingssleutel Key. Daarna wordt de back-up moet worden ingeschakeld.  Backup-service moet worden opgegeven met behulp van machtigingen [stappen die worden vermeld bij Hallo hierboven](#provide-permissions-to-azure-backup) of met behulp van PowerShell-stappen die worden vermeld in Hallo **beveiliging inschakelen** sectie Hallo PowerShell documentatie bij [gebruik AzureRM.RecoveryServices.Backup cmdlets tooback van virtuele machines](backup-azure-vms-automation.md#back-up-azure-vms). |  
