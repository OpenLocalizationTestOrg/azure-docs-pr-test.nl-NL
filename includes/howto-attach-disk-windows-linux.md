


## <a name="attach-an-empty-disk"></a>Een lege schijf koppelen
Koppelen van een lege schijf is een eenvoudige manier tooadd een gegevens-schijf, omdat Azure Hallo .vhd-bestand voor u gemaakt en opgeslagen in Hallo storage-account.

1. Klik op **virtuele Machines (klassiek)**, en vervolgens selecteert Hallo juiste VM.

2. Klik in het menu instellingen Hallo op **schijven**.

   ![Een nieuwe lege schijf koppelen](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Klik op de opdrachtbalk Hallo **Attach nieuwe**.  
    Hallo **nieuwe schijf koppelen** dialoogvenster wordt weergegeven.

    ![Een nieuwe schijf koppelen](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Vul Hallo volgende informatie:
    - In **bestandsnaam**, accepteer de standaardnaam Hallo of typ een andere naam voor Hallo .vhd-bestand. Hallo gegevensschijf maakt gebruik van een automatisch gegenereerde naam, zelfs als u een andere naam voor de VHD-bestand Hallo typt.
    - Selecteer Hallo **Type** van Hallo gegevensschijf. Alle virtuele machines ondersteunen standaardschijven. Premium-schijven bieden ook ondersteuning voor veel virtuele machines.
    - Selecteer Hallo **grootte (GB)** van Hallo gegevensschijf.
    - Voor **Hostcaching**, kiest u geen of alleen-lezen.
    - Klik op OK toofinish.

4. Nadat de gegevensschijf Hallo is gemaakt en gekoppeld, wordt deze vermeld in Hallo schijven gedeelte Hallo VM.

   ![Nieuwe en lege gegevensschijf gekoppeld](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Nadat u een gegevensschijf toevoegt, kunt u toolog op toohello VM nodig en Hallo schijf initialiseren zodat deze kan worden gebruikt.

## <a name="how-to-attach-an-existing-disk"></a>Procedure: een bestaande schijf koppelen
Als u een bestaande schijf wilt koppelen, dient u een .vhd beschikbaar te hebben in een opslagaccount. Gebruik Hallo [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload Hallo .vhd-bestand toohello storage-account. Nadat u hebt gemaakt en Hallo .vhd-bestand wordt geüpload, kunt u deze tooa VM koppelen.

1. Klik op **virtuele Machines (klassiek)**, en vervolgens selecteert Hallo juiste virtuele machine.

2. Klik in het menu instellingen Hallo op **schijven**.

3. Klik op de opdrachtbalk Hallo **Attach bestaande**.

    ![Een gegevensschijf koppelen](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Klik op **locatie**. Hallo beschikbaar opslagaccounts weergegeven. Selecteer vervolgens een juiste storage-account in de lijst.

    ![Schijf storage-account opgeven](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. Een **opslagaccount** bevat een of meer containers die harde schijven (VHD's) bevatten. Selecteer de juiste container Hallo in de lijst.

    ![Container van virtuele machines-windows bieden](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Hallo **VHD's** deelvenster Hallo schijfstations ondergebracht in Hallo container bevat. Klik op een van de schijven Hallo en klik op selecteren.

    ![Schijfimage bieden voor virtuele machines-windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Hallo **bestaande schijf koppelen** Configuratiescherm opnieuw wordt weergegeven met Hallo-locatie met Hallo storage-account, de container en de geselecteerde harde schijf (vhd) tooadd toohello virtuele machine.

  Stel **Hostcaching** toonone of Read only, klik vervolgens op OK.

    ![Gegevensschijf gekoppeld](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
