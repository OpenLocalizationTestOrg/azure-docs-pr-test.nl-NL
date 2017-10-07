---
title: 'C#: Aan de slag met Azure SQL Database | Microsoft Docs'
description: Probeer SQL Database om SQL en C#-apps ontwikkelen en een Azure SQL Database te maken met C# met Hallo SQL Database-bibliotheek voor .NET.
keywords: Probeer sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Gebruik C# toocreate een SQL-database met Hallo SQL Database-bibliotheek voor .NET

Meer informatie over hoe toouse C# toocreate een Azure SQL database met Hallo [Microsoft Azure SQL Management-bibliotheek voor .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Dit artikel wordt beschreven hoe toocreate één database met SQL en C#. toocreate elastische pools, Zie [maken van een elastische pool](sql-database-elastic-pool-manage-csharp.md).

Hello Azure SQL Database Management-bibliotheek voor .NET biedt een [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-gebaseerde API die Hallo [Resource Manager gebaseerde SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Veel nieuwe functies van SQL-Database worden alleen ondersteund wanneer u Hallo [Azure Resource Manager-implementatiemodel](../azure-resource-manager/resource-group-overview.md), dus u moet Hallo altijd nieuwste gebruiken **Azure SQL Database Management-bibliotheek voor .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Hallo oudere [klassieke implementatiemodel op basis van bibliotheken](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) worden ondersteund voor achterwaartse compatibiliteit alleen, dus aangeraden Hallo nieuwere Resource Manager gebaseerde bibliotheken te gebruiken.
> 
> 

toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

* Een Azure-abonnement. Als u een Azure-abonnement gewoon klikt u op **gratis ACCOUNT** Hallo boven aan deze pagina en vervolgens terugkeren toofinish in dit artikel.
* Visual Studio. Zie voor een gratis exemplaar van Visual Studio Hallo [Visual Studio-Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) pagina.

> [!NOTE]
> Dit artikel maakt een nieuwe, lege SQL-database. Hallo wijzigen *CreateOrUpdateDatabase(...)*  methode in Hallo voorbeeld toocopy databases te volgen, databases schalen, maak een database in een groep van toepassingen, enzovoort.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Een consoletoepassing maken en Hallo vereiste bibliotheken installeren
1. Start Visual Studio.
2. Klik op **Bestand** > **Nieuw** > **Project**.
3. Maak een **consoletoepassing** met C# en noem deze *SqlDbConsoleApp*

een SQL-database met C#, load Hallo toocreate vereist management-bibliotheken (met behulp van Hallo [package manager-console](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Klik op **Hulpprogramma's** > **NuGet Package Manager** > **Package Manager-console**.
2. Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall Hallo nieuwste [Management-bibliotheek van Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [bibliotheek van Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [algemene Microsoft Azure-Verificatiebibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Hallo voorbeelden in dit artikel gebruiken een synchrone vorm van elke API-aanvraag en blokkeren totdat de REST-aanroep Hallo op Hallo onderliggende service is voltooid. Er zijn asynchrone methoden beschikbaar.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Een SQL Database-server, firewallregel en SQL Database maken: C#-voorbeeld
Hallo volgende voorbeeld maakt een resourcegroep, server firewallregel en een SQL-database. Zie, [resources maken van een service-principal tooaccess](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variabelen.

Hallo-inhoud van vervangen **Program.cs** met de volgende Hallo en update Hallo `{variables}` met uw app-waarden (omvatten geen Hallo `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a>Een service-principal tooaccess resources maken
Hallo maakt volgende PowerShell-script Hallo Active Directory (AD) en -Hallo service principal dat we tooauthenticate onze C#-app moeten. Hallo script levert waarden die we nodig voor voorgaande C# Hallo steekproef. Zie voor gedetailleerde informatie [gebruik Azure PowerShell toocreate een service-principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt geprobeerd SQL-Database en het instellen van een database met C#, bent u klaar voor Hallo artikelen te volgen:

* [Verbinding maken met tooSQL Database met SQL Server Management Studio en een voorbeeld T-SQL-query uitvoeren](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Aanvullende resources
* [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)
* [Databaseklasse](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
