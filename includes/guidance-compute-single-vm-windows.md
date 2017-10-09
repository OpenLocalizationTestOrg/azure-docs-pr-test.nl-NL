In dit artikel bevat een overzicht van een reeks bewezen virtuele Windows-machine (VM) uitgevoerd op Azure, betaalt aandacht tooscalability, beschikbaarheid, beheerbaarheid en beveiliging.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen: [Azure Resource Manager] [ resource-manager-overview] en klassieke. In dit artikel wordt gebruikgemaakt Resource Manager, dat Microsoft aanbeveelt voor nieuwe implementaties.
>
>

Het is geen goed idee om een enkele virtuele machine te gebruiken voor bedrijfskritieke taken, omdat er dan maar één storingspunt is. Implementeer voor hogere beschikbaarheid meerdere virtuele machines in een [beschikbaarheidsset][availability-set]. Zie [Meerdere virtuele machines uitvoeren in Azure][multi-vm] voor meer informatie.

## <a name="architecture-diagram"></a>Architectuurdiagram

Meer bewegende onderdelen dan alleen Hallo VM zelf omvat het inrichten van een virtuele machine in Azure. Er zijn compute-, netwerk- en -elementen.

> Een Visio-document met dit Architectuurdiagram is beschikbaar voor downloaden van Hallo [Microsoft Downloadcentrum][visio-download]. Dit diagram is op Hallo 'Compute - één VM' pagina.
>
>

![[0]][0]

* **Resourcegroep.** Een [*resourcegroep*][resource-manager-overview] is een container die verwante resources bevat. Maak een resource groep toohold Hallo resources voor deze virtuele machine.
* **Virtuele machine**. U kunt een virtuele machine uit een lijst met gepubliceerde afbeeldingen of vanuit een virtuele harde schijf (VHD)-bestand uploaden van Blob-opslag tooAzure inrichten.
* **Besturingssysteemschijf.** Hallo OS-schijf is een VHD die is opgeslagen in [Azure Storage][azure-storage]. Dit betekent dat zelfs als de hostmachine Hallo uitvalt blijft bestaan.
* **Tijdelijke schijf.** Hallo virtuele machine wordt gemaakt met een tijdelijke schijf (Hallo `D:` Windows-station). Deze schijf wordt opgeslagen op een fysiek station op de hostmachine Hallo. De schijf wordt *niet* opgeslagen in Azure Storage en wordt mogelijk verwijderd tijdens opnieuw opstarten en andere gebeurtenissen in de levensduur van de virtuele machine. Gebruik deze schijf alleen voor tijdelijke gegevens, zoals pagina- of wisselbestanden.
* **Gegevensschijven.** Een [gegevensschijf] [ data-disk] is een permanente VHD die wordt gebruikt voor toepassingsgegevens. Gegevensschijven worden opgeslagen in Azure Storage, zoals Hallo OS-schijf.
* **Virtueel netwerk (VNet) en subnet.** Elke virtuele machine in Azure wordt geïmplementeerd in een VNet dat verder wordt onderverdeeld in subnetten.
* **Openbaar IP-adres.** Een openbaar IP-adres is de benodigde toocommunicate Hello VM&mdash;bijvoorbeeld via Extern bureaublad (RDP).
* **Netwerkinterface (NIC)**. Hallo NIC kunt Hallo VM toocommunicate met Hallo virtueel netwerk.
* **Netwerkbeveiligingsgroep (NSG)**. Hallo [NSG] [ nsg] gebruikte tooallow/weigeren verkeer toohello netwerksubnet is. U kunt een NSG koppelen aan een afzonderlijke NIC of aan een subnet. Als u deze aan een subnet koppelen, toepassing hello NSG-regels tooall virtuele machines in dat subnet.
* **Diagnostiek.** Diagnostische logboekregistratie is essentieel voor het beheren van en probleemoplossing Hallo VM.

## <a name="recommendations"></a>Aanbevelingen

van toepassing Hello aanbevelingen voor de meeste scenario's. Volg deze aanbevelingen tenzij er een specifieke vereiste is die iets anders voorschrijft.

### <a name="vm-recommendations"></a>Aanbevelingen voor virtuele machines

Azure biedt veel andere virtuele machine grootten, maar we raden Hallo DS - en GS-serie omdat de grootte van deze machines ondersteunen [Premium-opslag][premium-storage]. Selecteer een machine met een van deze grootten tenzij u een speciale workload hebt, zoals high-performance verwerking. Zie [Grootten voor virtuele machines][virtual-machine-sizes] voor meer informatie.

Als u een bestaande workload tooAzure verplaatst, start met Hallo VM-grootte die het dichtstbijzijnde overeen tooyour Hallo lokale servers. Vervolgens meting Hallo prestaties van uw werkelijke workload met tooCPU, geheugen en schijfruimte i/o-bewerkingen per seconde (IOPS) te respecteren en Hallo grootte aanpassen, indien nodig. Als u meerdere NIC's voor uw virtuele machine vereist, worden op de hoogte dat Hallo kunt u het maximum aantal NIC's een functie van Hallo is [VM-grootte][vm-size-tables].   

Wanneer u Hallo VM en andere resources inricht, moet u een regio opgeven. Kies in het algemeen een regio dichtstbijzijnde tooyour interne gebruikers of klanten. Niet alle VM-grootten kunnen echter niet beschikbaar in alle regio's. Zie voor meer informatie [-services per regio][services-by-region]. toosee een lijst met Hallo VM-grootten beschikbaar in een bepaald gebied Hallo volgende Azure-opdrachtregelinterface (CLI)-opdracht uitvoeren:

```
azure vm sizes --location <location>
```

Zie voor meer informatie over het kiezen van een gepubliceerde VM-installatiekopie [navigeren door en selecteer installatiekopieën van Windows virtuele machines in Azure met Powershell of CLI][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Aanbevelingen voor schijven en opslag

Voor optimale schijfprestaties-i/o, raden wij aan [Premium-opslag][premium-storage], waarmee gegevens worden opgeslagen op Solid-State stations (SSD's). Kosten is gebaseerd op Hallo-grootte van het Hallo-provisioned schijf. IOPS en doorvoerlimieten ook afhankelijk zijn van de schijfgrootte, wanneer u een schijf inricht, moet deze alle drie factoren (capaciteit, IOPS en doorvoer).

Maak afzonderlijke Azure storage-accounts voor elke VM toohold Hallo virtuele harde schijven (VHD's) wordt uitgevoerd in volgorde tooavoid roept Hallo IOPS-limieten voor opslagaccounts.

Voeg een of meer gegevensschijven toe. Wanneer u een nieuwe VHD maakt, is het niet-opgemaakt. Meld u aan bij Hallo VM tooformat Hallo schijf. Als u een groot aantal gegevensschijven hebt, worden op de hoogte van de totale i/o-limieten van het opslagaccount Hallo Hallo. Zie [Schijflimieten voor virtuele machines][vm-disk-limits] voor meer informatie.

Indien mogelijk, kunt u toepassingen installeren op een gegevensschijf, niet de besturingssysteemschijf Hallo. Sommige oudere toepassingen moet echter tooinstall onderdelen op Hallo station C:. In dat geval kunt u [vergroten of verkleinen Hallo OS-schijf] [ resize-os-disk] met behulp van PowerShell.

Maak een afzonderlijke opslagaccount toohold diagnostische logboeken voor de beste prestaties. Een standaardaccount voor lokaal redundante opslag (LRS) is voldoende voor diagnostische logboeken.

### <a name="network-recommendations"></a>Aanbevelingen voor netwerken

Hallo openbaar IP-adres mag dynamische of statische. Hallo standaard is dynamisch.

* Reserve een [statisch IP-adres] [ static-ip] als moet u een vaste IP-adres dat niet verandert &mdash; bijvoorbeeld, als u toocreate moet een A registreren in DNS of IP-adres toobe toegevoegde tooa lijst met veilige moet Hallo.
* U kunt ook een volledig gekwalificeerde domeinnaam (FQDN) voor Hallo IP-adres maken. U kunt vervolgens registreren een [CNAME-record] [ cname-record] in DNS die toohello FQDN-naam. Zie voor meer informatie [maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal][fqdn].

Alle NSG's bevatten een set [standaardregels][nsg-default-rules], met inbegrip van een regel waarmee al het inkomende internetverkeer wordt geblokkeerd. Hallo-standaardregels kunnen niet worden verwijderd, maar andere regels kunnen u deze overschrijven. tooenable internetverkeer, regels maken waarmee binnenkomend verkeer toestaan toospecific poorten &mdash; bijvoorbeeld poort 80 voor HTTP.  

tooenable RDP, een regel voor het NSG waarmee binnenkomend verkeer tooTCP poort 3389 toevoegen.

## <a name="scalability-considerations"></a>Schaalbaarheidsoverwegingen

U kunt een virtuele machine omhoog of omlaag schalen door [Hallo VM-grootte wijzigen](../articles/virtual-machines/windows/sizes.md). twee of meer virtuele machines plaatsen tooscale uit horizontaal in een beschikbaarheidsset achter een load balancer. Zie voor meer informatie [meerdere virtuele machines worden uitgevoerd op Azure voor schaalbaarheid en beschikbaarheid][multi-vm].

## <a name="availability-considerations"></a>Beschikbaarheidsoverwegingen

Implementeer voor hogere beschikbaarheid meerdere virtuele machines in een beschikbaarheidsset. Dit biedt ook een hogere [serviceovereenkomst] [ vm-sla] (SLA).

De virtuele machine kan worden beïnvloed door [gepland onderhoud][planned-maintenance] of [niet-gepland onderhoud][manage-vm-availability]. U kunt [VM opnieuw opstarten logboeken] [ reboot-logs] toodetermine of een virtuele machine opnieuw opstarten is veroorzaakt door een gepland onderhoud.

VHD's worden opgeslagen in [Azure Storage][azure-storage]. Azure Storage wordt gerepliceerd voor duurzaamheid en beschikbaarheid.

tooprotect tegen onbedoeld gegevensverlies tijdens normale bewerkingen (bijvoorbeeld vanwege gebruikersfout), moet u ook punt in tijd back-ups, implementeren [blob-momentopnamen] [ blob-snapshot] of een ander hulpprogramma.

## <a name="manageability-considerations"></a>Beheerbaarheidsoverwegingen

**Resourcegroepen.** Deze share Hallo dezelfde levenscyclus cyclus in resources nauw gekoppeld plaatsen Hallo dezelfde [resourcegroep][resource-manager-overview]. Resourcegroepen kunnen u toodeploy en monitor resources als groep en facturering kosten door resourcegroep samengevouwen. Daarnaast kunt u resources verwijderen als set. Dit is handig voor testimplementaties. Geef resources een betekenisvolle naam. Die maakt het eenvoudiger toolocate een specifieke bron en inzicht in de rol. Zie [Aanbevolen naamgevingsregels voor Azure-resources][naming conventions].

**Diagnostische gegevens van virtuele machines.** Schakel bewaking en diagnostiek in, inclusief metrische basisgegevens over de status, diagnostische logboeken over de infrastructuur en [diagnostische gegevens over opstarten][boot-diagnostics]. Diagnostische gegevens over opstarten kunt u een opstartfout achterhalen of de virtuele machine in een status nonbootable opgehaald. Zie [Controle en diagnose inschakelen][enable-monitoring] voor meer informatie. Gebruik Hallo [Azure logboekverzameling] [ log-collector] extensie toocollect Azure-platform registreert en uploadt u tooAzure opslag.   

Hallo na CLI opdracht maakt gebruik van diagnostische gegevens:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Een virtuele machine stoppen.** Azure maakt onderscheid tussen een 'gestopte' status en een status waarbij de toewijzing is opgeheven. U in rekening worden gebracht wanneer Hallo VM-status is gestopt, maar niet wanneer Hallo VM is toewijzing ongedaan is gemaakt.

Gebruik Hallo CLI opdracht toodeallocate een virtuele machine te volgen:

```
azure vm deallocate <resource-group> <vm-name>
```

Hallo in hello Azure-portal, **stoppen** knop deallocates Hallo VM. Echter, als u via Hallo OS afsluit terwijl u bent aangemeld, hello VM is gestopt, maar *niet* toewijzing opgeheven, zodat u nog steeds gefactureerd.

**Een virtuele machine verwijderen.** Als u een virtuele machine verwijdert, worden Hallo VHD's worden niet verwijderd. Dit betekent dat u veilig Hallo VM zonder gegevensverlies kunt verwijderen. Er worden echter nog steeds kosten in rekening gebracht voor opslag. toodelete hello VHD, verwijder het bestand Hallo van [Blob storage][blob-storage].

tooprevent per ongeluk verwijderen, gebruik een [resource vergrendeling] [ resource-lock] toolock Hallo gehele resourcedatabase groep of vergrendelen afzonderlijke resources, zoals Hallo VM.

## <a name="security-considerations"></a>Beveiligingsoverwegingen

Gebruik [Azure Security Center] [ security-center] tooget een centrale weergave van Hallo beveiligingsstatus van uw Azure-resources. Security Center gecontroleerd mogelijke beveiligingsproblemen en biedt een uitgebreid overzicht van Hallo beveiligingsstatus van uw implementatie. Security Center is per Azure-abonnement geconfigureerd. Inschakelen van gegevensverzameling van beveiliging zoals beschreven in [Security Center gebruiken]. Wanneer gegevensverzameling is ingeschakeld, scant Security Center automatisch alle virtuele machines die zijn gemaakt voor dat abonnement.

**Beheer van de patch.** Indien ingeschakeld, wordt door Security Center controleert of beveiligingsupdates en essentiële updates ontbreken. Gebruik [instellingen voor groepsbeleid] [ group-policy] Hallo VM tooenable automatische updates.

**Anti-malware.** Indien ingeschakeld, wordt door Security Center controleert of de antimalware-software is geïnstalleerd. U kunt ook Security Center tooinstall antimalware-software van binnen hello Azure-portal.

**Bewerkingen.** Gebruik [toegangsbeheer op basis van rollen] [ rbac] (RBAC) toocontrol toegang toohello Azure resources die u implementeert. RBAC kunt u autorisatie rollen toomembers van uw DevOps-team toewijzen. Bijvoorbeeld kunt de rol Lezer Hallo weergeven Azure-resources, maar niet maken, beheren of verwijderen. Sommige rollen zijn specifieke tooparticular Azure resourcetypen. Bijvoorbeeld kunt Hallo Virtual Machine Contributor rol starten of ongedaan gemaakt van een virtuele machine, Hallo administrator-wachtwoord opnieuw instellen, een nieuwe virtuele machine maken, enzovoort. Andere [ingebouwde RBAC-rollen][rbac-roles] die nuttig kunnen zijn voor deze referentiearchitectuur, zijn [DevTest Labs-gebruiker][rbac-devtest] en [Inzender voor netwerken][rbac-network]. Een gebruiker toomultiple rollen kan worden toegewezen en u kunt aangepaste rollen maken voor nog meer afzonderlijke machtigingen.

> [!NOTE]
> RBAC beperkt geen Hallo-acties die een gebruiker aangemeld bij een virtuele machine kunt uitvoeren. Deze machtigingen worden bepaald door Hallo accounttype op Hallo gastbesturingssysteem.   
>
>

tooreset hello lokale administrator-wachtwoord uitvoeren Hallo `vm reset-access` Azure CLI-opdracht.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Gebruik [controlelogboeken] [ audit-logs] toosee acties en andere gebeurtenissen VM-inrichting.

**Versleuteling van gegevens.** Houd rekening met [Azure Disk Encryption] [ disk-encryption] als u nodig hebt tooencrypt hello OS- en gegevensschijven.

## <a name="solution-deployment"></a>Implementatie van de oplossing

Een implementatie voor deze verwijzende architectuur is beschikbaar op [GitHub][github-folder]. Deze bevat een VNet, NSG en een enkele virtuele machine. toodeploy Hallo architectuur, als volgt te werk:

1. Klik hieronder op Hallo met de rechtermuisknop en selecteer ofwel 'koppeling openen in nieuw tabblad' of "Koppeling openen in nieuw venster."  
   [![TooAzure implementeren](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Zodra het Hallo-koppeling is geopend in hello Azure-portal, moet u waarden opgeven voor een aantal Hallo-instellingen:

   * Hallo **resourcegroep** naam is al gedefinieerd in Hallo parameterbestand, dus selecteer **nieuw** en voer `ra-single-vm-rg` in het tekstvak Hallo.
   * Selecteer Hallo regio uit Hallo **locatie** vervolgkeuzelijst.
   * Bewerk niet Hallo **sjabloon basis-Uri** of Hallo **Parameter basis-Uri** tekstvakken.
   * Selecteer **windows** in Hallo **Type besturingssysteem** vervolgkeuzelijst.
   * Bekijk Hallo voorwaarden en bepalingen en klik op Hallo **ik ga akkoord toohello voorwaarden bovengenoemde** selectievakje.
   * Klik op Hallo **aankoop** knop.
3. Wachten op Hallo implementatie toocomplete.
4. Hallo parameterbestanden bevatten een beheerder vastgelegde-gebruikersnaam en wachtwoord en het is raadzaam dat u onmiddellijk beide wijzigen. Klik op de virtuele machine met de naam Hallo `ra-single-vm0 `in hello Azure-portal. Klik vervolgens op **wachtwoord opnieuw instellen** in Hallo **ondersteuning + probleemoplossing** blade. Selecteer **wachtwoord opnieuw instellen** in Hallo **modus** vak vervolgkeuzelijst, selecteer vervolgens een nieuwe **gebruikersnaam** en **wachtwoord**. Klik op Hallo **Update** knop toopersist Hallo nieuwe gebruikersnaam en wachtwoord.

Voor informatie over nieuwe manieren toodeploy deze verwijzen naar architectuur, Zie Hallo Leesmij-bestand in Hallo [richtlijnen één vm][github-folder]] GitHub-map.

## <a name="customize-hello-deployment"></a>Hallo-implementatie aanpassen
Als u de behoeften van uw toochange Hallo implementatie toomatch moet, volgt u de instructies Hallo in Hallo [Leesmij][github-folder].

## <a name="next-steps"></a>Volgende stappen
Implementeer voor hogere beschikbaarheid twee of meer virtuele machines achter een load balancer. Zie [Meerdere virtuele machines uitvoeren in Azure][multi-vm] voor meer informatie.

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Security Center gebruiken]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Architectuur voor eenmalige virtuele Windows-machine in Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
