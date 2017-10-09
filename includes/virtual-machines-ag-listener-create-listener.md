In deze stap moet u handmatig Hallo beschikbaarheidsgroep-listener in Failoverclusterbeheer en SQL Server Management Studio maken.

1. Open Failoverclusterbeheer op Hallo-knooppunt dat als host fungeert voor de primaire replica Hallo.

2. Selecteer Hallo **netwerken** knooppunt en Opmerking Hallo clusternetwerknaam. Deze naam wordt gebruikt in de variabele Hallo $ClusterNetworkName in Hallo PowerShell-script.

3. Hallo clusternaam uitvouwen en klik vervolgens op **rollen**.

4. In Hallo **rollen** deelvenster, klik met de rechtermuisknop Hallo beschikbaarheidsgroep naam en selecteert u vervolgens **Resource toevoegen** > **Client Access Point**.
   
    ![Toevoegen van Client Access Point voor de beschikbaarheidsgroep](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. In Hallo **naam** vak, een naam op voor deze nieuwe listener te maken, klikt u op **volgende** tweemaal, en klik vervolgens op **voltooien**.  
    Worden niet weergegeven in Hallo listener of bron online op dit moment.

6. Klik op Hallo **Resources** tabblad uit en vouw vervolgens Hallo clienttoegangspunt u zojuist hebt gemaakt. 
    Hallo IP-adres resource voor elk clusternetwerk in het cluster wordt weergegeven. Als dit een Azure-only-oplossing, wordt slechts één IP-adres resource wordt weergegeven.

7. Hallo volgende doen:
   
   * een hybride oplossing tooconfigure:
     
        a. Hallo IP-adres resource die overeenkomt met tooyour lokale subnet met de rechtermuisknop en selecteer vervolgens **eigenschappen**. Houd er rekening mee naam Hallo IP-adres- en netwerknaambronnen.
   
        b. Selecteer **statisch IP-adres**, een niet-gebruikte IP-adres toewijzen en klik vervolgens op **OK**.
 
   * tooconfigure een Azure-only-oplossing:

        a. Met de rechtermuisknop op Hallo IP-adres resource die overeenkomt met tooyour Azure-subnet en selecteer vervolgens **eigenschappen**.
       
       > [!NOTE]
       > Als u online toocome listener hello later mislukt vanwege een conflicterende IP-adres geselecteerd door DHCP, kunt u een geldig statisch IP-adres configureren in dit eigenschappenvenster.
       > 
       > 

       b. Hallo in dezelfde **IP-adres** eigenschappenvenster, wijziging Hallo **naam IP-adres**.  
        Deze naam wordt gebruikt in de variabele Hallo $IPResourceName Hallo PowerShell-script. Als uw oplossing meerdere virtuele Azure-netwerken omvat, Herhaal deze stap voor elke IP-resource.

