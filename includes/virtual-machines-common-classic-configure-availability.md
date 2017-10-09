


Een beschikbaarheidsset helpt uw virtuele machines beschikbaar zijn tijdens de uitvaltijd, zoals behouden tijdens onderhoud. Als u twee of meer op vergelijkbare wijze geconfigureerde virtuele machines in een beschikbaarheidsset maakt Hallo redundantie nodig toomaintain beschikbaarheid van het Hallo-toepassingen of services die de virtuele machine wordt uitgevoerd. Zie voor meer informatie over hoe dit werkt [Hallo beschikbaarheid van virtuele machines beheren][Manage hello availability of virtual machines].

Het is een best practice toouse zowel beschikbaarheidssets als eindpunten toohelp taakverdeling ervoor te zorgen dat uw toepassing altijd beschikbaar en worden uitgevoerd efficiënt is. Zie voor meer informatie over Netwerktaakverdeling eindpunten [taakverdeling voor Azure-infrastructuurservices][Load balancing for Azure infrastructure services].

U kunt de klassieke virtuele machines toevoegen in een beschikbaarheidsset met behulp van een van twee opties:

* [Optie 1: Een virtuele machine maken en een beschikbaarheidsset op Hallo dezelfde tijd][Option 1: Create a virtual machine and an availability set at hello same time]. Vervolgens voegt u een nieuwe virtuele machines toohello ingesteld bij het maken van deze virtuele machines.
* [Optie 2: Voeg een bestaande beschikbaarheidsset voor de virtuele machine tooan][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> In het klassieke model Hallo Hallo virtuele machines die u wilt tooput in dezelfde beschikbaarheidsset moet behoren toohello dezelfde cloudservice.
> 
> 

## <a id="createset"></a>Optie 1: een virtuele machine maken en een beschikbaarheidsset op Hallo dezelfde tijd
U kunt beide hello Azure-portal of Azure PowerShell-opdrachten toodo dit.

toouse hello Azure-portal:

1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu hub Hallo **+ nieuw**, en klik vervolgens op **virtuele Machine**.
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Selecteer Hallo Marketplace virtuele machine-installatiekopie die u wenst dat toouse. U kunt een virtuele machine van Linux of Windows toocreate.
4. Controleer of dat implementatiemodel hello te is ingesteld voor Hallo virtuele machine geselecteerde,**klassieke** en klik vervolgens op **maken**
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Voer een naam van virtuele machine, de gebruikersnaam en het wachtwoord (voor Windows-machines) of de openbare SSH-sleutel (voor Linux-machines). 
6. Kies Hallo VM-grootte en klik vervolgens op **Selecteer** toocontinue.
7. Kies **optionele configuratie > beschikbaarheidsset**, en selecteer Hallo beschikbaarheidsset tooadd Hallo virtuele machine gewenst.
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Controleer uw configuratie-instellingen. Wanneer u bent klaar, klikt u op **maken**.
9. Terwijl Azure de virtuele machine maakt, kunt u de voortgang Hallo onder bijhouden **virtuele Machines** in Hallo hub-menu.

toouse Azure PowerShell-opdrachten toocreate Azure een virtuele machine en toe te voegen nieuwe of bestaande beschikbaarheidsset tooa, Zie [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele machines op basis van Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Optie 2: een bestaande beschikbaarheidsset voor de virtuele machine tooan toevoegen
U kunt in hello Azure-portal, bestaande klassieke virtuele machines tooan bestaande beschikbaarheidsset toevoegen of een nieuwe voor hen maken. (Houd er rekening mee dat Hallo virtuele machines in dezelfde beschikbaarheidsset Hallo toohello moet behoren dezelfde cloudservice.) Hallo stappen zijn bijna hetzelfde Hallo. U kunt met Azure PowerShell Hallo virtuele machine tooan bestaande beschikbaarheidsset toevoegen.

1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op het menu Hub Hallo **virtuele Machines (klassiek)**.
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Selecteer in de lijst van de Hallo van virtuele machines, Hallo-naam van Hallo virtuele machine die u wilt dat tooadd toohello set.
4. Kies **beschikbaarheidsset** van Hallo virtuele machine **instellingen**.
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Hallo beschikbaarheidsset tooadd Hallo virtuele machine te gewenst selecteren. Hallo virtuele machine moet behoren toohello dezelfde cloudservice als Hallo beschikbaarheidsset.
   
    ![De installatiekopie van de alternatieve tekst](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Klik op **Opslaan**.

toouse Azure PowerShell-opdrachten, open een Azure PowerShell-sessie beheerdersniveau en Hallo volgende opdracht uitvoeren. Voor tijdelijke aanduidingen hello (zoals &lt;VmCloudServiceName&gt;), vervangt u alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met Hallo de juiste namen.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Hallo virtuele machine mogelijk opnieuw opgestart toobe toofinish toe te voegen toohello beschikbaarheidsset.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

