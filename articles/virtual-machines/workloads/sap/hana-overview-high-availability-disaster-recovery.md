---
title: Hoge beschikbaarheid en herstel na noodgevallen van SAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Tot stand brengen voor hoge beschikbaarheid en plan voor herstel na noodgevallen van SAP HANA in Azure (grote exemplaren).
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f95e944fc3ec3a831d97386443eb644420ae54dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen in Azure 

Hoge beschikbaarheid en herstel na noodgevallen zijn belangrijke aspecten van uw bedrijfskritieke SAP HANA worden uitgevoerd op Azure (grote exemplaren)-servers. Het is belangrijk om te werken met SAP, uw system integrator of Microsoft goed ontwerpen en implementeren van de strategie rechts high-availability/herstel na noodgevallen. Het is ook belangrijk dat u rekening houden met het beoogde herstelpunt en het beoogde hersteltijd, die specifiek voor uw omgeving zijn.

## <a name="high-availability"></a>Hoge beschikbaarheid

Microsoft ondersteunt SAP HANA hoge beschikbaarheid methoden 'out van het vak' waaronder:

- **Storage-replicatie:** het opslagsysteem mogelijkheid om alle gegevens te repliceren naar een andere locatie (binnen of gescheiden van hetzelfde datacenter). SAP HANA werkt onafhankelijk van deze methode.
- **HANA system replication:** de replicatie van alle gegevens in SAP HANA naar een afzonderlijke SAP HANA-systeem. De beoogde hersteltijd wordt geminimaliseerd door middel van gegevensreplicatie met regelmatige tussenpozen. SAP HANA biedt ondersteuning voor asynchrone, synchrone in het geheugen en synchrone modus (alleen aanbevolen voor SAP HANA-systemen die binnen de hetzelfde datacenter of minder dan 100 KM elkaar). In het huidige ontwerp HANA grote exemplaar stempels kan HANA system replicatie voor hoge beschikbaarheid alleen worden gebruikt.
- **Automatische failover hosten:** een lokale fout--hersteloplossing te gebruiken als alternatief voor systeem-replicatie. Wanneer het hoofdknooppunt niet meer beschikbaar is, een of meer stand-by SAP HANA-knooppunten zijn geconfigureerd in de modus voor scale-out en SAP HANA automatisch wordt overgenomen door een ander knooppunt.

Zie de volgende SAP-informatie voor meer informatie over hoge beschikbaarheid voor SAP HANA:

- [Technisch document SAP HANA hoge beschikbaarheid](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [Handleiding voor SAP HANA-beheer](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP Academy Video voor SAP HANA System replicatie](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP-notitie ondersteuning #1999880: veelgestelde vragen over SAP HANA System Replication](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP-ondersteuning Opmerking #2165547 – SAP HANA back-up en herstel binnen replicatieomgeving voor SAP HANA-systeem](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP-notitie ondersteuning #1984882 – met SAP HANA System replicatie voor Hardware-uitwisseling met minimale/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Herstel na noodgevallen

SAP HANA in Azure (grote exemplaren) wordt aangeboden in twee Azure-regio's in een geopolitieke regio. Is een rechtstreekse netwerkverbinding voor het repliceren van gegevens tijdens herstel na noodgevallen tussen de twee grote exemplaar stempels van twee verschillende regio's. De replicatie van de gegevens is opslaginfrastructuur gebaseerd. De replicatie is niet standaard uitgevoerd. Het is voltooid voor de klant-configuraties die besteld het herstel na noodgevallen. In het huidige ontwerp kan niet HANA system replicatie worden gebruikt voor herstel na noodgevallen.

Om te profiteren van het herstel na noodgevallen, moet u echter de netwerkverbinding met twee verschillende Azure-regio's ontwerpt. Om dit te doen, moet u een Azure ExpressRoute-circuit-verbinding van on-premises in uw Azure-regio en een andere circuit verbinding vanaf on-premises voor uw regio herstel na noodgevallen. Deze meting bevat gewoonlijk een situatie waarin een volledige Azure-regio, met inbegrip van een locatie van Microsoft enterprise edge router (MSEE) een probleem heeft.

Als een tweede maat, kunt u alle virtuele Azure-netwerken die verbinding met de SAP HANA in Azure (grote exemplaren maken) in een van de regio's tot zowel de ExpressRoute-circuits. Deze meting heeft betrekking op een aanvraag waarin slechts één van de MSEE-locaties die uw on-premises locatie met Azure verbindt niet actief gaat.

De volgende afbeelding ziet u de optimale configuratie voor herstel na noodgevallen:

![Optimale configuratie voor herstel na noodgevallen](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

De optimale aanvraag voor een configuratie voor herstel na noodgevallen van het netwerk is om twee ExpressRoute-circuits on-premises naar twee verschillende Azure-regio's. Een circuit gaat naar regio #1, met een exemplaar van de productie. Het tweede ExpressRoute-circuit gaat naar regio #2 sommige exemplaren van niet-productieve HANA uitgevoerd. (Dit is belangrijk als een volledige Azure-regio, inclusief de MSEE en grote exemplaar stempel, gaat het raster uit).

Als een tweede maat, worden de verschillende virtuele netwerken zijn verbonden met de verschillende ExpressRoute-circuits die zijn verbonden met een SAP HANA in Azure (grote exemplaren). U kunt de locatie waar een MSEE is mislukt, of kunt u het beoogde herstelpunt voor herstel na noodgevallen, verlagen overslaan als we later bespreken.

De volgende vereisten voor een installatie met herstel na noodgevallen zijn:

- U moet SAP HANA order niet uitvoeren op Azure (grote exemplaren) SKU's van dezelfde grootte hebben als uw productie-SKU's en deze implementeren in de regio van het herstel na noodgevallen. Deze instanties kunnen worden gebruikt om test, sandbox of QA HANA exemplaren.
- Voor elk van uw SAP HANA op Azure (grote exemplaren)-SKU's die u wilt herstellen in de site herstel na noodgevallen, indien nodig moet u een profiel voor herstel na noodgevallen rangschikken. Deze bewerking leidt tot de toewijzing van opslagvolumes die het doel van de storage-replicatie van uw productieregio in de regio voor herstel na noodgevallen.

Nadat u aan de bovenstaande vereisten voldoet, is uw verantwoordelijkheid om de storage-replicatie start. De basis van de storage-replicatie is in de opslaginfrastructuur die gebruikt voor SAP HANA in Azure (grote exemplaren), opslag-momentopnamen. U moet uitvoeren voor het starten van de replicatie van herstel na noodgevallen:

- Een momentopname van de opstartinstallatiekopie LUN, zoals eerder beschreven.
- Een momentopname van de volumes HANA-gerelateerde, zoals eerder beschreven.

Nadat u deze momentopnamen worden uitgevoerd, wordt een eerste replica van de volumes seeding op volumes die gekoppeld aan uw profiel herstel na noodgevallen in het gebied van herstel na noodgevallen zijn.

De meest recente opslag momentopname wordt elk uur vervolgens gebruikt voor replicatie van de delta's die op de opslagvolumes ontwikkelen.

Het beoogde herstelpunt dat wordt gerealiseerd met deze configuratie ligt tussen 60 en 90 minuten. Om te zorgen voor een betere beoogde herstelpunt in het geval van herstel na noodgevallen, de HANA transactielogboekback-ups van SAP HANA in Azure (grote exemplaren) te kopiëren naar de andere Azure-regio. Als u wilt bereiken deze beoogd herstelpunt, het volgende doen:

1. Meld u zo vaak mogelijk /hana/log/backup back-up van de transactie HANA.
2. Kopieer de transactielogboekback-ups wanneer ze klaar zijn met een Azure virtuele machine (VM), dat zich bevindt in een virtueel netwerk dat verbonden met de SAP HANA op Azure (grote exemplaren)-server zijn.
3. Kopieer de back-up naar een virtuele machine die zich in een virtueel netwerk in het gebied van herstel na noodgevallen van die VM.
4. De transactie logboekback-ups in deze regio in de virtuele machine behouden.

In noodgevallen nadat het herstel na noodgevallen-profiel is geïmplementeerd op een werkelijke-server, de transactielogboekback-ups van de virtuele machine kopiëren naar de SAP HANA in Azure (grote exemplaren), die nu de primaire server in de regio van het herstel na noodgevallen en herstellen die back-ups. Dit herstel is mogelijk omdat de status van HANA op de schijven voor herstel na noodgevallen die van een momentopname HANA. Dit is de offset voor verdere herstelprocedures van transactielogboekback-ups.

## <a name="backup-and-restore"></a>Back-ups en herstellen

Een van de belangrijkste aspecten van de operationele databases brengen ervoor dat de database van verschillende onherstelbare gebeurtenissen kan worden beveiligd. Deze gebeurtenissen kunnen zijn veroorzaakt door alles van natuurramp eenvoudig fouten.

Back-ups van een database met de mogelijkheid om het te herstellen naar een willekeurig punt in tijd (zoals voordat iemand kritieke gegevens verwijderd), kunt u herstellen naar een status die zo dicht mogelijk bij de manier waarop deze was voordat de onderbreking is opgetreden.

Twee soorten back-ups moeten worden uitgevoerd voor de beste resultaten:

- Databaseback-ups
- Transactielogboekback-ups

Naast volledige databaseback-ups op niveau van een toepassing wordt uitgevoerd, kunt u altijd zelfs uitgebreider door het uitvoeren van back-ups met de opslag-momentopnamen. Logboekback-ups uitvoeren, is ook belangrijk voor het herstellen van de database (en om de logboeken van al leeg doorgevoerd transacties).

SAP HANA in Azure (grote exemplaren) biedt twee opties voor back-up en herstel:

- Hiervoor zelf (DIY). Nadat u berekenen zodat er voldoende schijfruimte is, voert u de volledige database en logboekbestanden back-ups met behulp van back-methoden van de schijf (om deze schijven). Na verloop van tijd de back-ups worden gekopieerd naar een Azure storage-account (na het instellen van een Azure-bestandsserver met vrijwel onbeperkte opslag) of een Azure Backup-kluis of Azure koude opslag gebruiken. Een andere optie is het gebruik van een hulpprogramma van derden gegevens beveiliging, zoals Commvault, voor het opslaan van de back-ups nadat ze zijn gekopieerd naar een opslagaccount. De optie voor ZELFOPLOSSING back-up kan ook zijn nodig voor gegevens die moeten worden bewaard gedurende langere perioden voor compliancy en controledoeleinden.
- Gebruik de back-up en herstel van functionaliteit die de onderliggende infrastructuur van SAP HANA in Azure (grote exemplaren) biedt. Deze optie wordt voldaan aan de noodzaak van back-ups en maakt handmatige back-ups bijna verouderd (met uitzondering van gegevensback-ups indien noodzakelijk zijn voor naleving zijn). De rest van deze sectie heeft betrekking op de back-up en herstel functionaliteit die wordt aangeboden met HANA (grote exemplaren).

> [!NOTE]
> De momentopnametechnologie die wordt gebruikt door de onderliggende infrastructuur van HANA (grote exemplaren) heeft een afhankelijkheid voor SAP HANA-momentopnamen. SAP HANA momentopnamen werken niet in combinatie met SAP HANA Multitenant Database Containers. Deze methode van back-up kan niet als gevolg hiervan worden gebruikt voor het implementeren van Containers voor SAP HANA Multitenant-Database.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Met behulp van opslag-momentopnamen van SAP HANA in Azure (grote exemplaren)

De infrastructuur van de onderliggende SAP HANA in Azure (grote exemplaren) ondersteunt het principe van een momentopname van de opslag van volumes. Zowel back-up en herstel van een bepaald volume worden ondersteund met de volgende overwegingen:

- In plaats van de databaseback-ups, worden opslag volume momentopnamen regelmatig.
- De momentopname van de opslag initieert een momentopname van een SAP HANA voordat deze de momentopname van de opslag wordt uitgevoerd. Deze momentopname met de SAP HANA is de installatie voor uiteindelijke logboek herstelbewerkingen kunnen na het herstel van de momentopname van de opslag.
- Op het punt waar de opslag-momentopnamen met succes is uitgevoerd, wordt de momentopname SAP HANA verwijderd.
- Logboekback-ups zijn vaak gemaakt en opgeslagen in het logboek-back-volume of in Azure.
- Als de database moet worden hersteld naar een bepaald punt in tijd, een aanvraag wordt gedaan aan Microsoft Azure-ondersteuning (productie uitval) of SAP HANA op Azure-servicebeheer om te zetten op een bepaalde opslag-momentopnamen (bijvoorbeeld een geplande herstel van een sandbox voor de oorspronkelijke status).
- De SAP HANA-momentopname die opgenomen in de opslag momentopname is een offset punt voor het toepassen van logboekback-ups die zijn uitgevoerd en opgeslagen nadat de momentopname van de opslag is gemaakt.
- Deze logboekback-ups worden gemaakt op de database herstellen naar een bepaald punt in tijd.

Het opgeven van de back-up\_naam maakt een momentopname van de volgende volumes:

- Hana/gegevens
- Hana/logboek
- Hana/log\_back-up (gekoppeld als back-up in hana/logboek)
- Hana/gedeeld

### <a name="storage-snapshot-considerations"></a>Overwegingen met betrekking tot opslag-momentopnamen

>[!NOTE]
>Opslag-momentopnamen zijn _niet_ opgegeven gratis, omdat u extra opslagruimte moet worden toegewezen.

Het specifieke mechanisme van opslag-momentopnamen voor SAP HANA in Azure (grote exemplaren) zijn onder andere:

- Een momentopname van een bepaalde opslag (op het punt in tijd waarop deze is gemaakt) verbruikt weinig opslag.
- Als gegevens inhoud wordt gewijzigd en de inhoud van bestanden op het opslagvolume wijzigen SAP HANA-gegevens, moet de momentopname voor het opslaan van de oorspronkelijke inhoud blokkeren.
- De momentopname van de opslag wordt vergroot. Hoe langer de momentopname bestaat, hoe groter de momentopname van de opslag wordt.
- De meer wijzigingen zijn aangebracht aan het volume SAP HANA-database gedurende de levensduur van een momentopname opslag, hoe groter het verbruik van de ruimte van de momentopname van de opslag wordt.

SAP HANA in Azure (grote exemplaren) wordt geleverd met grootten voor het volume van gegevens en logboekbestanden SAP HANA vast volume. Uitvoeren van momentopnamen van de volumes eats in de ruimte op volume zodat de tekst zelf verantwoordelijk voor het plannen van opslag-momentopnamen (binnen de SAP HANA op Azure [grote exemplaren]-proces).

De volgende secties bevatten informatie voor het uitvoeren van deze momentopnamen, waaronder algemene aanbevelingen:

- Hoewel de hardware 255 momentopnamen per volume tolereren kan, wordt ten zeerste aanbevolen ruim onder dit nummer te blijven.
- Voordat u opslag-momentopnamen uitvoert, bewaken en bijhouden vrije ruimte.
- Verlaag het aantal momentopnamen van opslag op basis van de vrije ruimte. Mogelijk moet u het aantal momentopnamen die u bijhoudt, of moet u mogelijk de volumes uit te breiden. (U kunt extra opslagruimte bestellen in eenheden van 1 TB.)
- Tijdens de activiteiten zoals het verplaatsen van gegevens in SAP HANA met systeem hulpprogramma's voor migratie (R3load of door te SAP HANA-databases herstellen vanuit back-ups), raden we u alle opslag-momentopnamen niet uitvoeren. (Als de migratie van een systeem is op een nieuw SAP HANA-systeem wordt gedaan, opslag-momentopnamen zou niet moeten worden uitgevoerd.)
- Tijdens de grotere reorganisaties SAP HANA-tabellen, moeten de opslag-momentopnamen indien mogelijk worden vermeden.
- Opslag-momentopnamen zijn vereist voor de mogelijkheden voor herstel na noodgevallen van SAP HANA in Azure (grote exemplaren) bezighouden.

### <a name="setting-up-storage-snapshots"></a>Instellen van opslag-momentopnamen

1. Zorg ervoor dat Perl is geïnstalleerd in de Linux-besturingssysteem op de server HANA (grote exemplaren).
2. Wijzig/etc/ssh/ssh\_config voor toevoegen van de regel _MACs hmac-sha1_.
3. Maak een back-up SAP HANA-gebruikersaccount op het hoofdknooppunt voor elk SAP HANA-exemplaar dat u uitvoert (indien van toepassing).
4. De client SAP HANA HDB moet worden geïnstalleerd op alle servers voor SAP HANA (grote exemplaren).
5. Op de eerste server voor SAP HANA (grote exemplaren) van elke regio moet een openbare sleutel voor toegang tot de onderliggende opslaginfrastructuur die het maken van momentopnamen bepaalt worden gemaakt.
6. Kopieer het script azure\_hana\_backup.pl van/scripts naar de locatie van **hdbsql** van de SAP HANA-installatie.
7. Kopieer het bestand HANABackupDetails.txt uit/scripts naar dezelfde locatie als het Perl-script.
8. Het wijzigen van het bestand HANABackupDetails.txt die nodig zijn voor de gewenste klant-specificaties.

### <a name="step-1-install-sap-hana-hdbclient"></a>Stap 1: SAP HANA HDBClient installeren

De Linux is geïnstalleerd op een SAP HANA in Azure (grote exemplaren) omvat de mappen en scripts nodig zijn voor het uitvoeren van SAP HANA-opslag-momentopnamen voor back-up en herstel na noodgevallen. Het is echter zelf verantwoordelijk voor SAP HANA HDBclient installeren tijdens de installatie van SAP HANA. (Microsoft installeert de HDBclient, noch SAP HANA.)

### <a name="step-2-change-etcsshsshconfig"></a>Stap 2: Wijzig/etc/ssh/ssh\_config

Wijzig/etc/ssh/ssh\_config door toe te voegen _MACs hmac-sha1_ regel als volgt te werk:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Stap 3: Maak een openbare sleutel

Maak een openbare sleutel moet worden gebruikt voor toegang tot de infrastructuur voor opslag zodat u kunt momentopnamen maken op de eerste SAP HANA op Azure (grote exemplaren)-server in elk Azure-regio. De openbare sleutel zorgt ervoor dat een wachtwoord niet aan te melden bij de opslag is vereist en wachtwoordreferenties worden niet gehandhaafd. Voer de volgende opdracht om de openbare sleutel te genereren in Linux op de SAP HANA (grote exemplaren)-server:
```
  ssh-keygen –t dsa –b 1024
```
De nieuwe locatie is _/root/.ssh/id\_dsa.pub. Voer een wachtwoordzin werkelijke niet, anders moet u de wachtwoordzin invoeren telkens wanneer die u zich aanmeldt. In plaats daarvan, drukt u op **Enter** twee keer te verwijderen van de vereiste enter wachtwoordzin voor het aanmelden.

Controleer of de openbare sleutel is opgelost, zoals werd verwacht in mappen wijzigen in /root/.ssh/ en vervolgens uitvoert de **ls** opdracht. Als de sleutel aanwezig is, kunt u deze kunt kopiëren door de volgende opdracht uit te voeren:

![Openbare sleutel wordt gekopieerd met deze opdracht uit te voeren](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

Op dit moment Neem contact op met de SAP HANA op Azure-servicebeheer en de sleutel opgeven. De klantenservice maakt gebruik van de openbare sleutel registreren in de onderliggende infrastructuur voor opslag.

### <a name="step-4-create-an-sap-hana-user-account"></a>Stap 4: Een SAP HANA-gebruikersaccount maken

Maak een SAP HANA-gebruikersaccount in SAP HANA Studio voor back-updoeleinden. Dit account moet hebben de volgende bevoegdheden: _back-up Admin_ en _catalogus_. In dit voorbeeld wordt de gebruikersnaam SCADMIN wordt gemaakt.

![Maken van een gebruiker in HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-the-sap-hana-user-account"></a>Stap 5: Machtig de SAP HANA-gebruikersaccount

Toestaan dat het gebruikersaccount voor SAP HANA (moet worden gebruikt door de scripts zonder autorisatie telkens wanneer het script wordt uitgevoerd). De opdracht SAP HANA `hdbuserstore` het maken van een sleutel voor SAP HANA, die is opgeslagen op een of meer SAP HANA-knooppunten. De sleutel van de gebruiker kan ook de gebruiker toegang tot SAP HANA zonder het beheren van wachtwoorden op in het proces van het uitvoeren van scripts die later wordt besproken.

>[!IMPORTANT]
>Voer de volgende opdracht als `_root_`. Anders wordt kan niet het script correct werken.

Voer de `hdbuserstore` opdracht als volgt:

![Voer de opdracht hdbuserstore](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

In het volgende voorbeeld, waarbij de gebruiker SCADMIN01 en de hostnaam van de lhanad01, is de opdracht:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Beheer alle scripts van één server voor scale-out HANA exemplaren. In dit voorbeeld moet de sleutel voor SAP HANA SCADMIN01 voor elke host op een manier die overeenkomt met de host die is gerelateerd aan de sleutel worden gewijzigd. Dat wil zeggen, de back-up SAP HANA-account wordt gewijzigd met het exemplaarnummer van de DB HANA **lhanad**. De sleutel moet beheerdersbevoegdheden hebben op de host die is toegewezen en de back-gebruiker voor scale-out moet toegangsrechten tot alle SAP HANA-exemplaren.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-the-scripts-folder"></a>Stap 6: Items kopiëren vanuit de map/scripts

Kopieer de volgende items in map/scripts (opgenomen in de Gouden installatiekopie van de installatie) naar de werkmap voor **hdbsql**. Deze map is voor installaties van de huidige HANA /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Kopieer de volgende items als ze zijn met scale-out- of OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
Het bestand HANABackupCustomerDetails.txt is als volgt voor de implementatie van een scale-up kan worden gewijzigd. Het is het besturingselement en configuratie-bestand voor het script dat wordt uitgevoerd van de opslag-momentopnamen. U hebt ontvangen de _back-up Opslagnaam_ en _opslag IP-adres_ uit SAP HANA op Azure-servicebeheer wanneer uw exemplaren zijn geïmplementeerd. U kunt de volgorde bestellingen of afstand van een van de variabelen niet wijzigen of het script niet goed wordt uitgevoerd.

Voor de implementatie van een scale-up eruit het configuratiebestand als:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Voor een scale-out-configuratie eruit het bestand HANABackupCustomerDetailsBW.txt als:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Op dit moment worden alleen gegevens voor knooppunt 1 in het werkelijke HANA opslag momentopname script gebruikt. Het is raadzaam de toegang tot of van alle HANA knooppunten te testen, zodat als de back-hoofdknooppunt ooit wijzigt, al u zorgt dat een ander knooppunt kan worden uitgevoerd zijn door het wijzigen van de details in het knooppunt 1.

Om te controleren of de juiste configuratie in het configuratiebestand of de juiste verbinding met de exemplaren HANA, moet u een van de volgende scripts uitvoeren:
- Voor een scale-up-configuratie (onafhankelijk van de werkbelasting SAP):

 ```
testHANAConnection.pl
```
- Voor de configuratie van een scale-out:

 ```
testHANAConnectionBW.pl
```

Zorg ervoor dat het master HANA exemplaar toegang tot alle vereiste HANA-servers heeft. Er zijn geen parameters aan het script, maar moet u de juiste HANABackupCustomerDetails / HANABackupCustomerDetailsBW file voor het script correct kunnen worden uitgevoerd. Omdat alleen de shell-opdracht-foutcodes worden geretourneerd, is het niet mogelijk om het script te foutcontrole elke instantie. Het script biedt, zodat sommige nuttige opmerkingen voor u om te controleren.

Het script uitvoeren:
```
 ./testHANAConnection.pl
```
 Als het script is de status van het exemplaar HANA krijgt, wordt er een bericht weergegeven dat de HANA-verbinding geslaagd is.

Er is bovendien een tweede type script dat u gebruiken kunt om te controleren of master HANA exemplaar van de server aan te melden bij de opslag. Voordat u de azure uitvoert\_hana\_back-up (\_bw) .pl script, moet u het volgende script uitvoeren. Als een volume geen momentopnamen bevat, is het onmogelijk om te bepalen of het volume gewoon leeg is, of er is een ssh verkrijgen van de details van de momentopname is mislukt. Daarom wordt het script wordt uitgevoerd twee stappen:

- Er wordt gecontroleerd of de console opslag toegankelijk is.
- Een test- of pop, momentopname voor elk volume wordt gemaakt door HANA-exemplaar.

Daarom is het exemplaar HANA als argument. Nogmaals, het is niet mogelijk voor het leveren van controleren voor de opslagverbinding, maar het script geeft nuttige tips als de uitvoering mislukt.

Als wordt het script uitgevoerd:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Of die wordt uitgevoerd als:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
Het script wordt ook een bericht weergegeven dat u kunt op de juiste wijze aanmelden bij uw tenant geïmplementeerde opslag, die is ingedeeld op basis van de logische eenheden (LUN) die worden gebruikt door de server-exemplaren die u bezit.

Voordat u de eerste opslag op basis van een momentopname back-ups worden uitgevoerd, voert u de volgende scripts om ervoor te zorgen dat de configuratie juist is.

U kunt de momentopnamen na het uitvoeren van deze scripts verwijderen door te voeren:
```
./removeTestStorageSnapshot.pl <hana instance>
```
of
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Stap 7: Momentopnamen op aanvraag uitvoeren

Momentopnamen op aanvraag uitvoeren (evenals regelmatig momentopnamen plannen met behulp van cron) zoals hier wordt beschreven.

Omhoog schalen-configuraties, moet u het volgende script uitvoeren:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Voor scale-out-configuraties, moet u het volgende script uitvoeren:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
Het script scale-out biedt een aantal extra controles om ervoor te zorgen dat alle HANA servers toegankelijk zijn en alle exemplaren van HANA juiste status van het exemplaar voordat u doorgaat retourneren met het maken van momentopnamen voor SAP HANA of opslag.

De volgende argumenten zijn vereist:

- De HANA exemplaar vereisen back-up.
- Het voorvoegsel van de momentopname van de momentopname van de opslag.
- Het aantal momentopnamen worden bewaard voor de specifieke voorvoegsel.

```
./azure_hana_backup.pl lhanad01 customer 20
```

De uitvoering van het script maakt een momentopname van de opslag in deze drie afzonderlijke fasen:

- Uitvoeren van een momentopname HANA.
- Uitvoeren van een momentopname van de opslag.
- Verwijder de momentopname HANA.

Voer het script door het aanroepen van de uitvoerbare map op HDB die is gekopieerd. Deze back-ups van ten minste de volgende volumes, maar deze ook back-ups van volumes met de naam van de expliciete SAP HANA-sessie in de naam van het volume.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
De bewaarperiode is uitsluitend beheerd met het aantal momentopnamen verzonden als een parameter tijdens het uitvoeren van het script (zoals 20 eerder weergegeven). De hoeveelheid tijd is dus een functie van de periode van uitvoering en het aantal momentopnamen in de aanroep van het script. Als het aantal momentopnamen worden bewaard overschrijdt het aantal die als een parameter in de aanroep van het script de oudste opslag momentopname van dit label worden genoemd (in ons geval vorige _aangepaste_) is verwijderd voordat een nieuwe momentopname wordt uitgevoerd. Dit betekent dat het aantal geeft u de laatste parameter van de aanroep is het aantal kunt u bepalen het aantal momentopnamen.

>[!NOTE]
>Als u het label wijzigt, wordt de telling opnieuw gestart.

U moet de naam van het HANA-exemplaar dat wordt geleverd door SAP HANA op Azure Service Management als een argument als ze bij het maken van momentopnamen in omgevingen met meerdere knooppunten bevatten. In omgevingen met één knooppunt, de naam van de SAP HANA op Azure (grote exemplaren) eenheid voldoende is, maar de exemplaarnaam HANA nog steeds wordt aanbevolen.

Bovendien, kunt u back-up boot volumes\LUNs met behulp van hetzelfde script. U moet back-up het opstartvolume ten minste één keer tijdens de eerste uitvoering HANA, hoewel wordt aangeraden een back-upschema voor het opstarten in cron wekelijks of elke nacht. In plaats daarvan dan het toevoegen van een SAP HANA-instantienaam, invoegen _boot_ als het argument in het script als volgt:
```
./azure_hana_backup boot customer 20
```
Hetzelfde bewaarbeleid wordt geboden voor het opstartvolume bevinden. Op aanvraag momentopnamen, zoals is beschreven voorheen voor bijzondere gevallen, zoals tijdens een upgrade SAP verbetering pakket (EHP), of wanneer u wilt maken van een momentopname van een afzonderlijke opslag gebruiken.

We raden u aan het uitvoeren van geplande opslag-momentopnamen met cron en het is raadzaam dat u hetzelfde script voor alle back-ups en herstel na noodgevallen behoeften (de script-invoer overeenkomen met de verschillende aangevraagd back-ups wijzigen). Dit zijn alle anders gepland in cron, afhankelijk van hun uitvoeringstijd: elk uur, 12 uur, dagelijks of wekelijks. De cron-schema is ontworpen voor opslag-momentopnamen die overeenkomen met de eerder besproken bewaren labels voor lange termijn off-site back-up maken. Het script bevat opdrachten voor back-up van alle productievolumes, afhankelijk van de aangevraagde frequentie (gegevens en logboekbestanden worden back-up gemaakt elk uur, terwijl het opstartvolume back-up dagelijks).

De vermeldingen in het volgende cron-script wordt elk uur uitgevoerd op de tien minuten, elke 12 uur op de tien minuten en dagelijks op de tien minuten. De cron taken worden gemaakt op zodanige wijze die slechts één SAP HANA opslag momentopname plaatsvindt tijdens een bepaald uur zodat de back-ups per uur en per dag wordt niet op hetzelfde moment (12:10 uur bijgewerkt). SAP HANA op Azure Service Management biedt om te optimaliseren van uw momentopnamen worden gemaakt en replicatie, de aanbevolen tijd voor u uw back-ups uitvoeren.

De standaard cron planning in /etc/crontab is als volgt:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
De volumes HANA (zonder opstartvolume) ophalen in de voorgaande instructies voor het cron uur momentopname te maken met het label. Van deze momentopnamen worden 66 bewaard. Bovendien worden 14 momentopnamen met het label 12 uur bewaard. Mogelijk krijgt u elk uur momentopnamen voor drie dagen, plus momentopnamen van 12 uur voor een andere vier dagen, waarmee u een hele week van momentopnamen.

Planning binnen cron worden lastig, omdat er slechts één script moet worden uitgevoerd op een willekeurig moment, tenzij de scripts gespreid door enkele minuten. Als u dagelijkse back-ups op lange termijn wilt, een dagelijkse momentopname wordt opgeslagen samen met een momentopname 12 uur (met een telling van de bewaartermijn van elke zeven) of momentopname van het uur worden gehouden 10 minuten later is gespreid. Slechts één dagelijkse momentopname wordt opgeslagen in de productievolume.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
De hier vermelde frequenties zijn alleen voorbeelden. Als u wilt het optimale aantal momentopnamen worden afgeleid, gebruikt u de volgende criteria:

- De vereisten in de beoogde hersteltijd voor herstel van de punt in tijd.
- Gebruik van schijfruimte.
- Vereisten bij het herstellen van punt doel en de beoogde hersteltijd op mogelijk noodherstel.
- Uiteindelijke uitvoering van HANA volledige databaseback-ups op basis van schijven. Wanneer een volledige databaseback-up op basis van schijven, of _backint_ interface, wordt uitgevoerd, de uitvoering van opslag-momentopnamen is mislukt. Als u van plan bent om uit te voeren volledige databaseback-ups boven op de opslag-momentopnamen, zorg ervoor dat de uitvoering van opslag-momentopnamen gedurende deze tijd is uitgeschakeld.

>[!IMPORTANT]
> Het gebruik van opslag-momentopnamen voor SAP HANA back-ups is alleen geldig wanneer de momentopnamen die in combinatie met SAP HANA logboekback-ups worden uitgevoerd. Deze logboekback-ups moeten kunnen omvatten de tijd tussen de opslag-momentopnamen. Als u een toezegging voor gebruikers van een punt in tijd herstel van 30 dagen hebt ingesteld, moet u het volgende:

- De mogelijkheid voor toegang tot een momentopname van een opslaggroep die 30 dagen oud is.
- Aaneengesloten logboekback-ups gedurende de afgelopen 30 dagen.

In het bereik van logboekback-ups, een momentopname van de back-uplogboek-volume te maken. Echter, moet u regelmatig logboekback-ups uitvoeren, zodat u kunt:

- Hebben de aaneengesloten logboekback-ups die nodig zijn voor het punt in tijd herstelacties uitvoeren.
- Voorkomen dat de SAP HANA-logboekvolume uitgevoerd geen ruimte meer.

Een van de laatste stappen is SAP HANA back-uplogboeken in SAP HANA Studio plannen. De doellocatie voor SAP HANA-back-uplogboek is het speciaal gemaakt hana/logboek\_back-ups volume met het koppelpunt van /hana/log/backups.

![Back-uplogboeken SAP HANA in SAP HANA Studio plannen](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

U kunt back-ups die vaker plaatsvinden dan om de 15 minuten zijn. Sommige gebruikers zelfs uitvoeren logboekback-ups elke minuut, maar we niet gaat raden _via_ 15 minuten.

De laatste stap is het uitvoeren van een back-ups (na de initiële installatie van de SAP HANA) voor het maken van een afzonderlijke back-post moet bestaan binnen de back-catalogus. SAP HANA kan niet anders uw opgegeven logboekback-ups gestart.

![Maken van een back-ups maken van een afzonderlijke back-post](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-the-number-and-size-of-snapshots-on-the-disk-volume"></a>Het aantal en de grootte van momentopnamen op het schijfvolume bewaking

U kunt het aantal momentopnamen en het opslagverbruik van momentopnamen bewaken op een bepaalde opslagvolume. De `ls` opdracht de momentopname-map of bestanden wordt niet weergegeven. Echter, de opdracht Linux-besturingssysteem `du` komt met de volgende opdrachten:

- `du –sh .snapshot`biedt een totaal van alle momentopnamen binnen de momentopname-directory.
- `du –sh --max-depth=1`een lijst met alle momentopnamen die zijn opgeslagen in de map .snapshot en de grootte van elke momentopname.
- `du –hc`Geeft de totale grootte, die wordt gebruikt door alle momentopnamen.

Deze opdrachten gebruiken om ervoor te zorgen dat de momentopnamen die zijn gemaakt en opgeslagen geen de opslag op de volumes worden verbruikt.

### <a name="reducing-the-number-of-snapshots-on-a-server"></a>Het aantal momentopnamen op een server verminderen

Zoals eerder beschreven, kunt u Verminder het aantal bepaalde labels van de momentopnamen die u opslaat. De laatste twee parameters van de opdracht voor het initiëren van een momentopname zijn een label en het aantal momentopnamen die u wilt behouden.
```
./azure_hana_backup.pl lhanad01 customer 20
```
In het vorige voorbeeld de label van de momentopname is _klant_ en is het aantal momentopnamen met dit label moet worden bewaard _20_. Als u op verbruik van schijfruimte reageren, wilt u misschien Verminder het aantal opgeslagen momentopnamen. Er is een eenvoudige manier om het aantal momentopnamen beperken het script uitvoeren met de laatste parameter die is ingesteld op 5:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Als gevolg van het script uitgevoerd met deze instelling, het aantal momentopnamen, met inbegrip van de momentopname van de nieuwe opslag, is de _5_.

 >[!NOTE]
 > Dit script vermindert het aantal momentopnamen alleen als de meest recente vorige momentopname meer dan een uur oud is. Het script worden niet verwijderd voor momentopnamen die minder dan een uur oud.

Deze beperkingen zijn gerelateerd aan de optionele herstel na noodgevallen-functionaliteit.

Als u niet langer onderhouden van een set van momentopnamen met voorvoegsel wilt, kunt u het script uitvoeren _0_ nummer bewaarperiode alle momentopnamen die overeenkomt met dat voorvoegsel te verwijderen. Alle momentopnamen verwijderen kan echter de mogelijkheden van herstel na noodgevallen beïnvloeden.

### <a name="recovering-to-the-most-recent-hana-snapshot"></a>Herstellen naar de meest recente HANA momentopname

In het geval dat er een productie-down-scenario, kan het proces van het herstellen van een momentopname van de opslag kan worden gestart als een klant incident met SAP HANA op Azure Service Management. Een onverwachte scenario mogelijk een hoge urgentie kwestie als gegevens in een productiesysteem is verwijderd en de enige manier om de gegevens worden opgehaald, is de productiedatabase herstellen.

Anderzijds, kan het herstel van een punt in tijd lage urgentie en geplande dagen van tevoren. U kunt dit herstel met SAP HANA plannen op Azure Service Management in plaats van een probleem met hoge prioriteit verhogen. U kunt bijvoorbeeld planning probeert een upgrade van de SAP-software door het toepassen van een nieuw pakket in de uitbreiding, en u vervolgens wilt terugkeren naar een momentopname die de status voor de upgrade EHP vertegenwoordigt.

Voordat u de aanvraag verzendt, moet u de voorbereiding. SAP HANA in Azure Service Management-team kunt vervolgens de aanvraag te verwerken en de herstelde volumes bieden. Het is daarna tot u de HANA-database op basis van de momentopnamen terugzetten. Ga als volgt om voor te bereiden voor de aanvraag:

>[!NOTE]
>De gebruikersinterface kan afwijken van de volgende schermafbeeldingen, afhankelijk van de SAP HANA-versie die u gebruikt.

1. Bepaal welke momentopname om terug te zetten. Alleen hana/gegevensvolume zou worden teruggezet, tenzij anders wordt aangegeven.

2. Het exemplaar HANA afgesloten.

 ![Het exemplaar HANA afsluiten](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Ontkoppel de gegevensvolumes op elk knooppunt HANA-database. Het herstel van de momentopname mislukt als de gegevensvolumes niet ontkoppeld zijn.

 ![Ontkoppel de gegevensvolumes op elk knooppunt HANA-database](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Een Azure ondersteuningsaanvraag om het herstel van een momentopname van een specifieke opdracht te openen.

 - Tijdens het terugzetten: SAP HANA op Azure Service Management kan u vragen om een telefonische om ervoor te zorgen dat er geen gegevens ophalen van kwijt bent is letten.

 - Na het herstel van de: SAP HANA op Azure Service Management waarschuwt u als de opslag momentopname is teruggezet.

5. Nadat het herstelproces voltooid is, opnieuw koppelen alle gegevensvolumes.

 ![Alle gegevensvolumes opnieuw koppelen](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Selecteer opties voor herstel in SAP HANA Studio als ze niet automatisch afkomstig zijn van wanneer u opnieuw verbinding met HANA-database met SAP HANA-Studio maken. Het volgende voorbeeld ziet een herstelbewerking tot de laatste HANA momentopname. Een momentopname van een HANA opslag momentopnamen en als u naar de meest recente momentopname voor de opslag terugzetten wilt, moet de meest recente HANA momentopname. (Als u naar oudere opslag-momentopnamen terugzetten wilt, moet u zoeken van de momentopname HANA is gebaseerd op de tijd dat de opslag momentopname werd gemaakt.)

 ![Selecteer de opties herstellen vanuit SAP HANA-Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Selecteer **herstel de database naar een specifieke gegevens back-up of opslag momentopname**.

 ![Het venster "Hersteltype opgeven"](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Selecteer **Geef back-up zonder catalogus**.

 ![Het venster 'Back-up locatie opgeven'](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. In de **doeltype** selecteert **momentopname**.

 ![Het venster 'Geef de back-up te herstellen'](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Klik op **voltooien** het herstelproces te starten.

 ![Klik op 'Voltooid' aan het herstelproces start](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. De HANA-database is hersteld en hersteld naar de HANA momentopname die opgenomen in de momentopname van de opslag.

 ![HANA-database is hersteld en hersteld op de momentopname HANA](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-to-the-most-recent-state"></a>Herstellen naar de meest recente status

Het volgende proces herstelt de HANA momentopname die is opgenomen in de momentopname van de opslag. Vervolgens worden hersteld de transactielogboekback-ups naar de meest recente status van de database voordat u de opslag momentopname terugzet.

>[!IMPORTANT]
>Voordat u doorgaat, zorg ervoor dat er een volledige en aaneengesloten reeks transactielogboekback-ups. Zonder deze back-ups, kunt u de huidige status van de database niet terugzetten.

1. Voltooi de stappen 1-6 van de vorige procedure in "Herstellen met de momentopname van de meest recente HANA."

2. Selecteer **herstel de database naar de meest recente status**.

 ![Selecteer 'De database naar de meest recente status herstellen'](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Geef de locatie van de meest recente HANA logboekback-ups. De locatie moet bevatten alle HANA transactielogboekback-ups van de momentopname HANA naar de meest recente status.

 ![Geef de locatie van de meest recente HANA logboekback-ups](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Selecteer een back-up als uitgangspunt van waaruit de database herstellen. In ons voorbeeld is dit de HANA momentopname die is opgenomen in de opslag-momentopnamen. (Alleen een momentopname is opgenomen in de volgende schermopname).

 ![Selecteer een back-up als uitgangspunt van waaruit de database herstellen](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Schakel de **gebruik Delta back-ups** selectievakje in als delta's niet bestaan tussen de tijd van de momentopname HANA en de meest recente status.

 ![Schakel het selectievakje 'Gebruik Delta back-ups' uit als er geen delta's bestaan](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Klik op het scherm Samenvatting **voltooien** te beginnen met de procedure voor herstel.

 ![Klik op 'Voltooid' in het scherm Samenvatting](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-to-another-point-in-time"></a>Herstellen naar een ander punt in tijd
Als u wilt herstellen naar een punt in tijd tussen de HANA-momentopname (opgenomen in de opslag momentopname) en één die later is dan het herstel HANA momentopname punt in tijd, het volgende doen:

1. Zorg ervoor dat u alle transactielogboekback-ups van de momentopname HANA aan de tijd die u wilt herstellen.
2. Beginnen met de procedure onder 'Herstellen naar de meest recente status'.
3. In stap 2 van de procedure in de **hersteltype opgeven** Selecteer **herstel de database naar het volgende punt in tijd**, Geef op het punt in tijd en voltooi stap 3-6.

## <a name="monitoring-the-execution-of-snapshots"></a>Bewaking van de uitvoering van momentopnamen

U moet controleren van de uitvoering van opslag-momentopnamen. Het script dat wordt uitgevoerd een opslag-momentopnamen schrijft uitvoer naar een bestand en slaat deze op dezelfde locatie als de Perl-scripts. Een afzonderlijk bestand is geschreven voor elke momentopname. De uitvoer van elk bestand duidelijk ziet u de verschillende fasen dat de momentopname-script wordt uitgevoerd:

- Zoeken naar de volumes die u nodig hebt om een momentopname te maken
- Zoeken naar de momentopnamen die afkomstig zijn uit deze volumes
- Eventuele momentopnamen bestaande overeenkomen met het aantal momentopnamen die u hebt opgegeven
- Maken van een momentopname HANA
- Maken van een momentopname opslag via de volumes
- Verwijderen van de momentopname HANA
- Naam van de meest recente momentopname **.0**

Het belangrijkste deel van het script is als volgt:
```
**********************Creating HANA snapshot**********************
Creating the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
U kunt van dit voorbeeld zien hoe het script registreert voor het maken van de momentopname HANA. Dit proces wordt in het geval van scale-out is gestart op het hoofdknooppunt. Het hoofdknooppunt initieert de synchrone maken van de momentopnamen op elke worker-knooppunten. De momentopname van de opslag is gehaald. Na de voltooiing van uitvoering van de opslag-momentopnamen, wordt de momentopname HANA verwijderd.
