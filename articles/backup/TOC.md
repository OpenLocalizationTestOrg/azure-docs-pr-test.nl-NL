
# Overzicht
## [Wat is Azure Backup?](backup-introduction-to-azure-backup.md)

# Aan de slag
## [Back-ups maken van Azure-VM's](backup-azure-vms-first-look-arm.md)
## [Back-ups maken van Windows Server of Windows-computers](backup-try-azure-backup-in-10-mins.md)
## [Back-ups maken van VMware-servers](backup-azure-backup-server-vmware.md)

# Procedures

## Azure Backup-server
### [Beveiligingsmatrix voor Azure Backup Server](backup-mabs-protection-matrix.md)
### Installeren of upgraden
#### [Azure Backup Server-workloads voorbereiden in Azure Portal](backup-azure-microsoft-azure-backup.md)
#### [Azure Backup Server-workloads voorbereiden in klassieke portal](backup-azure-microsoft-azure-backup-classic.md)
#### [Opslag tooAzure back-upserver toevoegen](backup-mabs-add-storage.md)
#### [Azure Backup-Server toov.2 upgraden](backup-mabs-upgrade-to-v2.md)
#### [Installatie zonder toezicht van Azure Backup Server](backup-mabs-unattended-install.md)
### Workloads beveiligen
#### [Azure Backup-Server tooback van een VMware-server gebruiken](backup-azure-backup-server-vmware.md)
#### [Azure Backup-Server tooback up Exchange gebruiken](backup-azure-exchange-mabs.md)
#### [Azure Backup-Server tooback van een SharePoint-farm gebruiken](backup-azure-backup-sharepoint-mabs.md)
#### [Tooback up SQL Azure Backup-Server gebruiken](backup-azure-sql-mabs.md)
#### [Systeemstatus beveiligen en bare metal recovery](backup-mabs-system-state-and-bmr.md)
### [Gegevens herstellen vanaf Azure Backup Server](backup-azure-alternate-dpm-server.md)

## Azure-VM's
### Hallo VM voorbereiden
#### [Virtuele machines geïmplementeerd met Resource Manager voorbereiden](backup-azure-arm-vms-prepare.md)
#### [Toepassingsconsistente back-ups van virtuele Linux-machines](backup-azure-linux-app-consistent.md)
#### [Virtuele Azure-machines voorbereiden](backup-azure-vms-prepare.md)
### Uw omgeving plannen
#### [VM-back-upinfrastructuur plannen](backup-azure-vms-introduction.md)
### Back-ups maken van virtuele machines
#### [Maak een back-up van virtuele machines in Azure tooa Recovery Services-kluis](backup-azure-arm-vms.md)
#### [Back-ups maken van versleutelde virtuele machines](backup-azure-vms-encryption.md)
#### [Back-ups maken van virtuele Azure-machines](backup-azure-vms.md)
### Virtuele machines beheren en controleren
#### [Back-ups van virtuele Azure-machines beheren in Azure Portal](backup-azure-manage-vms.md)
#### [Waarschuwingen voor virtuele Azure-machines controleren in Azure Portal](backup-azure-monitor-vms.md)
#### [Back-ups van virtuele Azure-machines beheren en controleren in klassieke portal](backup-azure-manage-vms-classic.md)
### Gegevens van virtuele machines herstellen
#### [Bestanden herstellen vanuit back-ups van virtuele Azure-machines](backup-azure-restore-files-from-vm.md)
#### [Virtuele machines die zijn geïmplementeerd met Resource Manager herstellen in Azure Portal](backup-azure-arm-restore-vms.md)
#### [Versleutelde virtuele machines terugzetten](backup-azure-vms-encryption.md)
#### [Virtuele machines herstellen in Azure](backup-azure-restore-vms.md)
#### [Key Vault-sleutel en -geheim voor versleutelde virtuele machines terugzetten](backup-azure-restore-key-secret.md)

## Azure Backup-rapporten configureren
### [Azure Backup-rapporten configureren](backup-azure-configure-reports.md)
### [Gegevensmodel voor Azure Backup-rapporten](backup-azure-reports-data-model.md)
### [Log Analytics-gegevensmodel voor Azure Backup](backup-azure-log-analytics-data-model.md)

## Data Protection Manager
### [DPM-workloads voorbereiden in Azure Portal](backup-azure-dpm-introduction.md)
### [DPM-workloads voorbereiden in klassieke portal](backup-azure-dpm-introduction-classic.md)
### [System Center DPM tooback Exchange-Server gebruiken](backup-azure-backup-exchange-server.md)
### [Gegevens tooan alternatieve DPM-server herstellen](backup-azure-alternate-dpm-server.md)
### [DPM tooback van de werkbelasting van de SQL Server gebruiken](backup-azure-backup-sql.md)
### [DPM tooback van een SharePoint-farm gebruiken](backup-azure-backup-sharepoint.md)

## PowerShell gebruiken
### [Virtuele Azure-machines in Azure Portal](backup-azure-vms-automation.md)
### [Virtuele Azure-machines in de klassieke portal](backup-azure-vms-classic-automation.md)
### [DPM in Azure Portal](backup-dpm-automation.md)
### [DPM in klassieke portal](backup-dpm-automation-classic.md)
### [Windows Server in Azure Portal](backup-client-automation.md)
### [Windows Server in klassieke portal](backup-client-automation-classic.md)

## Azure SQL Database
### [Langetermijnretentie van back-ups configureren](../sql-database/sql-database-configure-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Back-ups in een Recovery Services-kluis weergeven](../sql-database/sql-database-view-backups-in-vault.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Back-ups herstellen vanuit een langetermijnretentie](../sql-database/sql-database-restore-from-long-term-retention.md?toc=%2fazure%2fbackup%2ftoc.json)
### [Langetermijnback-ups van Azure SQL verwijderen](../sql-database/sql-database-long-term-retention-delete.md?toc=%2fazure%2fbackup%2ftoc.json)

## Windows Server
### [Back-ups maken van Windows Server-bestanden en -mappen](backup-configure-vault.md)
### [Back-ups maken van Windows Server-systeemstatus](backup-azure-system-state.md)
### [Bestanden terugzetten vanuit Azure tooWindows Server](backup-azure-restore-windows-server.md)
### [Windows Server-systeemstatus herstellen](backup-azure-restore-system-state.md)
### [Recovery Services-kluizen beheren en controleren](backup-azure-manage-windows-server.md)
### Back-up en herstellen met behulp van de klassieke portal Hallo
#### [Windows Server met het klassieke implementatiemodel Hallo](backup-configure-vault-classic.md)
#### [Backup-kluizen met het klassieke implementatiemodel Hallo beheren](backup-azure-manage-windows-server-classic.md)
#### [Herstellen van bestanden tooa Windows Server met het klassieke implementatiemodel Hallo](backup-azure-restore-windows-server-classic.md)

## Recovery Services-kluis
### [Overzicht van Recovery Services-kluizen](backup-azure-recovery-services-vault-overview.md)
### [Upgraden van een back-up kluis tooRecovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md)
### [Een Recovery Services-kluis verwijderen](backup-azure-delete-vault.md)

## Problemen oplossen
### [Problemen met back-ups van virtuele Azure-machines in Azure Portal](backup-azure-vms-troubleshoot.md)
### [Problemen met back-ups van virtuele Azure-machines in klassieke portal](backup-azure-vms-troubleshoot-classic.md)
### [Azure VM-back-up mislukt: kan niet communiceren met de Hallo VM-agent voor de status van de momentopname - momentopname VM sub-taak is een time-out](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md)
### [Langzame back-ups van bestanden en mappen in Azure Backup](backup-azure-troubleshoot-slow-backup-performance-issue.md)
### [Problemen oplossen met Azure Backup Server](backup-azure-mabs-troubleshoot.md)

# Concepten

## Veelgestelde vragen
### [Veelgestelde vragen over Recovery Services-kluis](backup-azure-backup-faq.md)
### [Veelgestelde vragen over Azure VM-back-ups](backup-azure-vm-backup-faq.md)
### [Veelgestelde vragen over het maken van back-ups van bestandsmappen met behulp van de Azure Backup-agent](backup-azure-file-folder-backup-faq.md)

## [Op rollen gebaseerd toegangsbeheer](backup-rbac-rs-vault.md)
## [Beveiliging voor hybride back-ups](backup-azure-security-feature.md)
## [Offline back-ups configureren](backup-azure-backup-import-export.md)
## [De tapewisselaar vervangen](backup-azure-backup-cloud-as-tape.md)


# Naslaginformatie
## [PowerShell](/powershell/module/azurerm.recoveryservices.backup)
## [.NET](/dotnet/api/microsoft.azure.management.recoveryservices.backup)

# Resources
## [Azure-roadmap](https://azure.microsoft.com/roadmap/)
## [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowsazureonlinebackup)
## [Prijzen](https://azure.microsoft.com/pricing/details/backup/)
## [Prijscalculator](https://azure.microsoft.com/pricing/calculator/)
## [Service-updates](https://azure.microsoft.com/updates/?product=backup)
## [Video's](https://azure.microsoft.com/documentation/videos/index/?services=backup)
