Als uw virtuele machine (VM) in Azure een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf. Een veelvoorkomend voorbeeld is het bijwerken van een mislukte toepassing dat verhindert dat Hallo VM is opgestart. Dit artikel wordt beschreven hoe toouse Azure portal tooconnect uw virtuele harde schijf tooanother VM toofix eventuele fouten en uw oorspronkelijke VM opnieuw maken.

## <a name="recovery-process-overview"></a>Overzicht van het herstelproces
Hallo procedure voor probleemoplossing is als volgt:

1. Verwijderen van Hallo VM die problemen ondervindt, maar Hallo virtuele harde schijven te behouden.
2. Koppelen en Hallo virtuele harde schijf tooanother VM koppelen voor het oplossen van problemen.
3. Verbinding maken met toohello VM probleemoplossing. Bestanden bewerken of toofix fouten van hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.
4. Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.
5. Een virtuele machine maken met behulp van Hallo oorspronkelijke virtuele harde schijf.

## <a name="delete-hello-original-vm"></a>Verwijder Hallo oorspronkelijke VM
Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure. Een virtuele harde schijf is waar Hallo-besturingssysteem, toepassingen en configuraties worden opgeslagen. Hallo VM zijn gewoon metagegevens die definieert Hallo grootte of de locatie en dat verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC). Elke virtuele harde schijf een lease toegewezen wanneer die schijf gekoppelde tooa VM opgehaald. Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd. Hallo lease blijft tooassociate Hallo OS schijf tooa VM, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.

eerste stap toorecovering Hallo uw VM is toodelete Hallo VM-resource zelf. Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount. Na Hallo die virtuele machine is verwijderd, kunt u Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen. 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com). 
2. Klik op het menu aan de linkerkant Hallo Hallo **virtuele Machines (klassiek)**.
3. Selecteer Hallo VM waarop Hallo probleem optreedt, klikt u op **schijven**, en controleert u de naam van de virtuele harde schijf Hallo Hallo. 
4. Selecteer Hallo OS virtuele hardeschijf en controleer Hallo **locatie** tooidentify Hallo storage-account met deze virtuele harde schijf. In Hallo voorbeeld te volgen, direct voor tekenreeks Hallo ". blob.core.windows.net ' hello opslagaccountnaam is.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![Hallo-installatiekopie over de locatie van de virtuele machine](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Met de rechtermuisknop op Hallo VM en selecteer vervolgens **verwijderen**. Zorg ervoor dat Hallo schijven zijn niet ingeschakeld wanneer u Hallo VM verwijdert.
6. Maak een nieuwe VM voor herstel. Deze virtuele machine moet Hallo dezelfde regio en resource groep (Cloudservice) als Hallo probleem VM.
7. Selecteer Hallo herstel-VM en selecteer vervolgens **schijven** > **bestaande koppelen**.
8. tooselect uw bestaande virtuele harde schijf klikt u op **VHD-bestand**:

    ![Zoeken naar bestaande VHD](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Selecteer Hallo opslagaccount > VHD-container > Hallo van virtuele harde schijf, klikt u op Hallo **Selecteer** knop tooconfirm uw keuze.

    ![Uw bestaande VHD selecteren](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Met de VHD die is geselecteerd, selecteer **OK** tooattach Hallo bestaande virtuele harde schijf.
11. Na enkele seconden Hallo **schijven** deelvenster voor uw virtuele machine, ziet u de bestaande virtuele harde schijf als een gegevensschijf verbonden:

    ![Bestaande virtuele harde schijf gekoppeld als een gegevensschijf](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Los problemen op Hallo oorspronkelijke virtuele harde schijf
Wanneer Hallo bestaande virtuele harde schijf is gekoppeld, kunt u nu een onderhoud en stappen voor probleemoplossing naar behoefte uitvoeren. Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Ontkoppel en loskoppelen Hallo oorspronkelijke virtuele harde schijf
Wanneer er fouten opgelost zijn, ontkoppel en loskoppelen Hallo bestaande virtuele harde schijf van uw VM voor het oplossen van problemen. U kunt de virtuele harde schijf samen met eventuele andere virtuele machine niet gebruiken totdat Hallo lease die verbindt Hallo virtuele harde schijf toohello probleemoplossing VM is uitgebracht.  

1. Meld u aan toohello [Azure-portal](https://portal.azure.com). 
2. Klik op het menu aan de linkerkant Hallo Hallo **virtuele Machines (klassiek)**.
3. Zoek Hallo herstel-VM. Selecteer schijven, klik met de rechtermuisknop Hallo schijf, en selecteer vervolgens **Detach**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Een virtuele machine uit Hallo oorspronkelijke harde schijf maken

toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [klassieke Azure-portal](https://manage.windowsazure.com).

1. Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer onderaan Hallo Hallo-portal, **nieuw** > **Compute** > **virtuele Machine** > **uit galerie** .
3. In Hallo **een afbeelding kiezen die** sectie **mijn schijven**, en vervolgens selecteert Hallo oorspronkelijke virtuele harde schijf. Controleer de locatiegegevens Hallo. Dit is Hallo regio waar Hallo VM moet worden geïmplementeerd. Selecteer de volgende knop Hallo.
4. In Hallo **Virtuele-machineconfiguratie** sectie Hallo VM naam en een grootte voor Hallo VM selecteren.
