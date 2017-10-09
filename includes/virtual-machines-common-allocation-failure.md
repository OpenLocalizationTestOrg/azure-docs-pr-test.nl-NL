
Als uw Azure probleem niet wordt besproken in dit artikel, gaat u naar Hallo [Azure-forums op MSDN en Stack Overflow](https://azure.microsoft.com/support/forums/). U kunt het probleem op deze forums boeken of too@AzureSupport op Twitter. U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.

## <a name="general-troubleshooting-steps"></a>Algemene stappen voor probleemoplossing
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Algemene toewijzingsfouten in het klassieke implementatiemodel Hallo
Deze stappen oplossen veel toewijzingsfouten in virtuele machines:

* Het formaat van Hallo VM tooa andere VM-grootte.<br>
    Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > uw virtuele machine > **instellingen** > **grootte**. Zie voor gedetailleerde stappen [Hallo virtuele machine vergroten of verkleinen](https://msdn.microsoft.com/library/dn168976.aspx).
* Alle virtuele machines van de cloudservice Hallo verwijderen en opnieuw maken virtuele machines.<br>
    Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > uw virtuele machine > **verwijderen**. Klik vervolgens op **nieuw** > **Compute** > [installatiekopie van virtuele machine].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Algemene toewijzingsfouten in hello Azure Resource Manager-implementatiemodel
Deze stappen oplossen veel toewijzingsfouten in virtuele machines:

* Gestopt (toewijzing ongedaan maken) alle VM's in Hallo dezelfde beschikbaarheid instellen, start vervolgens elke service.<br>
    toostop: klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.
  
    Nadat alle virtuele machines stoppen, selecteert de eerste VM Hallo en klik op **Start**.

## <a name="background-information"></a>Achtergrondinformatie
### <a name="how-allocation-works"></a>De werking van toewijzing
Hallo-servers in Azure-datacenters worden in clusters gepartitioneerd. Normaal gesproken een toewijzingsaanvraag wordt uitgevoerd in meerdere clusters, maar het is mogelijk dat bepaalde beperkingen van Hallo toewijzingsaanvraag hello Azure-platform tooattempt Hallo aanvraag in slechts één cluster dwingen. In dit artikel verwijzen we toothis als 'vastgemaakt tooa cluster'. Afbeelding 1 hieronder ziet u Hallo geval van een normale toewijzing waartoe in meerdere clusters. Diagram 2 wordt Hallo geval van een toewijzing die is vastgemaakt tooCluster 2 omdat waar Hallo Cloud Service CS_1 of beschikbaarheid set bestaande wordt gehost.
![Diagram van toewijzing](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Waarom toewijzingsfouten gebeuren
Wanneer een aanvraag voor geheugentoewijzing vastgemaakt tooa cluster is, is er een hogere kans van resources vrij voor toofind mislukken omdat Hallo beschikbare resourcegroep kleiner is. Bovendien als uw aanvraag voor geheugentoewijzing vastgemaakt tooa cluster is maar Hallo type resource dat u hebt aangevraagd wordt niet ondersteund door dit cluster, mislukt uw aanvraag zelfs als Hallo cluster resources vrij heeft. Diagram 3 hieronder ziet u Hallo geval waarbij een vastgezette toewijzing mislukt, omdat Hallo alleen candidate cluster geen gratis resources heeft. Diagram 4 wordt Hallo geval waarbij een vastgezette toewijzing mislukt, omdat Hallo alleen candidate cluster biedt geen ondersteuning voor Hallo aangevraagde VM-grootte, hoewel Hallo cluster resources vrij heeft.

![Vastgemaakte geheugentoewijzing is mislukt](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Gedetailleerde stappen specifieke toewijzing in scenario's fouten in het klassieke implementatiemodel Hallo oplossen
Hier vindt u algemene scenario's toewijzing die ertoe leiden een toewijzing aanvraag toobe vastgemaakt dat. We je Duik in elk scenario verderop in dit artikel.

* Formaat van een virtuele machine of virtuele machines of rollen exemplaren tooan bestaande cloudservice toevoegen
* Gedeeltelijk gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
* Volledig gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
* Fasering/productie-implementaties (platform als een service alleen)
* Affiniteitsgroep (VM-/ service nabijheid)
* Virtueel netwerk op basis van affiniteit-groep

Wanneer u een toewijzingsfout ontvangt, kunt u zien of er Hallo scenario's beschreven toepassing tooyour fout. Gebruik Hallo toewijzingsfout geretourneerd door hello Azure-platform tooidentify Hallo betreffende scenario. Als uw aanvraag is vastgemaakt, verwijder een aantal Hallo vastmaken beperkingen tooopen uw aanvraag toomore clusters, waardoor Hallo kans van slagen van de toewijzing.

In het algemeen, zolang het Hallo-fout niet 'hello aangevraagde VM-grootte wordt niet ondersteund' wordt aangegeven, u kunt altijd opnieuw uitvoeren op een later tijdstip voldoende bronnen zijn vrijgemaakt in Hallo cluster tooaccommodate uw aanvraag. Als Hallo probleem dat Hallo aangevraagde VM-grootte wordt niet ondersteund is, kunt u een andere VM-grootte. Anders is de enige optie Hallo tooremove Hallo beperking vastmaken.

Twee algemene scenario's met fouten zijn tooaffinity gerelateerde groepen. In de afgelopen hello, een affiniteitsgroep gebruikte tooprovide dicht tooVMs/service-exemplaren, of het gebruikte tooenable Hallo maken van een virtueel netwerk. Met de Hallo introductie van regionale virtuele netwerken zijn affiniteitsgroepen niet langer vereist toocreate een virtueel netwerk. Met de Hallo vermindering van de netwerklatentie in Azure-infrastructuur, Hallo aanbeveling toouse affiniteitsgroepen voor VM-/ service nabijheid is gewijzigd.

Diagram 5 hieronder toont Hallo taxonomie hello (vastgemaakt) toewijzing scenario's.
![Vastgezette toewijzing taxonomie](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Hallo-fout weergegeven in elk scenario van toewijzing is een korte vorm. Raadpleeg toohello [fout tekenreeks lookup](#Error string lookup) voor gedetailleerde foutberichten.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Scenario van toewijzing: vergroten of verkleinen van een virtuele machine of virtuele machines of rollen exemplaren tooan bestaande cloudservice toevoegen
**Fout**

Upgrade_VMSizeNotSupported of GeneralError

**Oorzaak van het cluster vastmaken**

Een aanvraag tooresize een virtuele machine of een virtuele machine toevoegen of een bestaande cloudservice van rol exemplaar tooan heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de bestaande cloudservice hello toobe. Een nieuwe cloudservice maakt, hello Azure-platform toofind een ander cluster dat is gratis resources of ondersteunt Hallo VM-grootte die u hebt aangevraagd.

**Tijdelijke oplossing**

Als de fout Hallo Upgrade_VMSizeNotSupported *, probeer een andere VM-grootte. Met behulp van een andere VM-grootte kan niet worden gebruikt, maar als het is acceptabel toouse een ander virtueel IP-adres (VIP), maakt u een nieuwe cloud service toohost Hallo van nieuwe virtuele machine als toevoegen Hallo nieuwe cloud service toohello regionaal virtueel netwerk waar hello bestaande virtuele machines worden uitgevoerd. Als uw bestaande cloudservice niet voor een regionaal virtueel netwerk gebruikt wordt, kunt u nog steeds een nieuw virtueel netwerk voor Hallo nieuwe cloudservice maken en vervolgens verbinding uw [bestaande virtuele netwerk toohello nieuw virtueel netwerk](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zie voor meer informatie over [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Als de fout Hallo GeneralError *, is het waarschijnlijk dat Hallo type resource (zoals een bepaalde VM-grootte) wordt ondersteund door het Hallo-cluster, maar Hallo cluster geen gratis resources op Hallo moment heeft. Vergelijkbare toohello bovenstaande scenario Hallo gewenst compute resource bij het maken van een nieuwe cloudservice (Let erop dat de nieuwe cloudservice Hallo toouse een andere VIP heeft) toevoegen en gebruiken van een regionaal virtueel netwerk tooconnect uw cloudservices.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario van toewijzing: gedeeltelijk gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
**Fout**

GeneralError *

**Oorzaak van het cluster vastmaken**

Gedeeltelijke toewijzing is opgeheven betekent dat u (toewijzing ongedaan gemaakt) een of meer, maar niet alle virtuele machines in een cloudservice gestopt. Wanneer u stopt (ongedaan gemaakt) een virtuele machine die is gekoppeld Hallo resources zijn vrijgegeven. Opnieuw starten die gestopt (toewijzing ongedaan gemaakt) VM is daarom een nieuwe aanvraag voor geheugentoewijzing. Opnieuw opstarten van virtuele machines in een gedeeltelijk toewijzing ongedaan is gemaakt van de cloudservice is gelijkwaardig tooadding VMs tooan bestaande cloudservice. Hallo-toewijzingsaanvraag heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de bestaande cloudservice hello toobe. Maken van een andere cloud-service kan hello Azure-platform toofind een ander cluster dat is gratis resource of ondersteunt Hallo VM-grootte die u hebt aangevraagd.

**Tijdelijke oplossing**

Het is acceptabel toouse een andere VIP, delete Hallo gestopt (toewijzing ongedaan gemaakt) VMs (maar houd Hallo gekoppeld schijven) als Hallo VMs teruggestuurd via een andere cloudservice toevoegen. Gebruik een regionaal virtueel netwerk tooconnect uw cloudservices:

* Als uw bestaande cloudservice een regionaal virtueel netwerk gebruikt, gewoon Hallo nieuwe cloud service toohello toevoegen hetzelfde virtuele netwerk.
* Als uw bestaande cloudservice een regionaal virtueel netwerk niet gebruiken biedt, maakt u een nieuw virtueel netwerk voor het nieuwe cloudservice hello, en vervolgens [verbinding maken met uw bestaande virtuele netwerk toohello nieuw virtueel netwerk](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zie voor meer informatie over [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Scenario van toewijzing: volledig gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
**Fout**

GeneralError *

**Oorzaak van het cluster vastmaken**

Volledige toewijzing is opgeheven betekent dat u gestopt (toewijzing opgeheven) alle VM's van een cloudservice. Hallo toewijzing toorestart die deze virtuele machines hebben geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe aanvragen. Een nieuwe cloudservice maakt, hello Azure-platform toofind een ander cluster dat is gratis resources of ondersteunt Hallo VM-grootte die u hebt aangevraagd.

**Tijdelijke oplossing**

Als het acceptabele toouse een andere VIP, delete Hallo oorspronkelijke gestopt (toewijzing ongedaan gemaakt) VMs (maar houd Hallo gekoppeld schijven) en verwijderen van Hallo bijbehorende cloudservice (Hallo gekoppeld compute resources zijn al is vrijgegeven wanneer u gestopt (toewijzing ongedaan gemaakt) Hallo VM's). Maak een nieuwe cloud service tooadd Hallo VM's weer.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Scenario van toewijzing: tijdelijke/productie-implementaties (platform als een service alleen)
**Fout**

New_General * of New_VMSizeNotSupported *

**Oorzaak van het cluster vastmaken**

Hallo staging-implementatie en Hallo productie-implementatie van een cloudservice worden gehost in Hallo hetzelfde cluster. Wanneer u de tweede implementatie Hallo toevoegt, wordt een bijbehorende toewijzingsaanvraag Hallo in hetzelfde cluster die als host fungeert voor de eerste implementatie Hallo Hallo poging.

**Tijdelijke oplossing**

Hallo eerste implementatie en de oorspronkelijke cloudservice Hallo verwijderen en implementeer Hallo cloud-service opnieuw. Deze actie kan de eerste implementatie Hallo terechtkomen in een cluster met onvoldoende resources vrij toofit beide implementaties of in een cluster die ondersteuning biedt voor VM-grootten voor Hallo die u hebt aangevraagd.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Scenario van toewijzing: affiniteitsgroep (VM-/ service nabijheid)
**Fout**

New_General * of New_VMSizeNotSupported *

**Oorzaak van het cluster vastmaken**

Een compute resource toegewezen tooan affiniteitsgroep is gekoppeld tooone cluster. Nieuwe compute resource aanvragen in die groep affiniteit worden geprobeerd in Hallo dezelfde cluster waar Hallo bestaande bronnen worden gehost. Dit geldt of Hallo nieuwe resources zijn gemaakt via een nieuwe cloudservice of een bestaande cloudservice.

**Tijdelijke oplossing**

Als een affiniteitsgroep niet nodig is, gebruikt u een affiniteitsgroep of uw rekenresources te groeperen in meerdere affiniteitsgroepen.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Scenario van toewijzing: virtueel netwerk op basis van affiniteit-groep
**Fout**

New_General * of New_VMSizeNotSupported *

**Oorzaak van het cluster vastmaken**

Voordat de regionale virtuele netwerken zijn geïntroduceerd, zijn vereiste tooassociate een virtueel netwerk met een affiniteitsgroep. Als gevolg hiervan rekenresources in een affiniteitsgroep geplaatst zijn gebonden aan Hallo dezelfde beperkingen, zoals beschreven in Hallo ' scenario van toewijzing: affiniteitsgroep (VM-/ service nabijheid) ' hierboven. Hallo rekenresources zijn gebonden tooone cluster.

**Tijdelijke oplossing**

Als u niet in een affiniteitsgroep hoeft, maakt u een nieuw regionaal virtueel netwerk voor Hallo nieuwe resources die u toevoegen wilt, en vervolgens [verbinding maken met uw bestaande virtuele netwerk toohello nieuw virtueel netwerk](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zie voor meer informatie over [regionale virtuele netwerken](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

U kunt ook [migreren van uw virtuele netwerk op basis van affiniteit-groep tooa regionaal virtueel netwerk](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), en voeg vervolgens Hallo gewenst resources opnieuw toe.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Gedetailleerde probleemoplossing stappen specifieke toewijzing in scenario's fouten in hello Azure Resource Manager-implementatiemodel
Hier vindt u algemene scenario's toewijzing die ertoe leiden een toewijzing aanvraag toobe vastgemaakt dat. We je Duik in elk scenario verderop in dit artikel.

* Formaat van een virtuele machine of virtuele machines of rollen exemplaren tooan bestaande cloudservice toevoegen
* Gedeeltelijk gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
* Volledig gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten

Wanneer u een toewijzingsfout ontvangt, kunt u zien of er Hallo scenario's beschreven toepassing tooyour fout. Gebruik Hallo toewijzingsfout geretourneerd door hello Azure-platform tooidentify Hallo betreffende scenario. Als uw aanvraag vastgemaakt tooan bestaande cluster is, verwijder een aantal Hallo vastmaken beperkingen tooopen uw aanvraag toomore clusters, waardoor Hallo kans van slagen van de toewijzing.

In het algemeen, zolang het Hallo-fout niet 'hello aangevraagde VM-grootte wordt niet ondersteund' wordt aangegeven, u kunt altijd opnieuw uitvoeren op een later tijdstip voldoende bronnen zijn vrijgemaakt in Hallo cluster tooaccommodate uw aanvraag. Als het Hallo-probleem is dat Hallo aangevraagde VM-grootte wordt niet ondersteund, Zie hieronder voor tijdelijke oplossingen.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Scenario van toewijzing: vergroten of verkleinen van een virtuele machine of virtuele machines tooan bestaande beschikbaarheidsset toevoegen
**Fout**

Upgrade_VMSizeNotSupported * of GeneralError *

**Oorzaak van het cluster vastmaken**

Een aanvraag tooresize een virtuele machine of een VM-tooan bestaande beschikbaarheidsset heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de bestaande beschikbaarheidsset hello toobe toevoegen. Een nieuwe beschikbaarheidsset maakt, hello Azure-platform toofind een ander cluster dat is gratis resources of ondersteunt Hallo VM-grootte die u hebt aangevraagd.

**Tijdelijke oplossing**

Als de fout Hallo Upgrade_VMSizeNotSupported *, probeer een andere VM-grootte. Als u met behulp van een andere VM-grootte kan niet worden gebruikt, stopt u alle virtuele machines in de beschikbaarheidsset Hallo. U kunt vervolgens de wijziging van grootte door Hallo van Hallo virtuele machine die wordt toegewezen Hallo VM tooa cluster die ondersteuning biedt voor Hallo gewenste VM-grootte.

Als de fout Hallo GeneralError *, is het waarschijnlijk dat Hallo type resource (zoals een bepaalde VM-grootte) wordt ondersteund door het Hallo-cluster, maar Hallo cluster geen gratis resources op Hallo moment heeft. Als Hallo VM deel van een andere beschikbaarheidsset uitmaken kan, maakt u een nieuwe virtuele machine in een andere beschikbaarheidsset (in Hallo dezelfde regio). Deze nieuwe virtuele machine kan vervolgens worden toegevoegd toohello hetzelfde virtuele netwerk.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario van toewijzing: gedeeltelijk gestopt (toewijzing ongedaan gemaakt) virtuele machines opnieuw opstarten
**Fout**

GeneralError *

**Oorzaak van het cluster vastmaken**

Gedeeltelijke toewijzing is opgeheven betekent dat u (toewijzing ongedaan gemaakt) een of meer gestopt, maar niet alle virtuele machines in een beschikbaarheidsset ingesteld. Wanneer u stopt (ongedaan gemaakt) een virtuele machine die is gekoppeld Hallo resources zijn vrijgegeven. Opnieuw starten die gestopt (toewijzing ongedaan gemaakt) VM is daarom een nieuwe aanvraag voor geheugentoewijzing. Opnieuw opstarten van virtuele machines in een gedeeltelijk toewijzing ongedaan is gemaakt beschikbaarheidsset gelijkwaardige tooadding bestaande beschikbaarheid van virtuele machines tooan ingesteld. Hallo-toewijzingsaanvraag heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de bestaande beschikbaarheidsset hello toobe.

**Tijdelijke oplossing**

Alle virtuele machines in Hallo beschikbaarheidsset voordat opnieuw starten van eerste Hallo stoppen. Dit zorgt ervoor dat er een nieuwe poging van de toewijzing wordt uitgevoerd en dat een nieuw cluster kan worden geselecteerd met de beschikbare capaciteit.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Scenario van toewijzing: opnieuw opstarten volledig gestopt (toewijzing ongedaan gemaakt)
**Fout**

GeneralError *

**Oorzaak van het cluster vastmaken**

Volledige toewijzing is opgeheven betekent dat u gestopt (toewijzing opgeheven) alle VM's in een beschikbaarheidsset. Hallo-toewijzingsaanvraag voor deze virtuele machines heeft betrekking op alle clusters die ondersteuning bieden voor toorestart Hallo gewenste grootte.

**Tijdelijke oplossing**

Selecteer een nieuwe VM-grootte tooallocate. Probeer het later opnieuw als dit niet werkt.

## <a name="error-string-lookup"></a>Fout bij het opzoeken tekenreeks
**New_VMSizeNotSupported***

'Hallo VM grootte (of combinatie van VM-formaten) vereist voor deze implementatie kan niet worden ingericht vanwege beperkingen voor toodeployment-aanvraag. Indien mogelijk, probeer beperkingen, zoals de bindingen van virtueel netwerk, implementatie tooa gehoste service met geen andere implementatie in het meest en implementeren van verschillende affiniteit tooa groep of zonder affiniteitsgroep of probeer andere regio tooa. "

**New_General***

'Toewijzing is mislukt; kan geen toosatisfy beperkingen in de aanvraag. Hallo aangevraagde nieuwe service-implementatie is gebonden tooan affiniteitsgroep, of er een bestaande implementatie onder deze gehoste service is gericht op een virtueel netwerk. Deze omstandigheden Hallo nieuwe implementatie toospecific Azure handtekeningcertificaatsleutel resources. Probeer het later opnieuw of verklein Hallo VM-grootte of rolinstanties. U kunt ook indien mogelijk, verwijderen van de hiervoor genoemde beperkingen Hallo of probeer andere regio tooa implementeren.'

**Upgrade_VMSizeNotSupported***

"Kan geen tooupgrade Hallo-implementatie. Hallo aangevraagde VM-grootte XXX mogelijk niet beschikbaar in Hallo bronnen Hallo bestaande implementatie ondersteunen. Probeer het later opnieuw, probeer met een andere VM-grootte of met minder rolinstanties, of maak een implementatie onder een lege gehoste service met een nieuwe affiniteitsgroep of niets affiniteitsgroep binding."

**GeneralError***

'Hallo-server is een interne fout opgetreden. Probeer het Hallo-aanvraag." Of "Mislukt tooproduce een toewijzing voor de service Hallo".

