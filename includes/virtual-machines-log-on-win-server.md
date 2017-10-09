1. Als u op **Verbinden** klikt, wordt een Remote Desktop Protocol-bestand (.rdp) gemaakt en gedownload. Klik op **Open** toouse dit bestand.
2. U ontvangt een waarschuwing dat .rdp Hallo van een onbekende uitgever is. Dit is normaal. Klik in het venster extern bureaublad Hallo op **Connect** toocontinue.
   
    ![Schermafbeelding met waarschuwing over een onbekende uitgever](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. In Hallo **Windows-beveiliging** venster Hallo referenties voor een account op Hallo virtuele machine en klik vervolgens op **OK**.
   
     **Lokaal account** -dit is meestal Hallo lokale account, gebruikersnaam en wachtwoord die u hebt opgegeven tijdens het maken van de virtuele machine Hallo. In dit geval Hallo domein Hallo-naam van Hallo virtuele machine en het is ingevoerd als *vmname*&#92; *gebruikersnaam*.  
   
    **Domein opgenomen VM** - als Hallo VM tooa domein behoort, gebruikersnaam Hallo Hallo indeling *domein*&#92; *Gebruikersnaam*. Hallo-account moet ook tooeither worden in de groep beheerders Hallo groep of externe toegang bevoegdheden toohello VM hebben gekregen.
   
    **Domeincontroller** - als Hallo VM een domeincontroller, het type Hallo-gebruikersnaam en het wachtwoord van een domeinbeheerdersaccount voor dat domein is.
4. Klik op **Ja** tooverify Hallo identiteit van Hallo virtuele machine en aanmelden te voltooien.
   
   ![Schermafbeelding met een bericht over het verifiëren van identiteit Hallo Hallo VM.](./media/virtual-machines-log-on-win-server/cert-warning.png)

