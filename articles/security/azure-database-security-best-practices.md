---
title: aanbevolen beveiligingsprocedures aaaAzure database | Microsoft Docs
description: In dit artikel biedt een set met aanbevolen procedures voor beveiliging van de Azure-database.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Aanbevolen beveiligingsprocedures voor Azure-database

Beveiliging is een bovenste probleem bij het beheren van databases en is altijd een prioriteit voor Azure SQL Database. Uw databases kunnen worden nauw beveiligde toohelp voldoen aan de meest regelgevende of beveiligingsvereisten, zoals HIPAA, ISO 27001/27002 en PCI DSS-niveau 1, onder andere. Een huidige lijst van naleving veiligheidscertificaten is beschikbaar op Hallo [Microsoft Trust Center site](http://azure.microsoft.com/support/trust-center/services/). U kunt ook uw databases in specifieke Azure-datacenters op basis van de regelgeving tooplace kiezen.

In dit artikel bespreken we een verzameling aanbevolen beveiligingsprocedures voor Azure-database. Deze aanbevolen procedures zijn afgeleid van onze ervaring met beveiliging van de Azure-database en Hallo ervaringen van klanten, zoals zelf.

Voor elke beste kunnen worden uitgelegd:

-   Welke beste Hallo
-   Waarom u wilt dat tooenable die best practices
-   Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
-   Hoe meer u tooenable Hallo best practices

In dit artikel Azure Security Best Practices is gebaseerd op een advies consensus- en mogelijkheden van Azure-platform en functie wordt ingesteld als deze bestaan in Hallo tijd die in dit artikel is geschreven. Adviezen en technologieën op den duur veranderen en dit artikel worden de wijzigingen op een tooreflect regelmatig wordt bijgewerkt.

Azure-database aanbevolen beveiligingsprocedures besproken in dit artikel zijn onder andere:

-   Toegang tot de firewall-regels toorestrict database gebruiken
-   Database-verificatie inschakelen
-   Uw gegevens beschermen met versleuteling
-   De gegevens onderweg te beschermen
-   Databasecontrole inschakelen
-   Detectie van dreigingen database inschakelen


## <a name="use-firewall-rules-toorestrict-database-access"></a>Toegang tot de firewall-regels toorestrict database gebruiken

Microsoft Azure SQL Database levert een relationele-databaseservice voor Azure en andere op internet gebaseerde toepassingen. tooprovide beveiligingsmaatregelen toegang, SQL Database toegang met firewallregels connectiviteit beperken door IP-adres, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatiemechanismen gebruikers toospecific acties en gegevens te beperken. Firewalls verhinderen alle toegang tooyour database-server tot u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toodatabases op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn.

![Firewall-regels](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Hello Azure SQL Database-service is alleen beschikbaar via TCP-poort 1433. tooaccess een SQL-Database van uw computer, zorg ervoor dat de firewall van uw client-computer uitgaande TCP-communicatie op TCP-poort 1433 toestaat. Als u niet nodig is voor andere toepassingen, binnenkomende verbindingen blokkeren op TCP-poort 1433 met behulp van firewallregels.

Als onderdeel van het verbindingsproces hello zijn de verbindingen van virtuele machines in Azure omgeleide tooa verschillende IP-adres en poort, uniek zijn voor elke worker-rol. Hallo-poortnummer is Hallo tussen 11000 too11999 liggen. Zie voor meer informatie over de TCP-poorten, [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database2](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Zie [SQL Database-firewallregels](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) voor meer informatie over de firewallregels in SQL Database.

## <a name="enable-database-authentication"></a>Database-verificatie inschakelen
SQL Database ondersteunt twee typen verificatie, SQL-verificatie en Azure Active Directory-verificatie (verificatie met Azure AD).

**SQL-verificatie** wordt aanbevolen in de volgende gevallen:

-   Kunt u SQL Azure toosupport omgevingen met gemengde besturingssystemen, waarbij niet alle gebruikers worden geverifieerd door een Windows-domein.
-   Kan SQL Azure toosupport oudere toepassingen en toepassingen die worden geleverd door derden waarvoor SQL Server-verificatie.
-   Hiermee kunt gebruikers tooconnect van onbekende of niet-vertrouwde domeinen. Bijvoorbeeld, een toepassing waarin klanten tot stand gebrachte verbinding met maken SQL Server-aanmeldingen tooreceive Hallo status toegewezen van hun orders.
-   Kan SQL Azure toosupport Web gebaseerde toepassingen waar gebruikers hun eigen identiteiten maken.
-   Kan software ontwikkelaars toodistribute hun toepassingen met behulp van een hiërarchie complexe machtiging op basis van SQL Server-aanmeldingen bekend, definitie.

> [!Note]
> SQL Server-verificatie niet Kerberos veiligheidsprotocol echter niet gebruiken.

Als u **SQL-verificatie** moet:

-   Hallo sterke referenties beheren zelf.
-   Hallo-referenties in de verbindingsreeks Hallo beveiligen.
-   Hallo-referenties die zijn doorgegeven via Hallo netwerk uit Hallo Web server toohello-database (potentieel) beveiligen. Zie voor meer informatie [hoe: verbinding maken met de Server met behulp van SQL-verificatie in ASP.NET 2.0 tooSQL](https://msdn.microsoft.com/library/ms998300.aspx).

**Azure Active Directory-verificatie** is een mechanisme voor verbinding te maken met Azure SQL Database tooMicrosoft en [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) met behulp van identiteiten in Azure Active Directory (Azure AD). Azure AD-verificatie, kunt u Hallo identiteiten van databasegebruikers en andere Microsoft-services op één centrale locatie centraal beheren. Centrale ID-beheer biedt één plaats toomanage databasegebruikers en vereenvoudigt het beheer van machtigingen. Voordelen zijn Hallo volgende:

-   Het biedt een alternatieve tooSQL Server-verificatie.
-   Helpt bij het stoppen Hallo verspreiding van gebruikersidentiteiten voor databaseservers.
-   Kan wachtwoord draaien op één plaats.
-   Klanten kunnen met behulp van externe (AAD) groepen databasemachtigingen beheren.
-   Deze kunt wachtwoorden moet opslaan voorkomen door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure Active Directory.
-   Azure AD-verificatie gebruikt ingesloten database gebruikers tooauthenticate identiteiten op Hallo databaseniveau.
-   Azure AD biedt ondersteuning voor verificatie op basis van tokens voor toepassingen die verbinding maken met tooSQL Database.
-   Azure AD-verificatie ondersteunt AD FS (domeinfederatie) of systeemeigen gebruikerswachtwoord verificatie voor een lokale Azure Active Directory zonder Domeinsynchronisatie.
-   Azure AD ondersteunt verbindingen van SQL Server Management Studio die gebruikmaken van Universal verificatie van Active Directory, waaronder de multi-factor Authentication (MFA). MFA sterke verificatie met een bereik van eenvoudige verificatie-opties bevat: telefoonoproep, tekstbericht, smartcards en pincode of mobiele app-melding. Zie voor meer informatie [SSMS ondersteuning voor Azure AD MFA met SQL-Database en SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

Hallo configuratiestappen bevatten Hallo tooconfigure procedures te volgen en gebruiken van Azure Active Directory-verificatie.

-   Maken en Azure AD te vullen.
-   Optioneel: Koppelen of Hallo active directory die is gekoppeld aan uw Azure-abonnement wijzigen.
-   Een Azure Active Directory-beheerder voor Azure SQL-server maken of [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
- De clientcomputers configureren.
-   Ingesloten databasegebruikers in uw database toegewezen tooAzure AD identiteiten maken.
-   Verbinding maken met tooyour database met behulp van Azure AD-identiteiten.

U vindt gedetailleerde informatie over [hier](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Uw gegevens beschermen met versleuteling

[Azure SQL Database transparante gegevensversleuteling (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) beschermt tegen Hallo dreiging van schadelijke activiteiten door te voeren realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogbestanden in rust zonder wijzigingen toohello toepassing vereisen. TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel.

Zelfs wanneer Hallo volledige opslag wordt gecodeerd, is het belangrijk tooalso versleutelen van uw database zelf. Dit is een implementatie van Hallo ingrijpende diepte benadering voor gegevensbescherming. Als u van Azure SQL Database gebruikmaakt en tooprotect gevoelige gegevens zoals creditcard of burgerservicenummers wilt, kunt u databases met FIPS 140-2-gevalideerde 256 bits AES-versleuteling die voldoet aan de vereisten Hallo van veel industrienormen (bijv, HIPAA, coderen PCI).

Het is belangrijk toounderstand dat bestanden te gerelateerde[uitbreiding (BPE) van de buffer](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) worden niet versleuteld wanneer een database worden versleuteld met TDE. Moet u versleuteling op bestandsniveau hulpprogramma's zoals [BitLocker](https://technet.microsoft.com/library/cc732774) of Hallo [Encrypting File System (EFS)](https://technet.microsoft.com/library/cc700811.aspx) gerelateerde bestanden voor de BPE.

Omdat een geautoriseerde gebruiker zoals een beveiligingsbeheerder of een databasebeheerder toegankelijk Hallo gegevens zelfs als het Hallo-database is versleuteld met TDE, moet u ook volgen Hallo aanbevelingen hieronder:

-   SQL-verificatie op databaseniveau Hallo inschakelen.
-   Gebruik Azure AD-verificatie met [RBAC-rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Gebruikers en toepassingen moeten afzonderlijke accounts tooauthenticate gebruiken. Op deze manier kunt u Hallo machtigingen toousers en toepassingen beperken en verminderen het Hallo risico's van schadelijke activiteiten.
-   Beveiliging van de database op gebruikersniveau implementeren met behulp van de vaste databaserollen (zoals db_datareader of db_datawriter), of u kunt maken van aangepaste rollen voor uw toepassing toogrant expliciete machtigingen tooselected databaseobjecten.

Voor andere manieren tooencrypt kunt uw gegevens:

-   [-Celcodering](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt bepaalde kolommen of zelfs cellen van gegevens met verschillende versleutelingssleutels.
-   Versleuteling gebruikt met altijd versleuteld: [altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx) kunnen clients tooencrypt gevoelige gegevens binnen clienttoepassingen en nooit onthullen Hallo versleuteling sleutels toohello Database-Engine (SQL-Database of SQL Server). Als gevolg hiervan altijd versleuteld biedt een scheiding tussen degenen die eigenaar zijn van Hallo gegevens (en het kunnen bekijken) en degenen die Hallo gegevens beheren (maar moet hebben geen toegang).
-   Met behulp van beveiliging: beveiliging op rijniveau kunt klanten toocontrol toegang toorows in een databasetabel op basis van kenmerken Hallo van Hallo gebruiker (bijv, groep lidmaatschap of -uitvoering context) van een query uit te voeren. Zie [Beveiliging op rijniveau](https://msdn.microsoft.com/library/dn765131) voor meer informatie.

## <a name="protect-data-in-transit"></a>De gegevens onderweg te beschermen
Beveiligen van gegevens die onderweg moet essentieel onderdeel van uw strategie voor gegevensbescherming. Omdat de gegevens wordt heen en weer worden verplaatst vanaf verschillende locaties, is algemeen aanbeveling Hallo SSL/TLS-protocollen tooexchange gegevens altijd te gebruiken op verschillende locaties. In sommige gevallen kunt u tooisolate Hallo gehele communicatiekanaal tussen uw on-premises en cloud infrastructuur met behulp van een virtueel particulier netwerk (VPN).

Gegevens verplaatsen tussen uw on-premises infrastructuur en Azure, moet u passende beveiligingsmaatregelen zoals HTTPS- of VPN.

Gebruik voor organisaties die toegang vanuit meerdere werkstations zich lokaal tooAzure toosecure nodig, [Azure site-naar-site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Voor organisaties die toosecure toegang vanaf afzonderlijke werkstations die zich on-premises of buiten het bedrijf tooAzure, kunt u overwegen [punt-naar-Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Grotere gegevenssets kan worden verplaatst via een speciale snelle WAN-verbinding, zoals [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Als u ervoor toouse ExpressRoute kiest, kunt u ook gegevens op het niveau van de toepassing met behulp van Hallo Hallo coderen [SSL/TLS](https://support.microsoft.com/kb/257591) of andere protocollen voor extra beveiliging.

Als u met Azure Storage via hello Azure Portal communiceert, worden alle transacties plaatsvinden via HTTPS. [REST API voor Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS kan ook worden gebruikt toointeract met [Azure Storage](https://azure.microsoft.com/services/storage/) en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).

Organisaties die niet voldoen aan tooprotect gegevens die onderweg zijn vatbaar voor [man-in-the-middle-aanvallen](https://technet.microsoft.com/library/gg195821.aspx), [afgeluisterd](https://technet.microsoft.com/library/gg195641.aspx) en sessiehijacking. Deze aanvallen kunnen Hallo eerste stap bij het krijgen van toegang tot tooconfidential gegevens zijn.

meer informatie over Azure VPN-optie door te lezen Hallo artikel toolearn [Planning en ontwerp voor VPN-Gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Databasecontrole inschakelen
Controle van een exemplaar van SQL Server Database Engine hello of een individuele database omvat het vastleggen van gebeurtenissen die op Hallo Database-Engine plaatsvinden en bij te houden. SQL Server audit maakt u server audits die server audit specificaties voor niveau gebeurtenissen van de server en database audit specificaties voor database niveau gebeurtenissen kunnen bevatten. Controlegebeurtenissen kunnen worden geschreven gebeurtenislogboeken toohello of tooaudit bestanden.

Er zijn verschillende niveaus van controle voor SQL Server, afhankelijk van de overheid of standaarden vereisten voor uw installatie. SQL Server Audit biedt Hallo-hulpprogramma's en processen die u moet tooenable, opslaan en weergeven audits hebben op verschillende server en database-objecten.

[Azure SQL Database Auditing](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) houdt databasegebeurtenissen en schrijft deze tooan controlelogboek in uw Azure Storage-account.

Dankzij controles kunt u zorgen voor naleving van wet- en regelgeving, krijgt u inzicht in de activiteit in uw database en in de afwijkingen en discrepanties die kunnen wijzen op problemen voor het bedrijf of vermoedelijke schendingen van de beveiliging.

Controle kunt en vergemakkelijkt de naleving toocompliance standaarden, maar niet garanderen dat.

toolearn meer over het controleren van de database en hoe tooenable, lees Hallo-artikel [inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Detectie van dreigingen database inschakelen
Detectie van dreigingen SQL kunt u toodetect en toopotential bedreigingen reageren als deze problemen optreden doordat beveiligingswaarschuwingen op vreemde activiteiten worden gedetecteerd. U ontvangt een waarschuwing bij verdachte databaseactiviteiten, mogelijke beveiligingsproblemen en SQL-injectieaanvallen, evenals database afwijkende toegangspatronen. Detectie van dreigingen SQL waarschuwingen Geef details op van de verdachte activiteit en actie voor het beste tooinvestigate en Hallo bedreigingen te verhelpen.

SQL-injectie is bijvoorbeeld een Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen. Aanvallers profiteren van toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing, schendingen veroorzaken of wijzigen van gegevens in Hallo-database.

toolearn over het tooset van detectie van dreigingen voor uw database in Azure portal Zie Hallo [SQL Database met detectie van dreigingen](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Bovendien detectie van dreigingen SQL waarschuwingen met integreert [Azure Security Center](https://azure.microsoft.com/services/security-center/). We nodigen u tootry uit 60 dagen gratis.

meer informatie over de detectie van dreigingen Database toolearn en hoe tooenable, lees Hallo-artikel [inschakelen van controle en detectie van bedreigingen op SQL-servers in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Conclusie
Azure-Database is een databaseplatform robuuste met een volledige reeks beveiligingsfuncties die voldoen aan veel organisatie- en regelgeving nalevingsvereisten. U kunt gegevens beschermen door Hallo fysieke toegang tot tooyour gegevens beheren en het gebruik van een groot aantal opties voor beveiliging van gegevens op het Hallo file-, kolom- of rijniveau met transparante gegevensversleuteling, -Celcodering of beveiliging. Altijd kan versleutelde ook bewerkingen op gecodeerde gegevens van toepassingsupdates hello vereenvoudigen. Op zijn beurt toegang tooauditing logboeken van de activiteit van de SQL-Database biedt u Hallo informatie die u nodig hebt, zodat u tooknow hoe en wanneer gegevens worden geopend.

## <a name="next-steps"></a>Volgende stappen
- toolearn meer informatie over firewallregels, Zie [Firewall-regels](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn over gebruikers en -aanmeldingen, Zie [aanmeldingen beheren](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
