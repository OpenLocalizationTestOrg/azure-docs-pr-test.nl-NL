---
title: aaaImplement multitenant SaaS-toepassing met Azure SQL Database | Microsoft Docs
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="36181-103">Implementeren van een multitenant SaaS-toepassing met behulp van Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="36181-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="36181-104">Een multitenant-toepassing is een toepassing die wordt gehost in een cloudomgeving en biedt Hallo dezelfde set services toohundreds of duizenden tenants die niet delen of elkaars gegevens zien.</span><span class="sxs-lookup"><span data-stu-id="36181-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="36181-105">Een voorbeeld is een SaaS-toepassing die voorziet in tootenants in een omgeving met cloud-gebaseerde services.</span><span class="sxs-lookup"><span data-stu-id="36181-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="36181-106">Dit model isoleert Hallo-gegevens voor elke tenant en optimaliseert de Hallo distributie van resources voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="36181-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="36181-107">Deze zelfstudie laat zien hoe toocreate een multitenant SaaS-toepassing met behulp van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="36181-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="36181-108">In deze zelfstudie leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="36181-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="36181-109">Instellen van een database omgeving toosupport een multitenant SaaS-toepassing hello Database per tenant patroon</span><span class="sxs-lookup"><span data-stu-id="36181-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="36181-110">Een tenant-catalogus maken</span><span class="sxs-lookup"><span data-stu-id="36181-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="36181-111">Een tenant-database in te richten en deze te registreren in Hallo tenant catalogus</span><span class="sxs-lookup"><span data-stu-id="36181-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="36181-112">Een voorbeeld van een Java-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="36181-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="36181-113">Toegang tot tenant databases eenvoudig een Java-consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="36181-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="36181-114">Verwijderen van een tenant</span><span class="sxs-lookup"><span data-stu-id="36181-114">Delete a tenant</span></span>

<span data-ttu-id="36181-115">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="36181-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36181-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="36181-116">Prerequisites</span></span>

<span data-ttu-id="36181-117">toocomplete deze zelfstudie, zorg ervoor dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="36181-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="36181-118">Geïnstalleerde Hallo nieuwste versie van PowerShell en Hallo [nieuwste Azure PowerShell-SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="36181-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="36181-119">Meest recente versie van geïnstalleerde Hallo [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="36181-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="36181-120">Installatie van SQL Server Management Studio ook Hallo meest recente versie van SQLPackage, een opdrachtregelprogramma waarmee gebruikte tooautomate een bereik van database ontwikkeling taken kan worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="36181-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="36181-121">Geïnstalleerde Hallo [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) en Hallo [meest recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) op deze computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="36181-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="36181-122">Geïnstalleerd [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="36181-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="36181-123">Maven gebruikt toohelp afhankelijkheden beheren, bouwen, testen en Hallo voorbeeld Java-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="36181-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="36181-124">Data-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="36181-124">Set up data environment</span></span>

<span data-ttu-id="36181-125">U worden een database per tenant ingericht.</span><span class="sxs-lookup"><span data-stu-id="36181-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="36181-126">Hallo database per tenant model biedt Hallo grootste mate van isolatie tussen de tenants met weinig DevOps-kosten.</span><span class="sxs-lookup"><span data-stu-id="36181-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="36181-127">toooptimize hello kosten van cloudresources, u omvat ook de inrichting van Hallo tenant databases in een elastische pool waarmee u toooptimize Hallo prijs prestaties voor een groep met databases.</span><span class="sxs-lookup"><span data-stu-id="36181-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="36181-128">toolearn over andere database inrichting modellen [Hier ziet](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="36181-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="36181-129">Volg deze stappen toocreate een SQL-server en een elastische pool die als host voor alle databases in uw tenant fungeert.</span><span class="sxs-lookup"><span data-stu-id="36181-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="36181-130">Variabelen toostore waarden die worden gebruikt in de rest van de zelfstudie Hallo Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="36181-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="36181-131">Zorg ervoor dat toomodify Hallo IP-adres variabele tooinclude uw IP-adres</span><span class="sxs-lookup"><span data-stu-id="36181-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="36181-132">Aanmelding tooAzure en een SQL server en de elastische pool maken</span><span class="sxs-lookup"><span data-stu-id="36181-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="36181-133">Tenant-catalogus maken</span><span class="sxs-lookup"><span data-stu-id="36181-133">Create tenant catalog</span></span> 

<span data-ttu-id="36181-134">Het is belangrijk tooknow waar informatie voor een tenant wordt opgeslagen in een multitenant SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="36181-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="36181-135">Dit wordt meestal opgeslagen in een catalogusdatabase.</span><span class="sxs-lookup"><span data-stu-id="36181-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="36181-136">Hallo catalogus-database is gebruikte toohold een toewijzing tussen een tenant en een database waarin deze tenant gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="36181-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="36181-137">Hallo basispatroon is van toepassing als een multitenant of een één-tenant-database wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="36181-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="36181-138">Volg deze stappen toocreate een catalogusdatabase voor de voorbeeldtoepassing SaaS Hallo.</span><span class="sxs-lookup"><span data-stu-id="36181-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="36181-139">Database voor 'tenant1' in te richten en te registreren in de catalogus voor tenant</span><span class="sxs-lookup"><span data-stu-id="36181-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="36181-140">Gebruik Powershell tooprovision een database voor een nieuwe tenant 'tenant1' en registreer deze tenant in Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="36181-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="36181-141">Database voor 'tenant2' in te richten en te registreren in de catalogus voor tenant</span><span class="sxs-lookup"><span data-stu-id="36181-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="36181-142">Gebruik Powershell tooprovision een database voor een nieuwe tenant 'tenant2' en registreer deze tenant in Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="36181-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="36181-143">Voorbeeld van Java-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="36181-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="36181-144">Maak een maven-project.</span><span class="sxs-lookup"><span data-stu-id="36181-144">Create a maven project.</span></span> <span data-ttu-id="36181-145">Typ Hallo volgende in een opdrachtpromptvenster:</span><span class="sxs-lookup"><span data-stu-id="36181-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="36181-146">Voeg deze afhankelijkheid, taalniveau en bouwen optie toosupport manifestbestanden in potten toohello pom.xml-bestand:</span><span class="sxs-lookup"><span data-stu-id="36181-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="36181-147">Voeg de volgende Hallo in Hallo App.java bestand:</span><span class="sxs-lookup"><span data-stu-id="36181-147">Add hello following into hello App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. <span data-ttu-id="36181-148">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="36181-148">Save hello file.</span></span>

5. <span data-ttu-id="36181-149">Ga toocommand console en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="36181-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="36181-150">Als u klaar bent Hallo na toorun Hallo toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="36181-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="36181-151">Hallo-uitvoer ziet er als volgt als deze is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="36181-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="36181-152">Eerste tenant verwijderen</span><span class="sxs-lookup"><span data-stu-id="36181-152">Delete first tenant</span></span> 
<span data-ttu-id="36181-153">Gebruik PowerShell toodelete hello tenant-database en de catalogus vermelding voor de eerste Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="36181-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="36181-154">Probeer verbinding te maken met behulp van 'tenant1' hello te Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="36181-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="36181-155">U krijgt een foutmelding weergegeven dat die Hallo tenant bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="36181-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36181-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36181-156">Next steps</span></span> 

<span data-ttu-id="36181-157">In deze zelfstudie hebt u geleerd:</span><span class="sxs-lookup"><span data-stu-id="36181-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="36181-158">Instellen van een database omgeving toosupport een multitenant SaaS-toepassing hello Database per tenant patroon</span><span class="sxs-lookup"><span data-stu-id="36181-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="36181-159">Een tenant-catalogus maken</span><span class="sxs-lookup"><span data-stu-id="36181-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="36181-160">Een tenant-database in te richten en deze te registreren in Hallo tenant catalogus</span><span class="sxs-lookup"><span data-stu-id="36181-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="36181-161">Een voorbeeld van een Java-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="36181-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="36181-162">Toegang tot tenant databases eenvoudig een Java-consoletoepassing</span><span class="sxs-lookup"><span data-stu-id="36181-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="36181-163">Verwijderen van een tenant</span><span class="sxs-lookup"><span data-stu-id="36181-163">Delete a tenant</span></span>

* <span data-ttu-id="36181-164">Voorbeelden van PowerShell voor algemene taken, Zie [SQL Database PowerShell-voorbeelden](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="36181-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="36181-165">Ontwerppatronen voor multitenant SaaS-toepassingen Zie [ontwerppatronen](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="36181-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="36181-166">Java-voorbeelden van veel voorkomende taken van Azure, Zie [Java Developer Center](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="36181-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



