
1. In Hallo **hybride verbindingen** blade Hallo hybride verbinding die u zojuist hebt gemaakt, klik op **Listener Setup**.
   
    ![Klik op Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Hallo **hybride verbindingseigenschappen** blade wordt geopend. Onder **On-premises hybride Verbindingsbeheer**, kies **handmatig downloaden en configureren**Hallo gedownload HybridConnectionManager.msi pakket opslaan en kopieer Hallo gateway-verbindingsreeks.
   
    ![Klik hier tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Type Hallo volgende opdracht vanaf een beheerdersopdrachtprompt toostart Hallo installatieprogramma:
   
        start HybridConnectionManager.msi
4. Na het Hallo-installatieprogramma wordt uitgevoerd, klikt u op **niet nu**, bladert u toohello %ProgramFiles%\Microsoft\HybridConnectionManager map, HCMConfigWizard.exe uitvoeren en klik op **Ja** in Hallo **gebruiker Besturingselement account** dialoogvenster.
5. Plak de verbindingsreeks van het Hallo-hybride die u eerder hebt gekopieerd en klik op **OK**. 
   
    ![Installeren](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten**.
   
    ![Klik op sluiten](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    Op Hallo **hybride verbindingen** blade, Hallo **Status** kolom ziet u nu **verbonden**. 
   
    ![Status verbonden](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

