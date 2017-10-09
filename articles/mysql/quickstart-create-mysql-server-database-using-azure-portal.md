---
title: 'Quick Start: een Azure-database voor MySQL-server maken - Azure Portal | Microsoft-documenten'
description: Dit artikel stappen die u door het gebruik van Azure portal tooquickly Hallo maken een voorbeeld van een Azure-Database voor de MySQL-server in ongeveer 5 minuten.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Een Azure-database voor MySQL-server maken met behulp van Azure Portal
Azure MySQL-Database is een beheerde service waarmee u toorun, beheren en schalen van maximaal beschikbare MySQL-databases in de cloud Hallo. Deze snelstartgids ziet u hoe toocreate een Azure-Database voor de MySQL-server met behulp van hello Azure-portal in ongeveer vijf minuten. 

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure
Open uw webbrowser en navigeer toohello [Microsoft Azure-portal](https://portal.azure.com/). Voer uw referenties toosign in toohello-portal. Hallo standaardweergave is uw servicedashboard.

## <a name="create-azure-database-for-mysql-server"></a>Een Azure-database voor MySQL-server maken
Een Azure Database voor MySQL-server wordt gemaakt met een gedefinieerde set [reken- en opslagresources](./concepts-compute-unit-and-storage.md). Hallo-server is gemaakt binnen een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md).

Volg deze stappen toocreate een Azure-Database voor de MySQL-server:

1. Klik op Hallo **nieuw** knop (+) gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Databases** van Hallo **nieuw** pagina en selecteer **Azure Database voor MySQL** van Hallo **Databases** pagina. U kunt ook typen **MySQL** in Hallo nieuwe pagina vak toofind Hallo service voor zoeken.
![Azure Portal - nieuw - database - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Hallo nieuwe server detailformulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:

    **Instelling** | **Voorgestelde waarde** | **Beschrijving van veld** 
    ---|---|---
    Servernaam | myserver4demo | Kies een unieke naam ter identificatie van de Azure Database voor MySQL-server. Hallo-domeinnaam *mysql.database.azure.com* toegevoegde toohello servernaam u toepassingen tooconnect om te voorzien. Hallo-servernaam mag alleen kleine letters, cijfers en Hallo koppelteken (-) bevatten en moet tussen 3 en 63 tekens bevatten.
    Abonnement | Uw abonnement | Hello Azure-abonnement dat u wilt de toouse voor uw server. Als u meerdere abonnementen hebt, kiest u Hallo juiste abonnement waarin Hallo resource wordt gefactureerd voor.
    Resourcegroep | myResourceGroup | U kunt een nieuwe resourcegroepnaam maken of een bestaande naam uit uw abonnement gebruiken.
    Aanmeldgegevens van serverbeheerder | myadmin | Controleer uw eigen account aanmelding toouse wanneer toohello server verbinding kunnen maken. Hallo beheerder aanmeldingsnaam mag niet 'azure_superuser', 'admin', ' administrator', 'root', 'gast' of 'openbaar'.
    Wachtwoord | *Uw keuze* | Maak een nieuw wachtwoord voor Hallo server-beheerdersaccount. Moet uit 8 too128 tekens bevatten. Uw wachtwoord moet tekens bevatten uit drie van Hallo volgende categorieën: Nederlandse hoofdletters letters, Nederlandse kleine letters, cijfers (0-9) en niet-alfanumerieke tekens (!, $, #, %, etc.).
    Wachtwoord bevestigen | *Uw keuze*| Hallo beheerder accountwachtwoord bevestigen.
    Locatie | *Hallo regio dichtstbijzijnde tooyour gebruikers*| Kies Hallo locatie die het dichtst tooyour gebruikers of andere Azure-toepassingen.
    Versie | *Kies de meest recente versie Hallo*| Kies de meest recente versie Hallo tenzij er specifieke vereisten.
    Prijscategorie | **Basic**, **50 rekeneenheden**, **50 GB** | Klik op **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor de nieuwe database. Kies **basisstaffel** in Hallo boven op Hallo-tabblad. Klik op Hallo linkereinde Hallo **eenheden Compute** schuifregelaar tooadjust Hallo waarde toohello minste bedrag beschikbaar voor deze snelstartgids. Klik op **Ok** toosave Hallo laag selectie prijzen. Zie Hallo volgende schermopname.
    Pincode toodashboard | Selecteren | Controleer de Hallo **pincode toodashboard** optie tooallow eenvoudig bijhouden van uw server op Hallo front dashboardpagina van uw Azure-portal.

    > [!IMPORTANT]
    > aanmeldgegevens van serverbeheerder Hallo en het wachtwoord die u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in deze snelstartgids. Onthoud of noteer deze informatie voor later gebruik.
    > 

    ![Azure-portal - MySQL maken door op te geven invoer Hallo vereist](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Klik op **maken** tooprovision Hallo-server. Inrichting duurt een paar minuten, up too20 minuten maximum.
   
5.  Op de werkbalk Hallo **meldingen** (belpictogram) toomonitor Hallo-implementatieproces.

## <a name="configure-a-server-level-firewall-rule"></a>Een serverfirewallregel configureren

Hello Azure Database voor de MySQL-service maakt een firewall op serverniveau Hallo. Deze firewall voorkomt dat externe toepassingen en hulpprogramma's verbinden toohello server en alle databases op Hallo van server, tenzij een firewallregel tooopen Hallo firewall voor specifieke IP-adressen is gemaakt. 

1.  Ga naar de server nadat het Hallo-implementatie is voltooid. U kunt desgewenst naar de server zoeken. Bijvoorbeeld, klik op **alle Resources** van links menu Hallo en typt u de servernaam Hallo (zoals Hallo voorbeeld *myserver4demo*) toosearch voor de nieuwe virtuele server. Klik op de naam van uw server weergegeven in zoekresultaten Hallo. Hallo **overzicht** pagina voor de server wordt geopend en opties voor verdere configuratie biedt.

2. Selecteer in de pagina Hallo **verbindingsbeveiliging**.

3.  Onder Hallo **Firewall-regels** kop, klik in de lege tekstvak Hallo in Hallo **regelnaam** kolom toobegin Hallo firewallregel maken. 

    Voor deze snelstartgids we toestaan alle IP-adressen in Hallo-server door in te vullen in het tekstvak in elke kolom Hallo Hello volgende waarden:

    Regelnaam | Start-IP | Eind-IP 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Op de bovenste werkbalk Hallo Hallo **verbindingsbeveiliging** pagina, klikt u op **opslaan**. Wacht enkele ogenblikken en bericht Hallo melding weergegeven dat het bijwerken van de beveiliging van de verbinding is voltooid, voordat u doorgaat.

    > [!NOTE]
    > Verbindingen tooAzure Database voor MySQL communiceren via poort 3306. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 3306 niet worden toegestaan door de firewall van uw netwerk. Zo ja, zich u niet kunnen tooconnect tooyour server tenzij uw IT-afdeling poort 3306 wordt geopend.
    > 

## <a name="get-hello-connection-information"></a>Hallo-verbindingsgegevens ophalen
tooconnect tooyour database-server, moet u tooremember Hallo volledige server name en beheer aanmeldingsreferenties. Hebt u mogelijk deze waarden eerder in Hallo Quick Start artikel hebt genoteerd. Als u niet hebt gedaan, kunt u gemakkelijk vinden Hallo server servernaam en informatie van Hallo server **overzicht** pagina of Hallo **eigenschappen** pagina in hello Azure-portal.

1. Open de pagina **Overzicht** van de server. Maak een notitie van Hallo **servernaam** en **aanmeldingsnaam van Server-beheerder**. 
    Beweeg de muisaanwijzer de cursor over elk veld en pictogram voor Hallo kopiëren toohello rechts van de tekst hello wordt weergegeven. Klik op pictogram van Hallo kopiëren als benodigde toocopy Hallo waarden.

    In dit voorbeeld Hallo-servernaam is *myserver4demo.mysql.database.azure.com*, en aanmeldgegevens van serverbeheerder Hallo  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Verbinding maken met het opdrachtregelprogramma mysql tooMySQL
Er zijn een aantal van toepassingen voor kunt u tooconnect tooyour Azure Database MySQL-server. Laten we eerst gebruiken Hallo [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) opdrachtregelprogramma tooillustrate hoe hulpprogramma tooconnect toohello server.  U kunt een webbrowser en hello Azure Cloud Shell zoals hier wordt beschreven zonder Hallo moet tooinstall geen extra software. Als u Hallo mysql hulpprogramma lokaal is geïnstalleerd op uw computer hebt, kunt u daar ook.

1. Hello Azure Cloud Shell via Hallo terminal pictogram starten (> _) op Hallo top rechts van hello Azure portal webpagina.

2. Hello Azure Cloud Shell wordt geopend in uw browser, zodat u tootype bash-shell-opdrachten.

    ![Opdrachtprompt - voorbeeld van opdrachtregel mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. Verbinding maken tooyour Azure Database voor de MySQL-server door Hallo mysql-opdrachtregel bij Hallo groen prompt te typen bij Hallo Cloud Shell-prompt.

    Hallo na indeling is gebruikte tooconnect tooan Azure Database voor MySQL-server met Hallo mysql hulpprogramma:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Bijvoorbeeld: tooour voorbeeld server verbindt met in Hallo volgende opdracht:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    mysql-parameter |Voorgestelde waarde|Beschrijving
    ---|---|---
    --host | *servernaam* | Hallo-server de naam van waarde dat werd gebruikt toen u eerder hebt gemaakt hello Azure Database voor MySQL opgeven. De server in ons voorbeeld is myserver4demo.mysql.database.azure.com. Gebruik Hallo volledig gekwalificeerde domeinnaam (\*. mysql.database.azure.com) zoals weergegeven in Hallo-voorbeeld. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer de servernaam van uw weet. 
    --user | *aanmeldnaam van serverbeheerder* |Typ Hallo server admin aanmelding gebruikersnaam opgegeven toen u eerder hebt gemaakt hello Azure Database voor MySQL. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer Hallo gebruikersnaam weet.  Hallo-indeling is  *username@servername* .
    --password | *wacht totdat u hierom wordt gevraagd* | U wordt gevraagd te 'Wachtwoord opgeven' na het Hallo-opdracht invoeren. Wanneer u wordt gevraagd, typt u in Hallo hetzelfde wachtwoord dat u hebt opgegeven toen u Hallo server gemaakt.  Opmerking Hallo getypt wachtwoord tekens niet op Hallo bash vragen weergegeven worden wanneer u ze zelf typen. Druk op enter nadat u alle Hallo tekens tooauthenticate hebt getypt en verbinding maakt.

   Eenmaal zijn verbonden, Hallo mysql hulpprogramma geeft een `mysql>` vragen om u tootype opdrachten. 

    Voorbeeld van mysql-uitvoer:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Als het Hallo-firewall is niet geconfigureerd tooallow Hallo IP-adres van hello Azure Cloud-Shell, hello volgende fout is opgetreden:
    >
    > Fout 2003 (28000): De Client met IP-adres 123.456.789.0 is niet toegestaan voor tooaccess Hallo-server.
    >
    > Fout in tooresolve hello, zorg ervoor dat Hallo server configuratie komt overeen met Hallo stappen voor het Hallo *een firewallregel op serverniveau configureren* sectie Hallo artikel.

4. Weergave status tooensure Hallo serververbinding is functioneel. Type `status` op Hallo mysql > vragen wanneer deze is verbonden.
    ```sql
    status
    ```

   > [!TIP]
   > Zie [hoofdstuk 4.5.1 in de Engelstalige naslaghandleiding van MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) voor aanvullende opdrachten.

5.  Een lege database maken op Hallo mysql > vragen door Hallo volgende opdracht te typen:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    Hallo opdracht duurt enkele ogenblikken toocomplete. 

    Op een Azure Database voor MySQL-server kunt u een of meerdere databases maken. U kunt kiezen toocreate een individuele database per server tooutilize alle Hallo resources of meerdere databases tooshare Hallo resources maken. Er geldt geen limiet toohello aantal databases dat kan worden gemaakt, maar meerdere databases Hallo delen dezelfde serverbronnen. 

6. Hallo-databases op Hallo mysql lijst > vragen door Hallo volgende opdracht te typen:

    ```sql
    SHOW DATABASES;
    ```

7.  Type `\q` en druk vervolgens op ENTER tooquit Hallo mysql hulpprogramma. Nadat u klaar bent, kunt u hello Azure Cloud Shell sluiten.

U hebt nu verbinding toohello Azure Database MySQL en heeft een lege database gemaakt. Doorgaan toohello volgende sectie toorepeat een vergelijkbare oefening tooconnect toohello dezelfde server met een andere algemene hulpprogramma, MySQL-Workbench.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Verbinding maken met toohello-server met Hallo MySQL Workbench GUI-hulpprogramma
tooAzure tooconnect MySQL-server met Hallo GUI-hulpprogramma MySQL Workbench:

1.  Start Hallo MySQL Workbench van toepassing op de clientcomputer. U kunt MySQL Workbench [hier](https://dev.mysql.com/downloads/workbench/) downloaden en installeren.

2.  In **Setup nieuwe verbinding** dialoogvenster en voer de volgende informatie op Hallo **Parameters** tabblad:

    ![nieuwe verbinding instellen](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Instelling** | **Voorgestelde waarde** | **Beschrijving van veld** |
    |---|---|---|
    |   Verbindingsnaam | Demo-verbinding | Geef een label op voor deze verbinding. |
    | Verbindingsmethode | Standard (TCP/IP) | Standard (TCP/IP) is voldoende. |
    | Hostnaam | *servernaam* | Hallo-server de naam van waarde dat werd gebruikt toen u eerder hebt gemaakt hello Azure Database voor MySQL opgeven. De server in ons voorbeeld is myserver4demo.mysql.database.azure.com. Gebruik Hallo volledig gekwalificeerde domeinnaam (\*. mysql.database.azure.com) zoals weergegeven in Hallo-voorbeeld. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer de servernaam van uw weet.  |
    | Poort | 3306 | Gebruik altijd poort 3306 bij het verbinden van tooAzure Database voor MySQL. |
    | Gebruikersnaam |  *aanmeldnaam van serverbeheerder* | Typ Hallo server admin aanmelding gebruikersnaam opgegeven toen u eerder hebt gemaakt hello Azure Database voor MySQL. De gebruikersnaam in ons voorbeeld is myadmin@myserver4demo. Stappen Hallo in Hallo vorige sectie tooget Hallo verbindingsgegevens als u niet meer Hallo gebruikersnaam weet. Hallo-indeling is  *username@servername* .
    | Wachtwoord | Uw wachtwoord | Klik in de kluis... knop toosave Hallo wachtwoord opslaan. |

    Klik op **testverbinding** tootest als alle parameters juist zijn geconfigureerd. Klik op OK toosave Hallo verbinding. 

    > [!NOTE]
    > SSL wordt standaard op uw server afgedwongen en extra configuratie in volgorde tooconnect is vereist. Zie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md).  Desgewenst kunt u toodisable SSL voor deze snelstartgids hello Azure-portal te bezoeken en klik Hallo verbinding beveiliging pagina toodisable Hallo SSL afdwingen verbinding in-of uitschakelen.

## <a name="clean-up-resources"></a>Resources opschonen
Hallo-resources die u hebt gemaakt in Hallo Quick Start opruimen door het verwijderen van Hallo [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md), waaronder alle Hallo resources in de resourcegroep Hallo of bron Hallo één server als u wilt dat tookeep Hallo andere bronnen intact.

> [!TIP]
> Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd. Als u van plan toocontinue toowork met latere bent Hallo snelstartgidsen, komen niet opschoning van resources in deze snelstartgids hebt gemaakt. Als u niet van plan toocontinue bent, gebruikt u Hallo na stappen toodelete alle resources gemaakt door deze snelstartgids in hello Azure-portal.
>

toodelete hello hele resourcegroep waaronder Hallo nieuwe server:
1.  De resourcegroep niet vinden in hello Azure-portal. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van de resourcegroep, zoals ons voorbeeld **myresourcegroup**.
2.  Klik op de pagina van de resourcegroep op **Verwijderen**. Vervolgens Hallo typenaam van de resourcegroep, zoals ons voorbeeld **myresourcegroup**in Hallo tekst vak tooconfirm verwijderen en klik vervolgens op **verwijderen**.

Of in plaats daarvan toodelete Hallo nieuw server gemaakt:
1.  De server niet vinden in hello Azure-portal, als u niet hebt geopend. Hallo links menu in Azure-portal en klik op **alle resources**, en zoek vervolgens naar het Hallo-server die u hebt gemaakt.
2.  Op Hallo **overzicht** pagina, klikt u op Hallo **verwijderen** knop op het bovenste deelvenster Hallo.
![Azure Database voor MySQL - server verwijderen](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Bevestig Hallo servernaam u toodelete wilt gebruiken en weergeven van Hallo databases in deze die worden beïnvloed. Typ de naam van uw server in het tekstvak hello, zoals ons voorbeeld **myserver4demo**, en klik vervolgens op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Uw eerste Azure-database voor MySQL-database ontwerpen](./tutorial-design-database-using-portal.md)

