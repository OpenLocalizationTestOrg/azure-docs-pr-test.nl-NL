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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="5155e-103">PostgreSQL installeren en configureren op Azure</span><span class="sxs-lookup"><span data-stu-id="5155e-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="5155e-104">PostgreSQL is een vergelijkbaar tooOracle geavanceerde open-source-database en DB2.</span><span class="sxs-lookup"><span data-stu-id="5155e-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="5155e-105">Het bevat enterprise-ready functies zoals volledige ACID naleving, betrouwbare transactionele verwerking en meerdere versie gelijktijdigheidbeheer.</span><span class="sxs-lookup"><span data-stu-id="5155e-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="5155e-106">Het ondersteunt ook standaarden zoals ANSI SQL en SQL/MED (inclusief externe gegevens wrappers voor Oracle, MySQL, MongoDB en vele andere).</span><span class="sxs-lookup"><span data-stu-id="5155e-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="5155e-107">Het is maximaal worden uitgebreid met ondersteuning voor meer dan 12 procedurele talen, GIN en basisvertalingen indexen, ondersteuning voor ruimtelijke gegevens en meerdere NoSQL-achtige functies voor JSON of toepassingen op basis van sleutels-waarde.</span><span class="sxs-lookup"><span data-stu-id="5155e-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="5155e-108">In dit artikel leert u hoe tooinstall en PostgreSQL configureren op een virtuele machine van Azure waarop Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5155e-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="5155e-109">PostgreSQL installeren</span><span class="sxs-lookup"><span data-stu-id="5155e-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="5155e-110">U moet al een virtuele machine van Azure waarop Linux wordt uitgevoerd in de volgorde toocomplete in deze zelfstudie hebben.</span><span class="sxs-lookup"><span data-stu-id="5155e-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="5155e-111">toocreate en stel een Linux-VM voordat u doorgaat, Zie de [Azure Linux VM-zelfstudie](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5155e-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="5155e-112">In dit geval poort 1999 gebruiken als Hallo PostgreSQL-poort.</span><span class="sxs-lookup"><span data-stu-id="5155e-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="5155e-113">Verbinding maken met toohello Linux VM u via de PuTTY hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5155e-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="5155e-114">Als dit Hallo eerste keer dat u een Azure Linux VM, Zie [hoe tooUse SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn hoe toouse PuTTY tooconnect tooa Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5155e-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="5155e-115">Voer Hallo opdracht tooswitch toohello hoofdmap (admin) te volgen:</span><span class="sxs-lookup"><span data-stu-id="5155e-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="5155e-116">Sommige distributies hebben afhankelijkheden die moeten worden geïnstalleerd voordat u installeert PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="5155e-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="5155e-117">Controleren op uw distro in deze lijst en voer de juiste opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5155e-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="5155e-118">Red Hat base Linux:</span><span class="sxs-lookup"><span data-stu-id="5155e-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="5155e-119">Debian base Linux:</span><span class="sxs-lookup"><span data-stu-id="5155e-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="5155e-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="5155e-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="5155e-121">PostgreSQL downloaden naar een Hallo-hoofdmap en pak vervolgens Hallo-pakket:</span><span class="sxs-lookup"><span data-stu-id="5155e-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="5155e-122">Hallo hierboven is een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5155e-122">hello above is an example.</span></span> <span data-ttu-id="5155e-123">U vindt Hallo meer gedetailleerde adres in Hallo downloaden [Index/pub/bron /](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="5155e-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="5155e-124">toostart hello build en voer deze opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="5155e-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="5155e-125">Als u wilt dat toobuild alles die kunnen worden opgebouwd, met inbegrip van Hallo documentatie (HTML en man's) en aanvullende modules (contrib), Voer Hallo volgende opdracht in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="5155e-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="5155e-126">U ontvangt Hallo volgende bevestigingsbericht:</span><span class="sxs-lookup"><span data-stu-id="5155e-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="5155e-127">PostgreSQL configureren</span><span class="sxs-lookup"><span data-stu-id="5155e-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="5155e-128">(Optioneel) Maken van een symbolische koppeling tooshorten hello PostgreSQL verwijzing toonot Hallo versienummer omvatten:</span><span class="sxs-lookup"><span data-stu-id="5155e-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="5155e-129">Maak een map voor Hallo database:</span><span class="sxs-lookup"><span data-stu-id="5155e-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="5155e-130">Een niet-hoofdgebruiker profiel maken en beheren van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5155e-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="5155e-131">Schakel de nieuwe gebruiker toothis (aangeroepen *postgres* in ons voorbeeld):</span><span class="sxs-lookup"><span data-stu-id="5155e-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="5155e-132">Uit veiligheidsoverwegingen PostgreSQL maakt gebruik van een niet-hoofdgebruiker tooinitialize, openen of afgesloten Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="5155e-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="5155e-133">Hallo bewerken *bash_profile* bestand hiertoe onderstaande Hallo-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="5155e-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="5155e-134">Deze regels worden toegevoegd toohello einde van Hallo *bash_profile* bestand:</span><span class="sxs-lookup"><span data-stu-id="5155e-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="5155e-135">Hallo uitvoeren *bash_profile* bestand:</span><span class="sxs-lookup"><span data-stu-id="5155e-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="5155e-136">Uw installatie valideren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5155e-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="5155e-137">Als de installatie geslaagd is, ziet u Hallo antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="5155e-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="5155e-138">U kunt ook controleren Hallo PostgreSQL-versie:</span><span class="sxs-lookup"><span data-stu-id="5155e-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="5155e-139">Hallo database initialiseren:</span><span class="sxs-lookup"><span data-stu-id="5155e-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="5155e-140">U ontvangt Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5155e-140">You should receive hello following output:</span></span>

![Afbeelding](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="5155e-142">PostgreSQL instellen</span><span class="sxs-lookup"><span data-stu-id="5155e-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="5155e-143">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5155e-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="5155e-144">Wijzig de twee variabelen in Hallo /etc/init.d/postgresql-bestand.</span><span class="sxs-lookup"><span data-stu-id="5155e-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="5155e-145">Hallo voorvoegsel toohello installatiepad van PostgreSQL is ingesteld: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="5155e-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="5155e-146">PGDATA toohello gegevens opslagpad van PostgreSQL is ingesteld: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="5155e-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Afbeelding](./media/postgresql-install/no2.png)

<span data-ttu-id="5155e-148">Hallo bestand toomake wijzigen van het uitvoerbare bestand:</span><span class="sxs-lookup"><span data-stu-id="5155e-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="5155e-149">PostgreSQL starten:</span><span class="sxs-lookup"><span data-stu-id="5155e-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="5155e-150">Controleer of Hallo-eindpunt van PostgreSQL op:</span><span class="sxs-lookup"><span data-stu-id="5155e-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="5155e-151">Hallo volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5155e-151">You should see hello following output:</span></span>

![Afbeelding](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="5155e-153">Verbinding maken met toohello Postgres database</span><span class="sxs-lookup"><span data-stu-id="5155e-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="5155e-154">Toohello postgres gebruiker nogmaals switch:</span><span class="sxs-lookup"><span data-stu-id="5155e-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="5155e-155">Een database Postgres maken:</span><span class="sxs-lookup"><span data-stu-id="5155e-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="5155e-156">Verbinding maken met een database van de toohello-gebeurtenissen die u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5155e-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="5155e-157">Maken en verwijderen van een tabel Postgres</span><span class="sxs-lookup"><span data-stu-id="5155e-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="5155e-158">Nu dat u toohello database hebt gekoppeld, kunt u tabellen maken in het.</span><span class="sxs-lookup"><span data-stu-id="5155e-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="5155e-159">Bijvoorbeeld, een nieuwe tabel van de voorbeeld-Postgres maken met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5155e-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="5155e-160">U hebt nu een tabel met vier kolommen Hello ingesteld na de kolomnamen en beperkingen:</span><span class="sxs-lookup"><span data-stu-id="5155e-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="5155e-161">Hallo "name" kolom heeft is beperkt door Hallo VARCHAR opdracht toobe minder dan 20 tekens lang.</span><span class="sxs-lookup"><span data-stu-id="5155e-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="5155e-162">Hallo 'voeding' kolom geeft Hallo voeding item ervoor te dat elke persoon zorgen.</span><span class="sxs-lookup"><span data-stu-id="5155e-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="5155e-163">VARCHAR beperkt deze toobe tekst onder 30 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="5155e-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="5155e-164">Hallo bevestigd' ' kolom records of Hallo persoon uitnodiging heeft geaccepteerd toohello Amerikaans.</span><span class="sxs-lookup"><span data-stu-id="5155e-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="5155e-165">Hallo acceptabele waarden zijn "Y" en "N".</span><span class="sxs-lookup"><span data-stu-id="5155e-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="5155e-166">Hallo 'datum' kolom worden weergegeven wanneer ze zich aangemeld voor Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5155e-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="5155e-167">Postgres vereist dat datums worden geschreven als jjjj-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="5155e-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="5155e-168">U ziet de volgende Hallo als de tabel is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5155e-168">You should see hello following if your table has been successfully created:</span></span>

![Afbeelding](./media/postgresql-install/no4.png)

<span data-ttu-id="5155e-170">U kunt ook de tabelstructuur Hallo controleren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="5155e-170">You can also check hello table structure by using hello following command:</span></span>

![Afbeelding](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="5155e-172">Gegevens tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="5155e-172">Add data tooa table</span></span>
<span data-ttu-id="5155e-173">Voeg eerst de informatie in een rij:</span><span class="sxs-lookup"><span data-stu-id="5155e-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="5155e-174">U ziet deze uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5155e-174">You should see this output:</span></span>

![Afbeelding](./media/postgresql-install/no6.png)

<span data-ttu-id="5155e-176">U kunt een aantal meer mensen toohello tabel ook toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5155e-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="5155e-177">Hier volgen enkele opties of u kunt uw eigen maken:</span><span class="sxs-lookup"><span data-stu-id="5155e-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="5155e-178">Tabellen weergeven</span><span class="sxs-lookup"><span data-stu-id="5155e-178">Show tables</span></span>
<span data-ttu-id="5155e-179">Gebruik Hallo opdracht tooshow een tabel te volgen:</span><span class="sxs-lookup"><span data-stu-id="5155e-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="5155e-180">Hallo-uitvoer is:</span><span class="sxs-lookup"><span data-stu-id="5155e-180">hello output is:</span></span>

![Afbeelding](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="5155e-182">Gegevens in een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="5155e-182">Delete data in a table</span></span>
<span data-ttu-id="5155e-183">Gebruik Hallo opdracht toodelete gegevens in een tabel te volgen:</span><span class="sxs-lookup"><span data-stu-id="5155e-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="5155e-184">Hiermee verwijdert u alle Hallo-informatie in Hallo 'John' rij.</span><span class="sxs-lookup"><span data-stu-id="5155e-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="5155e-185">Hallo-uitvoer is:</span><span class="sxs-lookup"><span data-stu-id="5155e-185">hello output is:</span></span>

![Afbeelding](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="5155e-187">Gegevens bijwerken in een tabel</span><span class="sxs-lookup"><span data-stu-id="5155e-187">Update data in a table</span></span>
<span data-ttu-id="5155e-188">Gebruik hello opdracht tooupdate gegevens in een tabel te volgen.</span><span class="sxs-lookup"><span data-stu-id="5155e-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="5155e-189">Voor deze een Sandy heeft bevestigd dat ze is aanwezig, zodat we haar RSVP van "N" te wijzigen 'Y':</span><span class="sxs-lookup"><span data-stu-id="5155e-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="5155e-190">Meer informatie over PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5155e-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="5155e-191">Nu dat u Hallo-installatie van PostgreSQL in een Azure Linux VM hebt voltooid, kunt u profiteren van gebruiken in Azure.</span><span class="sxs-lookup"><span data-stu-id="5155e-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="5155e-192">toolearn meer informatie over PostgreSQL, gaat u naar Hallo [PostgreSQL website](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="5155e-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

