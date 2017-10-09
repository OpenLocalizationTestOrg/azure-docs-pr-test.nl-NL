

## <a name="multi-and-single-instance-vms"></a>Multi- en virtuele machines van één exemplaar
Veel klanten uitgevoerd op Azure aantal kritieke dat ze plannen kunnen wanneer de bijbehorende virtuele machines ondergaan gepland onderhoud vanwege toohello uitvaltijd--ongeveer 15 minuten--die deze gebeurtenis treedt op tijdens het onderhoud. U kunt beschikbaarheid sets toohelp besturingselement ingerichte VM's ontvangen gepland onderhoud.

Er zijn twee mogelijke configuraties voor virtuele machines die worden uitgevoerd op Azure. Virtuele machines zijn geconfigureerd als één of meerdere exemplaren. Als VMs in een beschikbaarheidsset zijn, zijn vervolgens die geconfigureerd als meerdere exemplaren. Houd er rekening mee, zelfs één virtuele machines kunnen worden geïmplementeerd in een beschikbaarheidsset, zodat ze worden behandeld als meerdere exemplaren. Als virtuele machines niet in een beschikbaarheidsset, zijn vervolgens die geconfigureerd als één exemplaar.  Zie voor meer informatie over beschikbaarheidssets [beheren Hallo beschikbaarheid van uw virtuele Machines van Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [beheren Hallo beschikbaarheid van uw virtuele Linux-Machines](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Gepland onderhoud updates toosingle-instance en meerdere exemplaren VMs afzonderlijk gebeuren. Opnieuw configureren van uw virtuele machines toobe single instance (als ze meerdere exemplaren zijn) of meerdere exemplaren van toobe (als ze single instance zijn), kunt u bepalen wanneer de bijbehorende virtuele machines Hallo gepland onderhoud ontvangt. Zie [gepland onderhoud voor Azure Linux virtuele machines](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [gepland onderhoud voor Windows Azure virtuele machines](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie over gepland onderhoud voor Azure Virtual machines.

## <a name="for-multi-instance-configuration"></a>Configuratie van meerdere instanties
Hallo tijd gepland onderhoud van invloed is op uw virtuele machines die door het verwijderen van deze virtuele machines van beschikbaarheidssets in een configuratie van de Beschikbaarheidsset zijn geïmplementeerd, kunt u selecteren.

1. Een e-mailbericht wordt verzonden tooyou zeven kalenderdagen voordat Hallo gepland onderhoud tooyour virtuele machines in een configuratie met meerdere exemplaren. Hallo abonnement-id's en namen van virtuele machines met meerdere instanties van Hallo van invloed op een zijn opgenomen in de hoofdtekst Hallo Hallo e-mailadres.
2. Tijdens deze zeven dagen, kunt u Hallo tijd uw exemplaren worden bijgewerkt door het verwijderen van uw exemplaar van meerdere virtuele machines in deze regio uit hun beschikbaarheidsset. Deze wijziging in de configuratie wordt opgestart, als Hallo virtuele Machine wordt verplaatst van één fysieke host, gericht voor onderhoud, tooanother fysieke host die niet is gericht voor onderhoud.
3. U kunt Hallo VM verwijderen van de beschikbaarheidsset voor hello Azure-portal.

   1. Selecteer in Hallo portal Hallo VM tooremove van Hallo Beschikbaarheidsset.  

   2. Onder **instellingen**, klikt u op **beschikbaarheidsset**.

      ![Selectie van de Beschikbaarheidsset](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. In de beschikbaarheid van Hallo vervolgkeuzemenu instellen, selecteert u "Geen deel uit van een beschikbaarheidsset."

      ![Verwijderen uit de Set](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Klik aan de bovenkant Hallo **opslaan**. Klik op **Ja** tooacknowledge die deze actie opnieuw wordt opgestart Hallo VM.

   >[!TIP]
   >U kunt Hallo VM toomulti-instance later opnieuw configureren door een Hallo vermeld beschikbaarheidssets te selecteren.

4. Virtuele machines die zijn verwijderd uit de beschikbaarheidssets zijn verplaatste tooSingle-Instance hosts en worden niet bijgewerkt tijdens Hallo gepland onderhoud tooAvailability configuraties instellen.
5. Zodra de Hallo update tooAvailability VM's is voltooid moet (op basis van tooschedule die worden beschreven in de oorspronkelijke e-mailbericht Hallo), u toevoegen Hallo VM's weer in hun beschikbaarheidssets. Als onderdeel van een beschikbaarheidsset Hallo VMs geconfigureerd als meerdere exemplaren en resulteert in een opnieuw opstarten. Normaal gesproken zodra alle meerdere exemplaren updates zijn voltooid op Hallo volledige Azure-omgeving, volgt single instance onderhoud.

Een virtuele machine verwijderen uit een beschikbaarheidsset kan ook worden bereikt met Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Voor de configuratie van één exemplaar
U kunt Hallo tijd gepland onderhoud van invloed is op u virtuele machines in een configuratie met Single instance door deze virtuele machines toe te voegen in beschikbaarheidssets selecteren.

Stapsgewijs

1. Een e-mailbericht wordt verzonden tooyou zeven kalenderdagen voordat Hallo gepland onderhoud tooVMs in een configuratie met één exemplaar. Hallo abonnement-id's en namen van virtuele machines van Hallo van invloed op een Single Instance zijn opgenomen in de hoofdtekst Hallo Hallo e-mailadres.
2. Tijdens deze zeven dagen, kunt u Hallo tijd uw exemplaar opnieuw wordt opgestart door het toevoegen van de beschikbaarheid van uw virtuele machines Single instance tooan ingesteld in dat dezelfde regio. Deze wijziging in de configuratie wordt opgestart, als Hallo virtuele Machine wordt verplaatst van één fysieke host, gericht voor onderhoud, tooanother fysieke host die niet is gericht voor onderhoud.
3. Volg de instructies hier tooadd bestaande virtuele machines in beschikbaarheidssets met hello Azure-portal en Azure PowerShell. (Zie hello Azure PowerShell-voorbeeldtoepassing die u als volgt.)
4. Zodra deze VMs zijn geconfigureerd als meerdere exemplaren, worden uitgesloten van Hallo gepland onderhoud tooSingle exemplaar virtuele machines.
5. Wanneer de Hallo single instance VM update is voltooid kunt (op basis van tooschedule in Hallo oorspronkelijke e-mailbericht), u terugkeren Hallo VMs toosingle-instance door het verwijderen van virtuele machines Hallo van hun beschikbaarheidssets.

Toevoegen van een VM-tooan kan beschikbaarheidsset ook worden bereikt met Azure PowerShell:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
