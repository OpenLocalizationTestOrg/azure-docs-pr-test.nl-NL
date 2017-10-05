---
title: Multitenant SaaS-toepassing met Azure SQL Database implementeren | Microsoft Docs
description: "Multitenant SaaS-toepassing met Azure SQL Database worden geïmplementeerd."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementeren van een multitenant SaaS-toepassing met behulp van Azure SQL Database

Een multitenant-toepassing is een toepassing die wordt gehost in een cloudomgeving en biedt dezelfde set van services op honderden of duizenden tenants die niet delen of elkaars gegevens zien. Een voorbeeld is een SaaS-toepassing die services aan tenants in een cloud gehoste omgeving levert. Dit model worden geïsoleerd van de gegevens voor elke tenant en optimaliseert de distributie van resources voor de kosten. 

Deze zelfstudie laat zien hoe een multitenant SaaS-toepassing met behulp van Azure SQL Database maken.

In deze zelfstudie leert u hoe:
> [!div class="checklist"]
> * Een databaseomgeving instellen voor de ondersteuning van een multitenant SaaS-toepassing met behulp van het patroon Database per tenant
> * Een tenant-catalogus maken
> * Een tenant-database in te richten en deze te registreren in de tenant-catalogus
> * Een voorbeeld van een Java-toepassing instellen 
> * Toegang tot tenant databases eenvoudig een Java-consoletoepassing
> * Verwijderen van een tenant

Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten

Zorg ervoor dat u hebt voor het voltooien van deze zelfstudie:

* De nieuwste versie van PowerShell hebt geïnstalleerd en de [nieuwste Azure PowerShell-SDK](http://azure.microsoft.com/downloads/)

* De meest recente versie van geïnstalleerd [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Installatie van SQL Server Management Studio, installeert ook de nieuwste versie van SQLPackage, een opdrachtregelprogramma dat kan worden gebruikt om een scala aan database ontwikkeling taken automatiseren.

* Geïnstalleerd de [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) en de [meest recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) op deze computer geïnstalleerd. 

* Geïnstalleerd [Apache Maven](https://maven.apache.org/download.cgi). Maven zal worden gebruikt bij het beheren van afhankelijkheden, bouwen, testen en voer het voorbeeld Java-project

## <a name="set-up-data-environment"></a>Data-omgeving instellen

U worden een database per tenant ingericht. De model-database per tenant biedt de grootste mate van isolatie tussen de tenants met weinig DevOps-kosten. Voor het optimaliseren van de kosten van cloudresources u omvat ook de inrichting van de tenant-databases in een elastische pool zodat u kunt de prestaties van de prijs voor een groep met databases. Voor meer informatie over andere database inrichting modellen [Hier ziet](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Volg deze stappen om een SQL-server en een elastische pool die als host voor alle databases in uw tenant fungeert te maken. 

1. Variabelen voor het opslaan van de waarden die worden gebruikt in de rest van de zelfstudie maken. Zorg ervoor dat u de IP-adres variabele om op te nemen van uw IP-adres wijzigen 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. Aanmelden bij Azure en een SQL server en de elastische pool maken 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a>Tenant-catalogus maken 

In een multitenant SaaS-toepassing is het belangrijk te weten waar informatie voor een tenant wordt opgeslagen. Dit wordt meestal opgeslagen in een catalogusdatabase. De catalogusdatabase wordt gebruikt voor het opslaan van een toewijzing tussen een tenant en een database waarin deze tenant gegevens worden opgeslagen.  Het basispatroon is van toepassing als een multitenant of een één-tenant-database wordt gebruikt.

Volg deze stappen voor het maken van een catalogusdatabase voor de SaaS-voorbeeldtoepassing.

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Database voor 'tenant1' in te richten en te registreren in de catalogus voor tenant 
Powershell gebruiken om een database in te richten voor een nieuwe tenant 'tenant1' en deze tenant te registreren in de catalogus. 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Database voor 'tenant2' in te richten en te registreren in de catalogus voor tenant
Powershell gebruiken om een database in te richten voor een nieuwe tenant 'tenant2' en deze tenant te registreren in de catalogus. 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a>Voorbeeld van Java-toepassing instellen 

1. Maak een maven-project. Typ het volgende in een opdrachtpromptvenster:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Voeg deze afhankelijkheid, taalniveau en bouwen optie ter ondersteuning van de manifest-bestanden in potten van het bestand pom.xml:
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. Voeg de volgende in het bestand App.java:

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. Sla het bestand op.

5. Ga naar de opdrachtconsole en uitvoeren

   ```bash
   mvn package
   ```

6. Als u klaar bent, voer het volgende uit als de toepassing wilt uitvoeren 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
De uitvoer ziet er als volgt als deze is uitgevoerd:

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a>Eerste tenant verwijderen 
PowerShell gebruiken om te verwijderen van de tenant-database en de catalogus-vermelding voor de eerste tenant.

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

Verbinding met 'tenant1' te maken met de Java-toepassing. U krijgt een foutmelding weergegeven dat de tenant niet bestaat.

## <a name="next-steps"></a>Volgende stappen 

In deze zelfstudie hebt u geleerd:
> [!div class="checklist"]
> * Een databaseomgeving instellen voor de ondersteuning van een multitenant SaaS-toepassing met behulp van het patroon Database per tenant
> * Een tenant-catalogus maken
> * Een tenant-database in te richten en deze te registreren in de tenant-catalogus
> * Een voorbeeld van een Java-toepassing instellen 
> * Toegang tot tenant databases eenvoudig een Java-consoletoepassing
> * Verwijderen van een tenant

* Voorbeelden van PowerShell voor algemene taken, Zie [SQL Database PowerShell-voorbeelden](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Ontwerppatronen voor multitenant SaaS-toepassingen Zie [ontwerppatronen](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Java-voorbeelden van veel voorkomende taken van Azure, Zie [Java Developer Center](https://azure.microsoft.com/develop/java/)



