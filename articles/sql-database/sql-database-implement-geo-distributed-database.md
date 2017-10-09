---
title: een Azure SQL Database geografisch verspreide oplossing aaaImplement | Microsoft Docs
description: Meer informatie over tooconfigure uw Azure SQL Database en de toepassing voor failover tooa gerepliceerd database en failover testen.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a>Een database geografisch verspreide implementeren

In deze zelfstudie een Azure SQL-database en de toepassing voor failover-tooa externe regio configureren en vervolgens uw plan failover te testen. Procedures voor: 

> [!div class="checklist"]
> * Maken van databasegebruikers en machtigingen verlenen
> * Een firewallregel op databaseniveau instellen
> * Maak een [geo-replicatie failover-groep](sql-database-geo-replication-overview.md)
> * Maken en het compileren van een Java-toepassing tooquery een Azure SQL database
> * Uitvoeren van een herstel na noodgevallen detailanalyse

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.


## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

- Laatste geïnstalleerde Hallo [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Een Azure SQL database geïnstalleerd. In deze zelfstudie wordt de voorbeelddatabase van AdventureWorksLT Hallo met de naam **mySampleDatabase** van een van deze snel aan de slag:

   - [Database maken - Portal](sql-database-get-started-portal.md)
   - [Database maken - CLI](sql-database-get-started-cli.md)
   - [Database maken - PowerShell](sql-database-get-started-powershell.md)

- Een methode tooexecute SQL hebt geïdentificeerd-scripts uitvoeren op uw database, kunt u een van de volgende hulpprogramma's voor query Hallo:
   - query-editor in Hallo Hallo [Azure-portal](https://portal.azure.com). Zie voor meer informatie over het gebruik van Hallo query-editor in Azure-portal Hallo [Connect en query Query-Editor met](sql-database-get-started-portal.md#query-the-sql-database).
   - de nieuwste versie Hallo van [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), dit is een geïntegreerde omgeving voor het beheren van elke SQL-infrastructuur van tooSQL van SQL Server-Database voor Microsoft Windows.
   - Hallo nieuwste versie van [Visual Studio Code](https://code.visualstudio.com/docs), die een grafische code-editor voor Linux, Mac OS, en Windows die ondersteuning biedt voor extensies, met inbegrip Hallo [mssql-extensie](https://aka.ms/mssql-marketplace) voor query's in Microsoft SQL Server , Azure SQL Database en SQL datawarehouse. Zie voor meer informatie over het gebruik van dit hulpprogramma met Azure SQL Database [Connect en query met de Code van de VS](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Maken van databasegebruikers en machtigingen verlenen

Verbinding maken met database tooyour en Maak gebruikersaccounts met behulp van een Hallo hulpmiddelen voor query's te volgen:

- Hallo Query-editor in hello Azure-portal
- SQL Server Management Studio
- Visual Studio Code

Deze gebruikersaccounts repliceren automatisch tooyour secundaire server (en gesynchroniseerd blijven). toouse SQL Server Management Studio of Visual Studio Code, moet u mogelijk een firewallregel tooconfigure als u verbinding maakt vanaf een client op een IP-adres waarvoor u nog niet hebt geconfigureerd een firewall. Zie voor gedetailleerde stappen [maken van een firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- Uitvoeren in een query-venster Hallo query toocreate twee accounts voor gebruikers in uw database te volgen. Dit script verleent **db_owner** machtigingen toohello **app_admin** -account en verleent **Selecteer** en **UPDATE** machtigingen toohello **app_user** account. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Firewallregel op databaseniveau maken

Maak een [firewallregel op databaseniveau](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) voor uw SQL-database. Deze firewallregel op databaseniveau repliceert automatisch toohello secundaire server die u in deze zelfstudie maakt. Gebruik voor eenvoud (in deze zelfstudie) Hallo openbaar IP-adres van Hallo-computer waarop u Hallo stappen in deze zelfstudie uitvoert. toodetermine hello IP-adres voor Hallo serverniveau firewallregel voor de huidige computer, Zie [maken van een firewall serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- Hallo query te volgen, Hallo IP-adressen vervangen door een geschikte IP-adressen voor uw omgeving Hallo vervangen Hallo vorige query in het venster openen query.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Een actieve geo-replicatie automatische failover-groep maken 

Met Azure PowerShell maken een [actieve geo-replicatie automatische failover groep](sql-database-geo-replication-overview.md) tussen uw bestaande Azure SQL-server en Hallo nieuwe Azure SQL-server in een Azure-regio leeg en voeg vervolgens uw voorbeeld database toohello failover-groep.

> [!IMPORTANT]
> Deze cmdlets vereist Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Variabelen voor de PowerShell-scripts met Hallo waarden voor uw bestaande server en de voorbeelddatabase vullen en geef een globaal unieke waarde voor failover-groepsnaam op.

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. Een leeg back-server maken in uw regio failover.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Een groep failover tussen twee servers Hallo maken.

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. Uw database toohello failover-groep toevoegen.

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a>Java-software installeren

Hallo stappen in deze sectie wordt ervan uitgegaan dat u bekend bent met het ontwikkelen van u Java gebruikt en nieuwe tooworking met Azure SQL Database worden. 

### <a name="mac-os"></a>**Mac OS**
Open de terminal en navigeer van tooa directory waar u van plan bent een Java-project te maken. Installeer **brew** en **Maven** hiertoe Hallo volgende opdrachten: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer **Mac OS**, en volg Hallo gedetailleerde instructies voor het configureren van Java en Maven in stap 1.2 en 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Open de terminal en navigeer van tooa directory waar u van plan bent een Java-project te maken. Installeer **Maven** hiertoe Hallo volgende opdrachten:

```bash
sudo apt-get install maven
```

Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer **Ubuntu**, en volg Hallo gedetailleerde instructies voor het configureren van Java en Maven in stap 1.2, 1.3 en 1.4.

### <a name="windows"></a>**Windows**
Installeer [Maven](https://maven.apache.org/download.cgi) met Hallo officiële installer. Gebruik Maven toohelp afhankelijkheden beheren, bouwen, testen en uw Java-project uitvoeren. Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer Windows en volg Hallo gedetailleerde instructies voor Java en de Maven geconfigureerd in stap 1.2 en 1.3.

## <a name="create-sqldbsample-project"></a>SqlDbSample-project maken

1. In de opdrachtconsole hello (zoals Bash), een Maven-project te maken. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Type **Y** en klik op **Enter**.
3. Wijzig de mappen in het nieuwe project.

   ```bash
   cd SqlDbSamples
   ```

4. Open uw favoriete editor met Hallo pom.xml-bestand in de projectmap. 

5. Hallo Microsoft JDBC-stuurprogramma voor SQL Server-afhankelijkheid tooyour Maven-project via uw favoriete teksteditor toevoegen en kopiëren en plakken Hallo volgende regels in uw pom.xml-bestand. Hallo bestaande waarden vooraf ingevuld in het Hallo-bestand niet overschrijven. Hallo JDBC afhankelijkheid moet binnen Hallo groter 'afhankelijkheden' sectie () worden geplakt.   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Hallo-versie van Java-project toocompile Hallo tegen door toe te voegen na de sectie 'Eigenschappen' in hello pom.xml-bestand na Hallo 'afhankelijkheden' sectie Hallo opgeven. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Voeg de volgende Hallo 'maken' sectie Hallo pom.xml-bestand na Hallo 'Eigenschappen' sectie toosupport manifestbestanden in potten.       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. Opslaan en sluiten Hallo pom.xml-bestand.
9. Open Hallo App.java-bestand (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) en Hallo inhoud vervangen door Hallo inhoud te volgen. Hallo failover groepsnaam vervangen door Hallo-naam voor de failover-groep. Als u Hallo waarden voor de databasenaam hello, gebruiker of wachtwoord hebt gewijzigd, moet u deze waarden ook wijzigen.

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. Opslaan en sluiten Hallo App.java bestand.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Compileren en Hallo SqlDbSample project uitvoeren

1. In de opdrachtconsole hello, toofollowing opdracht niet uitvoeren.

   ```bash
   mvn package
   ```
2. Als u klaar bent uitvoeren Hallo opdracht toorun Hallo toepassing (deze wordt uitgevoerd voor ongeveer 1 uur tenzij u handmatig stopt) te volgen:

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Disaster recovery inzoomen uitvoeren

1. Handmatige failover van de groep failover-aanroep. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Houd rekening met Hallo resultaten van de toepassing tijdens de failover. Sommige voegt mislukt tijdens het Hallo DNS-cache wordt vernieuwd.     

3. Ontdek welke rol u uw herstel na noodgevallen server wordt uitgevoerd.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Failback.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Hallo resultaten van de toepassing tijdens de failback zien. Sommige voegt mislukt tijdens het Hallo DNS-cache wordt vernieuwd.     

6. Ontdek welke rol u uw herstel na noodgevallen server wordt uitgevoerd.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Volgende stappen 

Zie voor meer informatie [actieve geo-replicatie en failover groepen](sql-database-geo-replication-overview.md).
