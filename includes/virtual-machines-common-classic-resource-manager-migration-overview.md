# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund
In dit artikel wordt beschreven hoe we de migratie van infrastructuur als een dienst (IaaS) resources van Hallo klassieke tooResource Manager-implementatiemodel bent inschakelen. U kunt meer lezen over [Azure Resource Manager-functies en voordelen](../articles/azure-resource-manager/resource-group-overview.md). We beschreven hoe tooconnect resources uit Hallo twee implementatiemodellen die naast elkaar worden gebruikt in uw abonnement met behulp van virtueel netwerk-site-naar-site gateways.

## <a name="goal-for-migration"></a>Doel voor de migratie
Resource Manager kunt implementeren van complexe toepassingen via sjablonen, configureert u virtuele machines met behulp van de VM-extensies en opgenomen met het beheer van toegang en labels. Azure Resource Manager bevat schaalbare parallelle implementatie voor virtuele machines in beschikbaarheidssets. Hallo nieuwe implementatiemodel biedt ook levenscyclusbeheer van compute, netwerk en opslag onafhankelijk. Er is ten slotte een focus over het inschakelen van beveiliging standaard met Hallo afdwinging van virtuele machines in een virtueel netwerk.

Bijna alle Hallo functies vanuit het klassieke implementatiemodel Hallo worden ondersteund voor compute, netwerk en opslag in Azure Resource Manager. toobenefit van Hallo nieuwe mogelijkheden in Azure Resource Manager kunt u migreren bestaande implementaties van Hallo klassieke implementatiemodel.

## <a name="supported-resources-for-migration"></a>Ondersteunde bronnen voor migratie
Deze klassieke IaaS-bronnen worden ondersteund tijdens de migratie

* Virtuele machines
* Beschikbaarheidssets
* Cloudservices
* Opslagaccounts
* Virtuele netwerken
* VPN Gateways
* Express Route-Gateways _(in Hallo alleen hetzelfde abonnement als virtueel netwerk)_
* Netwerkbeveiligingsgroepen 
* Routetabellen 
* Gereserveerde IP-adressen 

## <a name="supported-scopes-of-migration"></a>Ondersteunde scopes van de migratie
Er zijn verschillende manieren 4 toocomplete migratie van compute, network en storage-resources. Dit zijn 

* Migratie van virtuele machines (niet in een virtueel netwerk)
* Migratie van virtuele machines (in een virtueel netwerk)
* Opslagmigratie van accounts
* Niet-gekoppelde resources (Netwerkbeveiligingsgroepen, routetabellen & gereserveerde IP's)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migratie van virtuele machines (niet in een virtueel netwerk)
Beveiliging wordt Hallo Resource Manager-implementatiemodel, standaard afgedwongen voor uw toepassingen. Alle virtuele machines moeten toobe in een virtueel netwerk in Hallo Resource Manager-model. Hallo opnieuw opstarten van Azure-platform (`Stop`, `Deallocate`, en `Start`) virtuele machines als onderdeel van de migratie Hallo Hallo. U hebt twee opties voor Hallo virtuele netwerken die Hallo van virtuele Machines worden gemigreerd naar:

* U kunt aanvragen Hallo platform toocreate een nieuw virtueel netwerk en Hallo virtuele machine migreren naar nieuw virtueel netwerk Hallo.
* U kunt Hallo virtuele machine migreren naar een bestaand virtueel netwerk in Resource Manager.

> [!NOTE]
> In dit bereik migratie beide operations management vlak Hallo en Hallo gegevens vlak bewerkingen niet zijn toegestaan voor een bepaalde periode tijdens de migratie Hallo.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migratie van virtuele machines (in een virtueel netwerk)
Voor de meeste configuraties van virtuele machine wordt alleen de metagegevens Hallo migreren tussen Hallo klassieke en het Resource Manager-implementatiemodel hebben. onderliggende virtuele machines worden uitgevoerd op Hallo Hallo dezelfde hardware in Hallo dezelfde netwerk- en Hallo met dezelfde opslag. Hallo management vlak operations kunnen niet worden toegestaan voor een bepaalde periode tijdens de migratie van Hallo. Hallo gegevens vlak blijft echter toowork. Dat wil zeggen, de toepassingen die worden uitgevoerd op virtuele machines (klassiek) komen niet in rekening gebracht uitvaltijd tijdens de migratie Hallo.

Hallo volgende configuraties worden momenteel niet ondersteund. Als ondersteuning wordt toegevoegd in toekomstige hello, een aantal virtuele machines in deze configuratie zich kunnen brengen van uitvaltijd (Ga toewijzing via stoppen en opnieuw opstarten van VM-bewerkingen).

* U hebt meer dan één beschikbaarheidsset in een enkel cloudservice.
* U hebt een of meer beschikbaarheidssets en virtuele machines die zich niet in een beschikbaarheidsset in een enkel cloudservice.

> [!NOTE]
> In dit bereik migratie zijn Hallo management vlak niet toegestaan voor een bepaalde periode tijdens de migratie Hallo. Voor bepaalde configuraties zoals eerder beschreven, gegevens vlak uitval optreedt.
>
>

### <a name="storage-accounts-migration"></a>Opslagmigratie van accounts
tooallow naadloze migratie, kunt u Resource Manager virtuele machines implementeren in een klassieke opslagaccount. Met deze mogelijkheid berekenings- en netwerkbronnen kunnen en onafhankelijk van de storage-accounts moeten worden gemigreerd. Als u via uw virtuele Machines en virtuele netwerken migreren, moet u toomigrate via uw storage-accounts toocomplete Hallo-migratieproces.

> [!NOTE]
> Hallo Resource Manager-implementatiemodel biedt geen Hallo concept van klassieke installatiekopieën en schijven. Wanneer Hallo storage-account gemigreerd, klassieke installatiekopieën is en schijven zijn niet zichtbaar in het Resource Manager-stack Hallo maar Hallo back-ups blijven VHD's in Hallo storage-account.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Niet-gekoppelde resources (Netwerkbeveiligingsgroepen, routetabellen & gereserveerde IP's)
Netwerkbeveiligingsgroepen, routetabellen & gereserveerde IP-adressen die niet zijn gekoppeld tooany virtuele Machines en virtuele netwerken kunnen onafhankelijk worden gemigreerd.

<br>

## <a name="unsupported-features-and-configurations"></a>Niet-ondersteunde functies en configuraties
We ondersteunen momenteel geen bepaalde functies en configuraties. Hallo volgende secties beschrijven onze aanbevelingen omheen.

### <a name="unsupported-features"></a>Niet-ondersteunde functies
Hallo volgende kenmerken worden momenteel niet ondersteund. U kunt deze instellingen desgewenst verwijderen, het Hallo virtuele machines migreren en Hallo-instellingen in de Resource Manager-implementatiemodel Hallo opnieuw inschakelen.

| Resourceprovider | Functie | Aanbeveling |
| --- | --- | --- |
| Compute |Niet-gekoppelde virtuele machine-schijven. | Hallo VHD-blobs achter deze schijven worden ophalen gemigreerd wanneer Hallo Storage-Account wordt gemigreerd |
| Compute |Installatiekopieën van virtuele machines. | Hallo VHD-blobs achter deze schijven worden ophalen gemigreerd wanneer Hallo Storage-Account wordt gemigreerd |
| Netwerk |Eindpunt-ACL's. | Verwijder de eindpunt-ACL's en migratie nogmaals uitvoeren. |
| Netwerk |Virtueel netwerk met zowel de ExpressRoute-Gateway en de VPN-Gateway  | Hallo VPN-Gateway verwijderen vóór de migratie en Hallo VPN-Gateway opnieuw zodra de migratie is voltooid. Meer informatie over [ExpressRoute migratie](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Netwerk |ExpressRoute met autorisatie koppelingen  | Hallo ExpressRoute-circuit toovirtaul netwerkverbinding vóór de migratie verwijderen en vervolgens opnieuw verbinding Hallo maken zodra de migratie is voltooid. Meer informatie over [ExpressRoute migratie](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Netwerk |Application Gateway | Hallo Application Gateway verwijderen vóór de migratie en vervolgens opnieuw maken Hallo Application Gateway zodra de migratie is voltooid. |
| Netwerk |Virtuele netwerken met VNet-Peering. | TooResource Virtual Network Manager migreren en klik vervolgens op hetzelfde niveau. Meer informatie over [VNet-Peering](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Niet-ondersteunde configuraties
Hallo volgende configuraties worden momenteel niet ondersteund.

| Service | Configuratie | Aanbeveling |
| --- | --- | --- |
| Resource Manager |Rollen gebaseerd toegangsbeheer (RBAC) voor klassieke resources |Omdat het Hallo-URI van Hallo resources is gewijzigd na migratie, is het raadzaam dat u van plan bent Hallo RBAC beleidsupdates die moeten worden toohappen na de migratie. |
| Compute |Meerdere subnetten die zijn gekoppeld aan een virtuele machine |Hallo subnet configuratie tooreference alleen subnetten worden bijgewerkt. |
| Compute |Virtuele machines die deel uitmaken van het virtuele netwerk tooa, maar geen een expliciete subnet toegewezen |U kunt Hallo VM desgewenst verwijderen. |
| Compute |Virtuele machines met waarschuwingen, beleid voor automatisch schalen |Hallo migratie doorloopt en deze instellingen worden verwijderd. Het is raadzaam dat u uw omgeving evalueren voordat u de migratie Hallo. U kunt ook Hallo waarschuwingsinstellingen configureren nadat de migratie is voltooid. |
| Compute |XML-VM-extensies (BGInfo-1.*, Visual Studio Debugger Web Deploy en foutopsporing op afstand) |Dit wordt niet ondersteund. Het wordt aanbevolen dat u deze uitbreidingen van Hallo virtuele machine toocontinue migratie verwijderen of wordt automatisch tijdens het migratieproces Hallo worden verwijderd. |
| Compute |Diagnostische gegevens over opstarten met Premium-opslag |Diagnostische gegevens over opstarten functie voor Hallo VMs uitschakelen voordat u doorgaat met de migratie. U kunt diagnostische gegevens over opstarten in het Resource Manager-stack Hallo weer inschakelen nadat Hallo migratie voltooid is. Bovendien moeten blobs die worden gebruikt voor schermafbeelding en seriële logboeken worden verwijderd zodat u niet langer in rekening voor de blobs gebracht worden. |
| Compute |Cloudservices met web/werkrollen |Dit wordt momenteel niet ondersteund. |
| Netwerk |Virtuele netwerken die virtuele machines en web/werkrollen bevatten |Dit wordt momenteel niet ondersteund. |
| Azure App Service |Virtuele netwerken met App Service-omgevingen |Dit wordt momenteel niet ondersteund. |
| Azure HDInsight |Virtuele netwerken die HDInsight services bevatten |Dit wordt momenteel niet ondersteund. |
| Microsoft Dynamics levenscyclus van Services |Virtuele netwerken met virtuele machines die worden beheerd door Dynamics levenscyclus van Services |Dit wordt momenteel niet ondersteund. |
| Azure AD Domain Services |Virtuele netwerken die Azure AD Domain services bevatten |Dit wordt momenteel niet ondersteund. |
| Azure RemoteApp |Virtuele netwerken met Azure RemoteApp-implementaties |Dit wordt momenteel niet ondersteund. |
| Azure API Management |Virtuele netwerken met Azure API Management-implementaties |Dit wordt momenteel niet ondersteund. toomigrate hello IaaS VNET, wijzig Hallo VNET Hallo API Management-implementatie die een geen uitvaltijd-bewerking is. |
| Compute |Azure Security Center-uitbreidingen met een VNET met een VPN-gateway in de doorvoer-verbinding of ExpressRoute-gateway met on-premises DNS-server |Azure Security Center wordt automatisch worden extensies geïnstalleerd op uw virtuele Machines toomonitor hun beveiliging en waarschuwingen worden gegeven. Deze uitbreidingen ophalen meestal automatisch geïnstalleerd als hello Azure Security Center-beleid is ingeschakeld op het Hallo-abonnement. Migratie van de ExpressRoute-gateway wordt momenteel niet ondersteund en VPN-gateways met onderweg connectiviteit verliest lokale toegang. Verwijderen van ExpressRoute gateway of migreren VPN-gateway met onderweg connectiviteit zorgt ervoor dat internet toegang tooVM storage account toobe verloren als u doorgaat met het doorvoeren van Hallo-migratie. Hallo migratie niet worden voortgezet als dit gebeurt als statusblob voor Hallo guest-agent kan niet worden ingevuld. Het verdient toodisable Azure Security Center-beleid op Hallo abonnement drie uur voordat u doorgaat met de migratie. |

