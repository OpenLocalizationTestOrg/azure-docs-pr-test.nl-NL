

VM-extensies kunnen u helpen bij het volgende:

* Het wijzigen van beveiligings- en identiteitsfuncties, zoals het opnieuw instellen van accountwaarden en het gebruik van antimalware
* Het starten, stoppen of configureren van bewaking en diagnostische functies
* Het opnieuw instellen of installeren van connectiviteitsfuncties, zoals RDP en SSH
* Het diagnosticeren, bewaken en beheren van virtuele machines

Daarnaast zijn er nog vele andere functies. Er worden regelmatig nieuwe functies voor VM-extensie vrijgegeven. Dit artikel wordt beschreven hello Azure VM Agents voor Windows- en Linux- en hoe ze ondersteuning bieden voor VM-extensie-functionaliteit. Zie voor een overzicht van VM-extensies op functie [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM-extensies en -functies in Azure).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Azure VM-agents voor Windows en Linux
Hallo Agent voor Azure virtuele Machines (VM-Agent) is een beveiligde, lichte proces dat wordt geïnstalleerd, configureert en verwijdert u de VM-extensies op exemplaren van Azure Virtual Machines. Hallo VM-Agent fungeert als Hallo beveiligde lokale control-service voor uw Azure VM. Hallo-uitbreidingen die agent belasting Hallo bieden specifieke functies tooincrease uw productiviteit met Hallo-exemplaar.

Er bestaan twee Azure VM-agents: één voor virtuele Windows-machines en één voor virtuele Linux-machines.

Als u een virtuele machine exemplaar toouse op een of meer VM-extensies wilt, moet een geïnstalleerde VM-Agent in Hallo exemplaar hebben. De installatiekopie van een virtuele machine gemaakt met behulp van hello Azure-portal en een installatiekopie van Hallo **Marketplace** installeert automatisch een VM-Agent in het proces voor het maken van Hallo. Als de instantie van een virtuele machine beschikt niet over een VM-Agent, kunt u Hallo VM-Agent installeren nadat de instantie van de virtuele machine hello wordt gemaakt. Of u kunt Hallo-agent installeren in een aangepaste VM-installatiekopie vervolgens uploaden.

> [!IMPORTANT]
> Deze VM-agents zijn zeer eenvoudige services die veilig beheer van VM-exemplaren mogelijk maken. Mogelijk zijn er gevallen waarin u niet dat Hallo VM-Agent wilt. Als dit het geval is, worden ervoor toocreate VM's waarvoor geen Hallo VM-Agent is geïnstalleerd met behulp van hello Azure CLI of PowerShell. Hoewel Hallo VM-Agent kan fysiek worden verwijderd, is Hallo gedrag van VM-extensies op Hallo-exemplaar is niet gedefinieerd. Daarom wordt het verwijderen van een geïnstalleerde VM-agent niet ondersteund.
>

Hallo VM-Agent is ingeschakeld in Hallo volgende situaties:

* Wanneer u een exemplaar van een virtuele machine met behulp van maakt hello Azure-portal en het selecteren van een afbeelding van Hallo **Marketplace**,
* Wanneer u een exemplaar van een virtuele machine maakt met behulp van Hallo [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) of Hallo [nieuw AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. U kunt een virtuele machine zonder een VM-Agent maken door toe te voegen Hallo **– DisableGuestAgent** parameter toohello [toevoegen AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet,

* Wanneer u handmatig downloaden en Hallo VM-Agent installeren op een bestaande VM-instantie en stel Hallo **ProvisionGuestAgent** waarde te**true**. U kunt deze methode voor Windows- en Linux-agents gebruiken door een PowerShell-opdracht of een REST-aanroep te gebruiken. (Als Hallo niet is ingesteld **ProvisionGuestAgent** waarde na de installatie handmatig Hallo VM-Agent, Hallo toevoeging van VM-Agent is niet goed vastgesteld Hallo.) Hallo van de volgende code voorbeeld ziet u hoe toodo deze met behulp van PowerShell waar hello `$svc` en `$name` argumenten zijn al vastgesteld:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Wanneer u een VM-installatiekopie maakt die een geïnstalleerde VM-agent bevat. Zodra het Hallo-installatiekopie met de Hallo VM-Agent aanwezig is, kunt u die afbeelding tooAzure uploaden. Download voor een virtuele machine van Windows hello [Windows VM-Agent MSI-bestand](http://go.microsoft.com/fwlink/?LinkID=394789) en Hallo VM-Agent installeren. Installeren voor een Linux-VM VM-Agent van de GitHub-opslagplaats Hallo zich bevindt op Hallo <https://github.com/Azure/WALinuxAgent>. Zie voor meer informatie over hoe tooinstall VM-Agent op Linux Hallo Hallo [gebruikershandleiding voor Azure Linux VM-Agent](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> In PaaS, hello VM-Agent heet **WindowsAzureGuestAgent**, en is altijd beschikbaar zijn op Web- en virtuele machines Worker-rol. (Zie voor meer informatie [Azure rol architectuur](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) Hallo VM-Agent voor rol virtuele machines kunt nu extensies toohello cloudservice virtuele machines toevoegen in Hallo dezelfde manier als dit het geval voor permanente virtuele Machines is. Hallo grootste verschil tussen de VM-extensies op VM-rol en permanente virtuele machines is wanneer Hallo VM-extensies worden toegevoegd. Uitbreidingen worden met de rol virtuele machines, eerste toohello-cloudservice, klikt u vervolgens toohello implementaties binnen de cloudservice worden toegevoegd.
>
> Gebruik de [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet toolist alle beschikbare functie VM-extensies.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>VM-extensies zoeken, toevoegen, bijwerken en verwijderen
Zie [Azure VM-extensies toevoegen, zoeken, bijwerken en verwijderen](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) voor meer informatie over deze taken.
