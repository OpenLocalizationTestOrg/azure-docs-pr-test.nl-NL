Als u problemen bij het verbinden van tooa virtuele machine via de VPN-verbinding ondervindt, controleert u Hallo volgende:

- Controleer of uw VPN-verbinding tot stand is gebracht.
- Controleer of u verbinding maken met toohello privé IP-adres voor Hallo VM.
- Als u verbinding met toohello VM maken kunt gebruik Hallo persoonlijke IP-adres, maar niet Hallo computernaam, Controleer of DNS juist geconfigureerd. Zie [Naamomzetting voor VM's](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over de werking van naamomzetting voor VM's.

Wanneer u verbinding via punt-naar-Site maakt, controleert u Hallo volgende aanvullende items:

- Gebruik 'ipconfig' toocheck Hallo IPv4-adres toegewezen toohello Ethernet-adapter op Hallo computer van waaruit u de verbinding maakt. Als Hallo IP-adres binnen het adresbereik Hallo Hallo VNet waarmee u verbinding maakt of binnen het adresbereik Hallo van uw VPNClientAddressPool, wordt deze aangeduid tooas een overlappende adresruimte. Wanneer uw adresruimte overlapt op deze manier, netwerkverkeer hello Azure niet bereiken, blijft deze op Hallo lokale netwerk.
- Controleer of dat Hallo VPN-clientpakket configuratie is gegenereerd nadat Hallo DNS-server IP-adressen zijn opgegeven voor Hallo VNet. Als u IP-adressen van Hallo DNS-server wordt bijgewerkt, genereren en een nieuwe VPN-client-configuratiepakket installeren.

Zie voor meer informatie over het oplossen van een RDP-verbinding [problemen met extern bureaublad-verbindingen tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
