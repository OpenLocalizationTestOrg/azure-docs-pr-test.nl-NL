> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Sjabloon](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Een Azure-virtuele Machine (VM) heeft een of meer netwerkinterfaces (NIC) tooit gekoppeld. Een NIC kan een of meer statische of dynamische openbare en particuliere IP-adressen toegewezen tooit. Toewijzen van meerdere IP-kunt adressen tooa VM Hallo volgende mogelijkheden:

* Het hosten van meerdere websites of services met verschillende IP-adressen en SSL-certificaten op één server.
* Het fungeren als een virtueel netwerkapparaat, zoals een firewall of load balancer.
* Hallo mogelijkheid tooadd van Hallo privé-IP adressen voor een van de Hallo NIC's tooan back-end-pool Load Balancer van Azure. Primaire IP-adres voor Hallo die primaire NIC kan worden toegevoegd in Hallo voorbij alleen Hallo tooa back-end-pool. toolearn informatie over hoe tooload een balans vinden tussen meerdere IP-configuraties lezen Hallo [meerdere IP-configuraties voor taakverdeling](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.

Elke NIC die is gekoppeld tooa VM heeft een of meer IP-configuraties die zijn gekoppeld tooit. Aan elke configuratie is één statisch of dynamisch privé-IP-adres toegewezen. Elke configuratie kan ook een openbare IP-adres bron die is gekoppeld tooit hebben. De bron van een openbare IP-adres heeft ofwel een dynamische of statische openbare IP-adres toegewezen tooit. toolearn meer over IP-adressen in Azure, Hallo lezen [IP-adressen in Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) artikel. 

Er is een limiet toohow veel persoonlijke IP-adressen kunnen worden toegewezen tooa NIC. Er is ook een limiet toohow veel openbare IP-adressen die kunnen worden gebruikt in een Azure-abonnement. Zie Hallo [Azure beperkt](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artikel voor meer informatie.
