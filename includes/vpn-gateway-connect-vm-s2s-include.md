U kunt virtuele machine die door het maken van een verbinding met extern bureaublad-tooyour VM geïmplementeerde tooyour VNet tooa verbinden. Hallo aanbevolen manier tooinitially controleren of u kunt verbinding maken tooyour VM is tooconnect door met de persoonlijke IP-adres in plaats van de computernaam. Op die manier u test toosee als u verbinding kunt maken, niet of naamomzetting correct is geconfigureerd.

1. Hallo privé IP-adres vinden. U vindt Hallo privé IP-adres van een virtuele machine op verschillende manieren. Hieronder, laten we zien Hallo stappen voor hello Azure-portal en PowerShell.

  - Azure-portal - de virtuele machine niet vinden in hello Azure-portal. Hallo-eigenschappen voor Hallo VM weergeven. Hallo privé IP-adres wordt vermeld.

  - PowerShell - gebruik Hallo voorbeeld tooview een lijst met virtuele machines en privé IP-adressen van uw resourcegroepen. U hoeft niet toomodify in dit voorbeeld voordat u deze gebruikt.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Controleer of u verbonden tooyour VNet met Hallo VPN-verbinding.
3. Open **verbinding met extern bureaublad** getypt 'RDP' of 'Verbinding met extern bureaublad' in het zoekvak Hallo op Hallo taakbalk, selecteer vervolgens verbinding met extern bureaublad. U kunt ook de verbinding met extern bureaublad met behulp van de opdracht 'mstsc' hello in PowerShell openen. 
4. Voer Hallo privé IP-adres van VM Hallo in verbinding met extern bureaublad. U kunt extra instellingen van 'Weergeven Options' tooadjust Klik op verbinding maken.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot een RDP-verbinding tooa VM

Als u problemen bij het verbinden van tooa virtuele machine via de VPN-verbinding ondervindt, controleert u Hallo volgende:

- Controleer of uw VPN-verbinding tot stand is gebracht.
- Controleer of u verbinding maken met toohello privé IP-adres voor Hallo VM.
- Als u verbinding met toohello VM maken kunt gebruik Hallo persoonlijke IP-adres, maar niet Hallo computernaam, Controleer of DNS juist geconfigureerd. Zie [Naamomzetting voor VM's](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over de werking van naamomzetting voor VM's.
- Zie voor meer informatie over RDP-verbindingen [problemen met extern bureaublad-verbindingen tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
