---
title: SSL-verbindingen in Azure-Database voor PostgreSQL aaaConfigure | Microsoft Docs
description: Instructies en informatie tooconfigure Azure-Database voor PostgreSQL en de bijbehorende toepassingen tooproperly gebruik van SSL-verbindingen.
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>SSL-verbindingen in de Azure-Database configureren voor PostgreSQL
Azure-Database voor PostgreSQL verkiest verbinding maken met uw client toepassingen toohello PostgreSQL-service met Secure Sockets Layer (SSL). Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.

Hallo PostgreSQL-database-service is standaard geconfigureerd toorequire SSL-verbinding. Desgewenst kunt u uitschakelen dat SSL vereist voor het verbinden van tooyour database-service als de clienttoepassing biedt geen ondersteuning voor SSL-verbindingen. 

## <a name="enforcing-ssl-connections"></a>Afdwingen van SSL-verbindingen
Afdwinging van SSL-verbindingen is standaard ingeschakeld voor alle Azure-Database voor PostgreSQL-servers die zijn ingericht via hello Azure-portal en CLI. 

Evenzo bevatten verbindingsreeksen die vooraf zijn gedefinieerd in Hallo 'Verbindingsreeksen' instellingen onder uw server in Azure-portal Hallo Hallo vereiste parameters voor algemene talen tooconnect tooyour database-server via SSL. Hallo SSL parameter varieert op basis van Hallo-connector, bijvoorbeeld ' ssl = true ' of ' sslmode = vereisen ' of ' sslmode = vereist ' en andere variaties.

## <a name="configure-enforcement-of-ssl"></a>Afdwinging van SSL configureren
U kunt desgewenst uitschakelen afdwingen SSL-verbindingen. Microsoft Azure raadt tooalways inschakelen **afdwingen SSL-verbinding** instellen voor een betere beveiliging.

### <a name="using-hello-azure-portal"></a>Met behulp van hello Azure-portal
Ga naar uw Azure-Database voor PostgreSQL-server en op **verbindingsbeveiliging**. Hallo aan/uit-knop tooenable in- of uitschakelen van Hallo **afdwingen SSL-verbinding** instelling. Klik vervolgens op **Opslaan**. 

![Verbindingsbeveiliging - Disable SSL afdwingen](./media/concepts-ssl-connection-security/1-disable-ssl.png)

U kunt Hallo instelling bevestigen door het bekijken van Hallo **overzicht** pagina toosee Hallo **SSL afdwingen status** indicator.

### <a name="using-azure-cli"></a>Azure CLI gebruiken
U kunt inschakelen of uitschakelen van Hallo **ssl-afdwinging** met behulp van de parameter `Enabled` of `Disabled` waarden respectievelijk in Azure CLI.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Zorg ervoor dat uw toepassing of framework ondersteunt SSL-verbindingen
Veel voorkomende toepassingsframeworks die gebruikmaken van PostgreSQL voor databaseservices, zoals Drupal en Django, doen SSL niet standaard ingeschakeld tijdens de installatie. Inschakelen van SSL-verbindingen moet worden uitgevoerd na de installatie of via CLI-opdrachten specifieke toohello toepassing. Als uw server PostgreSQL is afdwingen van SSL-verbindingen en toepassing hello die zijn gekoppeld, is niet goed geconfigureerd, mislukken de toepassing hello tooconnect tooyour database-server. Hoe raadpleegt u uw toepassing documentatie toolearn tooenable SSL-verbindingen.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Toepassingen waarvoor certificaatverificatie van het voor SSL-verbindingen
In sommige gevallen moet toepassingen een lokaal certificaatbestand gegenereerd op basis van een vertrouwde certificeringsinstantie (CA)-certificaat (.cer)-bestand tooconnect veilig. Zie Hallo stappen tooobtain Hallo cer-bestand te volgen, Hallo certificaat decoderen en bindt dit tooyour toepassing.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Hallo-certificaatbestand van Hallo certificeringsinstantie (CA) downloaden 
Hallo-certificaat nodig toocommunicate via SSL met uw Azure-Database voor PostgreSQL-server zich bevindt [hier](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Hallo certificaat lokaal bestand downloaden.

### <a name="download-and-install-openssl-on-your-machine"></a>Download en installeer OpenSSL op uw computer 
Hallo-certificaatbestand toodecode die nodig zijn voor uw toepassing tooconnect veilig tooyour database-server, moet u tooinstall OpenSSL op uw lokale computer.

#### <a name="for-linux-os-x-or-unix"></a>Voor Linux, Unix of OS X
Hallo OpenSSL-bibliotheken vindt u in de broncode rechtstreeks vanuit Hallo [OpenSSL Software Foundation](http://www.openssl.org). Hallo leiden volgende instructies u door Hallo stappen nodig tooinstall OpenSSL op uw PC Linux. In dit artikel worden opdrachten bekend toowork op Ubuntu 12.04 en hoger.

Open een terminalsessie en OpenSSL installeren
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Hallo-bestanden extraheren uit het downloadpakket Hallo
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Voer Hallo directory waar het Hallo-bestanden zijn uitgepakt. Standaard moet als volgt.

```bash
cd openssl-1.1.0e
```
OpenSSL configureren door het uitvoeren van de volgende opdracht Hallo. Als u Hallo-bestanden in een map anders dan /usr/local/openssl wilt, maken of toochange Hallo na zo nodig.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Nu OpenSSL correct is geconfigureerd, moet u toocompile het tooconvert uw certificaat. toocompile hello volgende opdracht uitvoeren:

```bash
make
```
Zodra de compileren is voltooid, bent u klaar tooinstall OpenSSL als een uitvoerbaar bestand door het uitvoeren van de volgende opdracht Hallo:
```bash
make install
```
tooconfirm dat u hebt OpenSSL geïnstalleerd op uw systeem, Voer Hallo volgende opdracht uit en controleer zeker dat u krijgt Hallo toomake dezelfde uitvoer.

```bash
/usr/local/openssl/bin/openssl version
```
Als dit lukt, kunt u Hallo volgende bericht moeten zien.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Voor Windows
OpenSSL installeren op een Windows-PC kan worden uitgevoerd in de volgende manieren Hallo:
1. **(Aanbevolen)**  Hello ingebouwde Bash voor Windows-functionaliteit in Windows 10 en hoger, OpenSSL wordt standaard geïnstalleerd. Instructies over hoe tooenable Bash voor Windows-functionaliteit in Windows 10 kan worden gevonden [hier](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Via het downloaden van een toepassing Win32/64 is geleverd door het Hallo-community. Terwijl Hallo OpenSSL Software Foundation biedt niet of een specifieke Windows-installatieprogramma's tekent, bieden ze een lijst met beschikbare installatieprogramma's [hier](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Uw certificaatbestand decoderen
Hallo basis-CA-bestand in een versleutelde indeling is gedownload. Certificaatbestand van OpenSSL toodecode hello gebruiken. toodo worden dus deze OpenSSL-opdracht uitvoeren:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>TooAzure Database voor PostgreSQL verbinding te maken met SSL-verificatie
Nu dat u hebt uw certificaat is gedecodeerd, kunt u nu verbinding databaseserver tooyour veilig via SSL. certificaat-serververificatie met tooallow Hallo certificaat moet worden geplaatst in Hallo bestand ~/.postgresql/root.crt in Hallo basismap. (Op Microsoft Windows hello-bestand is met de naam % APPDATA%\postgresql\root.crt.). Hallo hieronder vindt u instructies voor het verbinden van tooAzure Database voor PostgreSQL.

> [!NOTE]
> Er is momenteel een bekend probleem als u ' sslmode controleren volledige = ' mislukt in uw service verbinding toohello Hallo verbinding met de volgende fout Hallo: _servercertificaat voor '&lt;regio&gt;. Control.database.Windows.NET' (en 7 andere namen) niet overeenkomt met hostnaam '&lt;servername&gt;. postgres.database.azure.com '._
> Als ' sslmode = controleren volledig ' is vereist, servernaamconventie Hallo gebruik  **&lt;servername&gt;. database.windows.net** als de hostnaam van uw verbinding-tekenreeks. We zullen deze beperking in toekomstige Hallo tooremove. Verbindingen met andere [SSL modi](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) toouse Hallo voorkeur host naamgevingsconventie moet worden voortgezet  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Werken met het opdrachtregelhulpprogramma psql
Hallo volgende voorbeeld ziet u hoe toosuccessfully tooyour PostgreSQL-server op Hallo psql opdrachtregelprogramma met verbinding. Gebruik Hallo `root.crt` -bestand gemaakt en Hallo `sslmode=verify-ca` of `sslmode=verify-full` optie.

Gebruik Hallo PostgreSQL-opdrachtregelinterface, Hallo volgende opdracht uitvoeren:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
Als dit lukt, wordt u Hallo volgende uitvoer:
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>Met behulp van pgAdmin GUI-hulpprogramma
Tooset hello pgAdmin 4 tooconnect veilig configureren via SSL vereist `SSL mode = Verify-CA` of `SSL mode = Verify-Full` als volgt:

![Schermopname van pgAdmin - verbinding - SSL-modus vereisen](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Volgende stappen
Bekijk verschillende toepassing connectiviteitsopties na [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)
