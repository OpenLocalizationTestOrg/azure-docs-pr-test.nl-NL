#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>openbare eindpunten op Hallo cloud toestel toocreate

1. Meld u aan toohello Azure-portal.
2. Ga te**virtuele Machines**, en selecteer en klik op Hallo virtuele machine die wordt gebruikt als uw toestel cloud.
    
3. Moet u een netwerk security group (NSG) regel toocontrol Hallo verkeersstroom toocreate in en uit de virtuele machine. Volgende stappen toocreate een regel voor het NSG Hallo uitvoeren.
    1. Selecteer **Netwerkbeveiligingsgroep**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Klik op Hallo standaard netwerkbeveiligingsgroep toevoegen wordt weergegeven.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Selecteer **Inkomende beveiligingsregels**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Klik op **+ toevoegen** toocreate een inkomende beveiligingsregel.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Binnenkomende beveiliging regel blade in Hallo toevoegen:

        1. Voor Hallo **naam**, type Hallo volgende naam voor het Hallo-eindpunt: WinRMHttps.
        
        2. Voor Hallo **prioriteit**, selecteer een getal kleiner zijn dan 1000 (dit is de prioriteit voor de standaardregel Hallo Hallo). Hogere Hallo waarde lagere Hallo prioriteit.

        3. Set Hallo **bron** te**eventuele**.

        4. Voor Hallo **Service**, selecteer **WinRM**. Hallo **Protocol** automatisch te ingesteld**TCP** en Hallo **poortbereik** te is ingesteld,**5986**.

        5. Klik op **OK** toocreate Hallo regel.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. De laatste stap is tooassociate groepeert u de netwerkbeveiliging van uw met een subnet of een specifieke netwerkinterface. Volgende stappen tooassociate Hallo uw netwerkbeveiligingsgroep aan een subnet uitvoeren.
    1. Ga te**subnetten**.
    2. Klik op **Koppelen**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Selecteer het virtuele netwerk en selecteer vervolgens de juiste subnet Hallo.
    4. Klik op **OK** toocreate Hallo regel.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Nadat het Hallo-regel is gemaakt, kunt u het adres details toodetermine Hallo openbare virtuele IP-adres (VIP) weergeven. Noteer dit adres.


