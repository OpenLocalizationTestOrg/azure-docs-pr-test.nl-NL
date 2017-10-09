<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>een opslagaccount in StorSimple 8000 Series Update 1.0 tooadd
1. Selecteer uw service op de landingspagina Hallo StorSimple Manager-service, en dubbelklik erop. Hiermee gaat u toohello **Quick Start** pagina. Selecteer Hallo **configureren** pagina.
2. Klik op **Opslagaccount toevoegen/bewerken**.
3. In Hallo **Opslagaccount toevoegen/bewerken** in het dialoogvenster, klikt u op **nieuwe toevoegen**.
4. In Hallo **Provider** optie Hallo juiste cloudserviceprovider. Hallo ondersteunde providers zijn Azure, Amazon S3, Amazon S3 met RRS, HP en OpenStack. Geef Hallo referenties en het Hallo-locatie gekoppeld Hallo storage-account van uw cloudserviceproviders. Hallo-velden voor referenties aangeboden worden verschillende, al naar gelang Hallo cloudserviceprovider die u hebt opgegeven. 
   
   * Als u Azure als uw cloudserviceprovider hebt geselecteerd, geeft u Hallo **naam** en Hallo primaire **toegangssleutel** voor uw Microsoft Azure storage-account. Voor een Azure-account Hallo locatie automatisch ingevuld.
     
        ![Een Azure Storage-account toevoegen](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Als u Amazon S3 of Amazon S3 met RRS hebt geselecteerd, geeft u een beschrijvende **opslagaccountnaam**, **toegangssleutel** en **geheime sleutel** op. Voor Amazon S3 en Amazon S3 met RRS Hallo volgende locaties ondersteund:
     
     * VS Standaard
     * VS West (Oregon)
     * VS West (Noord-Californië)
     * EU (Ierland)
     * Azië en Stille Oceaan (Singapore)
     * Azië en Stille Oceaan (Sydney)
     * Azië en Stille Oceaan (Tokio)
     * Zuid-Amerika (Sao Paulo)
       
       ![Amazon-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Als u HP als uw cloudserviceprovider hebt geselecteerd, geeft u een beschrijvende **opslagaccountnaam**, **tenant-id**, **gebruikersnaam** en **wachtwoord** op. Voor HP worden de volgende locaties Hallo worden ondersteund:
     
     * VS Oost
     * VS West
       
       ![HP-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Als u **Openstack** als uw cloudserviceprovider hebt geselecteerd, geeft u een **hostnaam**, **toegangssleutel** en **geheime sleutel** op.
     
     > [!NOTE]
     > Voor alle Hallo cloudserviceproviders, met uitzondering van Azure, is een beschrijvende naam toegestaan. U kunt verschillende beschrijvende namen gebruiken en meer dan één storage-account maken met de Hallo dezelfde referenties set.
     > 
     > 
     
        ![Openstack-opslagaccount toevoegen](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Selecteer **SSL-modus inschakelen** toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw apparaat en het Hallo-cloud. Schakel Hallo **SSL-modus inschakelen** selectievakje alleen als u in een privécloud werkt.
   
   > [!NOTE]
   > Als u HP als provider gebruikt, wordt SSL altijd ingeschakeld.
   > 
   > 
6. Klik op het vinkje Hallo ![vinkje](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). U ontvangt een melding nadat Hallo storage-account is gemaakt.
7. Hallo nieuw gemaakte storage-account wordt weergegeven op Hallo **configureren** pagina onder **opslagaccounts**. Klik op **opslaan** toosave Hallo nieuw opslagaccount. Klik op **OK** als u om bevestiging wordt gevraagd.

