---
title: aaaAdd hello Informix-connector in uw logische Apps | Microsoft Docs
description: Overzicht van de connector Informix met parameters van de REST-API
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Aan de slag met Hallo Informix-connector
Microsoft-connector voor Informix verbindt Logic Apps tooresources opgeslagen in een IBM Informix-database. Hallo Informix connector omvat een Microsoft toocommunicate tooremote Informix-server clientcomputers via een TCP/IP-netwerk. Dit omvat cloud databases, zoals IBM Informix voor Windows wordt uitgevoerd in Azure virtualisatie en het on-premises databases die gebruikmaken van Hallo lokale gegevensgateway. Zie Hallo [ondersteund lijst](connectors-create-api-informix.md#supported-informix-platforms-and-versions) IBM Informix-platformen en-versies (in dit onderwerp).

Hallo-connector ondersteunt Hallo databasebewerkingen te volgen:

* Lijst databasetabellen
* Lezen van één rij met selecteren
* Lezen van alle rijen met selecteren
* Een rij invoegen met toevoegen
* Wijzigen van één rij met UPDATE
* Verwijderen van één rij met DELETE

Dit onderwerp leest u hoe toouse Hallo-connector in een logische app tooprocess operations-database.

toolearn meer informatie over Logic Apps, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Beschikbare acties
Deze connector ondersteunt Hallo logic app acties te volgen:

* Getables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Lijst met tabellen
Maken van een logische app voor een bewerking bestaat uit veel stappen die worden uitgevoerd via Hallo Microsoft Azure-portal.

In Hallo logische app, kunt u een actie toolist tabellen toevoegen in een Informix-database. Deze actie geeft opdracht Hallo connector tooprocess een instructie Informix schema zoals `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `InformixgetTables`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**.  
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - Get-tabellen (Preview)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. In Hallo **Informix - Get-tabellen** deelvenster configuratie, selecteer **selectievakje** tooenable **verbinden via lokale gegevensgateway**. U ziet dat het Hallo-instellingen worden gewijzigd van cloud tooon-premises.
   
   * Typ de waarde voor **Server**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `ibmserver01:9089`.
   * Typ de waarde voor **Database**. Typ bijvoorbeeld `nwind`.
   * Selecteer de waarde voor **verificatie**. Selecteer bijvoorbeeld **Basic**.
   * Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `informix`.
   * Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
   * Selecteer de waarde voor **Gateway**. Selecteer bijvoorbeeld **datagateway01**.
7. Selecteer **maken**, en selecteer vervolgens **opslaan**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. In Hallo **InformixgetTables** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
9. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_tables**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die een lijst met tabellen bevatten.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Hallo-verbindingen maken
Deze connector ondersteunt verbindingen toodatabase lokaal en in Hallo cloud met behulp van Hallo verbindingseigenschappen te volgen. 

| Eigenschap | Beschrijving |
| --- | --- |
| server |Vereist. Accepteert een string-waarde die aangeeft een TCP/IP-adres of de alias in IPv4 of IPv6-indeling, gevolgd (puntkomma's gescheiden) door een TCP/IP-poortnummer. |
| database |Vereist. Accepteert een string-waarde die aangeeft een DRDA relationele Database naam (RDBNAM). Informix accepteert een 128-byte-tekenreeks (de database staat bekend als de naam van een IBM Informix-database (dbname)). |
| Verificatie |Optioneel. Een item lijstwaarde, Basic of Windows (kerberos) accepteert. |
| gebruikersnaam |Vereist. Een string-waarde accepteert. |
| wachtwoord |Vereist. Een string-waarde accepteert. |
| Gateway |Vereist. Een lijst item integer, Hallo lokale gegevens gateway gedefinieerd tooLogic Apps in de opslaggroep Hallo accepteert. |

## <a name="create-hello-on-premises-gateway-connection"></a>Hallo lokale gatewayverbinding maken
Deze connector hebben toegang tot een lokale Informix-database met behulp van Hallo lokale gegevensgateway. Zie gateway-onderwerpen voor meer informatie. 

1. In Hallo **Gateways** deelvenster configuratie, selecteer **selectievakje** tooenable **verbinden via de gateway**. Zie Hallo cloud tooon-premises instellingen worden gewijzigd.
2. Typ de waarde voor **Server**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `ibmserver01:9089`.
3. Typ de waarde voor **Database**. Typ bijvoorbeeld `nwind`.
4. Selecteer de waarde voor **verificatie**. Selecteer bijvoorbeeld **Basic**.
5. Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `informix`.
6. Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
7. Selecteer de waarde voor **Gateway**. Selecteer bijvoorbeeld **datagateway01**.
8. Selecteer **maken** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Hallo cloud verbinding maken
Deze connector hebben toegang tot een cloud Informix-database. 

1. In Hallo **Gateways** deelvenster configuratie, laat de eigenschap Hallo **selectievakje** uitgeschakeld (waar) **verbinden via de gateway**. 
2. Typ de waarde voor **verbindingsnaam**. Typ bijvoorbeeld `hisdemo2`.
3. Typ de waarde voor **Informix-servernaam**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `hisdemo2.cloudapp.net:9089`.
4. Typ de waarde voor **Informix databasenaam**. Typ bijvoorbeeld `nwind`.
5. Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `informix`.
6. Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
7. Selecteer **maken** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Ophalen van alle rijen met selecteren
U kunt een logische app actie toofetch maken alle rijen in Hallo Informix tabel. Deze actie geeft opdracht Hallo connector tooprocess een Informix SELECT-instructie, zoals `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam** (bijvoorbeeld) "**InformixgetRows**'), **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - Get-rijen (Preview)** .
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**.
7. In Hallo **verbindingen** deelvenster configuratie, selecteer **nieuw**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. In Hallo **Gateways** deelvenster configuratie, laat de eigenschap Hallo **selectievakje** uitgeschakeld (waar) **verbinden via de gateway**.
   
   * Typ de waarde voor **verbindingsnaam**. Typ bijvoorbeeld `HISDEMO2`.
   * Typ de waarde voor **Informix-servernaam**, in de vorm Hallo van-adres of alias dubbelepunt poortnummer. Typ bijvoorbeeld `HISDEMO2.cloudapp.net:9089`.
   * Typ de waarde voor **Informix databasenaam**. Typ bijvoorbeeld `NWIND`.
   * Typ de waarde voor **gebruikersnaam**. Typ bijvoorbeeld `informix`.
   * Typ de waarde voor **wachtwoord**. Typ bijvoorbeeld `Password1`.
9. Selecteer **maken** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
11. Selecteer desgewenst **geavanceerde opties weergeven** toospecify query-opties.
12. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. In Hallo **InformixgetRows** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
14. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die een lijst met rijen bevatten.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Een rij invoegen met toevoegen
U kunt een logische app actie tooadd één rij in een Informix-tabel maken. Deze actie geeft opdracht Hallo connector tooprocess een Informix-INSERT-instructie zoals `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `InformixinsertRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - rij invoegen (Preview)**.
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** deelvenster configuratie Selecteer tooselect een verbinding. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**, type `Area 99999`, en het type `102` voor **REGIONID**. 
10. Selecteer **Opslaan**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. In Hallo **InformixinsertRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die de nieuwe rij Hallo bevatten.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Ophalen van één rij met selecteren
U kunt een logische app actie toofetch één rij in een Informix-tabel maken. Deze actie geeft opdracht Hallo connector tooprocess een instructie Informix selecteren waar zoals `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `InformixgetRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - Get-rijen (Preview)** .
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster Selecteer tooselect een bestaande verbinding. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**. 
10. Selecteer desgewenst **geavanceerde opties weergeven** toospecify query-opties.
11. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. In Hallo **InformixgetRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
13. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die rij bevatten.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Wijzigen van één rij met UPDATE
U kunt een logische app actie toochange één rij in een Informix-tabel maken. Deze actie geeft opdracht Hallo connector tooprocess een Informix-UPDATE-instructie, zoals `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `InformixupdateRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - Update-rij (Preview)**.
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster Selecteer tooselect een bestaande verbinding. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**, type `Updated 99999`, en het type `102` voor **REGIONID**. 
10. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. In Hallo **InformixupdateRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die de nieuwe rij Hallo bevatten.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Verwijderen van één rij met DELETE
U kunt een logische app actie tooremove één rij in een Informix-tabel maken. Deze actie geeft opdracht Hallo connector tooprocess een Informix-instructie DELETE, zoals `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Een logische app maken
1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.
2. Voer Hallo **naam**, zoals `InformixdeleteRow`, **abonnement**, **resourcegroep**, **locatie**, en **App Service-Plan**. Selecteer **pincode toodashboard**, en selecteer vervolgens **maken**.

### <a name="add-a-trigger-and-action"></a>Toevoegen van een trigger en action
1. In Hallo **Logic Apps Designer**, selecteer **leeg LogicApp** in Hallo **sjablonen** lijst.
2. In Hallo **triggers** selecteert **terugkeerpatroon**. 
3. In Hallo **terugkeerpatroon** worden geactiveerd, selecteer **bewerken**, selecteer **frequentie** vervolgkeuzelijst tooselect **dag**, en selecteer vervolgens  **Interval** tootype **7**. 
4. Selecteer Hallo **+ een nieuwe stap** vak en selecteer vervolgens **een actie toevoegen**.
5. In Hallo **acties** typt **informix** in Hallo **zoeken naar meer acties** invoervak en selecteer vervolgens **Informix - rij verwijderen (Preview)**.
6. In Hallo **rijen (Preview) ophalen** actie, selecteer **verbinding wijzigen**. 
7. In Hallo **verbindingen** configuraties deelvenster een bestaande verbinding selecteren. Selecteer bijvoorbeeld **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In Hallo **tabelnaam** lijst, selecteer Hallo **pijl-omlaag**, en selecteer vervolgens **gebied**.
9. Geef waarden voor alle vereiste kolommen (Zie rode sterretjes). Typ bijvoorbeeld `99999` voor **gebieds-id**. 
10. Selecteer **Opslaan**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. In Hallo **InformixdeleteRow** blade binnen Hallo **alle sessies** lijst onder **samenvatting**, selecteer Hallo eerste vermeld item (meest recente uitvoeren).
12. In Hallo **logische app uitgevoerd** blade Selecteer **Details uitvoering van**. Binnen Hallo **actie** selecteert **Get_rows**. Hallo-waarde voor **Status**, die moet worden **geslaagd**. Selecteer Hallo **invoer koppeling** tooview Hallo invoer. Selecteer Hallo **uitvoer koppeling**, en levert weergave Hallo; die Hallo verwijderde rij bevatten.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Ondersteunde platforms Informix en versies
Deze connector ondersteunt de volgende IBM Informix-versies wanneer geconfigureerd Hallo toosupport gedistribueerd relationele Database architectuur DRDA ()-clientverbindingen.

* IBM Informix 12.1
* IBM Informix 11,7

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/informix/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).

