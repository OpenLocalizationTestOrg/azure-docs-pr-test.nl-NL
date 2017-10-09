---
title: aaaConnect tooSQL Database gebruiken met C en C++ | Microsoft Docs
description: Gebruik Hallo voorbeeld code in deze toobuild snel starten met een moderne toepassingen met C++ en ondersteund door een krachtige relationele database in Hallo cloud met Azure SQL Database.
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Verbinding maken met tooSQL Database gebruiken met C en C++
Dit bericht is gericht op C en C++ ontwikkelaars probeert tooconnect tooAzure SQL-database. Het is onderverdeeld in secties, zodat u kunt springen toohello sectie waarmee uw interesse beste wordt vastgelegd. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Vereisten voor Hallo C/C++-zelfstudie
Controleer of er Hallo volgende items:

* Een actief Azure-account. Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/). U moet Hallo C++ taal onderdelen toobuild installeren en uitvoeren van dit voorbeeld.
* [Visual Studio Linux ontwikkeling](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Als u op Linux ontwikkelt, moet u ook Hallo Visual Studio Linux uitbreiding installeren. 

## <a id="AzureSQL"></a>Azure SQL Database en SQL Server op virtuele machines
Azure SQL is gebaseerd op Microsoft SQL Server en is ontworpen tooprovide een hoge beschikbaarheid, zodat en schaalbare service. Er zijn veel voordelen toousing SQL Azure via uw eigen database met on-premises. Met Azure SQL niet u tooinstall hebt, instellen, beheren of beheren van uw database, maar alleen Hallo inhoud en structuur van uw database Hallo. Typische dingen die we bang met databases zoals zijn alle fouttolerantie en redundantie ingebouwd in. 

Azure heeft momenteel twee opties voor het hosten van SQL server-werkbelastingen: Azure SQL database, -database als een service en de SQL server op virtuele Machines (VM). We krijgt geen informatie over de verschillen tussen deze twee hello, behalve dat Azure SQL-database de beste keuze voor nieuwe voordeel van cloud-gebaseerde toepassingen tootake Hallo kostenbesparingen is en optimalisatie van de prestaties die cloudservices bieden. Als u plan te bent migreren of het uitbreiden van uw on-premises toepassingen toohello cloud, mogelijk SQL server op virtuele machine van Azure werken beter voor u. simpel tookeep voor dit artikel, maken we een Azure SQL database. 

## <a id="ODBC"></a>Data access-technologieën: ODBC en OLE DB
Maken van verbinding tooAzure SQL DB gaat niet anders en er zijn momenteel twee manieren tooconnect toodatabases: ODBC (Open Database connectivity) en OLE DB (database-Object koppelen en insluiten). Microsoft heeft in de afgelopen jaren uitgelijnd met [ODBC voor toegang tot systeemeigen relationele gegevens](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC is relatief eenvoudig en ook veel sneller dan OLE DB. Hallo hier alleen voorbehoud is dat een oude C-stijl-API maakt gebruik van ODBC. 

## <a id="Create"></a>Stap 1: Uw Azure SQL-Database maken
Zie Hallo [pagina aan de slag](sql-database-get-started-portal.md) toolearn hoe toocreate een voorbeelddatabase.  U kunt ook kunt u dit [korte video van twee minuten](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate een Azure SQL database met hello Azure-portal.

## <a id="ConnectionString"></a>Stap 2: De verbindingsreeks ophalen
Nadat u uw Azure SQL database is ingericht, kunt u toocarry uit de volgende stappen toodetermine verbindingsgegevens Hallo moet en voeg uw client-IP voor toegang tot de firewall. 

In [Azure-portal](https://portal.azure.com/), ODBC-verbindingsreeks voor tooyour Azure SQL database gaat via Hallo **databaseverbindingsreeksen tonen** vermeld als een deel van de sectie voor het overzicht voor uw database Hallo: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Kopieer de inhoud Hallo Hallo **ODBC (omvat Node.js) [SQL-verificatie]** tekenreeks. We gebruiken deze tekenreeks hoger tooconnect van onze C++ ODBC-opdrachtregel-interpreter. Deze tekenreeks bevat informatie zoals Hallo stuurprogramma, server en andere databaseparameters. 

## <a id="Firewall"></a>Stap 3: De firewall van uw IP-toohello toevoegen
Ga toohello firewallsectie voor uw Database-server en voeg uw [client IP-toohello firewall met de volgende stappen](sql-database-configure-firewall-settings.md) toomake ervoor dat er een geslaagde verbinding kan worden gemaakt: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

Op dit moment uw Azure SQL-database hebt geconfigureerd en klaar tooconnect vanuit uw code C++ zijn. 

## <a id="Windows"></a>Stap 4: Verbinding maken vanuit een Windows-C/C++-toepassing
U kunt eenvoudig verbinding maken met tooyour [Azure SQL DB met ODBC op Windows met behulp van dit voorbeeld](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) die wordt gemaakt met Visual Studio. Hallo voorbeeld implementeert een ODBC-opdrachtregel-interpreter die gebruikt tooconnect tooour Azure SQL-database worden kan. Dit voorbeeld wordt een Database source name (DSN) bestand als een opdrachtregelargument ofwel Hallo uitgebreide verbindingsreeks die we eerder hebt gekopieerd uit hello Azure-portal. Online zetten van de eigenschappenpagina Hallo voor dit project en plak Hallo-verbindingsreeks als een argument van de opdracht als volgt te werk: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Zorg ervoor dat u de juiste verificatiegegevens Hallo voor uw database opgeven als een deel van deze database-verbindingsreeks. 

Hallo toepassing toobuild start het. U ziet Hallo na venster valideren van de verbinding is geslaagd. U kunt zelfs enkele eenvoudige SQL-opdrachten zoals uitvoeren **tabel maken** toovalidate uw verbinding met de database:

![SQL-opdrachten](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

U kunt ook een Hallo wizard die wordt gestart wanneer er zijn geen argumenten worden geleverd met DSN-bestand maken. Het is raadzaam dat u deze optie ook proberen. U kunt deze DSN-bestand gebruiken voor automatisering en beveiligen van uw verificatie-instellingen: 

![DSN-bestand maken](./media/sql-database-develop-cplusplus-simple/datasource.png)

Gefeliciteerd. U hebt nu tooAzure SQL verbonden met C++ en ODBC in Windows. U kunt blijven lezen toodo hello dezelfde voor Linux-platform. 

## <a id="Linux"></a>Stap 5: Verbinding maakt vanaf een Linux-C/C++-toepassing
Als u dit nog niet hebt gehoord Hallo nieuws nog Visual Studio u nu toodevelop ook C++ Linux-toepassing kunt. U kunt lezen over deze nieuwe scenario in Hallo [Visual C++ voor Linux-ontwikkeling](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog. toobuild voor Linux moet u een externe computer waarop uw distro Linux wordt uitgevoerd. Als u niet hebt kunt u beschikbaar zijn, stel een snel met behulp van [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Voor deze zelfstudie laat het ons wordt ervan uitgegaan dat u hebt een Ubuntu 16.04 Linux-distributie instellen. Hallo stappen hier moeten ook gelden tooUbuntu 15.10, Red Hat 6 en 7 van Red Hat. 

Hallo installeren volgt Hallo-bibliotheken die nodig zijn voor SQL en ODBC voor uw distro:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Visual Studio starten. Onder Tools -> Opties -> Cross-Platform -> Verbindingsbeheer, het toevoegen van een verbinding met het tooyour Linux: 

![Extra opties](./media/sql-database-develop-cplusplus-simple/tools.png)

Nadat de verbinding via SSH is gemaakt, maakt u een leeg projectsjabloon (Linux): 

![Nieuw project-sjabloon](./media/sql-database-develop-cplusplus-simple/template.png)

Vervolgens kunt u toevoegen een [nieuwe C bronbestand en vervang deze door deze inhoud](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Hallo ODBC-API's SQLAllocHandle, SQLSetConnectAttr en SQLDriverConnect gebruikt, moet u kunnen tooinitialize worden en een database van de tooyour verbinding tot stand brengen. Net als bij Hallo Windows ODBC-voorbeeld moet u tooreplace Hallo SQLDriverConnect aanroep met Hallo details van uw databaseparameters voor de verbindingsreeks van hello Azure-portal eerder hebt gekopieerd. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

laatste ding toodo Hallo voordat tooadd compileren is **odbc** als een afhankelijkheid van de bibliotheek: 

![ODBC toe te voegen als een invoer-bibliotheek](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch uw toepassing online zetten van Hallo Linux-Console van Hallo **Debug** menu: 

![Linux-Console](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Als de verbinding geslaagd is, ziet u nu Hallo huidige databasenaam afgedrukt in Hallo Linux-Console: 

![Linux-Console-venster uitvoer](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Gefeliciteerd. U Hallo-zelfstudie hebt voltooid en kan nu verbinding maken tooyour Azure SQL DB uit C++ op Windows- en Linux-platforms.

## <a id="GetSolution"></a>Hallo voltooid C/C++-zelfstudieoplossing ophalen
U vindt Hallo GetStarted-oplossing waarin alle Hallo voorbeelden in dit artikel op github:

* [Voorbeeld van de ODBC-C++ Windows](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Hallo Windows C++ ODBC-voorbeeld tooconnect tooAzure SQL downloaden
* [Voorbeeld van de ODBC-C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Hallo Linux C++ ODBC-voorbeeld tooconnect tooAzure SQL downloaden

## <a name="next-steps"></a>Volgende stappen
* Bekijk Hallo [overzicht voor ontwikkelaars van SQL-Database](sql-database-develop-overview.md)
* Meer informatie over het Hallo [ODBC-API-referentiemateriaal](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Aanvullende bronnen
* [Ontwerppatronen voor SaaS-toepassingen met meerdere tenants met behulp van Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Alle Hallo verkennen [mogelijkheden van SQL-Database](https://azure.microsoft.com/services/sql-database/)

