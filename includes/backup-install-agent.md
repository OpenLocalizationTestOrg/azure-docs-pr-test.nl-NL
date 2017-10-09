## <a name="download-install-and-register-hello-azure-backup-agent"></a>Downloaden, installeren en registreren hello Azure backup-agent
Nadat hello Azure Backup-kluis is gemaakt, moet een agent worden geïnstalleerd op elk van uw Windows-machines (Windows Server, Windows-client, System Center Data Protection Manager-server of Azure Backup-Server-machine) waarmee een back-up van gegevens en toepassingen tooAzure.

1. Meld u aan toohello [-beheerportal](https://manage.windowsazure.com/)
2. Klik op **Recovery Services**, selecteer daarna Hallo back-upkluis die u tooregister met een server wilt. Hallo pagina snel starten voor deze back-upkluis wordt weergegeven.
   
    ![Snel starten](./media/backup-install-agent/quickstart.png)
3. Klik op de pagina snel starten Hallo Hallo **voor Windows Server, System Center Data Protection Manager of Windows client** onder de optie **Agent downloaden**. Klik op **opslaan** toocopy het toohello lokale computer.
   
    ![Opslaan van agent](./media/backup-install-agent/agent.png)
4. Zodra het Hallo-agent is geïnstalleerd, dubbelklikt u op MARSAgentInstaller.exe toolaunch Hallo installatie van hello Azure Backup agent. Hallo-installatiemap en de tijdelijke map is vereist voor de agent Hallo kiezen. Hallo cachelocatie opgegeven moet vrije ruimte die ten minste 5% van de back-upgegevens Hallo hebben.
5. Als u een proxy server tooconnect toohello internet in Hallo **proxyconfiguratie** scherm, Voer Hallo proxy server-gegevens. Als u een geverifieerde proxyserver gebruikt, voert u Hallo naam en het wachtwoord gebruikersgegevens in dit scherm.
6. Hello Azure backup-agent installeert u .NET Framework 4.5 en Windows PowerShell (indien deze nog niet beschikbaar is) toocomplete Hallo installatie.
7. Zodra het Hallo-agent is geïnstalleerd, klikt u op Hallo **tooRegistration gaan** knop toocontinue met Hallo workflow.
   
   ![Registreren](./media/backup-install-agent/register.png)
8. Blader in welkomstscherm kluis referenties, tooand Selecteer Hallo kluisreferentiebestand die eerder zijn gedownload.
   
    ![Referenties voor de kluis](./media/backup-install-agent/vc.png)
   
    Hallo kluisreferentiebestand is alleen geldig voor 48 uur (nadat deze gedownload vanuit de portal Hallo). Als er een fout in dit scherm (bijvoorbeeld ' kluis bestand opgegeven referenties is verlopen') optreden, aanmelding toohello Azure-portal en download Hallo kluisreferenties-bestand opnieuw.
   
    Zorg ervoor dat Hallo kluisreferentiebestand is beschikbaar in een locatie die toegankelijk zijn voor het Hallo-installatieprogramma. Als u toegang tot gerelateerde fouten Hallo kluis referenties tooa tijdelijke bestandslocatie op deze machine te kopiëren en probeer Hallo opnieuw.
   
    Als u een ongeldige kluis referentie foutbericht (bijvoorbeeld ' Ongeldige kluisreferenties opgegeven') krijgt Hallo-bestand is beschadigd of komt niet hebben Hallo meest recente referenties zijn gekoppeld aan de herstelservice Hallo. Probeer opnieuw na het downloaden van een nieuw kluisreferentiebestand via de portal Hallo Hallo. Deze fout wordt doorgaans te zien of gebruiker op Hallo Hallo **kluisreferentie downloaden** optie in hello Azure-portal, snel achter elkaar. In dit geval wordt is alleen Hallo tweede kluisreferentiebestand geldig.
9. In Hallo **versleutelingsinstelling** scherm kunt u een wachtwoordzin genereren of geef een wachtwoordzin (minimaal 16 tekens). Houd er rekening mee toosave Hallo wachtwoordzin op een veilige locatie.
   
    ![Versleuteling](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Als hello wachtwoordzin kwijtraakt of vergeet; Microsoft kan niet helpen bij het herstellen van back-upgegevens Hallo. Hallo gebruiker eigenaar is van Hallo-wachtwoordzin voor versleuteling en Microsoft heeft geen zichtbaarheid van Hallo wachtwoordzin die wordt gebruikt door de eindgebruiker Hallo. Sla Hallo-bestand op een veilige locatie als dit nodig tijdens een herstelbewerking wordt uitgevoerd is.
   > 
   > 
10. Nadat u op Hallo **voltooien** knop, hello computer wordt geregistreerd met succes toohello kluis en u bent nu klaar toostart back-ups van tooMicrosoft Azure.
11. Wanneer u zelfstandige Microsoft Azure Backup kunt u Hallo-instellingen die zijn opgegeven tijdens de registratiewerkstroom Hallo door te klikken op Hallo **eigenschappen wijzigen** optie in hello Azure Backup mmc-modules in.
    
    ![Eigenschappen wijzigen](./media/backup-install-agent/change.png)
    
    Als u Data Protection Manager, kunt u ook Hallo-instellingen die zijn opgegeven tijdens de registratiewerkstroom Hallo door te klikken op Hallo wijzigen **configureren** optie door te selecteren **Online** onder Hallo **Management** tabblad.
    
    ![Azure Backup configureren](./media/backup-install-agent/configure.png)

