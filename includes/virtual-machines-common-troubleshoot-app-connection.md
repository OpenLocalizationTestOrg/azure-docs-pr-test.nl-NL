Er zijn diverse redenen wanneer u mag niet beginnen of verbinding tooan toepassing die wordt uitgevoerd op Azure een virtuele machine (VM). Redenen Hallo toepassing niet actief zijn of luistert op Hallo verwacht poorten, Hallo luisterpoort geblokkeerd of netwerken regels die verkeer toohello toepassing niet juist wordt doorgegeven. Dit artikel wordt beschreven, een methodische wijze toofind en de juiste Hallo probleem.

Als u verbinding maken met tooyour VM problemen ondervindt met RDP of SSH, Zie een van de volgende Hallo eerst artikelen:

* [Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Secure Shell (SSH) verbindingen tooa op basis van Linux virtuele machine van Azure oplossen](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../articles/resource-manager-deployment-model.md). In dit artikel komen beide modellen, maar Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.

## <a name="quick-start-troubleshooting-steps"></a>Stappen voor probleemoplossing voor snel starten
Als u netwerkverbindingsproblemen tooan toepassing hebt, kunt u Hallo volgende algemene stappen voor probleemoplossing. Probeer opnieuw verbinding tooyour-toepassing na elke stap:

* Hallo virtuele machine opnieuw opstarten
* Hallo-eindpunt opnieuw / firewall-regels / netwerk beveiligingsregels voor de groep (NSG)
  * [Resource Manager-model - Netwerkbeveiligingsgroepen beheren](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Klassieke model - eindpunten Cloudservices beheren](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Verbinding maken vanaf een andere locatie, zoals een andere virtuele Azure-netwerk
* Hallo virtuele machine implementeren
  * [Implementeer Windows VM opnieuw](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Virtuele Linux-machine implementeren](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Hallo virtuele machine opnieuw maken

Zie voor meer informatie [probleemoplossing eindpunt connectiviteit (RDP/SSH/HTTP, enz. fouten)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Gedetailleerd overzicht voor het oplossen van problemen
Er zijn vier hoofdgebieden tootroubleshoot Hallo toegang van een toepassing die wordt uitgevoerd op een virtuele machine van Azure.

![problemen oplossen kan toepassing niet starten](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. Hallo-toepassing op Hallo Azure virtuele machine wordt uitgevoerd.
   * Hallo-toepassing zelf correct is gestart?
2. Hello Azure virtuele machine.
   * Hallo VM zelf is correct gestart en toorequests reageert?
3. Netwerk van Azure-eindpunten.
   * Voor virtuele machines in de klassieke implementatiemodel Hallo cloud service-eindpunten.
   * Netwerkbeveiligingsgroepen en binnenkomende NAT-regels voor virtuele machines in de Resource Manager-implementatiemodel.
   * Kan stroom van gebruikers toohello VM/toepassing op Hallo verwacht poorten verkeer?
4. Uw Internet-edge-apparaat.
   * Firewallregels erin verhinderen verkeer stroomt correct?

Voor clientcomputers die toegang hebben tot de toepassing hello via een site-naar-site VPN- of ExpressRoute-verbinding, Hallo hoofdgebieden die problemen kunnen veroorzaken toepassing hello en hello Azure virtuele machine.

toodetermine hello bron van Hallo probleem en de correctie als volgt te werk.

## <a name="step-1-access-application-from-target-vm"></a>Stap 1: De toepassing openen vanaf het doel VM
Probeer tooaccess Hallo toepassing met de juiste clientprogramma Hallo van Hallo VM waarop deze wordt uitgevoerd. De lokale hostnaam hello, Hallo lokale IP-adres of Hallo loopback-adres (127.0.0.1) gebruiken.

![toepassing rechtstreeks vanuit Hallo VM starten](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Bijvoorbeeld, als de toepassing hello een webserver is, open een browser op Hallo VM en probeer het tooaccess webpagina's die worden gehost op Hallo VM.

Als u toegang hebt tot de toepassing hello, gaat u verder te[stap 2](#step2).

Als u geen toegang de toepassing hello tot, Controleer of de Hallo volgende instellingen:

* Hallo-toepassing wordt uitgevoerd op de virtuele doelmachine Hallo.
* Hallo toepassing luistert op Hallo verwacht TCP en UDP-poorten.

Gebruik op Windows en Linux gebaseerde virtuele machines, Hallo **netstat - a** opdracht tooshow Hallo actieve controlepoorten. Bekijk de uitvoer Hallo voor Hallo verwacht poorten waarop uw toepassing moet luisteren. Hallo toepassing opnieuw starten of het toouse Hallo verwacht poorten naar wens configureren en probeer het opnieuw tooaccess Hallo toepassing lokaal.

## <a id="step2"></a>Stap 2: Toepassing openen vanaf een andere virtuele machine in Hallo hetzelfde virtuele netwerk
Probeer tooaccess Hallo toepassing van een andere virtuele machine, maar Hallo in hetzelfde virtuele netwerk, met behulp van Hallo VM-hostnaam of het toegewezen Azure public, private of provider IP-adres. Voor virtuele machines is gemaakt met het klassieke implementatiemodel hello, openbare IP-adres van de cloudservice Hallo Hallo niet te gebruiken.

![toepassing van een andere virtuele machine starten](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Als de toepassing hello een webserver is, Hallo probeer tooaccess een webpagina vanuit een browser op een andere virtuele machine in hetzelfde virtuele netwerk.

Als u toegang hebt tot de toepassing hello, gaat u verder te[stap 3](#step3).

Als u geen toegang de toepassing hello tot, Controleer of de Hallo volgende instellingen:

* Hallo hostfirewall op Hallo doel VM toestaat Hallo binnenkomende aanvraag en antwoord uitgaand verkeer.
* Inbraakdetectie of -software die wordt uitgevoerd op het Hallo-doel VM netwerkbewaking toestaat Hallo verkeer.
* Cloud Services-eindpunten of Netwerkbeveiligingsgroepen zijn Hallo verkeer toestaat:
  * [Klassieke model - eindpunten Cloudservices beheren](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Resource Manager-model - Netwerkbeveiligingsgroepen beheren](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Een afzonderlijk onderdeel dat wordt uitgevoerd in uw virtuele machine in Hallo pad tussen Hallo test virtuele machine en de virtuele machine, zoals een firewall of een load balancer toestaat Hallo verkeer.

Op een Windows-virtuele machine, gebruikt u Windows Firewall met geavanceerde beveiliging toodetermine of Hallo firewallregels voor binnenkomend en uitgaand verkeer van uw toepassing uitsluiten.

## <a id="step3"></a>Stap 3: Toegang tot toepassing vanaf extern Hallo virtuele netwerk
Probeer tooaccess Hallo toepassing vanaf een computer buiten het virtuele netwerk Hallo als Hallo VM waarop Hallo toepassing wordt uitgevoerd. Gebruik een ander netwerk als de oorspronkelijke clientcomputer.

![toepassing starten vanaf een computer buiten het virtuele netwerk Hallo](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Als de toepassing hello een webserver is, bijvoorbeeld tooaccess Hallo webpagina vanuit een browser op een computer die zich niet in het virtuele netwerk Hallo proberen.

Als u geen toegang de toepassing hello tot, Controleer of de Hallo volgende instellingen:

* Voor virtuele machines gemaakt met het klassieke implementatiemodel Hallo:
  
  * Controleer of deze eindpuntconfiguratie Hallo voor Hallo die VM Hallo binnenkomende verkeer, met name Hallo-protocol (TCP of UDP) en de openbare en persoonlijke poortnummers Hallo toestaat.
  * Controleer of toegangsbeheerlijsten (ACL's) op Hallo eindpunt zijn niet inkomend verkeer van Internet Hallo belemmeren.
  * Zie voor meer informatie [hoe tooSet Up eindpunten tooa virtuele Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Voor virtuele machines gemaakt met Resource Manager-implementatiemodel Hallo:
  
  * Controleer of die Hallo inkomende NAT-regel is een configuratie voor Hallo die VM Hallo binnenkomende verkeer, met name Hallo-protocol (TCP of UDP) en de openbare en persoonlijke poortnummers Hallo toestaat.
  * Controleer of dat de Netwerkbeveiligingsgroepen zijn toestaat Hallo binnenkomende aanvraag en antwoord uitgaand verkeer.
  * Zie voor meer informatie [Wat is een netwerkbeveiligingsgroep (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)

Als lid van een set met gelijke taakverdeling Hallo virtuele machine of eindpunt is:

* Controleer of de test Hallo-protocol (TCP of UDP) en het poortnummer juist zijn.
* Als het Hallo-test is protocol en poort anders dan Hallo set met gelijke taakverdeling protocol en poort:
  * Controleer of dat de toepassing hello op Hallo test protocol (TCP of UDP) en het poortnummer luistert (Gebruik **netstat-a** gericht op Hallo VM).
  * Controleer of deze Hallo hostfirewall op Hallo doel die VM Hallo test binnenkomende aanvraag en uitgaande test antwoord verkeer toestaat.

Als u toegang hebt tot de toepassing hello, zorg ervoor dat uw randapparaat Internet toestaat:

* Hallo uitgaande toepassing aanvraag verkeer vanaf uw client-computer toohello virtuele machine van Azure.
* Hallo inkomende toepassing antwoord verkeer van hello Azure virtuele machine.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Stap 4 als u geen toegang de toepassing hello, gebruik IP-Controleer de instellingen voor toocheck Hallo tot. 

Zie voor meer informatie [Azure-netwerk bewakingsoverzicht](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Aanvullende bronnen
[Problemen met extern bureaublad-verbindingen tooa op basis van Windows Azure virtuele Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Secure Shell (SSH) verbindingen tooa op basis van Linux virtuele machine van Azure oplossen](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

