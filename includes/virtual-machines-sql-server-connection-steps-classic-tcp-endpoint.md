### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Een TCP-eindpunt voor Hallo virtuele machine maken
In de volgorde tooaccess SQL Server uit Hallo internet, Hallo virtuele machine moet beschikken over een toolisten eindpunt voor binnenkomende TCP-communicatie. Deze stap configuratie van Azure zorgt ervoor dat de binnenkomende TCP-poort verkeer tooa TCP-poort die is toegankelijk toohello virtuele machine.

> [!NOTE]
> Als u verbinding maakt binnen Hallo dezelfde cloud service- of virtuele netwerk, u hoeft geen toocreate een openbaar toegankelijk eindpunt. U kunt de volgende stap toohello in dat geval kan doorgaan. Zie [Verbindingsscenario's](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios) voor meer informatie.
> 
> 

1. Selecteer op Hallo Azure Portal, **virtuele machines (klassiek)**.
2. Selecteer vervolgens uw virtuele machine voor SQL Server.
3. Selecteer **eindpunten**, en klik vervolgens op Hallo **toevoegen** knop Hallo boven aan het Hallo-eindpunten blade.
   
    ![Stappen in Azure Portal voor het maken van een eindpunt](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Op Hallo **eindpunt toevoegen** blade bieden een **naam** zoals SQLEndpoint.
5. Selecteer **TCP** voor Hallo **Protocol**.
6. Voor **Openbare poort** geeft u een poortnummer op, zoals **57500**.
7. Voor **particuliere poort**, geef de luisterende poorten van de SQL Server, die een te standaardwaarde**1433**.
8. Klik op **Ok** toocreate Hallo-eindpunt.

