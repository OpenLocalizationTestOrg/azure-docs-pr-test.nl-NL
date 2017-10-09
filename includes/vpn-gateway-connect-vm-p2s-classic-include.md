U kunt virtuele machine die door het maken van een verbinding met extern bureaublad-tooyour VM geïmplementeerde tooyour VNet tooa verbinden. Hallo aanbevolen manier tooinitially controleren of u kunt verbinding maken tooyour VM is tooconnect door met de persoonlijke IP-adres in plaats van de computernaam. Op die manier u test toosee als u verbinding kunt maken, niet of naamomzetting correct is geconfigureerd. 

1. Hallo privé IP-adres voor uw virtuele machine vinden. U vindt Hallo privé IP-adres van een virtuele machine door beide bekijkt hello eigenschappen voor de virtuele machine in Azure-portal Hallo Hallo of met behulp van PowerShell.
2. Controleer of u verbonden tooyour VNet met Hallo punt-naar-Site VPN verbinding. 
3. Verbinding met extern bureaublad openen door te typen van 'RDP' of 'Verbinding met extern bureaublad' in het zoekvak Hallo op Hallo taakbalk en selecteer vervolgens verbinding met extern bureaublad. U kunt ook de verbinding met extern bureaublad met behulp van de opdracht 'mstsc' hello in PowerShell openen. 
3. Voer Hallo privé IP-adres van VM Hallo in verbinding met extern bureaublad. U kunt extra instellingen van 'Weergeven Options' tooadjust Klik op verbinding maken.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot een RDP-verbinding tooa VM

Als u hebt met het tooa virtuele machine via uw VPN-verbinding verbinding te maken problemen, zijn er enkele dingen die u kunt controleren. Zie voor meer informatie over probleemoplossing [problemen met extern bureaublad-verbindingen tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Controleer of uw VPN-verbinding tot stand is gebracht.
- Controleer of u verbinding maken met toohello privé IP-adres voor Hallo VM.
- Gebruik 'ipconfig' toocheck Hallo IPv4-adres toegewezen toohello Ethernet-adapter op Hallo computer van waaruit u de verbinding maakt. Als Hallo IP-adres binnen het adresbereik Hallo Hallo VNet waarmee u verbinding maakt of binnen het adresbereik Hallo van uw VPNClientAddressPool, wordt deze aangeduid tooas een overlappende adresruimte. Wanneer uw adresruimte overlapt op deze manier, netwerkverkeer hello Azure niet bereiken, blijft deze op Hallo lokale netwerk.
- Als u verbinding met toohello VM maken kunt gebruik Hallo persoonlijke IP-adres, maar niet Hallo computernaam, Controleer of DNS juist geconfigureerd. Zie [Naamomzetting voor VM's](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over de werking van naamomzetting voor VM's.
- Controleer of dat Hallo VPN-clientpakket configuratie is gegenereerd nadat Hallo DNS-server IP-adressen zijn opgegeven voor Hallo VNet. Als u IP-adressen van Hallo DNS-server wordt bijgewerkt, genereren en een nieuwe VPN-client-configuratiepakket installeren.
