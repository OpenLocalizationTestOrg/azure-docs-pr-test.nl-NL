---
title: aaaAdd hello DB2-connector in uw logische Apps | Microsoft Docs
description: Overzicht van DB2-connector met de parameters van de REST-API
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Aan de slag met Hallo DB2-connector
Microsoft-connector voor DB2 verbindt Logic Apps tooresources opgeslagen in een IBM DB2-database. Deze connector omvat een toocommunicate Microsoft client met externe computers voor DB2-server via een TCP/IP-netwerk. Dit omvat cloud databases, zoals IBM Bluemix dashDB of IBM DB2 voor Windows wordt uitgevoerd in Azure virtualisatie en het on-premises databases die gebruikmaken van Hallo lokale gegevensgateway. Zie Hallo [ondersteund lijst](connectors-create-api-db2.md#supported-db2-platforms-and-versions) IBM DB2-platformen en-versies (in dit onderwerp).

Hallo DB2-connector ondersteunt Hallo databasebewerkingen te volgen:

* Lijst databasetabellen
* Lezen van één rij met selecteren
* Lezen van alle rijen met selecteren
* Een rij invoegen met toevoegen
* Wijzigen van één rij met UPDATE
* Verwijderen van één rij met DELETE

Dit onderwerp leest u hoe toouse Hallo-connector in een logische app tooprocess operations-database.

toolearn meer informatie over Logic Apps, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Beschikbare acties
Hallo DB2-connector ondersteunt Hallo logic app acties te volgen:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Lijst met tabellen
Maken van een logische app voor een bewerking bestaat uit veel stappen die worden uitgevoerd via Hallo Microsoft Azure-portal.

In Hallo logische app, kunt u een actie toolist tabellen toevoegen in een DB2-database. Hallo actie geeft opdracht Hallo connector tooprocess een DB2-schema-en verliesrekening, zoals `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `Db2getTables`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en stel vervolgens Hallo **Interval** tootype **7**.  
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt `db2` in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - Get-tabellen (Preview)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. In Hallo **DB2 - Get-tabellen** deelvenster configuratie, selecteer **selectievakje** tooenable **verbinden via lokale gegevensgateway**. U ziet dat het Hallo-instellingen worden gewijzigd van cloud tooon-premises.
   
   * Typ de waarde voor **Server**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `ibmserver01:50000`.
   * Typ de waarde voor **Database**. Typ bijvoorbeeld `nwind`.
   * Selecteer de waarde voor **verificatie**. Selecteer bijvoorbeeld **Basic**.
   * Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `db2admin`.
   * Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
   * Selecteer de waarde voor **Gateway**. Selecteer bijvoorbeeld **datagateway01**.
7. Selecteer **maken**, en selecteer vervolgens **opslaan**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. In Hallo **Db2getTables** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
9. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_tables**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die een lijst met tabellen bevatten.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Hallo-verbindingen maken
Deze connector ondersteunt verbindingen toodatabases gehost op de lokale en in de cloud Hallo met behulp van Hallo verbindingseigenschappen te volgen. 

| Eigenschap | Beschrijving |
| --- | --- |
| server |Vereist. Een tekenreekswaarde die staat voor een TCP/IP-adres of de alias in IPv4 of IPv6-indeling, gevolgd (gescheiden door puntkomma) door een TCP/IP-poortnummer accepteert. |
| database |Vereist. Accepteert een string-waarde die een DRDA relationele Database naam (RDBNAM aangeeft). DB2 voor z/OS accepteert een 16-byte-tekenreeks (de database staat bekend als een IBM DB2 voor de locatie van de z-/ OS). DB2 voor i5/OS accepteert geen 18-byte-tekenreeks (database staat bekend als een IBM DB2 voor i relationele database). DB2 voor LUW accepteert een 8-byte-tekenreeks. |
| Verificatie |Optioneel. Een item lijstwaarde, Basic of Windows (kerberos) accepteert. |
| gebruikersnaam |Vereist. Een string-waarde accepteert. DB2 voor z/OS accepteert een 8-byte-tekenreeks. DB2 voor i een 10-byte-tekenreeks accepteert. DB2 voor Linux of UNIX accepteert een 8-byte-tekenreeks. DB2 voor Windows accepteert een 30-byte-tekenreeks. |
| wachtwoord |Vereist. Een string-waarde accepteert. |
| Gateway |Vereist. Een lijst item integer, Hallo lokale gegevens gateway gedefinieerd tooLogic Apps in de opslaggroep Hallo accepteert. |

## <a name="create-hello-on-premises-gateway-connection"></a>Hallo lokale gatewayverbinding maken
Deze connector hebben toegang tot een lokale DB2-database met Hallo lokale gateway. Zie gateway-onderwerpen voor meer informatie. 

1. In Hallo **Gateways** deelvenster configuratie, selecteer **selectievakje** tooenable **verbinden via de gateway**. U ziet dat het Hallo-instellingen worden gewijzigd van cloud tooon-premises.
2. Typ de waarde voor **Server**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `ibmserver01:50000`.
3. Typ de waarde voor **Database**. Typ bijvoorbeeld `nwind`.
4. Selecteer de waarde voor **verificatie**. Selecteer bijvoorbeeld **Basic**.
5. Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `db2admin`.
6. Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
7. Selecteer de waarde voor **Gateway**. Selecteer bijvoorbeeld **datagateway01**.
8. Selecteer **maken** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Hallo cloud verbinding maken
Deze connector hebben toegang tot een cloud DB2-database. 

1. In Hallo **Gateways** deelvenster configuratie, laat de eigenschap Hallo **selectievakje** uitgeschakeld (waar) **verbinden via de gateway**. 
2. Typ de waarde voor **verbindingsnaam**. Typ bijvoorbeeld `hisdemo2`.
3. Typ de waarde voor **DB2-servernaam**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `hisdemo2.cloudapp.net:50000`.
4. Typ de waarde voor **DB2 databasenaam**. Typ bijvoorbeeld `nwind`.
5. Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `db2admin`.
6. Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
7. Selecteer **maken** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Ophalen van alle rijen met selecteren
U kunt een logische app actie toofetch definiëren alle rijen in een DB2-tabel. Dit geeft de instructie Hallo connector tooprocess een DB2 SELECT-instructie, zoals `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `Db2getRows`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt `db2` in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - Get-rijen (Preview)**.
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**.
7. In Hallo **verbindingen** deelvenster configuratie, selecteer **nieuw**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. In Hallo **Gateways** deelvenster configuratie, laat de eigenschap Hallo **selectievakje** uitgeschakeld (waar) **verbinden via de gateway**.
   
   * Typ de waarde voor **verbindingsnaam**. Typ bijvoorbeeld `HISDEMO2`.
   * Typ de waarde voor **DB2-servernaam**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `HISDEMO2.cloudapp.net:50000`.
   * Typ de waarde voor **DB2 databasenaam**. Typ bijvoorbeeld `NWIND`.
   * Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `db2admin`.
   * Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
9. Selecteer **maken** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
11. Selecteer desgewenst **geavanceerde opties weergeven** toospecify query-opties.
12. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. In Hallo **Db2getRows** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
14. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die een lijst met rijen bevatten.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Een rij invoegen met toevoegen
U kunt een logische app actie tooadd één rij definiëren in een DB2-tabel. Deze actie geeft opdracht Hallo connector tooprocess een DB2 INSERT-instructie zoals `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `Db2insertRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **db2** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - rij invoegen (Preview)**.
6. In Hallo **DB2 - rij invoegen (Preview)** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** deelvenster configuratie, selecteert u een verbinding. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**, type `Area 99999`, en het type `102` voor **REGIONID**. 
10. Selecteer **Opslaan**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. In Hallo **Db2insertRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die de nieuwe rij Hallo bevatten.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Ophalen van één rij met selecteren
U kunt een logische app actie toofetch één rij definiëren in een DB2-tabel. Deze actie geeft opdracht Hallo connector tooprocess een instructie DB2 selecteren waar zoals `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam** (bijvoorbeeld) "**Db2getRow**'), **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst. 
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **db2** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - Get-rijen (Preview)**.
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster een bestaande verbinding selecteren. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**. 
10. Selecteer desgewenst **geavanceerde opties weergeven** toospecify query-opties.
11. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. In Hallo **Db2getRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
13. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die rij bevatten.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Wijzigen van één rij met UPDATE
U kunt een logische app actie toochange één rij definiëren in een DB2-tabel. Deze actie geeft opdracht Hallo connector tooprocess een DB2-UPDATE-instructie, zoals `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `Db2updateRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **db2** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - Update-rij (Preview)**.
6. In Hallo **DB2 - Update-rij (Preview)** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster Selecteer tooselect een bestaande verbinding. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**, type `Updated 99999`, en het type `102` voor **REGIONID**. 
10. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. In Hallo **Db2updateRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die de nieuwe rij Hallo bevatten.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Verwijderen van één rij met DELETE
U kunt een logische app actie tooremove één rij definiëren in een DB2-tabel. Deze actie geeft opdracht Hallo connector tooprocess een DB2-instructie DELETE, zoals `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `Db2deleteRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst. 
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** selecteert **db2** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **DB2 - rij verwijderen (Preview)**.
6. In Hallo **DB2 - rij verwijderen (Preview)** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster een bestaande verbinding selecteren. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**. 
10. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. In Hallo **Db2deleteRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die Hallo verwijderde rij bevatten.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Ondersteunde platforms DB2 en versies
Deze connector ondersteunt Hallo IBM DB2 platforms en versies, evenals IBM DB2 compatibele producten (bijvoorbeeld IBM Bluemix dashDB) die ondersteuning bieden voor Distributed relationele Database architectuur (DRDA) SQL toegang Manager (SQLAM) versie 10 en 11 te volgen:

* IBM DB2 voor z/OS 11.1
* IBM DB2 voor z/OS 10.1
* IBM DB2 voor i 7.3
* IBM DB2 voor i 7.2
* IBM DB2 voor i 7.1
* IBM DB2 voor LUW 11
* IBM DB2 voor LUW 10.5

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/db2/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).

