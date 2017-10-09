Hallo benadering tooAzure eindpunten iets anders werkt tussen Hallo klassieke en het Resource Manager-implementatiemodel hebben. U hebt voor Hallo Resource Manager-implementatiemodel, Hallo flexibiliteit toocreate Netwerkfilters die Hallo transportbesturing van verkeer van en naar uw virtuele machines. Deze filters kunnen u toocreate complexe netwerkomgevingen buiten een eenvoudige eindpunt als in Hallo klassieke implementatiemodel. Dit artikel bevat een overzicht van Netwerkbeveiligingsgroepen en hoe ze verschillen van het gebruik van klassieke eindpunten, maken deze regels, filteren en implementatiescenario's steekproeven.

## <a name="overview-of-resource-manager-deployments"></a>Overzicht van implementaties van Resource Manager
Eindpunten in de klassieke implementatiemodel Hallo zijn vervangen door Netwerkbeveiligingsgroepen en toegang tot regels toegangsbeheerlijst (ACL). Snelle stappen voor het implementeren van Network Security groep ACL-regels zijn:

* Een Netwerkbeveiligingsgroep maken.
* tooallow of weigeren van verkeer, het definiëren van uw netwerk beveiliging groep ACL-regels.
* De Netwerkbeveiligingsgroep tooa netwerkinterface of virtueel netwerksubnet toewijzen.

Als u tooalso zijn productiviteitsniveau poort doorsturen uitvoeren, u moet een load balancer tooplace voor uw virtuele machine en gebruik van NAT-regels. Snelle stappen voor het implementeren van een load balancer en NAT-regels zou als volgt zijn:

* Maak een load balancer.
* Maak een back-endpool en uw virtuele machines toohello van toepassingen toevoegen.
* Definieer uw NAT-regels voor het doorsturen van de poort Hallo vereist.
* NAT-regels tooyour virtuele machines toewijzen.

## <a name="network-security-group-overview"></a>Overzicht van Netwerkbeveiligingsgroep
Netwerkbeveiligingsgroepen bieden een beveiligingslaag aan u tooallow bepaalde poorten en subnetten tooaccess uw virtuele machines. U hebben altijd doorgaans een Netwerkbeveiligingsgroep bieden deze beveiligingslaag tussen uw virtuele machines en Hallo buiten de wereld. Netwerkbeveiligingsgroepen kunnen toegepaste tooa virtueel netwerksubnet of een specifieke netwerkinterface voor een virtuele machine zijn. In plaats van het eindpunt ACL-regels maakt, moet u nu Network Security groep ACL-regels maken. Deze ACL-regels bieden veel meer controle dan gewoon een bepaalde poort maken een tooforward eindpunt. Zie voor meer informatie [wat is er een Netwerkbeveiligingsgroep?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> U kunt Netwerkbeveiligingsgroepen toomultiple subnetten of netwerkinterfaces toewijzen. Er is geen toewijzing 1:1. U kunt een Netwerkbeveiligingsgroep met een gemeenschappelijke set ACL-regels maken en toepassen van toomultiple subnetten of netwerkinterfaces. Bovendien Netwerkbeveiligingsgroep worden toegepaste tooresources in uw abonnement (op basis van [rollen gebaseerd toegangsbeheer](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Overzicht van Load Balancers
In de klassieke implementatiemodel Hallo zou Azure uitvoeren van alle Hallo Network Address Translation (NAT) en poort doorsturen op een Cloudservice voor u. Wanneer u een eindpunt maakt, geeft u Hallo externe poort tooexpose samen met de Hallo interne poort toodirect verkeer naar. Deze dezelfde NAT en poort doorsturen Netwerkbeveiligingsgroepen zelf geen uitgevoerd. 

tooallow toocreate NAT-regels voor deze poort wordt doorgestuurd, u een Azure load balancer in de resourcegroep. Ook Hallo load balancer wordt gedetailleerd genoeg tooonly toospecific VM's toepassen, indien nodig. Hello Azure load balancer NAT-regels werk samen met het netwerk beveiliging groep ACL-regels tooprovide veel meer flexibiliteit en beheer dan haalbare met Cloud Service-eindpunten. Zie voor meer informatie, Hallo [load balancer overzicht](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Netwerkbeveiligingsgroep ACL-regels
ACL-regels kunnen u definiëren welk verkeer kan stromen en naar uw virtuele machine op basis van bepaalde poorten of poortbereiken protocollen. Regels zijn toegewezen tooindividual virtuele machines of tooa subnet. Hallo volgende schermafbeelding is een voorbeeld van ACL-regels voor een algemene webserver:

![Lijst van Netwerkbeveiligingsgroep ACL-regels](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

ACL-regels worden toegepast op basis van een prioriteit metrische gegevens die u opgeeft - Hallo hogere Hallo waarde, Hallo lagere Hallo prioriteit. Elke Netwerkbeveiligingsgroep heeft drie standaard regels die zijn ontworpen toohandle Hallo stroom van Azure netwerkverkeer met een expliciete `DenyAllInbound` als Hallo laatste regel. Standaard ACL-regels zijn gegeven een lage prioriteit toonot verstoren regels die u maakt.

## <a name="assigning-network-security-groups"></a>Toewijzen van Netwerkbeveiligingsgroepen
U toewijzen een Netwerkbeveiligingsgroep tooa-subnet of een netwerkinterface. Deze aanpak kunt u toobe zo gedetailleerd is als nodig is tijdens het toepassen van uw ACL regels tooonly een specifieke virtuele machine, of zorg ervoor dat een gemeenschappelijke set van ACL-regels zijn toegepaste tooall virtuele machines deel uitmaken van een subnet:

![Nsg's toonetwork interfaces of subnetten toepassen](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

Hallo gedrag Hallo Netwerkbeveiligingsgroep veranderen niet, afhankelijk van het momenteel toegewezen tooa subnet of een netwerkinterface. Een veelvoorkomend implementatiescenario heeft Hallo die netwerkbeveiligingsgroep tooa subnet tooensure compatibiliteit van alle virtuele machines gekoppelde toothat subnet toegewezen. Zie voor meer informatie [tooresources toepassen Network Security groups](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Standaardgedrag van Netwerkbeveiligingsgroepen
Afhankelijk van hoe en wanneer u uw Netwerkbeveiligingsgroep maakt, kunnen de standaardregels voor VM's van Windows toopermit RDP-toegang op TCP-poort 3389 worden gemaakt. Standaardregels voor virtuele Linux-machines verlenen SSH-toegang op TCP-poort 22. Deze automatische ACL-regels zijn gemaakt onder Hallo volgende voorwaarden:

* Als u een Windows-virtuele machine via de portal Hallo maken en Hallo standaard actie toocreate een Netwerkbeveiligingsgroep accepteert, wordt een ACL regel tooallow TCP-poort 3389 (RDP) gemaakt.
* Als u een Linux-VM via Hallo portal maken en Hallo standaard actie toocreate een Netwerkbeveiligingsgroep accepteert, wordt een ACL regel tooallow TCP-poort 22 (SSH) gemaakt.

Deze standaard ACL-regels zijn onder andere voorwaarden niet gemaakt. U kunt tooyour VM kan geen verbinding zonder dat er Hallo juiste ACL-regels. Deze voorwaarden zijn van de volgende algemene activiteiten Hallo:

* Het maken van een Netwerkbeveiligingsgroep via de portal Hallo als een aparte actie toocreating Hallo VM.
* Maken van een Netwerkbeveiligingsgroep via een programma via PowerShell, Azure CLI, Rest-API's, enzovoort.
* Een virtuele machine maken en toewijzen van bestaande Netwerkbeveiligingsgroep die geen Hallo tooan passende ACL regel die is gedefinieerd.

In alle Hallo voorgaande gevallen, moet u toocreate ACL-regels voor uw VM tooallow Hallo juiste extern beheer-verbindingen.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Standaardgedrag van een virtuele machine zonder een Netwerkbeveiligingsgroep
U kunt een virtuele machine maken zonder te maken van een Netwerkbeveiligingsgroep. In deze situaties kunt u tooyour VM verbinding maken met behulp van RDP of SSH zonder te maken van een ACL-regels. Op dezelfde manier als u een webservice geïnstalleerd op poort 80, of de service automatisch toegankelijk is op afstand. Hallo VM heeft alle poorten open zijn.

> [!NOTE]
> U moet nog steeds toohave een openbare IP-adres toegewezen tooa VM om externe verbindingen. Een Netwerkbeveiligingsgroep voor het subnet- of interface Hallo niet hoeft niet Hallo VM tooany externe verkeer niet weergeven. Hallo standaardactie bij het maken van een virtuele machine via de portal Hallo is toocreate een nieuwe openbare IP-adres. Voor alle andere vormen van het maken van een virtuele machine zoals PowerShell, Azure CLI of Resource Manager-sjabloon, wordt een openbare IP-adres niet automatisch gemaakt tenzij expliciet aangevraagd. de standaardactie Hallo via de portal Hallo is ook een Netwerkbeveiligingsgroep toocreate. Deze standaardactie betekent dat u in een situatie met een blootgestelde VM die geen netwerk filteren in plaats mag niet eindigen.

## <a name="understanding-load-balancers-and-nat-rules"></a>Inzicht in de Load Balancers en NAT-regels
U kunt in de klassieke implementatiemodel Hallo eindpunten die ook uitgevoerd poort doorsturen maken. Wanneer u een virtuele machine in de klassieke implementatiemodel hello maakt, zouden ACL-regels voor RDP of SSH automatisch worden gemaakt. Deze regels geen rol TCP-poort 3389 of TCP-poort 22 respectievelijk toohello buiten de wereld. In plaats daarvan zou een hoge waarde TCP-poort worden weergegeven die de juiste interne poort toohello wordt toegewezen. U kunt ook uw eigen ACL-regels maken op een vergelijkbare manier, zoals zichtbaar een webserver op TCP-poort 4280 toohello buiten de wereld. U kunt deze ACL-regels en poorttoewijzingen in de volgende schermafbeelding uit Hallo klassieke portal Hallo zien:

![Poort-doorsturen met de klassieke eindpunten](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Met Netwerkbeveiligingsgroepen, kan die functie poort doorsturen opgelost door een load balancer. Zie voor meer informatie [taakverdelers in Azure](../articles/load-balancer/load-balancer-overview.md). Hallo volgende voorbeeld ziet u een load balancer met een NAT regel tooperform doorsturen van poort TCP-poort 4222 toohello interne TCP-poort 22 een virtuele machine:

![Load balancer NAT-regels voor het doorsturen van poort](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Wanneer u een load balancer implementeert, u doorgaans niet toewijst Hallo VM zelf een openbaar IP-adres. In plaats daarvan heeft Hallo load balancer een openbare IP-adres toegewezen tooit. U moet nog steeds toocreate de Netwerkbeveiligingsgroep en ACL-regels toodefine Hallo verkeersstroom in en uit de virtuele machine. Hallo zijn load balancer NAT-regels gewoon toodefine welke poorten via Hallo load balancer en hoe ze ophalen verdeeld over Hallo back-end virtuele machines zijn toegestaan. Zo moet u toocreate een NAT-regel voor verkeer tooflow via Hallo load balancer. tooallow hello verkeer tooreach Hallo VM, maak een regel Network Security groep ACL.
