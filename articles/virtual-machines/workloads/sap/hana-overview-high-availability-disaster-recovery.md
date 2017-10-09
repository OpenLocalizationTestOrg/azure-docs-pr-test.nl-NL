---
title: aaaHigh beschikbaarheid en herstel na noodgevallen van SAP HANA in Azure (grote exemplaren) | Microsoft Docs
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
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen in Azure 

Hoge beschikbaarheid en herstel na noodgevallen zijn belangrijke aspecten van uw bedrijfskritieke SAP HANA worden uitgevoerd op Azure (grote exemplaren)-servers. De belangrijke toowork met SAP, uw system integrator, of Microsoft tooproperly architect en implementeer Hallo rechts high-availability/herstel na noodgevallen-strategie. Het is ook belangrijk tooconsider Hallo beoogd herstelpunt en beoogde hersteltijd, specifieke tooyour omgeving worden.

## <a name="high-availability"></a>Hoge beschikbaarheid

Microsoft ondersteunt SAP HANA hoge beschikbaarheid methoden 'out van Hallo vak' waaronder:

- **Storage-replicatie:** Hallo van opslagsysteem mogelijkheid tooreplicate alle gegevenslocatie tooanother (binnen of apart, Hallo hetzelfde datacenter). SAP HANA werkt onafhankelijk van deze methode.
- **HANA system replication:** Hallo van replicatie van alle gegevens in SAP HANA tooa afzonderlijke SAP HANA-systeem. Hallo beoogde hersteltijd wordt geminimaliseerd door middel van gegevensreplicatie met regelmatige tussenpozen. SAP HANA ondersteunt asynchrone, synchrone in het geheugen en synchrone modus (alleen aanbevolen voor SAP HANA systemen die binnen hetzelfde datacenter of minder dan 100 KM elkaar Hallo). In de huidige ontwerp Hallo HANA grote exemplaar stempels, kan de HANA system replicatie voor hoge beschikbaarheid alleen worden gebruikt.
- **Automatische failover hosten:** een lokale fout herstel oplossing toouse als een alternatieve toosystem-replicatie. Wanneer Hallo hoofdknooppunt niet meer beschikbaar is, een of meer stand-by SAP HANA-knooppunten zijn geconfigureerd in de modus voor scale-out en SAP HANA automatisch failover tooanother knooppunt wordt uitgevoerd.

Zie voor meer informatie over hoge beschikbaarheid voor SAP HANA Hallo SAP-gegevens te volgen:

- [Technisch document SAP HANA hoge beschikbaarheid](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [Handleiding voor SAP HANA-beheer](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP Academy Video voor SAP HANA System replicatie](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP-notitie ondersteuning #1999880: veelgestelde vragen over SAP HANA System Replication](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP-ondersteuning Opmerking #2165547 – SAP HANA back-up en herstel binnen replicatieomgeving voor SAP HANA-systeem](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP-notitie ondersteuning #1984882 – met SAP HANA System replicatie voor Hardware-uitwisseling met minimale/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Herstel na noodgevallen

SAP HANA in Azure (grote exemplaren) wordt aangeboden in twee Azure-regio's in een geopolitieke regio. Is een rechtstreekse netwerkverbinding voor het repliceren van gegevens tijdens herstel na noodgevallen tussen twee grote exemplaar stempels Hallo van twee verschillende regio's. Hallo replicatie van gegevens van de Hallo is opslaginfrastructuur op basis van. Hallo-replicatie is niet standaard uitgevoerd. Dit geldt voor Hallo klant configuraties die besteld Hallo-noodherstel. In het huidige ontwerp hello, kunnen HANA system replicatie kan niet worden gebruikt voor herstel na noodgevallen.

Echter tootake profiteren van herstel na noodgevallen hello, hoeft u toostart toodesign Hallo network connectivity toohello twee verschillende Azure-regio's. toodo geval is, moet u een Azure ExpressRoute-circuit-verbinding van on-premises in uw Azure-regio en een andere circuit verbinding van lokale tooyour herstel na noodgevallen regio. Deze meting bevat gewoonlijk een situatie waarin een volledige Azure-regio, met inbegrip van een locatie van Microsoft enterprise edge router (MSEE) een probleem heeft.

Als een tweede maat, kunt u alle virtuele Azure-netwerken die verbinding tooSAP HANA in Azure (grote exemplaren maken) in een Hallo regio's tooboth van de ExpressRoute-circuits. Deze meting heeft betrekking op een aanvraag waarin slechts één van Hallo MSEE locaties die uw on-premises locatie met Azure verbindt niet actief gaat.

Hallo volgende afbeelding ziet u de optimale configuratie Hallo voor herstel na noodgevallen:

![Optimale configuratie voor herstel na noodgevallen](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Hallo wordt optimale voor een configuratie voor herstel na noodgevallen van Hallo netwerk toohave twee ExpressRoute-circuits van lokale toohello twee verschillende Azure-regio's. Een circuit gaat tooregion #1, met een exemplaar van de productie. de tweede ExpressRoute-circuit Hallo gaat tooregion #2 sommige exemplaren van niet-productieve HANA uitgevoerd. (Dit is belangrijk als een volledige Azure-regio, met inbegrip van hello MSEE- en datumstempel grote exemplaar, gaat Hallo raster uit).

Als een tweede maat Hallo verschillende virtuele netwerken zijn verbonden toohello verschillende ExpressRoute-circuits die verbonden tooSAP HANA in Azure (grote exemplaren zijn). Hallo locatie waar een MSEE is mislukt, of kunt u het verlagen Hallo beoogde herstelpunt voor herstel na noodgevallen, kunt u overslaan als we later bespreken.

de volgende vereisten Hallo voor een installatie met herstel na noodgevallen zijn:

- U moet een SAP HANA bestellen op SKU's van Azure (grote exemplaren) Hallo hetzelfde formaat als uw productie-SKU's en deze implementeren in Hallo herstel na noodgevallen regio. Deze instanties kunnen worden gebruikt toorun test, sandbox of QA HANA exemplaren.
- U moet de volgorde een profiel voor herstel na noodgevallen voor elk van uw SAP HANA op SKU's van Azure (grote exemplaren) dat u wilt dat toorecover op Hallo herstel na noodgevallen site, indien nodig. Deze actie leidt toohello toewijzing van opslagvolumes, de Hallo doel van Hallo storage-replicatie van uw productieregio Hallo herstel na noodgevallen regio.

Nadat u aan Hallo voorafgaand aan de vereisten voldoet, is uw verantwoordelijkheid toostart Hallo storage-replicatie. Hallo op basis van de storage-replicatie is in Hallo opslaginfrastructuur gebruikt voor SAP HANA in Azure (grote exemplaren), opslag-momentopnamen. replicatie van toostart Hallo herstel na noodgevallen, moet u tooperform:

- Een momentopname van de opstartinstallatiekopie LUN, zoals eerder beschreven.
- Een momentopname van de volumes HANA-gerelateerde, zoals eerder beschreven.

Nadat u deze momentopnamen worden uitgevoerd, wordt een eerste replica van de volumes Hallo seeding op Hallo van volumes die gekoppeld aan uw profiel herstel na noodgevallen in Hallo herstel na noodgevallen regio zijn.

Vervolgens elk uur wordt gebruikt in de meest recente opslag momentopname Hallo tooreplicate Hallo delta's die op Hallo opslagvolumes ontwikkelen.

Hallo beoogd herstelpunt dat wordt gerealiseerd met deze configuratie is van too90 de 60 minuten. een betere herstelmogelijkheden tooachieve wijst doelstelling in Hallo herstel na noodgevallen geval kopie Hallo HANA transactielogboekback-ups uit SAP HANA op Azure (grote exemplaren) toohello andere Azure-regio. tooachieve deze beoogd herstelpunt Hallo te volgen:

1. Maak een back-up van Hallo HANA transactie Meld u zo vaak mogelijk te/hana/log/back-up.
2. Kopieer Hallo transactielogboekback-ups wanneer ze klaar tooan Azure virtuele machine (VM), dat zich bevindt in een virtueel netwerk dat toohello SAP HANA op Azure (grote exemplaren)-server is verbonden.
3. Kopiëren van die VM Hallo back-tooa virtuele machine die zich in een virtueel netwerk in Hallo herstel na noodgevallen regio.
4. Houd Hallo transactie logboekback-ups in deze regio in Hallo VM.

In noodgevallen nadat Hallo herstel na noodgevallen profiel is geïmplementeerd op een werkelijke-server, kopieert u Hallo transactielogboekback-ups van Hallo VM toohello SAP HANA op primaire server is nu Hallo in Hallo herstel na noodgevallen regio, Azure (grote exemplaren) en Deze back-ups herstellen. Dit herstel is mogelijk omdat Hallo status van HANA op Hallo herstel na noodgevallen schijven die van een momentopname HANA. Dit is Hallo offset voor verdere herstelprocedures van transactielogboekback-ups.

## <a name="backup-and-restore"></a>Back-ups en herstellen

Een van de belangrijkste aspecten toooperating-databases Hallo is om ervoor te zorgen hello database kan worden beveiligd vanaf verschillende rampen. Deze gebeurtenissen kunnen zijn veroorzaakt door alles van natuurramp toosimple gebruikersfouten.

Maken van back-up van een database met Hallo mogelijkheid toorestore tooany punt in tijd (zoals voordat iemand kritieke gegevens verwijderd), kunt u het herstel van tooa staat die zo dicht mogelijk toohello manier deze was voordat de Hallo onderbreking is opgetreden.

Twee soorten back-ups moeten worden uitgevoerd voor de beste resultaten:

- Databaseback-ups
- Transactielogboekback-ups

Bovendien toofull databaseback-ups op niveau van een toepassing wordt uitgevoerd, u kunt altijd zelfs uitgebreider door het uitvoeren van back-ups met de opslag-momentopnamen. Logboekback-ups uitvoeren, is ook belangrijk voor het herstellen van database hello (en tooempty Hallo logboeken van al doorgevoerde transacties).

SAP HANA in Azure (grote exemplaren) biedt twee opties voor back-up en herstel:

- Hiervoor zelf (DIY). Nadat u tooensure voldoende schijfruimte is berekent, voert u de volledige database en logboekbestanden back-ups met behulp van back-up schijf-methoden (toothose schijven). Na verloop van tijd Hallo back-ups gekopieerde tooan Azure storage-account (na het instellen van een Azure-bestandsserver met vrijwel onbeperkte opslag) zijn of een Azure Backup-kluis of Azure koude opslag gebruiken. Een andere optie is een hulpprogramma van de beveiliging van derden gegevens toouse zoals Commvault, toostore Hallo back-ups nadat ze zijn gekopieerd tooa storage-account. Hallo ZELFOPLOSSING optie back-up kan ook nodig zijn om gegevens die moeten worden opgeslagen voor langere tijd voor compliancy en controledoeleinden toobe.
- Gebruik Hallo back-up en herstellen van de functionaliteit die Hallo onderliggende infrastructuur van SAP HANA in Azure (grote exemplaren) bevat. Deze optie wordt voldaan aan Hallo nodig voor back-ups en maakt handmatige back-ups bijna verouderd (met uitzondering van gegevensback-ups indien noodzakelijk zijn voor naleving zijn). Hallo rest van deze sectie heeft betrekking op Hallo back-up en herstel van functionaliteit die wordt aangeboden met HANA (grote exemplaren).

> [!NOTE]
> Hallo momentopnametechnologie die wordt gebruikt door de onderliggende infrastructuur Hallo van HANA (grote exemplaren) heeft een afhankelijkheid voor SAP HANA-momentopnamen. SAP HANA momentopnamen werken niet in combinatie met SAP HANA Multitenant Database Containers. Deze methode van back-up kan niet als gevolg hiervan gebruikte toodeploy SAP HANA Multitenant Database Containers zijn.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Met behulp van opslag-momentopnamen van SAP HANA in Azure (grote exemplaren)

Hallo opslaginfrastructuur onderliggende SAP HANA in Azure (grote exemplaren) ondersteunt Hallo begrip van een momentopname van de opslag van volumes. Zowel back-up en herstel van een bepaald volume worden ondersteund met Hallo overwegingen te volgen:

- In plaats van de databaseback-ups, worden opslag volume momentopnamen regelmatig.
- Hallo opslag momentopname initieert een momentopname van een SAP HANA voordat deze Hallo opslag momentopname wordt uitgevoerd. Deze momentopname met de SAP HANA is Hallo setup voor uiteindelijke logboek herstelbewerkingen kunnen na het herstel van Hallo opslag momentopname.
- Op Hallo punt waar Hallo opslag momentopname met succes is uitgevoerd, is Hallo SAP HANA momentopname verwijderd.
- Logboekback-ups zijn vaak gemaakt en opgeslagen in de back-logboekvolume Hallo of in Azure.
- Als het Hallo-database moet worden hersteld tooa die bepaalde punt in tijd, een aanvraag wordt gedaan tooMicrosoft ondersteuning van Azure (productie uitval) of SAP HANA op Azure Service Management toorestore tooa bepaalde opslag-momentopnamen (bijvoorbeeld een geplande herstel van een sandbox tooits oorspronkelijke staat).
- Hallo SAP HANA momentopname die is opgenomen in Hallo opslag momentopname is een offset punt voor het toepassen van logboekback-ups die zijn uitgevoerd en opgeslagen nadat Hallo opslag momentopname werd gemaakt.
- Deze logboekback-ups worden genomen toorestore Hallo database back tooa bepaalde tijdstip voor herstel.

Back-up van opgeven Hallo\_naam maakt een momentopname van Hallo volgende volumes:

- Hana/gegevens
- Hana/logboek
- Hana/log\_back-up (gekoppeld als back-up in hana/logboek)
- Hana/gedeeld

### <a name="storage-snapshot-considerations"></a>Overwegingen met betrekking tot opslag-momentopnamen

>[!NOTE]
>Opslag-momentopnamen zijn _niet_ opgegeven gratis, omdat u extra opslagruimte moet worden toegewezen.

Hallo specifieke mechanisme van opslag-momentopnamen voor SAP HANA in Azure (grote exemplaren) zijn onder andere:

- Een momentopname van een bepaalde opslag (op Hallo punt in tijd waarop deze is gemaakt) verbruikt weinig opslag.
- Als inhoud gegevenswijzigingen en het Hallo-inhoud in bestanden worden gewijzigd op Hallo opslagvolume SAP HANA-gegevens, moet Hallo momentopname toostore Hallo oorspronkelijke Blokinhoud.
- Hallo opslag momentopname wordt vergroot. Hallo langer Hallo momentopname bestaat, Hallo groter Hallo opslag momentopname wordt.
- Hallo meer wijzigingen toohello SAP HANA-databasevolume tijdens Hallo levensduur van een momentopname van de opslag, Hallo groter Hallo verbruik van schijfruimte van Hallo opslag momentopname wordt.

SAP HANA in Azure (grote exemplaren) wordt geleverd met grootten voor Hallo SAP HANA gegevens en logboekbestanden volume vast volume. Uitvoeren van momentopnamen van de volumes eats in de ruimte op volume zodat u uw verantwoordelijkheid tooschedule opslag-momentopnamen (binnen Hallo SAP HANA op Azure [grote exemplaren]-proces).

Hallo bevatten volgende secties informatie voor het uitvoeren van deze momentopnamen, waaronder algemene aanbevelingen:

- Hoewel Hallo hardware 255 momentopnamen per volume tolereren kan, wordt ten zeerste aanbevolen ruim onder dit nummer te blijven.
- Voordat u opslag-momentopnamen uitvoert, bewaken en bijhouden vrije ruimte.
- Minder Hallo van opslag-momentopnamen op basis van de vrije ruimte. Mogelijk moet u toolower Hallo aantal momentopnamen die u bijhoudt, of moet u mogelijk tooextend Hallo volumes. (U kunt extra opslagruimte bestellen in eenheden van 1 TB.)
- Tijdens de activiteiten zoals het verplaatsen van gegevens in SAP HANA met systeem hulpprogramma's voor migratie (R3load of door te SAP HANA-databases herstellen vanuit back-ups), raden we u alle opslag-momentopnamen niet uitvoeren. (Als de migratie van een systeem is op een nieuw SAP HANA-systeem wordt gedaan, opslag-momentopnamen hoeft dan niet toobe uitgevoerd.)
- Tijdens de grotere reorganisaties SAP HANA-tabellen, moeten de opslag-momentopnamen indien mogelijk worden vermeden.
- Opslag-momentopnamen zijn een vereiste tooengaging Hallo herstel na noodgevallen mogelijkheden van SAP HANA in Azure (grote exemplaren).

### <a name="setting-up-storage-snapshots"></a>Instellen van opslag-momentopnamen

1. Zorg ervoor dat Perl in Hallo Linux-besturingssysteem op Hallo HANA (grote exemplaren)-server is geïnstalleerd.
2. Wijzig/etc/ssh/ssh\_config tooadd Hallo regel _MACs hmac-sha1_.
3. Maak een back-SAP HANA-gebruikersaccount op Hallo hoofdknooppunt voor elk SAP HANA-exemplaar dat u uitvoert (indien van toepassing).
4. Hallo SAP HANA HDB client moet worden geïnstalleerd op alle servers voor SAP HANA (grote exemplaren).
5. Op Hallo eerste SAP HANA (grote exemplaren)-server van elke regio moet een openbare sleutel tooaccess Hallo onderliggende opslaginfrastructuur die het maken van momentopnamen bepaalt worden gemaakt.
6. Kopieer Hallo script azure\_hana\_backup.pl vanuit/scripts toohello locatie van de **hdbsql** Hallo SAP HANA-installatie.
7. Bestand kopiëren Hallo HANABackupDetails.txt van/scripts toohello dezelfde locatie als Hallo Perl-script.
8. Hallo HANABackupDetails.txt bestand die nodig zijn voor de gewenste klant-specificaties Hallo wijzigen.

### <a name="step-1-install-sap-hana-hdbclient"></a>Stap 1: SAP HANA HDBClient installeren

Hallo Linux is geïnstalleerd op een SAP HANA in Azure (grote exemplaren) bevat Hallo mappen en scripts nodig tooexecute SAP HANA-opslag-momentopnamen voor back-up en herstel na noodgevallen. Het is echter uw verantwoordelijkheid tooinstall SAP HANA HDBclient tijdens de installatie van SAP HANA. (Microsoft installeert Hallo HDBclient noch SAP HANA.)

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

Eerste SAP HANA op Azure (grote exemplaren)-server in elk Azure-regio, maak een openbare sleutel toobe gebruikt tooaccess Hallo-opslaginfrastructuur op Hallo zodat u kunt momentopnamen maken. Hallo openbare sleutel zorgt ervoor dat een wachtwoord niet vereist toosign in toohello opslag is en wachtwoordreferenties worden niet gehandhaafd. Uitvoeren in Linux op Hallo SAP HANA (grote exemplaren) server Hallo opdracht toogenerate Hallo openbare sleutel te volgen:
```
  ssh-keygen –t dsa –b 1024
```
de nieuwe locatie Hallo is _/root/.ssh/id\_dsa.pub. Voer een wachtwoordzin werkelijke niet, anders kunt u zich vereist tooenter Hallo wachtwoordzin telkens wanneer die u zich aanmeldt. In plaats daarvan, drukt u op **Enter** tweemaal tooremove Hallo Voer vereiste wachtwoordzin voor het aanmelden.

Controleer of de openbare sleutel van die Hallo is opgelost zoals werd verwacht in mappen too/root/.ssh/ wijzigen en vervolgens uitvoert Hallo toomake **ls** opdracht. Als de sleutel Hallo aanwezig is, kunt u deze door het uitvoeren van de volgende opdracht Hallo kopiëren:

![Openbare sleutel wordt gekopieerd met deze opdracht uit te voeren](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

Op dit moment Neem contact op met de SAP HANA op Azure-servicebeheer en Hallo sleutel opgeven. Hallo klantenservice maakt gebruik van de openbare sleutel tooregister Hallo in Hallo onderliggende opslaginfrastructuur.

### <a name="step-4-create-an-sap-hana-user-account"></a>Stap 4: Een SAP HANA-gebruikersaccount maken

Maak een SAP HANA-gebruikersaccount in SAP HANA Studio voor back-updoeleinden. Dit account moet hebben Hallo volgende bevoegdheden: _back-up Admin_ en _catalogus_. In dit voorbeeld Hallo gebruikersnaam SCADMIN wordt gemaakt.

![Maken van een gebruiker in HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Stap 5: Autoriseren hello SAP HANA-gebruikersaccount

Autoriseren hello SAP HANA-gebruikersaccount (toobe gebruikt door Hallo scripts zonder autorisatie telkens wanneer Hallo script wordt uitgevoerd). Hallo SAP HANA-opdracht `hdbuserstore` Hallo maken van een sleutel voor SAP HANA, die is opgeslagen op een of meer SAP HANA-knooppunten. Hallo gebruiker tooaccess SAP HANA kan Hallo gebruikerssleutel ook zonder toomanage wachtwoorden van binnen Hallo scripting proces dat later wordt besproken.

>[!IMPORTANT]
>Voer hello volgende opdracht als `_root_`. Anders kan niet Hallo script correct werken.

Voer Hallo `hdbuserstore` opdracht als volgt:

![Voer Hallo hdbuserstore opdracht](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

In Hallo volgt, waarbij Hallo gebruiker SCADMIN01 en Hallo hostnaam lhanad01, is Hallo-opdracht:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Beheer alle scripts van één server voor scale-out HANA exemplaren. In dit voorbeeld Hallo SAP HANA-sleutel die scadmin01 voor elke host op een manier die overeenkomt met Hallo-host die is gerelateerd toohello sleutel moet worden gewijzigd. Dat wil zeggen, Hallo SAP HANA-back-account wordt gewijzigd met Hallo exemplaar aantal Hallo HANA DB, **lhanad**. Hallo-sleutel moet beheerdersbevoegdheden hebben op Hallo-host die is toegewezen aan moet, en Hallo back-gebruiker voor scale-out toegang rechten tooall SAP HANA-exemplaren.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Stap 6: Items kopiëren vanuit de map/scripts Hallo

Kopiëren Hallo volgende items uit Hallo/map (opgenomen op Hallo gouden installatiekopie van Hallo-installatie) toohello werkmap voor scripts **hdbsql**. Deze map is voor installaties van de huidige HANA /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Hallo volgende items als ze zijn met scale-out- of OLAP-kopiëren:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
Hallo HANABackupCustomerDetails.txt bestand is als volgt voor de implementatie van een scale-up kan worden gewijzigd. Het is Hallo beheer- en configuratie-bestand voor Hallo-script dat wordt uitgevoerd Hallo-opslag-momentopnamen. U hebt ontvangen Hallo _back-up Opslagnaam_ en _opslag IP-adres_ uit SAP HANA op Azure-servicebeheer wanneer uw exemplaren zijn geïmplementeerd. U Hallo-reeks kan niet wijzigen ordening of afstand van een van de variabelen Hallo of Hallo script werkt niet goed.

Voor een implementatie omhoog schalen eruit Hallo configuratiebestand als:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Voor een scale-out-configuratie eruit Hallo HANABackupCustomerDetailsBW.txt bestand als:
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
>Op dit moment worden alleen gegevens voor knooppunt 1 in Hallo werkelijke HANA opslag momentopname script gebruikt. Het is raadzaam om de toegang tooor van alle HANA knooppunten te testen, zodat als de back-hoofdknooppunt Hallo ooit wijzigt, al u zorgt dat een ander knooppunt kan worden uitgevoerd zijn doordat Hallo details in het knooppunt 1.

toocheck voor de juiste configuraties Hallo in Hallo-configuratiebestand of de juiste connectiviteit toohello HANA exemplaren een van de volgende scripts Hallo uitvoeren:
- Voor een scale-up-configuratie (onafhankelijk van de werkbelasting SAP):

 ```
testHANAConnection.pl
```
- Voor de configuratie van een scale-out:

 ```
testHANAConnectionBW.pl
```

Zorg ervoor dat Hallo master HANA exemplaar HANA-servers voor clienttoegang tooall vereist. Er zijn geen parameters toohello script, maar u moet voltooien Hallo juiste HANABackupCustomerDetails / HANABackupCustomerDetailsBW file voor Hallo script toorun goed. Omdat alleen Hallo shell opdracht foutcodes worden geretourneerd, is het niet mogelijk voor elke instantie een script tooerror selectievakje Hallo. Hallo script biedt, zodat sommige nuttige opmerkingen voor toodouble-controle.

toorun hello script:
```
 ./testHANAConnection.pl
```
 Als het script Hallo krijgt met succes Hallo status van Hallo HANA exemplaar, wordt een bericht dat Hallo HANA verbinding geslaagd is.

Bovendien is er een tweede type van het script kunt u toocheck Hallo master HANA exemplaar van server mogelijkheid toosign in toohello opslag. Voordat u hello azure uitvoert\_hana\_back-up (\_bw) .pl script, moet u het volgende script Hallo uitvoeren. Als een volume geen momentopnamen bevat, is het onmogelijk toodetermine of Hallo volume gewoon leeg is of er is een ssh mislukte tooobtain Hallo momentopname maken van meer informatie. Hallo script uitvoert om deze reden twee stappen:

- Er wordt gecontroleerd dat die Hallo-opslag-console is toegankelijk.
- Een test- of pop, momentopname voor elk volume wordt gemaakt door HANA-exemplaar.

Om deze reden wordt Hallo HANA exemplaar opgenomen als een argument. Nogmaals, is niet mogelijk tooprovide foutcontrole voor Hallo opslagverbinding maar Hallo script biedt nuttige tips als Hallo uitvoering mislukt.

Hallo-script wordt uitgevoerd als:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Of die wordt uitgevoerd als:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
Hallo-script wordt ook een bericht weergegeven dat u kunt toosign in op de juiste wijze tooyour geïmplementeerd opslag-tenant, die is ingedeeld op basis van Hallo LUN's (LUN's) die worden gebruikt door het Hallo-serverexemplaren die u eigenaar bent.

Voordat u Hallo eerste opslag momentopname back-ups worden uitgevoerd, voert u Hallo volgende scripts toomake of dat die Hallo configuratie juist is.

U kunt Hallo momentopnamen na het uitvoeren van deze scripts verwijderen door te voeren:
```
./removeTestStorageSnapshot.pl <hana instance>
```
of
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Stap 7: Momentopnamen op aanvraag uitvoeren

Momentopnamen op aanvraag uitvoeren (evenals regelmatig momentopnamen plannen met behulp van cron) zoals hier wordt beschreven.

Configuraties met scale-up uitvoeren Hallo script volgen:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Voor scale-out configuraties uitvoeren Hallo script volgen:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
Hallo scale-out script doet een aantal aanvullende controle toomake ervoor dat alle HANA servers toegankelijk zijn en alle exemplaren van HANA juiste status van Hallo exemplaar voordat u doorgaat geretourneerde met het maken van momentopnamen voor SAP HANA of opslag.

Hallo volgende argumenten zijn vereist:

- Hallo HANA exemplaar vereisen back-up.
- Hallo momentopname voorvoegsel voor Hallo-opslag-momentopnamen.
- Hallo aantal momentopnamen toobe voor specifieke voorvoegsel Hallo behouden.

```
./azure_hana_backup.pl lhanad01 customer 20
```

Hallo-uitvoering van Hallo script maakt Hallo opslag momentopname in deze drie afzonderlijke fasen:

- Uitvoeren van een momentopname HANA.
- Uitvoeren van een momentopname van de opslag.
- Hallo HANA momentopname worden verwijderd.

Hallo-script uitvoeren door het aanroepen van Hallo HDB uitvoerbare map die is gekopieerd. Deze back-ups maakt ten minste Hallo na volumes, maar deze ook back-ups van volumes met Hallo expliciete SAP HANA-exemplaarnaam in Hallo volumenaam.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
Hallo bewaarperiode wordt uitsluitend beheerd met Hallo aantal momentopnamen verzonden als een parameter tijdens het uitvoeren van script hello (zoals 20 eerder weergegeven). Hallo hoeveelheid tijd is dus een functie van de uitvoering en Hallo aantal momentopnamen in aanroep van Hallo script Hallo Hallo periode. Als Hallo aantal momentopnamen worden bewaard Hallo aantal die worden genoemd als een parameter in aanroep van Hallo script Hallo overschrijdt, Hallo oudste opslag momentopname van dit label (in ons geval vorige _aangepaste_) is verwijderd voordat een nieuwe momentopname is uitgevoerd. Dit betekent dat Hallo nummer geeft u hello laatste parameter van het Hallo-aanroep is Hallo getal kunt u toocontrol Hallo aantal momentopnamen.

>[!NOTE]
>Zodra u Hallo label wijzigt, Hallo tellen opnieuw gestart.

U moet tooinclude Hallo HANA exemplaarnaam die wordt geleverd door SAP HANA op Azure Service Management als een argument als ze bij het maken van momentopnamen in omgevingen met meerdere knooppunten. In omgevingen met één knooppunt, Hallo naam Hallo SAP HANA op Azure (grote exemplaren) eenheid voldoende, maar wordt nog steeds Hallo HANA exemplaarnaam aanbevolen.

Bovendien, u kunt back-up volumes\LUNs opstarten met behulp van Hallo dezelfde script. U moet back-up het opstartvolume ten minste één keer tijdens de eerste uitvoering HANA, hoewel wordt aangeraden een back-upschema voor het opstarten in cron wekelijks of elke nacht. In plaats daarvan dan het toevoegen van een SAP HANA-instantienaam, invoegen _boot_ als argument als volgt Hallo in Hallo script:
```
./azure_hana_backup boot customer 20
```
Hallo wordt hetzelfde bewaarbeleid geboden ook toohello opstartvolume. Op aanvraag momentopnamen, zoals is beschreven voorheen voor bijzondere gevallen, zoals tijdens een upgrade SAP verbetering pakket (EHP), of wanneer u een momentopname van een afzonderlijke opslag toocreate moet gebruiken.

We raden u tooperform gepland opslag-momentopnamen met cron en aangeraden Hallo dezelfde script te gebruiken voor alle back-ups en herstel na noodgevallen behoeften (aanpassen Hallo script invoer toomatch hello verschillende aangevraagd back-ups). Dit zijn alle anders gepland in cron, afhankelijk van hun uitvoeringstijd: elk uur, 12 uur, dagelijks of wekelijks. Hallo cron-schema is ontworpen toocreate opslag-momentopnamen die overeenkomen met de eerder besproken Hallo bewaren labels voor lange termijn off-site back-up. Hallo-script bevat opdrachten tooback van alle productievolumes, afhankelijk van de aangevraagde frequentie (gegevens en logboekbestanden worden back-up gemaakt elk uur, terwijl het opstartvolume Hallo back-up dagelijks).

Hallo vermeldingen in de volgende cron script Hallo elk uur uitgevoerd op Hallo tien minuten, elke 12 uur op Hallo tien minuten en dagelijks op Hallo tien minuten. Hallo cron taken worden gemaakt op zodanige wijze die slechts één SAP HANA opslag momentopname plaatsvindt tijdens een bepaald uur zodat hello per uur en dagelijkse back-ups niet worden uitgevoerd op Hallo dat dezelfde tijd (12:10 uur). toohelp optimaliseren uw momentopnamen worden gemaakt en replicatie, SAP HANA op Azure Service Management biedt Hallo aanbevolen voor toorun u uw back-ups.

Hallo standaard cron planning in /etc/crontab is als volgt:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
In vorige cron instructies Hallo ophalen Hallo HANA volumes (zonder opstartvolume) een momentopname met Hallo label uur. Van deze momentopnamen worden 66 bewaard. Bovendien worden 14 momentopnamen met Hallo 12 uur label bewaard. Mogelijk krijgt u elk uur momentopnamen voor drie dagen, plus momentopnamen van 12 uur voor een andere vier dagen, waarmee u een hele week van momentopnamen.

Planning binnen cron worden lastig, omdat er slechts één script moet worden uitgevoerd op een willekeurig moment tenzij Hallo scripts gespreid door enkele minuten. Als u wilt dat dagelijkse back-ups op lange termijn, een dagelijkse momentopname wordt opgeslagen samen met een momentopname 12 uur (met een telling van de bewaartermijn van elke zeven) of Hallo per uur momentopname is gespreid tootake plaats 10 minuten later. Slechts één dagelijkse momentopname wordt opgeslagen in Hallo productievolume.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
Hallo frequenties hier vermeld zijn alleen voorbeelden. tooderive het optimale aantal momentopnamen, gebruik Hallo volgende criteria:

- De vereisten in de beoogde hersteltijd voor herstel van de punt in tijd.
- Gebruik van schijfruimte.
- Vereisten bij het herstellen van punt doel en de beoogde hersteltijd op mogelijk noodherstel.
- Uiteindelijke uitvoering van HANA volledige databaseback-ups op basis van schijven. Wanneer een volledige databaseback-up op basis van schijven, of _backint_ interface, wordt uitgevoerd, Hallo uitvoering van opslag-momentopnamen is mislukt. Als u van plan de volledige databaseback-ups tooexecute boven op de opslag-momentopnamen bent, ervoor zorgen dat de uitvoering van opslag-momentopnamen Hallo gedurende deze tijd is uitgeschakeld.

>[!IMPORTANT]
> Hallo gebruik van opslag-momentopnamen voor SAP HANA back-ups is alleen geldig wanneer Hallo momentopnamen in combinatie met SAP HANA logboekback-ups worden uitgevoerd. Deze Meld back-ups moeten toobe kunnen toocover Hallo tijd tussen het Hallo-opslag-momentopnamen. Als u een toousers streven van een punt in tijd herstel van 30 dagen hebt ingesteld, moet u de volgende Hallo:

- Mogelijkheid tooaccess momentopname van een opslag is 30 dagen oud.
- Aaneengesloten logboekback-ups via Hallo afgelopen 30 dagen.

In het bereik van de Hallo van logboekback-ups, een momentopname maken van back-uplogboek volume ook Hallo. Maar ook zeker tooperform normale logboekback-ups zodat u kunt:

- Hallo aaneengesloten logboekback-ups nodig tooperform punt in tijd herstelbewerkingen hebben.
- Voorkomen dat Hallo SAP HANA-logboekvolume met de beschikbare ruimte.

Een van de laatste stappen Hallo is tooschedule SAP HANA back-uplogboeken in SAP HANA Studio. Hallo SAP HANA back-uplogboek doellocatie is speciaal gemaakt Hallo hana/log\_volume van de back-ups met koppelpunt op Hallo /hana/log/backups.

![Back-uplogboeken SAP HANA in SAP HANA Studio plannen](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

U kunt back-ups die vaker plaatsvinden dan om de 15 minuten zijn. Sommige gebruikers zelfs uitvoeren logboekback-ups elke minuut, maar we niet gaat raden _via_ 15 minuten.

de laatste stap Hallo is een op bestanden gebaseerde tooperform back-up (na de eerste installatie Hallo van SAP HANA) toocreate een afzonderlijke back-post moet bestaan binnen de back-upcatalogus Hallo. SAP HANA kan niet anders uw opgegeven logboekback-ups gestart.

![Een back-toocreate op basis van bestanden van een enkele back-item maken](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Hallo aantal en de grootte van momentopnamen op Hallo schijfvolume bewaking

U kunt op een bepaalde opslagvolume Hallo aantal momentopnamen en het verbruik van de Hallo opslag van momentopnamen bewaken. Hallo `ls` opdracht Hallo momentopname map of bestanden wordt niet weergegeven. Linux-besturingssysteem opdracht echter Hallo `du` biedt Hello volgende opdrachten:

- `du –sh .snapshot`biedt een totaal van alle momentopnamen binnen Hallo momentopname directory.
- `du –sh --max-depth=1`een lijst met alle momentopnamen die zijn opgeslagen in Hallo .snapshot map en Hallo grootte van elke momentopname.
- `du –hc`totale grootte van Hallo gebruikt door alle momentopnamen bevat.

Gebruik deze opdrachten toomake ervoor dat Hallo momentopnamen die zijn gemaakt en opgeslagen geen alle Hallo opslag op Hallo volumes worden verbruikt.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Hallo aantal momentopnamen op een server verminderen

Zoals eerder beschreven, kunt u beperken Hallo aantal bepaalde labels van de momentopnamen die u opslaat. Hallo de laatste twee parameters van de Hallo opdracht tooinitiate een momentopname is een label en Hallo aantal momentopnamen die u wilt dat tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
In het vorige voorbeeld Hallo Hallo momentopname van het label is _klant_ en het aantal momentopnamen met dit label toobe bewaard Hallo _20_. Als u het verbruik van schijfruimte toodisk reageert, kunt u tooreduce Hallo aantal opgeslagen momentopnamen. eenvoudig Hello tooreduce Hallo aantal momentopnamen toorun Hallo script met de laatste parameter set-too5 Hallo is:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Als gevolg van het Hallo-script wordt uitgevoerd met deze instelling, Hallo aantal momentopnamen, met inbegrip van de nieuwe opslag Hallo momentopname, wordt _5_.

 >[!NOTE]
 > Dit script vermindert het aantal momentopnamen Hallo alleen als de meest recente vorige momentopname Hallo meer dan een uur oud is. Hallo script verwijdert niet de momentopnamen die minder dan een uur oud.

Deze beperkingen zijn verwante toohello optionele noodherstel functionaliteit beschikbaar wordt gesteld.

Als u een set van momentopnamen met voorvoegsel toomaintain niet langer wilt, kunt u Hallo script uitvoeren _0_ zoals hello bewaren number tooremove alle momentopnamen die overeenkomt met dat voorvoegsel. Alle momentopnamen verwijderen kan echter Hallo-mogelijkheden van herstel na noodgevallen beïnvloeden.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>De meest recente HANA momentopname toohello herstellen

In Hallo gebeurtenis kunnen zich een scenario voor productie-omlaag, Hallo proces van het herstellen van een momentopname van de opslag worden gestart als een klant incident met SAP HANA op Azure Service Management. Een onverwachte scenario mogelijk een hoge urgentie kwestie als gegevens in een productie-systeem en Hallo alleen manier tooretrieve Hallo gegevens toorestore Hallo-productiedatabase is verwijderd.

Op Hallo daarentegen een punt in tijd herstel kan lage urgentie en geplande dagen van tevoren. U kunt dit herstel met SAP HANA plannen op Azure Service Management in plaats van een probleem met hoge prioriteit verhogen. Bijvoorbeeld, u mogelijk mee moet houden tootry een upgrade van Hallo SAP-software door het toepassen van een nieuw pakket in de uitbreiding, en u vervolgens moet toorevert back-tooa momentopname die Hallo status vóór de upgrade Hallo EHP vertegenwoordigt.

Voordat u Hallo aanvraag verzendt, moet u toodo voorbereiding. SAP HANA in Azure Service Management-team kan vervolgens Hallo aanvraag verwerken en geef Hallo hersteld volumes. Daarna is tooyou toorestore Hallo HANA-database op basis van Hallo momentopnamen. Hier ziet u hoe tooprepare voor Hallo aanvragen:

>[!NOTE]
>De gebruikersinterface kan afwijken van Hallo volgende schermafbeeldingen, afhankelijk van Hallo SAP HANA-versie die u gebruikt.

1. Bepaal welke toorestore momentopname. Alleen Hallo hana/gegevensvolume zou worden teruggezet, tenzij anders wordt aangegeven.

2. Hallo HANA exemplaar afgesloten.

 ![Hallo HANA exemplaar afsluiten](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Ontkoppel de gegevensvolumes Hallo op elk knooppunt HANA-database. Hallo-herstellen van de momentopname Hallo mislukt als Hallo gegevensvolumes niet ontkoppeld zijn.

 ![Hallo gegevensvolumes ontkoppelen op elk knooppunt HANA-database](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Open een Azure-ondersteuning aanvraag tooinstruct Hallo herstel van een momentopname van een specifieke.

 - Tijdens het Hallo terugzetten: SAP HANA op Azure Service Management kan u vragen tooattend een telefonische tooensure die geen gegevens ophalen van gaan verloren.

 - Na het herstellen van Hallo: SAP HANA op Azure Service Management waarschuwt u als Hallo opslag momentopname is teruggezet.

5. Na het herstellen van Hallo proces is voltooid, opnieuw koppelen van alle gegevensvolumes.

 ![Alle gegevensvolumes opnieuw koppelen](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Selecteer herstelopties in SAP HANA Studio als ze niet automatisch afkomstig zijn van wanneer u tooHANA DB met SAP HANA Studio herstelt. Hallo volgende voorbeeld ziet u een herstelbewerking toohello laatste HANA momentopname. Een momentopname van een HANA opslag momentopnamen en als u de meest recente opslag momentopname toohello herstelt, moet de meest recente HANA momentopname Hallo. (Als u tooolder opslag-momentopnamen herstellen wilt, moet u toolocate Hallo HANA momentopname is gebaseerd op Hallo tijd Hallo opslag momentopname werd gemaakt.)

 ![Selecteer de opties herstellen vanuit SAP HANA-Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Selecteer **herstellen Hallo tooa specifieke gegevens back-up of opslag databasemomentopname**.

 ![Hallo 'Hersteltype opgeven' venster](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Selecteer **Geef back-up zonder catalogus**.

 ![Hallo 'Back-up locatie opgeven' venster](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. In Hallo **doeltype** selecteert **momentopname**.

 ![Hallo 'Geef Hallo back-up tooRecover' venster](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Klik op **voltooien** toostart Hallo herstelproces.

 ![Klik op toostart Hallo herstelproces "Voltooid"](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. Hallo HANA-database is hersteld en toohello HANA momentopname die opgenomen in Hallo opslag momentopname wordt hersteld.

 ![HANA-database is teruggezet en herstelde toohello HANA momentopname](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Herstellen van de meest recente is toohello

Hallo herstelt volgende proces Hallo HANA momentopname die is opgenomen in het Hallo-opslag-momentopnamen. Vervolgens worden Hallo transactie logboek back-ups toohello meest recente toestand van Hallo database hersteld voordat het Hallo opslag momentopname is teruggezet.

>[!IMPORTANT]
>Voordat u doorgaat, zorg ervoor dat er een volledige en aaneengesloten reeks transactielogboekback-ups. Zonder deze back-ups, kunt u de huidige status Hallo van Hallo-database niet terugzetten.

1. Stap 1-6 van de voorgaande procedure in 'Herstellen toohello meest recente HANA momentopname.' hello voltooien

2. Selecteer **hello tooits meest recente databasestatus herstellen**.

 ![Selecteer 'Hello tooits meest recente databasestatus herstellen'](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Geef de locatie op Hallo van Hallo meest recente HANA logboekback-ups. Hallo-locatie moet toocontain alle HANA transactielogboekback-ups van Hallo HANA momentopname toohello meest recente status.

 ![Geef de locatie Hallo van Hallo meest recente HANA logboekback-ups](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Selecteer een back-up uit welke toorecover Hallo-database. In ons voorbeeld is dit Hallo HANA momentopname die is opgenomen in het Hallo-opslag-momentopnamen. (Alleen een momentopname wordt vermeld in de volgende schermafbeelding Hallo.)

 ![Selecteer een back-up uit welke toorecover Hallo-database](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Schakel Hallo **gebruik Delta back-ups** selectievakje in als delta's niet bestaan tussen Hallo-tijd van Hallo HANA momentopname en de meest recente status Hallo.

 ![Schakel Hallo 'Gebruik Delta back-ups' selectievakje in als er geen delta's bestaan](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Klik op Samenvatting welkomstscherm **voltooien** toostart Hallo herstelbewerking procedure.

 ![Klik op 'Voltooid' in de samenvatting welkomstscherm](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Herstellende tooanother punt in tijd
toorecover tooa punt in tijd tussen het Hallo HANA momentopname (opgenomen in Hallo opslag momentopname) en die is hoger dan Hallo HANA momentopname maken van het herstel van een punt in tijd Hallo te volgen:

1. Zorg ervoor dat u alle transactielogboekback-ups van Hallo HANA momentopname toohello tijd die u toorecover wilt hebt.
2. Begin Hallo procedure onder "Toohello meest recente herstelstatus."
3. In stap 2 van het Hallo-procedure in Hallo **hersteltype opgeven** Selecteer **herstellen Hallo database toohello volgende tijdstip**, geef Hallo punt in tijd en voltooi stap 3-6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Bewaking van Hallo uitvoering van momentopnamen

U moet toomonitor Hallo uitvoering van opslag-momentopnamen. Hallo-script dat wordt uitgevoerd een opslag-momentopnamen tooa uitvoerbestand schrijft en slaat deze toohello dezelfde locatie als Hallo Perl-scripts. Een afzonderlijk bestand is geschreven voor elke momentopname. Hallo Hallo-uitvoer van elk bestand duidelijk aangeeft verschillende fasen die Hallo momentopname script wordt uitgevoerd:

- Hallo-volumes die toocreate moeten zoeken een momentopname
- Hallo momentopnamen die afkomstig zijn uit deze volumes zoeken
- Verwijderen van eventuele bestaande momentopnamen toomatch Hallo aantal momentopnamen die u hebt opgegeven
- Maken van een momentopname HANA
- Maken van een Hallo opslag momentopname via Hallo volumes
- Hallo HANA momentopname verwijderen
- Naam van recentste Hallo momentopname te maken van**.0**

Hallo belangrijkste deel van het Hallo-script is als volgt:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
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
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
U kunt van dit voorbeeld zien hoe Hallo script records maken van een momentopname van Hallo HANA Hallo. In geval van de scale-out hello, wordt dit proces gestart op Hallo hoofdknooppunt. Hallo-hoofdknooppunt initieert Hallo synchrone maken van momentopnamen op elke worker-knooppunten Hallo Hallo. Vervolgens wordt Hallo opslag momentopname gemaakt. Na de geslaagde uitvoering Hallo van Hallo-opslag-momentopnamen, is Hallo HANA momentopname verwijderd.
