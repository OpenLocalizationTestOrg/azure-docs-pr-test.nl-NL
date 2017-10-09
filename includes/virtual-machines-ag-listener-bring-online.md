1. Vouw in Failoverclusterbeheer **rollen**, en selecteer vervolgens de beschikbaarheidsgroep.  

2. Op Hallo **Resources** tabblad en klik vervolgens op met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello **eigenschappen**.

3. Klik op Hallo **afhankelijkheden** tabblad. Controleer of Hallo IP-adressen hebt of niet als meerdere resources worden weergegeven, en afhankelijkheden.  

4. Klik op **OK**.

5. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **Online brengen**.

6. Na het Hallo-listener is online op Hallo **Resources** tabblad en klik vervolgens op met de rechtermuisknop op het Hallo-beschikbaarheidsgroep **eigenschappen**.
   
    ![Hallo beschikbaarheidsgroepresource configureren](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Maken van een afhankelijkheid Hallo listener bron (niet Hallo IP-adres resources naam) en klik vervolgens op **OK**.
   
    ![Afhankelijkheid van de naam van de listener Hallo toevoegen](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Start SQL Server Management Studio en maak verbinding toohello primaire replica.

9. Ga te**AlwaysOn hoge beschikbaarheid** > **beschikbaarheidsgroepen** > **\<AvailabilityGroupName\>**   >  **Beschikbaarheidsgroep-Listeners**.  
    Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer moet worden weergegeven.

10. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **eigenschappen**.

11. In Hallo **poort** Geef Hallo-poortnummer voor Hallo beschikbaarheidsgroep-listener met behulp van Hallo $EndpointPort die u eerder hebt gebruikt (in deze zelfstudie is 1433 Hallo standaard), en klik vervolgens op **OK**.

