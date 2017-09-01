<!--author=alkohli last changed: 9/17/15-->

#### <a name="to-add-a-storage-account-in-storsimple-8000-series-update-10"></a>Een opslagaccount in StorSimple 8000 Series Update 1.0 toevoegen
1. Selecteer uw service op de landingspagina van de StorSimple Manager-service en dubbelklik erop. Hiermee gaat u naar de pagina **Quick Start**. Selecteer de pagina **Configureren**.
2. Klik op **Opslagaccount toevoegen/bewerken**.
3. Klik in het dialoogvenster **Opslagaccount toevoegen/bewerken** op **Nieuwe toevoegen**.
4. Selecteer in het veld **Provider** de juiste cloudserviceprovider. De ondersteunde providers zijn Azure, Amazon S3, Amazon S3 met RRS, HP en OpenStack. Geef de referenties en de locatie voor het opslagaccount van uw cloudserviceproviders op. Welke velden voor referenties worden weergegeven is afhankelijk van de cloudserviceprovider die u hebt opgegeven. 
   
   * Als u Azure hebt geselecteerd als uw cloudserviceprovider, geeft u de **naam** en de primaire **toegangssleutel** voor uw Microsoft Azure Storage-account op. Voor een Azure-account wordt de locatie automatisch ingevuld.
     
        ![Een Azure Storage-account toevoegen](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Als u Amazon S3 of Amazon S3 met RRS hebt geselecteerd, geeft u een beschrijvende **opslagaccountnaam**, **toegangssleutel** en **geheime sleutel** op. Voor Amazon S3 en Amazon S3 met RSS worden de volgende locaties ondersteund:
     
     * VS Standaard
     * VS West (Oregon)
     * VS West (Noord-Californië)
     * EU (Ierland)
     * Azië en Stille Oceaan (Singapore)
     * Azië en Stille Oceaan (Sydney)
     * Azië en Stille Oceaan (Tokio)
     * Zuid-Amerika (Sao Paulo)
       
       ![Amazon-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Als u HP als uw cloudserviceprovider hebt geselecteerd, geeft u een beschrijvende **opslagaccountnaam**, **tenant-id**, **gebruikersnaam** en **wachtwoord** op. Voor HP worden de volgende locaties ondersteund:
     
     * VS Oost
     * VS West
       
       ![HP-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Als u **Openstack** als uw cloudserviceprovider hebt geselecteerd, geeft u een **hostnaam**, **toegangssleutel** en **geheime sleutel** op.
     
     > [!NOTE]
     > Voor alle cloudserviceproviders, met uitzondering van Azure, is een beschrijvende naam toegestaan. U kunt verschillende beschrijvende namen gebruiken en meer dan een opslagaccount met dezelfde set referenties maken.
     > 
     > 
     
        ![Openstack-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Schakel **SSL-modus inschakelen** in om een beveiligd kanaal te maken voor de netwerkcommunicatie tussen uw apparaat en de cloud. Schakel het selectievakje **SSL-modus inschakelen** uit als u alleen binnen een privécloud werkt.
   
   > [!NOTE]
   > Als u HP als provider gebruikt, wordt SSL altijd ingeschakeld.
   > 
   > 
6. Klik op het vinkje ![vinkje](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). U ontvangt een melding nadat het opslagaccount is gemaakt.
7. Het nieuwe opslagaccount wordt weergegeven op de pagina **Configureren** onder **Opslagaccounts**. Klik op **Opslaan** om het nieuwe opslagaccount op te slaan. Klik op **OK** als u om bevestiging wordt gevraagd.

