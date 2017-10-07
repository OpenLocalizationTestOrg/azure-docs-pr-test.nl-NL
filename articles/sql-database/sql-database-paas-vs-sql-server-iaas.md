---
title: aaaSQL (PaaS) Database vs. SQL Server in de cloud Hallo op virtuele machines (IaaS) | Microsoft Docs
description: 'Meer informatie over welke cloud SQL Server-optie geschikt is voor uw toepassing: Azure SQL (PaaS) Database of SQL Server in het Hallo-cloud op Azure Virtual Machines.'
services: sql-database, virtual-machines
keywords: SQL Server cloud, SQL Server in de cloud hello, PaaS-database, SQL Server, DBaaS cloud
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Kies een SQL Server-cloudoptie: Azure SQL (PaaS) Database of SQL Server op Azure Virtual Machines (IaaS)
Azure heeft twee opties om SQL Server-workloads te hosten in Microsoft Azure:

* [Azure SQL Database](https://azure.microsoft.com/services/sql-database/): een SQL-database systeemeigen toohello cloud, ook wel bekend als een platform als een service (PaaS) database of een database als een service (DBaaS) die is geoptimaliseerd voor ontwikkeling van apps in software as a service (SaaS). Biedt compatibiliteit met de meeste functies van SQL Server. Zie [Wat is PaaS](https://azure.microsoft.com/overview/what-is-paas/) voor meer informatie over PaaS.
* [SQL Server op Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server geïnstalleerd en wordt gehost in Hallo cloud op Windows Server Virtual Machines (VM's) uitgevoerd op Azure, ook wel bekend als een infrastructuur als een service (IaaS).
  SQL Server op Azure Virtual Machines is geoptimaliseerd om bestaande SQL Server-toepassingen te migreren. Alle Hallo versies en edities van SQL Server beschikbaar zijn. Biedt 100% compatibel met SQL Server, waardoor toohost u zo veel databases als nodig en worden uitgevoerd tussen meerdere databases transacties. Biedt volledig beheer voor SQL Server en Windows.

Ontdek hoe elke optie in Hallo Microsoft-gegevensplatform past en ophalen van help overeenkomende Hallo juiste optie tooyour zakelijke vereisten. Of u nu kostenbesparingen of minimaal beheer het belangrijkst vindt, kunt in dit artikel u bepalen welke benadering levert die u het belangrijkst van Hallo zakelijke vereisten.

## <a name="microsofts-data-platform"></a>Gegevensplatform van Microsoft
Een van de eerste dingen toounderstand Hallo in een discussie over Azure ten opzichte van on-premises SQL Server-databases is dat u alles kunt gebruiken. Het gegevensplatform van Microsoft maakt gebruik van SQL Server-technologie en maakt deze beschikbaar op fysieke on-premises machines, privécloudomgevingen, externe gehoste privécloudomgevingen en openbare cloud. SQL Server op virtuele machines van Azure kunt u toomeet unieke en diverse bedrijfsbehoeften door een combinatie van on-premises en de cloud gehoste implementaties terwijl dezelfde set serverproducten, ontwikkelingsprogramma's en kennis over deze met behulp van Hallo omgevingen.

   ![Opties SQL Server cloud: SQL server op IaaS of SaaS-SQL-database in de cloud Hallo.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Zoals u in het diagram hello, elke aanbieding gekenmerkt door Hallo niveau van beheer dat u via Hallo-infrastructuur (op Hallo X-as hebt) en Hallo mate van kostenefficiëntie die wordt bereikt door database niveau consolidatie en automatisering (op Hallo Y-as).

Bij het ontwerpen van een toepassing zijn vier eenvoudige opties beschikbaar voor het hosten van SQL Server-onderdeel van de toepassing hello Hallo:

* SQL Server op niet-gevirtualiseerde fysieke computers
* SQL Server in on-premises gevirtualiseerde machines (privécloud)
* SQL Server in virtuele Azure-machines (openbare cloud van Microsoft)
* Azure SQL-database (openbare cloud van Microsoft)

In de Hallo uit te voeren, leert u SQL Server in de openbare cloud Microsoft hello: Azure SQL Database en SQL Server op Azure Virtual machines. Bovendien verkent u algemene zakelijke motivators om te bepalen welke optie het meest geschikt is voor uw toepassing.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>De Azure SQL Database en SQL Server op Azure Virtual Machines
**Azure SQL Database** is een relationele database-as-a-service (DBaaS) die worden gehost in Azure-cloud die in de branchecategorie Hallo van valt Hallo *Software-as-a-Service (SaaS)* en *Platform as a Service (PaaS)* . [SQL-database](sql-database-technical-overview.md) is gebouwd op gestandaardiseerde hardware en software die eigendom is van, en wordt gehost en beheerd door Microsoft. U kunt rechtstreeks op Hallo-service met behulp van de ingebouwde functies en functionaliteiten ontwikkelen met SQL-Database. Als u SQL-Database, u betalen naar gebruik met opties tooscale omhoog of uit voor meer vermogen zonder onderbrekingen.

**SQL Server op Azure Virtual Machines (VM's)** worden onderverdeeld in de branchecategorie Hallo *Infrastructure-as-a-Service (IaaS)* en kunt u SQL Server toorun binnen een virtuele machine in de cloud Hallo. Vergelijkbare tooSQL Database, het is gebouwd op gestandaardiseerde hardware die eigendom is, gehost en beheerd door Microsoft. Wanneer u SQL Server op een virtuele machine gebruikt, kunt u eenvoudig een bestaande licentie gebruiken, of kunt u een SQL Server-licentie gebruiken die al is opgenomen in een installatiekopie van SQL Server en alleen betalen voor wanneer u deze gebruikt. U kunt ook eenvoudig omhoog/omlaag schalen en onderbreken/hervatten Hallo VM indien nodig.

Over het algemeen zijn deze twee SQL-opties geoptimaliseerd voor verschillende doeleinden:

* **Azure SQL Database** is geoptimaliseerd tooreduce kosten toohello minimum voor het inrichten en beheren van veel databases. Dit vermindert beheerkosten omdat u geen toomanage alle virtuele machines, besturingssysteem of database-software. U hebt geen toomanage upgrades, hoge beschikbaarheid of [back-ups](sql-database-automated-backups.md). In het algemeen Azure SQL Database aanzienlijk verhogen Hallo aantal databases dat wordt beheerd door één IT of ontwikkelingsresource.
* **SQL Server wordt uitgevoerd op Azure Virtual machines** is geoptimaliseerd voor het migreren van bestaande toepassingen tooAzure of het uitbreiden van bestaande on-premises toepassingen toohello cloud in hybride implementaties. Bovendien kunt u SQL Server gebruiken in een virtuele machine toodevelop en testen van traditionele SQL Server-toepassingen. Met SQL Server op Azure Virtual machines hebt u Hallo volledige beheerdersrechten via een toegewezen exemplaar van SQL Server en een cloud-gebaseerde VM. Dit is een ideale keuze als een organisatie al IT resources beschikbaar toomaintain Hallo virtuele machines is. Deze mogelijkheden kunnen u een aangepast systeem tooaddress toobuild de specifieke prestaties en beschikbaarheidsvereisten van uw toepassing.

Hallo volgende tabel geeft een overzicht van de belangrijkste kenmerken Hallo van SQL-Database en SQL Server op Azure Virtual machines:

| **Ideaal voor:** | **Azure SQL Database** | **SQL Server op een virtuele Azure-machine** |
| --- | --- | --- |
|  |Nieuwe in de cloud ontworpen toepassingen met tijdsbeperkingen op het gebied van ontwikkeling en marketing. |Bestaande toepassingen waarvoor snelle migratie toohello cloud met minimale wijzigingen. Snelle ontwikkelings- en scenario's als u niet dat toobuy lokale niet-productieve SQL Server-hardware wilt. |
|  | Teams die ingebouwde hoge beschikbaarheid, herstel na noodgevallen en upgrade nodig voor Hallo-database. |Teams die hoge beschikbaarheid, herstel na noodgevallen en patchen van SQL Server kunnen configureren en beheren. Sommige geleverde geautomatiseerde functies vereenvoudigen dit aanzienlijk. | |
|  | Teams die niet toomanage Hallo onderliggende besturingssysteem en configuratie-instellingen wenst. |U moet een aangepaste omgeving met volledige beheerdersrechten. | |
|  | Databases van van too4 TB of meer databases die kunnen worden [horizontaal of verticaal gepartitioneerd](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) met behulp van een scale-out-patroon. |SQL Server-exemplaren met van too64 TB aan opslag. Hallo-exemplaar kan zo veel databases naar behoefte te ondersteunen. | |
|  | [SaaS-toepassingen (software als een service) ontwikkelen](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Bedrijfs- en hybride toepassingen migreren en ontwikkelen. | |
|  | | |
| **Bronnen:** |U wilt niet tooemploy IT-resources voor configuratie en beheer van de onderliggende infrastructuur, Hallo toofocus op de toepassingslaag Hallo maar wilt. |U hebt een aantal IT-resources voor configuratie en beheer. Sommige geleverde geautomatiseerde functies vereenvoudigen dit aanzienlijk. |
| **Totale eigendomskosten:** |Elimineert hardwarekosten en verlaagt administratieve kosten. |Elimineert hardwarekosten. |
| **Bedrijfscontinuïteit:** |In aanvulling toobuilt in infrastructuurmogelijkheden voor fouttolerantie, biedt Azure SQL Database-functies, zoals [geautomatiseerde back-ups](sql-database-automated-backups.md), [punt In tijd terugzetten](sql-database-recovery-using-backups.md#point-in-time-restore), [geo-herstel](sql-database-recovery-using-backups.md#geo-restore), en [actieve geo-replicatie](sql-database-geo-replication-overview.md) tooincrease zakelijke continuïteit. Zie voor meer informatie [SQL Database business continuity overview](sql-database-business-continuity.md). |Met SQL Server op Azure Virtual Machines kunt u een oplossing met hoge beschikbaarheid en herstel na een noodgeval instellen voor de specifieke behoeften van uw database. Daarmee creëert u een systeem dat is geoptimaliseerd voor uw toepassing. U kunt zelf tests en failovers uitvoeren wanneer dit nodig is. Zie voor meer informatie [High Availability and Disaster Recovery for SQL Server on Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Hybride cloud:** |Uw on-premises toepassing heeft toegang tot gegevens in Azure SQL Database. |Met SQL Server op Azure Virtual machines, kunt u toepassingen die deels in de cloud Hallo en deels on-premises. Bijvoorbeeld, kunt u uw on-premises netwerk en Active Directory-domein toohello cloud via uitbreiden [Azure Virtual Network](../virtual-network/virtual-networks-overview.md). Bovendien kunt u on-premises gegevensbestanden opslaan in Azure Storage met behulp van [SQL Server-gegevensbestanden in Azure](http://msdn.microsoft.com/library/dn385720.aspx). Zie voor meer informatie [inleiding tooSQL Server 2014 hybride Cloud](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Ondersteunt [transactionele replicatie van SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) als een abonnee tooreplicate gegevens. |Volledige ondersteuning voor [transactionele replicatie van SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [AlwaysOn Availability Groups](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services en gegevens voor logboekverzending tooreplicate. Ook worden traditionele SQL Server-back-ups volledig ondersteund. | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Zakelijke redenen om Azure SQL Database of SQL Server op Azure Virtual Machines te kiezen
### <a name="cost"></a>Kosten
Of u nu een startup die geld nodig voor de geld bent of een team in een goedlopend bedrijf met krap budget, beperkte middelen vaak Hallo primaire stuurprogramma is bij het bepalen hoe toohost uw databases. In dit gedeelte vindt u meer informatie over Hallo facturering en Licentieverlening algemeen in Azure met betrekking tot toothese twee opties voor relationele databases: SQL-Database en SQL Server op Azure Virtual machines. U leert ook over het berekenen van de kosten van de totale toepassing hello.

#### <a name="billing-and-licensing-basics"></a>Grondbeginselen facturering en licenties
**SQL-Database** toocustomers als een service, niet met een licentie wordt verkocht.  [SQL Server op Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) wordt verkocht met een licentie waarvoor u per minuut betaalt. Als u een bestaande licentie hebt, kunt u deze ook gebruiken.  

Op dit moment **SQL-Database** is beschikbaar in verschillende Servicelagen, die allemaal per uur worden gefactureerd tegen een vast tarief op basis van Hallo prijscategorie en prestatieniveau serviceniveau u kiest. Bovendien wordt uitgaand internetverkeer in rekening gebracht bij u tegen het reguliere [tarief voor gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/). Hallo Basic, Standard, Premium en Premium RS service lagen zijn ontworpen toodeliver voorspelbare prestaties met meerdere prestatie niveaus toomatch piekvereisten van uw toepassing. U kunt tussen servicecategorieën en prestaties niveaus toomatch die uiteenlopende doorvoer van uw toepassing moet wijzigen. Als uw database hoge transactionele volume en behoeften toosupport veel gelijktijdige gebruikers heeft, raden wij de Premium servicecategorie Hallo. Voor de meest recente informatie Hallo op Hallo huidige ondersteunde servicecategorieën, Zie [Azure SQL Database servicecategorieën](sql-database-service-tiers.md). U kunt ook maken [elastische pools](sql-database-elastic-pool.md) tooshare prestaties resources tussen database-exemplaren.

Met **SQL-Database**, Hallo databasesoftware automatisch geconfigureerd, hersteld en bijgewerkt door Microsoft, waardoor uw beheerkosten. Bovendien kunt u met de [ingebouwde back-up](sql-database-automated-backups.md)mogelijkheden aanzienlijk op kosten besparen, vooral wanneer u een groot aantal databases hebt.

Met **SQL Server op Azure Virtual machines**, kunt u een Hallo platform geleverde SQL Server-installatiekopieën (waaronder een licentie) gebruiken of uw SQL Server-licentie brengen. Hallo op alle ondersteunde versies van SQL Server (2008 R2, 2012, 2014, 2016) en editions (Developer, snelle, Web, Standard, Enterprise) beschikbaar zijn. Bovendien zijn Bring-Your-eigenaar-licentie-versies (BYOL) van Hallo installatiekopieën beschikbaar. Wanneer u hello die Azure installatiekopieën geleverde gebruikt, is Hallo operationele kosten afhankelijk van Hallo VM-grootte en Hallo-editie van SQL Server die u kiest. U betaalt per minuut licentieverlening kosten van SQL Server en Windows Server, samen met de kosten van Azure Storage voor VM-schijven Hallo Hallo ongeacht de VM-grootte of editie van SQL Server. Hallo per minuut facturering optie kunt u SQL Server toouse zolang zonder aanvullende SQL Server-licenties kopen. Als u uw eigen SQL Server-licentie tooAzure brengt, wordt u in rekening gebracht voor Windows Server en alleen kosten voor opslag. Zie voor meer informatie over meenemen van uw eigen licentie [License Mobility through Software Assurance on Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Berekenen van de totale toepassing hello kosten
Wanneer u met een cloudplatform begint, omvat Hallo kosten voor het uitvoeren van uw toepassing hello ontwikkeling en beheerkosten plus servicekosten voor Hallo openbare cloud-platform.

Hier volgt Hallo gedetailleerde kostenberekening voor uw toepassing die wordt uitgevoerd in SQL Database en SQL Server op Azure Virtual machines:

**Als u Azure SQL Database gebruikt:**

*Totale kosten van de toepassing = geminimaliseerde beheerkosten + softwareontwikkelingskosten + servicekosten voor SQL Database*

**Als u SQL Server op VM’s van Azure gebruikt:**

*Totale kosten van de toepassing = uiterst geminimaliseerde softwareontwikkelingskosten + beheerkosten + SQL Server- en Windows Server-licentiekosten + Azure Storage-kosten*

Zie voor meer informatie over prijzen Hallo resources te volgen:

* [Prijzen van SQL Database](https://azure.microsoft.com/pricing/details/sql-database/)
* [Prijzen virtuele machines](https://azure.microsoft.com/pricing/details/virtual-machines/) voor [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) en [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)
* [Azure prijscalculator](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> Er is een kleine subset van functies op SQL Server die niet van toepassing zijn op of niet beschikbaar zijn in SQL Database. Zie [SQL Database Features](sql-database-features.md) (Functies van SDL Database) en [SQL Database Transact-SQL information](sql-database-transact-sql-information.md) (Informatie over SQL Database Transact-SQL) voor meer informatie. Als u een bestaande SQL Server-oplossing toohello cloud verplaatst, Zie [migreren van een SQL Server-database tooAzure SQL-Database](sql-database-cloud-migrate.md). Wanneer u een bestaande lokale SQL Server-toepassing-tooSQL Database migreert, moet u overwegen bijwerken Hallo toepassing tootake gebruik van Hallo-mogelijkheden die cloudservices bieden. Bijvoorbeeld, kunt u overwegen gebruik [Azure Web App Service](https://azure.microsoft.com/services/app-service/web/) of [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) toohost uw toepassing laag tooincrease kosten voordelen.
> 
> 

### <a name="administration"></a>Beheer
Hallo besluit tootransition tooa-cloudservice is voor veel bedrijven, evenals veel over offloading van beheercomplexiteit als deze kosten. Met **SQL-Database**, Microsoft hello onderliggende hardware beheert. Microsoft automatisch gerepliceerd van alle gegevens tooprovide hoge beschikbaarheid, configureert en upgrades Hallo database-software, beheert taakverdeling en voert transparante failover uit als er een serverfout opgetreden. U kunt doorgaan tooadminister uw database, maar u hoeft niet meer toomanage Hallo database-engine, server-besturingssysteem of hardware.  Voorbeelden van items die u kunt doorgaan tooadminister databases en aanmeldingen, index en query afstemmen, en controle en beveiliging omvatten.

Met **SQL Server op Azure Virtual machines**, hebt u volledige controle over het Hallo-besturingssysteem en de configuratie van SQL Server-exemplaar. Met een VM is tooyou toodecide bij het bijwerken van tooupdate Hallo besturingssysteemsoftware van systeem en de database en bij tooinstall aanvullende software zoals antivirus. Sommige geautomatiseerde functies zijn opgegeven toodramatically vereenvoudigen patch, back-up en hoge beschikbaarheid. U kunt bovendien Hallo grootte Hallo VM, het aantal schijven Hallo en hun opslagconfiguraties beheren. Azure kunt u toochange Hallo grootte van een VM indien nodig. Zie voor meer informatie [Virtual Machine en Cloud Service Sizes for Azure](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Service Level Agreement (SLA)
Voor veel IT-afdelingen is het voldoen aan uptimeverplichtingen van een Service Level Agreement (SLA) een topprioriteit. In dit gedeelte kijken we welke SLA van toepassing is tooeach databasehosting-optie.

Voor de **SQL Database**-servicelagen Basic, Standard, Premium en Premium RS biedt Microsoft een beschikbaarheids-SLA van 99,99%. Zie voor de meest recente informatie Hallo [Service Level Agreement](https://azure.microsoft.com/support/legal/sla/sql-database/). Zie voor Hallo meest recente informatie over SQL Database Servicelagen en plannen voor bedrijfscontinuïteit hello wordt ondersteund, [Servicelagen](sql-database-service-tiers.md).

Voor **SQL Server wordt uitgevoerd op Azure Virtual machines**, biedt Microsoft een beschikbaarheids-SLA van 99,95% dat behandelt alleen Hallo virtuele Machine. Deze SLA heeft geen betrekking op Hallo processen (zoals SQL Server) op Hallo VM en vereist dat u ten minste twee VM-exemplaren in een beschikbaarheidsset host. Zie voor de meest recente informatie Hallo Hallo [VM SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Voor database hoge beschikbaarheid (HA) vanuit virtuele machines, configureer een van de opties voor hoge beschikbaarheid hello wordt ondersteund in SQL Server, zoals [AlwaysOn Availability Groups](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Met de optie van een ondersteunde maximale beschikbaarheid biedt een extra SLA niet, maar kunt u tooachieve > 99,99% beschikbaarheid van de database.

### <a name="market"></a>Tijd toomarket
**SQL-Database** is de juiste oplossing Hallo voor de cloud ontworpen toepassingen wanneer productiviteit van ontwikkelaars en snelle tijd op de markt essentieel zijn. Met programmatische DBA-functies is het ideaal voor cloud-architecten en ontwikkelaars zoals deze wordt verlaagd Hallo nodig voor het beheren van het onderliggende besturingssysteem Hallo en database. Bijvoorbeeld, kunt u Hallo [REST-API](http://msdn.microsoft.com/library/azure/dn505719.aspx) en [PowerShell-Cmdlets](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate en beheren van administratieve bewerkingen voor duizenden databases. Functies zoals [elastische pools](sql-database-elastic-pool.md) kunt u toofocus op Hallo toepassingslaag en uw oplossing toohello markt sneller leveren.

**SQL Server wordt uitgevoerd op Azure Virtual machines** is ideaal als uw bestaande of nieuwe toepassingen grote databases, met elkaar verbonden databases vereisen of toegang tooall functies in SQL Server of Windows tot. Het is ook geschikt wanneer u wilt dat toomigrate bestaande lokale toepassingen en databases tooAzure als-is. Aangezien u niet toochange Hallo presentatie-, toepassings- en gegevenslagen hoeft, bespaart u tijd en budget op het opnieuw vormgeven van uw bestaande oplossing. In plaats daarvan kunt u zich richten op het migreren van alle oplossingen-tooAzure en bij het uitvoeren van prestatieoptimalisatie die zijn voor hello Azure-platform vereist mogelijk. Zie voor meer informatie [Best practices prestaties for SQL Server on Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Samenvatting
In dit artikel werden SQL Database en SQL Server op Azure Virtual Machines (VM's) verkend en algemene zakelijke motivators besproken die invloed kunnen hebben op uw beslissing. Hallo Hier volgt een samenvatting van suggesties voor u tooconsider:

Kies voor een **Azure SQL Database** als:

* Bent u nieuwe cloudgebaseerde toepassingen maken tootake profiteren van Hallo kosten besparen en optimalisatie van prestaties die cloudservices bieden. Deze aanpak biedt Hallo voordelen van een volledig beheerde cloudservice, helpt lagere initiële tijd op de markt en kostenoptimalisatie op lange termijn kunt bieden.
* U wilt dat Microsoft toohave uitvoeren van algemene beheertaken uit te voeren op uw databases en vereist betere beschikbaarheids-Sla's voor databases.

Kies voor **SQL Server op Azure VM's** als:

* U hebt bestaande on-premises toepassingen die u toomigrate wilt of toohello cloud uitbreiden, of als u toobuild bedrijfstoepassingen groter is dan 4 TB wilt. Deze aanpak geeft Hallo voordeel van 100% SQL compatibiliteit van grote database capaciteit, volledige controle over SQL Server en Windows en beveiligde tunneling tooon-premises. Deze aanpak minimaliseert de kosten voor ontwikkeling en wijzigingen van bestaande toepassingen.
* U hebt bestaande IT-resources en kunt eigenaar zijn van patchen, back-ups en hoge beschikbaarheid van databases. Houd er rekening mee dat sommige geautomatiseerde functies deze bewerkingen aanzienlijk kunnen vereenvoudigen. 

## <a name="next-steps"></a>Volgende stappen
* Zie [uw eerste Azure SQL Database](sql-database-get-started-portal.md) tooget gestart met de SQL-Database.
* Zie [Prijzen van SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* Zie [een SQL Server-machine inrichten in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget gestart met SQL Server op Azure Virtual machines.

