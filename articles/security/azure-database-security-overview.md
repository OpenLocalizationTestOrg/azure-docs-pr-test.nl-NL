---
title: overzicht van de beveiliging aaaAzure database | Microsoft Docs
description: Dit artikel bevat een overzicht van beveiligingsfuncties van hello Azure-database.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Overzicht van Azure-database-beveiliging

Beveiliging is een bovenste probleem bij het beheren van databases en is altijd een prioriteit voor Azure SQL Database. Azure SQL Database ondersteunt de beveiliging van de verbinding met firewall-regels en versleutelde verbinding. Het ondersteunt verificatie met gebruikersnaam en wachtwoord en Azure Active Directory-verificatie met identiteiten die worden beheerd door Azure Active Directory. Autorisatie wordt gebruikt voor toegangsbeheer op basis van rollen.

Azure SQL Database ondersteunt versleuteling door realtime versleuteling en ontsleuteling van databases, gekoppelde back-ups en transactielogboekbestanden in rust zonder wijzigingen toohello toepassing uitvoeren.

Microsoft biedt extra manieren Ondernemingsgegevens tooencrypt:

-   Cel-niveau versleuteling tooencrypt bepaalde kolommen of zelfs cellen van gegevens met verschillende versleutelingssleutels.
-   Als u een Hardware Security Module of Centraal beheer van uw belangrijkste versleuteling-hiërarchie nodig hebt, kunt u overwegen Azure Key Vault met SQL Server in een Azure VM.
-   Altijd versleutelde (momenteel in preview) maakt van versleuteling transparante tooapplications en maakt het clients tooencrypt gevoelige gegevens binnen clienttoepassingen zonder Hallo versleutelingssleutels te delen met SQL-Database.

Azure SQL Database Auditing kunnen ondernemingen toorecord gebeurtenissen tooan audit aanmelding Azure Storage. SQL Database Auditing ook worden geïntegreerd met Microsoft Power BI toofacilitate inzoomen rapporten en analyses.

 Azure SQL-databases kunnen nauw beveiligde toosatisfy meest regelgevende of beveiligingsvereisten, zoals HIPAA, ISO 27001/27002 en PCI DSS-niveau 1, onder andere zijn. Een huidige lijst van naleving veiligheidscertificaten is beschikbaar op Hallo [Microsoft Azure Trust Center site](http://azure.microsoft.com/support/trust-center/services/).

In dit artikel wordt uitgelegd Hallo basisprincipes van beveiliging van Microsoft Azure SQL-Databases voor gestructureerde, in tabelvorm en relationele gegevens. Dit artikel helpt u in het bijzonder om aan de slag te gaan met resources voor gegevensbeveiliging, toegangsbeheer en proactieve controle.

In dit artikel beveiligingsoverzicht van Azure-Database is gericht op Hallo gebieden te volgen:

-   Gegevens beveiligen
-   Toegangsbeheer
-   Proactieve controle
-   Gecentraliseerd beheer
-   Azure Marketplace

## <a name="protect-data"></a>Gegevens beveiligen

SQL-Database beveiligt uw gegevens dankzij de versleuteling van gegevens in beweging met behulp van [Transport Layer Security](https://support.microsoft.com/kb/3135244)voor data-at-rest met [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242), en voor gegevens in het gebruik van gebruik [ Altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx).

We hebben in deze sectie over:

-   Codering in beweging
-   Versleuteling 'at rest'
-   Versleuteling gebruikt (Client)

Voor andere manieren tooencrypt kunt uw gegevens:

-   [-Celcodering](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt bepaalde kolommen of zelfs cellen van gegevens met verschillende versleutelingssleutels.
-   Als u een Hardware Security Module of centraal beheer van uw versleutelingssleutelhiërarchie nodig heeft, kunt u overwegen om [Azure Key Vault met SQL Server in een virtuele Azure-machine](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx) te gebruiken.

### <a name="encryption-in-motion"></a>Codering in beweging

Een veelvoorkomend probleem voor alle client/server-toepassingen is Hallo nodig privacy als gegevens worden verplaatst via openbare en particuliere netwerken. Als gegevens verplaatst via een netwerk is niet versleuteld, is er Hallo kans dat deze kan worden vastgelegd of worden gestolen door onbevoegde gebruikers. Wanneer het omgaan met database-services, moet u ervoor dat de gegevens worden versleuteld tussen Hallo databaseclient en server, evenals tussen database-servers die communiceren met elkaar en met de middelste laag toepassingen toomake.

Een probleem bij het beheren van een netwerk is de beveiliging van gegevens die tussen toepassingen via een niet-vertrouwd netwerk worden verzonden. U kunt [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate servers en clients en gebruik vervolgens tooencrypt berichten tussen Hallo geverifieerde partijen.

Een TLS/SSL-client verzendt een bericht tooa TLS/SSL-server tijdens het verificatieproces Hallo en Hallo server reageert met Hallo-informatie die Hallo-server moet tooauthenticate zelf. Hallo-client en server wisselen daarna sessiesleutels uit en Hallo dialoogvenster-verificatie is beëindigd. Als verificatie is voltooid, wordt SSL beveiligde communicatie kan beginnen tussen Hallo-server en Hallo-client met behulp van Hallo symmetrische versleutelingssleutels die tijdens het Hallo-verificatieproces zijn bepaald.

Alle verbindingen tooAzure SQL-Database versleuteling vereisen (SSL/TLS) op alle tijden als gegevens 'in transit' tooand uit Hallo-database. SQL Azure maakt gebruik van TLS/SSL tooauthenticate servers en clients en gebruik vervolgens tooencrypt berichten tussen Hallo geverifieerde partijen. In de verbindingsreeks van uw toepassing, moet u parameters tooencrypt Hallo verbinding en geen tootrust Hallo-servercertificaat (dit geldt voor u als u de verbindingsreeks buiten Hallo klassieke Azure-Portal kopieert) opgeven, anders Hallo verbinding wordt Hallo-identiteit van Hallo-server niet controleren en is vatbaar te 'man-in-the-middle'-aanvallen. Voor hello ADO.NET stuurprogramma, bijvoorbeeld: deze parameters voor de verbindingsreeks zijn versleutelen = True en TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Versleuteling 'at rest'
U kunt enkele voorzorgsmaatregelen toohelp beveiligde Hallo database zoals ontwerpen van een beveiligde systeem, vertrouwelijk assets coderen en bouwen van een firewall rond Hallo databaseservers nemen. Echter in een scenario waarbij Hallo fysieke media (zoals stations of back-uptapes) worden gestolen, kunt een schadelijke party alleen herstellen of Hallo database koppelen en Hallo gegevens bladeren.

Een oplossing is tooencrypt Hallo gevoelige gegevens in Hallo-database en beveiligt Hallo sleutels die gebruikt tooencrypt Hallo gegevens met een certificaat zijn. Voorkomen dat iemand zonder Hallo sleutels Hallo gegevens gebruiken, maar dit soort bescherming moet worden gepland.

ondersteuning voor dit probleem op door SQL Server en Azure SQL toosolve [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). TDE versleutelt SQL Server en Azure SQL Database-gegevensbestanden, van Versleutelingsgegevens in rust genoemd.

Azure SQL Database transparante gegevensversleuteling beschermt tegen Hallo dreiging van schadelijke activiteiten door realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogboekbestanden in rust in te voeren zonder dat hiervoor wijzigingen nodig toohello toepassing.  

TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel. In SQL-Database is Hallo databaseversleutelingssleutel beveiligd met een ingebouwde servercertificaat. ingebouwde Hallo-servercertificaat is uniek voor elke SQL-Database-server.

Als een database in een GeoDR-relatie is, is het beveiligd door een andere sleutel op elke server. Als twee databases verbonden toohello zijn dezelfde server, delen ze hetzelfde certificaat van de ingebouwde Hallo. Microsoft draait automatisch deze certificaten ten minste om de 90 dagen. Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Versleuteling gebruikt (client)

De meeste gegevens schendingen hebben betrekking op Hallo diefstal van kritieke gegevens, zoals creditcardnummers of persoonsgegevens. Databases kunnen worden rijkdommen vergaren troves van gevoelige informatie. Ze kunnen persoonlijke gegevens, vertrouwelijk gevoelige gegevens en intellectueel eigendom van klanten bevatten. Verloren of gestolen gegevens, vooral klantgegevens kan leiden tot beschadiging van het merk en concurrerende nadeel ernstige boetes, zelfs als deze rechtszaken.

![Altijd versleuteld](./media/azure-databse-security-overview/azure-database-fig1.png)

[Altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx) is een voorziening waarmee tooprotect gevoelige gegevens, zoals creditcardnummers of nationale ID-nummers (bijvoorbeeld Amerikaans sofi-nummer), opgeslagen in Azure SQL Database of SQL Server-databases. Altijd versleutelde kan clients tooencrypt gevoelige gegevens binnen clienttoepassingen en nooit onthullen Hallo versleuteling sleutels toohello Database-Engine (SQL-Database of SQL Server).

Versleutelde biedt altijd een scheiding tussen degenen die eigenaar zijn van Hallo gegevens (en het kunnen bekijken) en degenen die Hallo gegevens beheren (maar moet hebben geen toegang). Doordat de lokale databasebeheerders cloud database operators of andere verhoogde, maar niet-geautoriseerde gebruikers geen toegang tot de gegevens versleuteld hello,

Bovendien wordt altijd versleuteld transparante tooapplications versleuteling. Een stuurprogramma altijd versleuteld ingeschakeld is geïnstalleerd op de clientcomputer hello, zodat automatisch kan versleutelen en ontsleutelen van gevoelige gegevens in de clienttoepassing Hallo. Hallo stuurprogramma versleutelt Hallo-gegevens in gevoelige kolommen voordat deze Hallo gegevens toohello Database-Engine en query's automatisch herschrijft zodat Hallo semantiek toohello toepassing blijven behouden. Op deze manier ontsleutelt Hallo stuurprogramma transparant, opgeslagen gegevens in gecodeerde databasekolommen die zijn opgenomen in de queryresultaten.

## <a name="access-control"></a>Toegangsbeheer
tooprovide beveiligingsmaatregelen, SQL Database toegang met firewallregels connectiviteit beperken door IP-adres, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatiemechanismen gebruikers toospecific acties en gegevens te beperken.

### <a name="database-access"></a>Toegang tot de database

Gegevensbeveiliging begint met het beheren van toegang tot tooyour gegevens. Hallo datacenter die als host fungeert voor uw gegevens beheert fysieke toegang terwijl u een firewall-beveiliging toomanage op Hallo netwerklaag kunt configureren. U kunt ook toegang beheren door aanmeldingen voor verificatie configureren en machtigingen voor server en database-rollen te definiëren.

We hebben in deze sectie over:

-   Firewall en firewallregels
-   Authentication
-   Autorisatie

#### <a name="firewall-and-firewall-rules"></a>Firewall en firewallregels

Microsoft Azure SQL Database levert een relationele-databaseservice voor Azure en andere op internet gebaseerde toepassingen. toohelp uw gegevens beschermen, firewalls te voorkomen dat alle toegang tooyour-databaseserver totdat u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toodatabases op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn. Zie [Overzicht van de firewallregels voor SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) voor meer informatie.

Hallo [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) service is alleen beschikbaar via TCP-poort 1433. tooaccess een SQL-Database van uw computer, zorg ervoor dat de firewall van uw client-computer uitgaande TCP-communicatie op TCP-poort 1433 toestaat. Blokkeer binnenkomende verbindingen op TCP-poort 1433 als u deze niet nodig hebt voor andere toepassingen.

#### <a name="authentication"></a>Authentication

SQL database-verificatie verwijst toohow u uw identiteit bewijzen bij het verbinden van toohello database. SQL Database ondersteunt twee typen verificatie:

-   **SQL-verificatie:** een eenmalige aanmeldingsaccount wordt gemaakt wanneer een logische SQL-exemplaar is gemaakt, aangeroepen Hallo abonnee-Account voor SQL-Database. Dit account maakt verbinding met [SQL Server-verificatie](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (gebruikersnaam en wachtwoord). Dit account is dat een beheerder op Hallo logische server-exemplaar en op alle gebruikersdatabases toothat-exemplaar gekoppeld. Hallo machtigingen Hallo abonnee Account kunnen niet worden beperkt. Er kan slechts één van deze accounts bestaan.
-   **Azure Active Directory-verificatie:** [Azure Active Directory-verificatie](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) is een mechanisme voor verbinding te maken met tooMicrosoft Azure SQL Database en SQL Data Warehouse met behulp van identiteiten in Azure Active Directory ( Azure AD). Dit kunt u toocentrally identiteiten van database-gebruikers beheren.

![Authentication](./media/azure-databse-security-overview/azure-database-fig2.png)

 Voordelen van Azure Active Directory-verificatie zijn:
  - Het biedt een alternatieve tooSQL Server-verificatie.
  - Ook helpt te stoppen Hallo verspreiding van gebruikers-id's tussen de databaseservers & kunt wachtwoord draaien op één plaats.
  - U kunt met behulp van externe (Azure Active Directory) groepen databasemachtigingen beheren.
  - Deze kunt wachtwoorden moet opslaan voorkomen door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure Active Directory.

#### <a name="authorization"></a>Autorisatie
[Autorisatie](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) toowhat verwijst een gebruiker binnen een Azure SQL Database kunt uitvoeren, en dit wordt bepaald door uw gebruikersaccount database [rollidmaatschappen](https://msdn.microsoft.com/library/ms189121) en [op objectniveau machtigingen](https://msdn.microsoft.com/library/ms191291.aspx). Autorisatie is Hallo proces om te bepalen welke beveiligbare bronnen hebben toegang tot een principal en welke bewerkingen zijn toegestaan voor deze resources.

### <a name="application-access"></a>Toegang tot toepassingen

We hebben in deze sectie over:

-   Dynamische gegevensmaskering
-   Beveiliging op rijniveau

#### <a name="dynamic-data-masking"></a>Dynamische gegevensmaskering
Een medewerker van de in het midden van een aanroep van aanroepfuncties door verschillende cijfers van hun sociaal-fiscaal nummer of creditcardnummer kan worden geïdentificeerd, maar die items mag niet volledig zijn gegevens van de klantenservice toohello weergegeven.

Een maskeringsregel kan worden gedefinieerd dat alle maskers maar Hallo vier cijfers van een sofi-nummer of creditcardnummer in de resultatenset Hallo van een query laatste.

![Dynamische gegevensmaskering](./media/azure-databse-security-overview/azure-database-fig3.png)

Als een ander voorbeeld mag een masker relevante gegevens gedefinieerde tooprotect persoonsgegevens (PII) gegevens, zodat een ontwikkelaar productieomgevingen opvragen kan voor het oplossen van problemen regelgeving overtreden.

[SQL Database dynamische-Gegevensmaskering](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) blootstelling van gevoelige gegevens beperkt door het toonon beheerdersmogelijkheden maskeren. Dynamische gegevensmaskering wordt ondersteund voor Hallo V12 versie van Azure SQL Database.

[Dynamische gegevensmaskering](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) helpt voorkomen dat onbevoegde toegang toosensitive gegevens doordat u toodesignate hoeveel Hallo gevoelige gegevens tooreveal met minimale gevolgen voor de toepassingslaag Hallo. Het is een beveiligingsfunctie op basis van beleid dat gevoelige gegevens in de resultatenset Hallo van een query Hallo via aangewezen databasevelden, verbergt tijdens het Hallo-gegevens in Hallo-database wordt niet gewijzigd.


> [!Note]
> Dynamische-gegevensmaskering kan worden geconfigureerd door Hallo Azure Database beheerder, serverbeheerder of officer beveiligingsrollen.

#### <a name="row-level-security"></a>Beveiliging op rijniveau
Een andere algemene beveiligingsvereiste voor multitenant databases is [beveiliging](https://msdn.microsoft.com/library/dn765131.aspx). Deze functie kunt u toocontrol toegang toorows in een databasetabel op basis van kenmerken Hallo van Hallo gebruiker (bijv, groep lidmaatschap of -uitvoering context) van een query uit te voeren.

![-Beveiliging op rijniveau](./media/azure-databse-security-overview/azure-database-fig4.png)

Hallo toegang beperking logica is gevonden in de databaselaag Hallo in plaats van opslag van Hallo-gegevens in een andere toepassingslaag. elke keer dat de toegang tot die gegevens van elke categorie wordt uitgevoerd, past Hallo databasesysteem Hallo toegangsbeperkingen. Dit maakt het beveiligingssysteem betrouwbaarder en robuuste doordat Hallo surface area van het beveiligingssysteem.

Beveiliging op rijniveau introduceert predikaat gebaseerd toegangsbeheer. Biedt een flexibele, gecentraliseerde, op basis van het predikaat evaluatieversie die kan worden uitgevoerd in overweging metagegevens of andere criteria Hallo beheerder bepaalt waar nodig. Hallo-predikaat wordt gebruikt als een criterium toodetermine of Hallo gebruiker Hallo juiste toegang tot toohello gegevens op basis van gebruikerskenmerken heeft of niet. Toegangsbeheer op basis van het label kan worden geïmplementeerd met behulp van toegangsbeheer op basis van een predikaat.

## <a name="proactive-monitoring"></a>Proactieve controle
SQL-Database beveiligt uw gegevens dankzij de **controle** en **bedreigingendetectie** mogelijkheden.

### <a name="auditing"></a>Controleren
SQL Database Auditing, verhoogt de mogelijkheid toogain-inzicht in gebeurtenissen en wijzigingen die binnen Hallo-database plaatsvinden, inclusief updates en query's op Hallo-gegevens.

[Azure SQL Database Auditing](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) houdt databasegebeurtenissen en schrijft deze tooan controlelogboek in uw Azure Storage-account. Dankzij controles kunt u zorgen voor naleving van wet- en regelgeving, krijgt u inzicht in de activiteit in uw database en in de afwijkingen en discrepanties die kunnen wijzen op problemen voor het bedrijf of vermoedelijke schendingen van de beveiliging. Controle kunt en vergemakkelijkt de naleving toocompliance standaarden, maar niet garanderen dat.

SQL Database Auditing, kunt u:

-   **Behouden** een audittrail van de geselecteerde gebeurtenissen. Categorieën van database acties toobe gecontroleerd, kunt u definiëren.
-   **Rapport** op database-activiteit. U kunt vooraf geconfigureerde rapporten en een dashboard tooget snel de slag met de activiteit en rapportage gebruiken.
-   **Analyseren** rapporten. U kunt verdachte gebeurtenissen, ongebruikelijke activiteiten en trends vinden.

Er zijn twee methoden voor controle:

-   **Auditingfunctie voor blobs** -Logboeken geschreven tooAzure Blob Storage. Dit is een nieuwere controle methode, waarbij biedt betere prestaties en rendabeler biedt ondersteuning voor hogere granulatie controlefunctionaliteit op objectniveau.
-   **Controle van de tabel** -Logboeken geschreven tooAzure Table Storage.

### <a name="threat-detection"></a>Detectie van bedreigingen
[Azure SQL Database voor de detectie van dreigingen](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) verdachte activiteiten worden gedetecteerd die duiden op beveiligingsdreigingen. Detectie van dreigingen kunt u toorespond toosuspicious gebeurtenissen in de database hello, zoals SQL-injectie wanneer deze zich voordoen. Het biedt waarschuwingen en staat het Hallo-gebruik van Azure SQL Database Auditing tooexplore Hallo verdachte gebeurtenissen.

![Detectie van dreigingen](./media/azure-databse-security-overview/azure-database-fig5.jpg)

SQL-injectie is bijvoorbeeld een Hallo algemene Web application beveiligingsproblemen op Hallo Internet, gebruikte tooattack gegevensgestuurde toepassingen. Aanvallers profiteren van toepassing beveiligingslekken tooinject schadelijke SQL-instructies in de invoervelden toepassing, schendingen veroorzaken of wijzigen van gegevens in Hallo-database.

-Afdelingen of andere aangewezen beheerders kunnen een onmiddellijke melding over verdachte databaseactiviteiten krijgen wanneer deze zich voordoen. Elke melding vindt u informatie over Hallo verdachte activiteit en wordt aanbevolen hoe toofurther onderzoeken en Hallo bedreiging beperken.        

## <a name="centralized-security-management"></a>Gecentraliseerd beheer

[Azure Security Center](https://azure.microsoft.com/documentation/services/security-center/) helpt u bij het detecteren, voorkomen van en reageren toothreats. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

[Security Center](https://docs.microsoft.com/azure/security-center/security-center-sql-database) helpt u gegevens in SQL-Database beveiligt door te geven inzicht in Hallo beveiliging van uw servers en databases. U kunt met Security Center:

-   Beleid voor versleuteling van de SQL-Database en controle definiëren.
-   Hallo beveiliging van SQL Database-resources bewaken voor al uw abonnementen.
-   Snel identificeren en te verhelpen beveiligingsproblemen.
-   Waarschuwingen van integreren [Azure SQL Database met detectie van dreigingen](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Security Center biedt ondersteuning voor toegang op basis van rollen.

## <a name="azure-marketplace"></a>Azure Marketplace

Hello Azure Marketplace is een online toepassingen en services marketplace waarmee startende en independent software vendors (ISV's) toooffer hun klanten oplossingen tooAzure Hallo wereld.
Hello Azure Marketplace combineert ecosystemen van Microsoft Azure-partner in een enkel uniform platform toobetter fungeren onze klanten en partners. Klik op [hier](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance database-beveiligingsproducten beschikbaar zijn op Azure-marktplaats.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [beveiligen van uw Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Meer informatie over [Azure Security Center en Azure SQL Database-service](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- Zie toolearn meer informatie over de detectie van dreigingen [SQL Database met detectie van dreigingen](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- toolearn meer, Zie [prestaties verbeteren SQL-database](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
