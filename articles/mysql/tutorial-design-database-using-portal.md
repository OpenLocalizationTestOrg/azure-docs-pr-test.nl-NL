---
title: uw eerste Azure-Database voor de MySQL-database. Azure-Portal aaaDesign | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe toocreate en beheren van Azure-Database voor de MySQL-server en database gebruiken met Azure Portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Ontwerp van uw eerste Azure-Database voor de MySQL-database
Azure MySQL-Database is een beheerde service waarmee u toorun, beheren en schalen van maximaal beschikbare MySQL-databases in de cloud Hallo. Hello Azure-portal gebruikt, kunt u eenvoudig beheren van uw server en ontwerpen van een database.

In deze zelfstudie gebruikt u Azure portal toolearn Hallo hoe naar:

> [!div class="checklist"]
> * Een Azure-Database maken voor MySQL
> * Hallo serverfirewall configureren
> * Gebruik van mysql opdrachtregelprogramma toocreate een database
> * Voorbeeldgegevens laden
> * Querygegevens
> * Gegevens bijwerken
> * Gegevens terugzetten

## <a name="sign-in-toohello-azure-portal"></a>Meld u aan toohello Azure-portal
Open uw favoriete webbrowser en Ga naar Hallo [Microsoft Azure-portal](https://portal.azure.com/). Voer uw referenties toosign in toohello-portal. Hallo standaardweergave is uw servicedashboard.

## <a name="create-an-azure-database-for-mysql-server"></a>Een Azure-database voor MySQL-server maken
Een Azure Database voor MySQL-server wordt gemaakt met een gedefinieerde set [reken- en opslagresources](./concepts-compute-unit-and-storage.md). Hallo-server is gemaakt binnen een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Navigeer te**Databases** > **Azure Database voor MySQL**. Als u niet kunt vinden MySQL-Server onder **Databases** categorie, klikt u op **alle** tooshow alle beschikbare services-database. U kunt ook typen **Azure Database voor MySQL** in Hallo zoeken vak tooquickly Hallo service vinden.
![2-1 navigeren tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Klik op **Azure Database voor MySQL** tegel en klik vervolgens op **maken**.

Vul in ons voorbeeld hello Azure Database voor MySQL formulier Hello volgende informatie:

| **Instelling** | **Voorgestelde waarde** | **Beschrijving van veld** |
|---|---|---|
| *Servernaam* | myserver4demo  | De servernaam van de heeft toobe globaal uniek zijn. |
| *Abonnement* | mysubscription | Uw abonnement te selecteren in de vervolgkeuzelijst Hallo. |
| *Resourcegroep* | myResourceGroup | Maak een nieuwe resourcegroep of selecteer een bestaande. |
| *Aanmeldgegevens van serverbeheerder* | myadmin | Accountnaam van de Setup-beheerder. |
| *Wachtwoord* |  | Stel een wachtwoord voor het beheerdersaccount in. |
| *Wachtwoord bevestigen* |  | Hallo beheerder accountwachtwoord bevestigen. |
| *Locatie* |  | Selecteer een beschikbare regio. |
| *Versie* | 5.7 | Kies de meest recente versie Hallo. |
| *Prestaties configureren* | Basis, 50 compute-eenheden, 50 GB  | Kies **Prijscategorie**, **Rekeneenheden**, **Opslag (GB)** en klik vervolgens op **OK**. |
| *Pincode tooDashboard* | Selecteren | Toocheck aanbevolen dit selectievakje in zodat u mogelijk eenvoudig later op Hallo server zoeken |
Klik vervolgens op **Maken**. In een minuut of twee, wordt een nieuwe Azure-Database voor de MySQL-server in de cloud Hallo uitgevoerd. U kunt klikken op **meldingen** knop op Hallo werkbalk toomonitor Hallo-implementatieproces.

## <a name="configure-firewall"></a>Firewall configureren
Azure voor MySQL-Databases worden beveiligd door een firewall. Standaard worden alle verbindingen toohello server- en Hallo databases binnen Hallo server geweigerd. Voordat u verbinding maakt tooAzure Database voor MySQL voor Hallo eerst, Hallo firewall tooadd Hallo clientmachine van openbare IP-adres (of IP-adresbereik) te configureren.

1. Klik op de nieuwe virtuele server en klik vervolgens op **verbindingsbeveiliging**.
   ![Beveiliging 3-1-verbindingen](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. U kunt **Mijn IP toevoegen**, of hier firewallregels configureren. Houd er rekening mee tooclick **opslaan** nadat u Hallo regels hebt gemaakt.
U kunt nu verbinding toohello-server met het opdrachtregelprogramma mysql of MySQL Workbench GUI-hulpprogramma.

> [!TIP]
> Azure-Database voor de MySQL-server communiceert via poort 3306. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 3306 niet worden toegestaan door de firewall van uw netwerk. Als dit het geval is, kunt u tooAzure MySQL-server kan geen verbinding tenzij uw IT-afdeling poort 3306 wordt geopend.

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen
Get-Hallo volledig gekwalificeerd **servernaam** en **aanmeldingsnaam van Server-beheerder** voor uw Azure-Database voor de server MySQL van hello Azure-portal. U gebruikt Hallo server volledig gekwalificeerde naam tooconnect tooyour server met het opdrachtregelprogramma mysql. 

1. In [Azure-portal](https://portal.azure.com/), klikt u op **alle resources** van menu links van hello, Hallo typenaam en zoeken naar uw Azure-Database voor de MySQL-server. Selecteer Hallo naam tooview Hallo-servergegevens.

2. Onder Hallo instellingen kop, klikt u op **eigenschappen**. Noteer **servernaam** en **AANMELDINGSNAAM van SERVER-beheerder**. Klikt u op Hallo knop volgende tooeach veld toocopy toohello Klembord kopiëren.
   ![Eigenschappen van de server 4-2](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

In dit voorbeeld Hallo-servernaam is *myserver4demo.mysql.database.azure.com*, en aanmeldgegevens van serverbeheerder Hallo  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Verbinding maken met behulp van mysql toohello-server
Gebruik [mysql opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish een verbinding tooyour Azure Database voor de MySQL-server. U kunt Hallo mysql opdrachtregelprogramma uitvoeren vanuit hello Azure Cloud Shell in Hallo browser of vanuit uw eigen computer lokaal met behulp van mysql-hulpprogramma's geïnstalleerd. toolaunch hello Azure Cloud-Shell, klikt u op Hallo `Try It` knop op een codeblok in dit artikel of gaat u naar hello Azure-portal en klikt u op Hallo `>_` pictogram in het bovenste rechts werkbalk Hallo. 

Hallo opdracht tooconnect typt u:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Een lege database maken
Als u verbonden toohello server bent, maakt u een lege database toowork met.
```sql
CREATE DATABASE mysampledb;
```

Voer bij Hallo-prompt Hallo opdracht tooswitch verbinding toothis nieuw gemaakte database te volgen:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Tabellen maken in Hallo-database
Als u weet hoe tooconnect toohello Azure Database voor de MySQL-database, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.

We kunnen eerst een tabel maken en deze met enkele gegevens te laden. We maken een tabel met inventarisatie-informatie.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Gegevens laden in Hallo tabellen
Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het. Op Hallo open opdrachtpromptvenster, typt u Hallo query tooinsert volgen een aantal rijen van gegevens.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

U hebt nu twee rijen van de voorbeeldgegevens in Hallo tabel die u eerder hebt gemaakt.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Vragen en het Hallo-gegevens in het Hallo-tabellen bijwerken
Hallo volgende tooretrieve querygegevens uit Hallo-databasetabel worden uitgevoerd.
```sql
SELECT * FROM inventory;
```

U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Een database tooa eerder punt herstellen in-time
Stel dat u een belangrijke databasetabel per ongeluk hebt verwijderd en Hallo gegevens gemakkelijk niet herstellen. Azure MySQL-Database kunt u toorestore Hallo server tooa punt in tijd, het maken van een kopie van Hallo databases in de nieuwe server. U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken. Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.

1. Zoek uw Azure-Database voor MySQL in Azure-portal hello. Op Hallo **overzicht** pagina, klikt u op **herstellen** op Hallo-werkbalk. Hallo terugzetten pagina wordt geopend.

   ![10-1 herstel van een database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Hallo invullen **herstellen** formulier met Hallo vereiste informatie.
   
   ![10-2-formulier voor herstel](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Herstelpunt**: Selecteer een point-in-time-dat u wilt dat toorestore, binnen Hallo tijdsbestek vermeld. Zorg ervoor dat tooconvert de tooUTC van uw lokale tijdzone.
   - **Herstellen van de server toonew**: Geef een nieuwe naam van een server gewenste toorestore aan.
   - **Locatie**: Hallo regio is hetzelfde als de bronserver Hallo en kan niet worden gewijzigd.
   - **Prijscategorie**: Hallo prijscategorie is Hallo dezelfde zijn als Hallo bron van de server en kan niet worden gewijzigd.
   
3. Klik op **OK** toorestore Hallo server te[tooa herstelpunt in de tijd](./howto-restore-server-portal.md) voordat het Hallo-tabel is verwijderd. Herstellen van een server, maakt een nieuwe kopie van de server hello, vanaf Hallo punt in tijd die u opgeeft. 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie gebruikt u Azure portal toolearned Hallo hoe naar:

> [!div class="checklist"]
> * Een Azure-Database maken voor MySQL
> * Hallo serverfirewall configureren
> * Gebruik van mysql opdrachtregelprogramma toocreate een database
> * Voorbeeldgegevens laden
> * Querygegevens
> * Gegevens bijwerken
> * Gegevens terugzetten

> [!div class="nextstepaction"]
> [Hoe tooconnect toepassingen tooAzure voor MySQL-Database](./howto-connection-string.md)
