# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regio's en beschikbaarheid voor virtuele machines in Azure
Azure draait in meerdere datacenters Hallo wereld. Deze datacenters worden gegroepeerd in toogeographic regio's, waardoor u flexibiliteit bij het kiezen waar toobuild uw toepassingen. Het is belangrijk toounderstand hoe en waar uw virtuele machines (VM's) in Azure, werken samen met uw opties toomaximize prestaties, beschikbaarheid en redundantie. In dit artikel biedt een overzicht van Hallo beschikbaarheid en redundantie functies van Azure.

## <a name="what-are-azure-regions"></a>Wat zijn Azure-regio's?
U kunt Azure-resources maken in gedefinieerde geografische regio's zoals 'VS-West', 'Noord-Europa' of Zuidoost-Azië. U kunt bekijken Hallo [lijst met regio's en de locaties](https://azure.microsoft.com/regions/). Binnen elke regio bestaan meerdere datacenters tooprovide voor redundantie en beschikbaarheid. Deze aanpak kunt u als u toepassingen toocreate VMs dichtstbijzijnde tooyour gebruikers en toomeet eventuele juridische, compatibiliteit ontwerpen of BTW-doeleinden.

## <a name="special-azure-regions"></a>Speciale Azure-regio's
Azure heeft bepaalde speciale gebieden die u kunt toouse desgewenst tijdens het bouwen van uw toepassingen voor juridische redenen of compatibiliteit. Voorbeelden van dergelijke speciale regio's zijn:

* **VS (overheid) - Virginia** en **VS (overheid) - Iowa**
  * Een fysiek en logisch van netwerken afgeschermd exemplaar van Azure voor de Amerikaanse overheid en zijn partners, bediend door gecontroleerde Amerikaanse staatsburgers. Dit exemplaar beschikt over aanvullende nalevingscertificeringen, zoals [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) en [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Meer informatie over [Azure Government](https://azure.microsoft.com/features/gov/).
* **China - noord** en **China - oost**
  * Deze regio's zijn beschikbaar via een unieke samenwerking tussen Microsoft en 21Vianet, waarbij Microsoft niet rechtstreeks Hallo datacenters onderhouden. Zie meer informatie over [Microsoft Azure in China](http://www.windowsazure.cn/).
* **Duitsland - centraal** en **Duitsland - noordoost**
  * Deze gebieden zijn beschikbaar via een gegevensmodel beheerder waarbij klantgegevens in Duitsland onder het beheer van T-systemen, een bedrijf Deutsche Telekom blijft, fungeert als Hallo Duitse gegevens beheerder.

## <a name="region-pairs"></a>Regioparen
Elke Azure-regio is gekoppeld aan een andere regio binnen Hallo hetzelfde Geografie (zoals Verenigde Staten, Europa of Azië). Deze methode kan voor de replicatie van Hallo van resources, zoals VM-opslag, via een Geografie die moet kans Hallo natuurramp, civiele unrest, stroomstoringen of fysieke netwerkstoringen tegelijk die invloed hebben op beide regio's. Het gebruik van regioparen biedt meer voordelen:

* In geval van een bredere Azure onderbreking Hallo één regio is geplaatst buiten elk paar toohelp Hallo tijd toorestore voor toepassingen beperken. 
* Geplande Azure updates zijn uitgerold toopaired regio's een op een tijd toominimize uitvaltijd en het risico op uitval van toepassing.
* Gegevens tooreside binnen Hallo blijft hetzelfde Geografie als de combinatie van (met uitzondering van Brazilië-Zuid) voor de btw en het recht afdwinging bevoegdheid doeleinden.

Voorbeelden van regioparen zijn:

| Primair | Secundair |
|:--- |:--- |
| VS - west |VS - oost |
| Noord-Europa |West-Europa |
| Zuidoost-Azië |Oost-Azië |

Ziet u Hallo volledige [lijst van regionale paren hier](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Beschikbaarheid van functies
Sommige services of VM-functies zijn alleen beschikbaar in bepaalde regio's, zoals specifieke VM-grootten of opslagtypen. Er zijn ook enkele algemene Azure-services die u geen tooselect een bepaald gebied, zoals hoeft [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), of [Azure DNS](../articles/dns/dns-overview.md). tooassist u bij het ontwerpen van uw toepassingsomgeving, kunt u controleren Hallo [beschikbaarheid van de Azure-services in elke regio](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Opslagbeschikbaarheid
Inzicht in de Azure-regio's en locaties is belangrijk wanneer u de beschikbare opslagruimte replicatieopties voor Hallo overwegen. Afhankelijk van het opslagtype hello zijn er verschillende replicatieopties.

**Azure Managed Disks**
* Lokaal redundante opslag (LRS)
  * Uw gegevens driemaal in Hallo regio waarin u uw opslagaccount hebt gemaakt, gerepliceerd.

**Schijven voor opslag op basis van een account**
* Lokaal redundante opslag (LRS)
  * Uw gegevens driemaal in Hallo regio waarin u uw opslagaccount hebt gemaakt, gerepliceerd.
* Zone-redundante opslag (ZRS)
  * Repliceert uw gegevens driemaal op twee toothree faciliteiten in één regio of tussen twee regio's.
* Geografisch redundante opslag (GRS)
  * Uw gegevens tooa secundaire regio die honderden mijl weg Hallo primaire regio worden gerepliceerd.
* Geografisch redundante opslag met leestoegang (RA-GRS)
  * Uw gegevens tooa secundaire regio, net als bij GRS worden gerepliceerd, maar dan ook biedt alleen-lezentoegang toohello gegevens op de secundaire locatie Hallo.

Hallo bevat volgende tabel een overzicht van Hallo verschillen tussen de opslagtypen replicatie Hallo:

| Replicatiestrategie | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Gegevens worden gerepliceerd bij meerdere faciliteiten. |Nee |Ja |Ja |Ja |
| Gegevens kunnen worden gelezen uit de secundaire locatie Hallo en Hallo primaire locatie. |Nee |Nee |Nee |Ja |
| Het aantal exemplaren van de gegevens op afzonderlijke knooppunten. |3 |3 |6 |6 |

Meer informatie over [Azure Storage-replicatieopties vindt u hier](../articles/storage/common/storage-redundancy.md). Zie voor meer informatie over beheerde schijven [overzicht Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Opslagkosten
Prijzen zijn afhankelijk van het opslagtype Hallo en beschikbaarheid die u selecteert.

**Azure Managed Disks**
* Premium-beheerde schijven zijn Solid-State stations (SSD's) en beheerd standaardschijven worden ondersteund door reguliere draaiende schijven. Zowel Premium en Standard-beheerde schijven worden in rekening gebracht op basis van de capaciteit voor Hallo schijf Hallo ingericht.

**Niet-beheerde schijven**
* Premium-opslag wordt ondersteund door Solid-State stations (SSD's) en wordt in rekening gebracht op basis van het Hallo-capaciteit van Hallo schijf.
* Standard-opslag wordt ondersteund door reguliere draaiende schijven en wordt in rekening gebracht op basis van de capaciteit van Hallo in gebruik en beschikbaarheid van opslag gewenst.
  * Er is een extra kosten gegevensoverdracht met Geo-replicatie voor Hallo bandbreedte voor het repliceren van die gegevens tooanother Azure-regio voor RA-GRS.

Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor informatie over de verschillende opslagtypen Hallo en Beschikbaarheidsopties over prijzen.

## <a name="availability-sets"></a>Beschikbaarheidssets
Een beschikbaarheidsset is een logische groepering van virtuele machines waarmee Azure toounderstand hoe uw toepassing tooprovide voor redundantie en beschikbaarheid wordt gemaakt. Het is raadzaam dat twee of meer virtuele machines worden gemaakt binnen een tooprovide beschikbaarheid instellen voor een maximaal beschikbare toepassingen en toomeet hello [99,95% Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Wanneer het gebruik van één VM [Azure Premium-opslag](../articles/storage/common/storage-premium-storage.md), hello Azure SLA voor gebeurtenissen met niet-gepland onderhoud geldt. 

Een beschikbaarheidsset bestaat uit twee extra groeperingen die bescherming tegen hardwarestoringen en toestaan dat updates toosafely worden toegepast - fault-domeinen (FDs) en domeinen (UDs) bijwerken.

![Conceptuele tekening Hallo update domein en de fout van de configuratie van](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

U kunt meer lezen over hoe toomanage beschikbaarheid van Hallo [virtuele Linux-machines](../articles/virtual-machines/linux/manage-availability.md) of [VM's van Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Foutdomeinen
Een domein met fouten is een logische groep van de onderliggende hardware die een gemeenschappelijke stroombron delen en netwerkswitch, vergelijkbare tooa rack binnen een on-premises datacenter. Bij het maken van virtuele machines binnen een beschikbaarheidsset verdeelt hello Azure-platform uw virtuele machines automatisch over deze domeinen met fouten. Deze aanpak beperkt Hallo impact van mogelijke problemen met de fysieke hardware, netwerkstoringen of power onderbrekingen.

### <a name="update-domains"></a>Updatedomeinen
Een updatedomein is een logische groep van de onderliggende hardware die onderhoud kan ondergaan of opnieuw worden opgestart op Hallo hetzelfde moment. Bij het maken van virtuele machines binnen een beschikbaarheidsset hello Azure-platform automatisch distributie van uw virtuele machines over deze domeinen bijwerken. Deze aanpak zorgt ervoor dat ten minste één exemplaar van uw toepassing wordt altijd hello Azure-platform ondergaat periodiek onderhoud worden uitgevoerd. Hallo-volgorde van update-domeinen opnieuw wordt opgestart kan niet worden voortgezet sequentieel tijdens gepland onderhoud, maar slechts één updatedomein wordt opnieuw opgestart tegelijk.

### <a name="managed-disk-fault-domains"></a>Domeinen met fouten schijf beheerd
Voor virtuele machines die gebruikmaken van [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md) en deel uitmaken van een beheerde beschikbaarheidsset, worden de virtuele machines afgestemd op Managed Disk-foutdomeinen. Deze uitlijning zorgt ervoor dat alle beheerde schijven gekoppelde tooa VM binnen Hallo Hallo hetzelfde foutdomein van beheerde schijven. In een beheerde beschikbaarheidsset kunnen alleen virtuele machines met beheerde schijven worden gemaakt. Hallo aantal foutdomeinen beheerde schijven, varieert per regio - twee of drie beheerde schijven domeinen met fouten per regio.

![Foutdomeinen voor beheerde schijven](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> het aantal foutdomeinen voor beheerde beschikbaarheidssets Hallo varieert per regio - twee of drie per regio. Hallo bevat volgende tabel Hallo nummer per regio

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Volgende stappen
U kunt nu gestart toouse deze beschikbaarheid en redundantie functies toobuild uw Azure-omgeving. Zie voor informatie over aanbevolen procedures de [aanbevolen procedures voor Azure-beschikbaarheid](../articles/best-practices-availability-checklist.md).

