---
title: aaaAzure SQL Database connectivity-architectuur | Microsoft Docs
description: Dit document wordt uitgelegd hello Azure SQLDB connectiviteit-architectuur van Azure of vanuit buiten Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Azure SQL Database Connectivity-architectuur 

In dit artikel wordt uitgelegd hello Azure SQL Database connectivity-architectuur en wordt uitgelegd hoe de verschillende onderdelen Hallo toodirect verkeer tooyour exemplaar van Azure SQL Database werken. Deze Azure SQL Database connectivity-componenten werken toodirect netwerkverkeer toohello Azure-database met clients die verbinding maken vanuit Azure en clients die verbinding maakt vanaf buiten Azure. In dit artikel biedt ook script voorbeelden toochange hoe connectiviteit plaatsvindt en Hallo overwegingen gerelateerd toochanging Hallo connectivity standaardinstellingen. Als er vragen na het lezen van dit artikel, neem contact op met Dhruv op dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Connectiviteitsarchitectuur

Hallo volgende diagram biedt een overzicht van hello Azure SQL Database connectivity-architectuur. 

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/architecture-overview.png)


Hallo volgende stappen wordt beschreven hoe een verbinding tot stand gebrachte tooan Azure SQL database via hello Azure SQL Database software load balancer (SLB) en hello Azure SQL Database-gateway is.

- Clients in Azure of buiten Azure verbinding toohello SLB dat een openbare IP-adres en luistert op poort 1433.
- Hallo SLB stuurt verkeer toohello Azure SQL Database-gateway.
- Hallo-gateway wordt omgeleid Hallo verkeer toohello juiste proxy middleware.
- Hallo proxy middleware leidt Hallo verkeer toohello juiste Azure SQL database.

> [!IMPORTANT]
> Elk van deze onderdelen is denial of service (DDoS) beveiliging ingebouwde op Hallo netwerk- en app-laag Hallo gedistribueerd.
>

## <a name="connectivity-from-within-azure"></a>Verbinding tussen in Azure

Als u verbinding vanaf in Azure maakt, uw verbindingen hebben een beleid van **omleiden** standaard. Een beleid van **omleiden** betekent dat verbindingen nadat Hallo TCP-sessie tot stand gebrachte toohello Azure SQL-database is, Hallo clientsessie vervolgens omgeleid toohello proxy middleware met een wijziging toohello bestemming virtuele IP-adres uit die van hello Azure SQL Database gateway toothat van Hallo proxy middleware. Daarna alle latere pakketten stromen rechtstreeks via Hallo proxy middleware, omzeilen hello Azure SQL Database-gateway. Hallo volgende diagram illustreert dit netwerkverkeer.

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Connectiviteit van buiten Azure

Als u verbinding vanaf buiten Azure maakt, uw verbindingen hebben een beleid van **Proxy** standaard. Een beleid van **Proxy** betekent dat dat Hallo TCP-sessie tot stand is gebracht via hello Azure SQL Database-gateway en alle latere pakketten via stromen Hallo gateway. Hallo volgende diagram illustreert dit netwerkverkeer.

![overzicht van de architectuur](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>IP-adressen van Azure SQL Database-gateway

tooconnect tooan Azure SQL-database van lokale bronnen, moet u tooallow uitgaand verkeer toohello Azure SQL Database netwerkgateway voor uw Azure-regio. Uw verbindingen gaat alleen via Hallo gateway om verbinding te maken in de Proxy-modus, die de standaardeigenschap hello om verbinding te maken van lokale bronnen.

Hallo volgende Tabellijsten Hallo primaire en secundaire IP-adressen van hello Azure SQL Database-gateway voor alle regio's van gegevens. Er zijn twee IP-adressen voor bepaalde gebieden. In deze regio's, Hallo primaire IP-adres is het huidige IP-adres Hallo van Hallo gateway en Hallo tweede IP-adres is een failover-IP-adres. Hallo failover-adres is Hallo adres toowhich kunnen we uw server tookeep Hallo servicebeschikbaarheid hoge verplaatsen. Voor deze regio's, is het raadzaam dat u uitgaande tooboth Hallo IP-adressen toestaat. Hallo tweede IP-adres is het eigendom van Microsoft en luistert niet op alle services totdat deze is geactiveerd door Azure SQL Database tooaccept verbindingen.

| Naam regio | Primaire IP-adres | Secundaire IP-adres |
| --- | --- |--- |
| Australië - oost | 191.238.66.109 | 13.75.149.87 |
| Australië - zuidoost | 191.239.192.109 | 13.73.109.251 |
| Brazilië - zuid | 104.41.11.5 | |    
| Canada - midden | 40.85.224.249 | |    
| Canada - oost | 40.86.226.166 | |
| VS - midden | 23.99.160.139 | 13.67.215.62 |
| Oost-Azië | 191.234.2.139 | 52.175.33.150 |
| VS-Oost 1 | 191.238.6.43 | 40.121.158.30 |
| VS - oost 2 | 191.239.224.107 | 40.79.84.180 |
| India - midden | 104.211.96.159  | |   
| India - zuid | 104.211.224.146  | |
| India - west | 104.211.160.80 | |
| Japan - oost | 191.237.240.43 | 13.78.61.196 |
| Japan - west | 191.238.68.11 | 104.214.148.156 |
| Korea - centraal | 52.231.32.42 | |
| Korea - zuid | 52.231.200.86 |  |
| Noord-centraal VS | 23.98.55.75 | 23.96.178.199 |
| Noord-Europa | 191.235.193.75 | 40.113.93.91 |
| Zuid-centraal VS | 23.98.162.75 | 13.66.62.124 |
| Zuidoost-Azië | 23.100.117.95 | 104.43.15.0 |
| VK, noord | 13.87.97.210 | |
| VK Zuid 1 | 51.140.184.11 | |    
| VK, zuid 2 | 13.87.34.7 | |
| Verenigd Koninkrijk West | 51.141.8.11  | |
| West-centraal VS | 13.78.145.25 | |
| West-Europa | 191.237.232.75 | 40.68.37.158 |
| VS-West 1 | 23.99.34.75 | 104.42.238.205 |
| VS - west 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Azure SQL Database verbindingsbeleid wijzigen

toochange hello verbindingsbeleid Azure SQL Database voor een Azure SQL Database-server, gebruik Hallo [REST-API](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Als uw verbindingsbeleid voor de is ingesteld, te**Proxy**, alle netwerkapparaten stroom van pakketten via hello Azure SQL Database-gateway. Voor deze instelling moet u tooallow uitgaande tooonly hello Azure SQL Database gateway IP. Met behulp van een instelling van **Proxy** heeft latentie van meer dan een instelling van **omleiden**. 
- Als uw verbindingsbeleid voor de tot stand **omleiden**, alle netwerkpakketten stromen rechtstreeks toohello middleware proxy. Voor deze instelling moet u tooallow uitgaande toomultiple IP-adressen. 

## <a name="script-toochange-connection-settings"></a>Script toochange verbindingsinstellingen

> [!IMPORTANT]
> Dit script vereist Hallo [Azure PowerShell-module](/powershell/azure/install-azurerm-ps).
>

Hallo volgende PowerShell-script toont hoe toochange verbindingsbeleid Hallo.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Volgende stappen

- Zie voor informatie over hoe toochange Hallo verbindingsbeleid Azure SQL Database voor een Azure SQL Database-server, [REST-API met behulp van maken of Update Server verbindingsbeleid Hallo](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Zie voor informatie over de werking van Azure SQL Database-verbinding voor clients die gebruikmaken van ADO.NET 4.5 of hoger, [poorten buiten 1433 ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Zie voor informatie over algemene toepassing ontwikkeling overzicht, [SQL Database ontwikkelen-overzicht](sql-database-develop-overview.md).
