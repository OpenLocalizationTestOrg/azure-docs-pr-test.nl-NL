U een poort openen of maken van een eindpunt tooa virtuele machine (VM) in Azure door het maken van een netwerk-filter op een subnet of een VM-netwerkinterface. U plaatsen deze filters die binnenkomend en uitgaand verkeer worden beheerd, van een Netwerkbeveiligingsgroep gekoppeld toohello resource die Hallo verkeer ontvangt.

We gebruiken een voorbeeld van webverkeer op poort 80. Zodra u hebt een virtuele machine die is geconfigureerd tooserve webaanvragen op Hallo standaard TCP-poort 80 (onthouden toostart Hallo nodig services en alle firewallregels OS op Hallo VM ook openen), u:

1. Een Netwerkbeveiligingsgroep maken.
2. Maak een regel voor inkomend verkeer met toestaat:
   * Hallo doelpoortbereik '80'
   * poortbereik van bron van Hallo ' * ' (zodat alle bronpoorten)
   * de prioriteitswaarde minder 65,500 (hoger in prioriteit dan hello standaard catch all-regel voor weigeren van inkomende toobe)
3. Hallo Netwerkbeveiligingsgroep koppelen aan Hallo VM-netwerkinterface of subnet.

U kunt complexe netwerk configuraties toosecure uw omgeving met behulp van Netwerkbeveiligingsgroepen en -regels maken. Dit voorbeeld wordt slechts één of twee regels waarmee HTTP-verkeer of extern beheer. Zie voor meer informatie de volgende Hallo ["Meer informatie"](#more-information-on-network-security-groups) sectie of [wat is er een Netwerkbeveiligingsgroep?](../articles/virtual-network/virtual-networks-nsg.md)

