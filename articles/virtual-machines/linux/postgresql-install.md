---
title: aaaSet up PostgreSQL op een Linux-VM | Microsoft Docs
description: Meer informatie over hoe tooinstall en PostgreSQL configureren op een virtuele Linux-machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>PostgreSQL installeren en configureren op Azure
PostgreSQL is een vergelijkbaar tooOracle geavanceerde open-source-database en DB2. Het bevat enterprise-ready functies zoals volledige ACID naleving, betrouwbare transactionele verwerking en meerdere versie gelijktijdigheidbeheer. Het ondersteunt ook standaarden zoals ANSI SQL en SQL/MED (inclusief externe gegevens wrappers voor Oracle, MySQL, MongoDB en vele andere). Het is maximaal worden uitgebreid met ondersteuning voor meer dan 12 procedurele talen, GIN en basisvertalingen indexen, ondersteuning voor ruimtelijke gegevens en meerdere NoSQL-achtige functies voor JSON of toepassingen op basis van sleutels-waarde.

In dit artikel leert u hoe tooinstall en PostgreSQL configureren op een virtuele machine van Azure waarop Linux wordt uitgevoerd.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>PostgreSQL installeren
> [!NOTE]
> U moet al een virtuele machine van Azure waarop Linux wordt uitgevoerd in de volgorde toocomplete in deze zelfstudie hebben. toocreate en stel een Linux-VM voordat u doorgaat, Zie de [Azure Linux VM-zelfstudie](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

In dit geval poort 1999 gebruiken als Hallo PostgreSQL-poort.  

Verbinding maken met toohello Linux VM u via de PuTTY hebt gemaakt. Als dit Hallo eerste keer dat u een Azure Linux VM, Zie [hoe tooUse SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn hoe toouse PuTTY tooconnect tooa Linux VM.

1. Voer Hallo opdracht tooswitch toohello hoofdmap (admin) te volgen:
   
        # sudo su -
2. Sommige distributies hebben afhankelijkheden die moeten worden geïnstalleerd voordat u installeert PostgreSQL. Controleren op uw distro in deze lijst en voer de juiste opdracht Hallo:
   
   * Red Hat base Linux:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian base Linux:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. PostgreSQL downloaden naar een Hallo-hoofdmap en pak vervolgens Hallo-pakket:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Hallo hierboven is een voorbeeld. U vindt Hallo meer gedetailleerde adres in Hallo downloaden [Index/pub/bron /](https://ftp.postgresql.org/pub/source/).
4. toostart hello build en voer deze opdrachten uit:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Als u wilt dat toobuild alles die kunnen worden opgebouwd, met inbegrip van Hallo documentatie (HTML en man's) en aanvullende modules (contrib), Voer Hallo volgende opdracht in plaats daarvan:
   
        # gmake install-world
   
    U ontvangt Hallo volgende bevestigingsbericht:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>PostgreSQL configureren
1. (Optioneel) Maken van een symbolische koppeling tooshorten hello PostgreSQL verwijzing toonot Hallo versienummer omvatten:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Maak een map voor Hallo database:
   
        # mkdir -p /opt/pgsql_data
3. Een niet-hoofdgebruiker profiel maken en beheren van de gebruiker. Schakel de nieuwe gebruiker toothis (aangeroepen *postgres* in ons voorbeeld):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Uit veiligheidsoverwegingen PostgreSQL maakt gebruik van een niet-hoofdgebruiker tooinitialize, openen of afgesloten Hallo-database.
   > 
   > 
4. Hallo bewerken *bash_profile* bestand hiertoe onderstaande Hallo-opdrachten. Deze regels worden toegevoegd toohello einde van Hallo *bash_profile* bestand:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Hallo uitvoeren *bash_profile* bestand:
   
        $ source .bash_profile
6. Uw installatie valideren met behulp van de volgende opdracht Hallo:
   
        $ which psql
   
    Als de installatie geslaagd is, ziet u Hallo antwoord te volgen:
   
        /opt/pgsql/bin/psql
7. U kunt ook controleren Hallo PostgreSQL-versie:
   
        $ psql -V
8. Hallo database initialiseren:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    U ontvangt Hallo volgende uitvoer:

![Afbeelding](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>PostgreSQL instellen
<!--    [postgres@ test ~]$ exit -->

Voer Hallo volgende opdrachten:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Wijzig de twee variabelen in Hallo /etc/init.d/postgresql-bestand. Hallo voorvoegsel toohello installatiepad van PostgreSQL is ingesteld: **/opt/pgsql**. PGDATA toohello gegevens opslagpad van PostgreSQL is ingesteld: **/opt/pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Afbeelding](./media/postgresql-install/no2.png)

Hallo bestand toomake wijzigen van het uitvoerbare bestand:

    # chmod +x /etc/init.d/postgresql

PostgreSQL starten:

    # /etc/init.d/postgresql start

Controleer of Hallo-eindpunt van PostgreSQL op:

    # netstat -tunlp|grep 1999

Hallo volgende uitvoer weergegeven:

![Afbeelding](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Verbinding maken met toohello Postgres database
Toohello postgres gebruiker nogmaals switch:

    # su - postgres

Een database Postgres maken:

    $ createdb events

Verbinding maken met een database van de toohello-gebeurtenissen die u zojuist hebt gemaakt:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Maken en verwijderen van een tabel Postgres
Nu dat u toohello database hebt gekoppeld, kunt u tabellen maken in het.

Bijvoorbeeld, een nieuwe tabel van de voorbeeld-Postgres maken met behulp van de volgende opdracht Hallo:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

U hebt nu een tabel met vier kolommen Hello ingesteld na de kolomnamen en beperkingen:

1. Hallo "name" kolom heeft is beperkt door Hallo VARCHAR opdracht toobe minder dan 20 tekens lang.
2. Hallo 'voeding' kolom geeft Hallo voeding item ervoor te dat elke persoon zorgen. VARCHAR beperkt deze toobe tekst onder 30 tekens bevatten.
3. Hallo bevestigd' ' kolom records of Hallo persoon uitnodiging heeft geaccepteerd toohello Amerikaans. Hallo acceptabele waarden zijn "Y" en "N".
4. Hallo 'datum' kolom worden weergegeven wanneer ze zich aangemeld voor Hallo-gebeurtenis. Postgres vereist dat datums worden geschreven als jjjj-mm-dd.

U ziet de volgende Hallo als de tabel is gemaakt:

![Afbeelding](./media/postgresql-install/no4.png)

U kunt ook de tabelstructuur Hallo controleren met behulp van de volgende opdracht Hallo:

![Afbeelding](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Gegevens tooa tabel toevoegen
Voeg eerst de informatie in een rij:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

U ziet deze uitvoer:

![Afbeelding](./media/postgresql-install/no6.png)

U kunt een aantal meer mensen toohello tabel ook toevoegen. Hier volgen enkele opties of u kunt uw eigen maken:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Tabellen weergeven
Gebruik Hallo opdracht tooshow een tabel te volgen:

    select * from potluck;

Hallo-uitvoer is:

![Afbeelding](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Gegevens in een tabel verwijderen
Gebruik Hallo opdracht toodelete gegevens in een tabel te volgen:

    delete from potluck where name=’John’;

Hiermee verwijdert u alle Hallo-informatie in Hallo 'John' rij. Hallo-uitvoer is:

![Afbeelding](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Gegevens bijwerken in een tabel
Gebruik hello opdracht tooupdate gegevens in een tabel te volgen. Voor deze een Sandy heeft bevestigd dat ze is aanwezig, zodat we haar RSVP van "N" te wijzigen 'Y':

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Meer informatie over PostgreSQL
Nu dat u Hallo-installatie van PostgreSQL in een Azure Linux VM hebt voltooid, kunt u profiteren van gebruiken in Azure. toolearn meer informatie over PostgreSQL, gaat u naar Hallo [PostgreSQL website](http://www.postgresql.org/).

