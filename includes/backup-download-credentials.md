## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Met behulp van de kluis referenties tooauthenticate Hello Azure Backup-service
Hallo lokale server (Windows-client of Windows Server of Data Protection Manager-server) moet toobe geverifieerd met een back-upkluis voordat de back-up tooAzure gegevens kunt maken. Hallo-verificatie wordt bereikt met 'vault referenties'. Hallo-concept van kluisreferenties is vergelijkbaar toohello concept van een 'publicatie-instellingen'-bestand dat wordt gebruikt in Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>Wat is het kluisreferentiebestand Hallo?
Hallo kluisreferentiebestand is een certificaat dat is gegenereerd door Hallo-portal voor elke back-upkluis. Hallo portal geüpload en Hallo openbare sleutel toohello Access Control Service (ACS). persoonlijke sleutel van certificaat Hallo Hallo wordt beschikbaar toohello gebruiker als onderdeel van het Hallo-werkstroom die is opgegeven als invoer in Hallo machine registratiewerkstroom gemaakt. Hiermee wordt geverifieerd Hallo machine toosend back-upgegevens tooan geïdentificeerd kluis in hello Azure Backup-service.

Hallo kluisreferentie wordt alleen gebruikt tijdens de registratiewerkstroom Hallo. Het is van de gebruiker Hallo verantwoordelijkheid tooensure die Hallo kluisreferenties bestand niet is geknoeid. Als het kluisreferentiebestand in handen Hallo van een rogue-gebruiker, Hallo kluisreferentiebestand kan worden gebruikt tooregister andere machines bij dezelfde kluis Hallo. Als de back-upgegevens Hallo is versleuteld met een wachtwoordzin die deel uitmaakt van de klant toohello, kan niet u bestaande back-upgegevens geschonden. toomitigate dit te voorkomen, de kluisreferenties tooexpire in 48hrs. U kunt Hallo kluisreferenties van een back-upkluis downloaden vaak – maar alleen Hallo nieuwste kluisreferentiebestand is van toepassing tijdens de registratiewerkstroom Hallo.

### <a name="download-hello-vault-credential-file"></a>Download het kluisreferentiebestand Hallo
Hallo kluisreferentiebestand is gedownload via een beveiligd kanaal van hello Azure-portal. Hello Azure Backup-service is niet op de hoogte van de persoonlijke sleutel van certificaat Hallo Hallo en Hallo persoonlijke sleutel is niet permanent in het Hallo-portal of Hallo-service. Gebruik hello te volgen stappen toodownload Hallo kluis referentie bestand tooa lokale computer.

1. Meld u aan toohello [-beheerportal](https://manage.windowsazure.com/)
2. Klik op **Recovery Services** in het linkernavigatievenster Hallo en selecteer Hallo back-upkluis die u hebt gemaakt. Klik op Hallo cloud pictogram tooget toohello weergave van de back-upkluis Hallo snel starten.
   
   ![Snel weergeven](./media/backup-download-credentials/quickview.png)
3. Klik op de pagina snel starten Hallo **kluisreferenties downloaden**. Hallo portal genereert Hallo kluisreferentiebestand, die beschikbaar is gemaakt voor downloaden.
   
   ![Downloaden](./media/backup-download-credentials/downloadvc.png)
4. Hallo portal genereert een kluisreferentie met behulp van een combinatie van Hallo kluisnaam en Hallo huidige datum. Klik op **opslaan** toodownload Hallo kluis referenties toohello lokale account van de map downloads of selecteer OpslaanAls een van de Hallo Sla menu toospecify een locatie voor de kluisreferenties Hallo.

### <a name="note"></a>Opmerking
* Zorg ervoor dat de kluisreferenties hello wordt opgeslagen op een locatie die toegankelijk is vanaf uw computer. Als deze is opgeslagen in een bestand share/SMB, controleert u de toegangsmachtigingen Hallo.
* Hallo kluisreferentiebestand wordt alleen gebruikt tijdens de registratiewerkstroom Hallo.
* Hallo kluisreferentiebestand na 48hrs verlopen en kan worden gedownload vanaf het Hallo-portal.
* Raadpleeg toohello Azure Backup [Veelgestelde vragen over](../articles/backup/backup-azure-backup-faq.md) voor vragen over de Hallo-werkstroom.

