---
title: 'Azure PowerShell: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die in Azure-portal.
keywords: zelfstudie over sql-database, een sql-database maken
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Een individuele Azure SQL Database maken met PowerShell

PowerShell is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. Deze handleiding PowerShell toodeploy wilt weergeven voor een Azure SQL database in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in een [logische Azure SQL Database-server](sql-database-features.md).

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

Deze zelfstudie vereist hello Azure PowerShell-moduleversie 4.0 of hoger. Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Tooyour aanmelden met Azure-abonnement met Hallo [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) opdracht in en volg Hallo op het scherm instructies.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Variabelen maken

Definieer de variabelen voor gebruik in Hallo-scripts in deze snel starten.

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Een logische server maken

Maak een [logische Azure SQL Database-server](sql-database-features.md) met Hallo [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) opdracht. Een logische server bevat een groep met databases die worden beheerd als groep. Hallo volgende voorbeeld wordt een willekeurige naam server in de resourcegroep met de beheerderaanmelding van een met de naam `ServerAdmin` en het wachtwoord `ChangeYourAdminPassword1`. U kunt deze vooraf gedefinieerde waarden vervangen.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Een serverfirewallregel configureren

Maak een [Azure SQL Database firewallregel op serverniveau](sql-database-firewall-configure.md) met Hallo [nieuw AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) opdracht. Een firewallregel op serverniveau kunt een externe toepassing, zoals SQL Server Management Studio of Hallo SQLCMD-hulpprogramma tooconnect tooa SQL-database via Hallo SQL Database-service firewall. In Hallo voorbeeld te volgen, wordt alleen Hallo firewall geopend voor andere Azure-resources. tooenable externe connectiviteit wijziging Hallo IP-adres tooan juiste adres voor uw omgeving. tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Een database in het Hallo-server met voorbeeldgegevens maken

Maken van een database met een [prestatieniveau S0](sql-database-service-tiers.md) in Hallo-server op Hallo met [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) opdracht. Hallo volgende voorbeeld maakt u een database met de naam `mySampleDatabase` en belastingen Hallo AdventureWorksLT voorbeeldgegevens in deze database. Vervang deze vooraf gedefinieerde waarden naar wens (andere snel aan de slag in deze verzameling gebouwd op Hallo-waarden in deze snel starten).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Resources opschonen

Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd. 

> [!TIP]
> Als u van plan toocontinue toowork met latere snel aan de slag bent, Hallo-resources die zijn gemaakt in deze snelle opruimen start niet. Als u niet van plan toocontinue bent, gebruikt u Hallo na stappen toodelete alle resources gemaakt door deze snel starten in hello Azure-portal.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Volgende stappen

Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren. Klik op de onderstaande hulpprogramma's voor meer informatie:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

