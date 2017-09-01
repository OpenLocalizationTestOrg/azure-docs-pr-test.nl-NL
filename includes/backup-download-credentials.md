## <a name="using-vault-credentials-to-authenticate-with-the-azure-backup-service"></a>Met behulp van referenties voor de kluis te verifiëren met de Azure Backup-service
De on-premises server (Windows-client of Windows Server of Data Protection Manager-server) moet worden geverifieerd met een back-upkluis voordat deze kan back-ups naar Azure. De verificatie wordt bereikt met 'vault referenties'. Het concept van kluisreferenties is vergelijkbaar met het concept van een 'publicatie-instellingen'-bestand dat wordt gebruikt in Azure PowerShell.

### <a name="what-is-the-vault-credential-file"></a>Wat is het kluisreferentiebestand?
Het kluisreferentiebestand is een certificaat dat de portal voor elke back-upkluis genereert. De portal uploadt de openbare sleutel vervolgens naar de Access Control Service (ACS). De persoonlijke sleutel van het certificaat wordt beschikbaar gesteld aan de gebruiker als onderdeel van de werkstroom die is opgegeven als invoer in de werkstroom van de registratie machine. Hiermee verifieert de machine voor het verzenden van back-upgegevens naar een geïdentificeerde kluis in de Azure Backup-service.

De kluisreferenties worden alleen gebruikt tijdens de registratiewerkstroom. Het is de verantwoordelijkheid van de gebruiker om ervoor te zorgen dat het kluisreferentiebestand niet worden gecompromitteerd. Als het kluisreferentiebestand in handen valt van een rogue-gebruiker, kan het bestand worden gebruikt om andere machines bij dezelfde kluis te registreren. Als de back-upgegevens worden versleuteld met een wachtwoordzin die deel uitmaakt van de klant, kan niet u bestaande back-upgegevens geschonden. Om dit probleem verhelpen, de kluisreferenties verlopen na 48hrs. U kunt de kluisreferenties van een back-upkluis downloaden vaak – maar alleen het meest recente kluisreferentiebestand is van toepassing tijdens de registratiewerkstroom.

### <a name="download-the-vault-credential-file"></a>Download het kluisreferentiebestand
Het kluisreferentiebestand is gedownload via een beveiligd kanaal vanuit de Azure-portal. De Azure Backup-service is niet op de hoogte van de persoonlijke sleutel van het certificaat en de persoonlijke sleutel is niet permanent in de portal of de service. Gebruik de volgende stappen voor het downloaden van het kluisreferentiebestand naar een lokale computer.

1. Aanmelden bij de [-beheerportal](https://manage.windowsazure.com/)
2. Klik op **Recovery Services** in het navigatiedeelvenster links en selecteer de back-upkluis die u hebt gemaakt. Klik op het pictogram cloud naar de weergave snel starten van de back-upkluis.
   
   ![Snel weergeven](./media/backup-download-credentials/quickview.png)
3. Klik op de pagina Quick Start op **kluisreferenties downloaden**. De portal genereert het kluisreferentiebestand wordt beschikbaar gesteld voor downloaden.
   
   ![Downloaden](./media/backup-download-credentials/downloadvc.png)
4. De portal genereert een kluisreferentie met een combinatie van de kluisnaam van de en de huidige datum. Klik op **opslaan** de kluisreferenties downloaden naar de map downloads van het lokale account in of selecteer OpslaanAls in het menu opslaan naar een locatie opgeven voor de kluisreferenties.

### <a name="note"></a>Opmerking
* Zorg ervoor dat de referenties voor de kluis wordt opgeslagen op een locatie die toegankelijk is vanaf uw computer. Als deze is opgeslagen in een bestand share/SMB, controleert de toegangsmachtigingen.
* Het kluisreferentiebestand wordt alleen gebruikt tijdens de registratiewerkstroom.
* Het kluisreferentiebestand na 48hrs verlopen en kan worden gedownload vanuit de portal.
* Raadpleeg de Azure Backup [Veelgestelde vragen over](../articles/backup/backup-azure-backup-faq.md) voor vragen over de werkstroom.

