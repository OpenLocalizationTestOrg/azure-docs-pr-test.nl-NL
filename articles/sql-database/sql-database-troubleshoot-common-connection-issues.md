---
title: aaaTroubleshoot algemene verbinding problemen tooAzure SQL-Database
description: Stappen tooidentify en los algemene verbindingsfouten voor Azure SQL Database.
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Verbinding problemen tooAzure SQL Database oplossen
Wanneer Hallo verbinding tooAzure SQL-Database is mislukt, krijgt u [foutberichten](sql-database-develop-error-messages.md). Dit artikel is een gecentraliseerde onderwerp helpt u problemen met Azure SQL Database. Het geeft [Hallo algemene oorzaken](#cause) van verbindingsproblemen, raadt [een hulpprogramma voor het oplossen van problemen](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) die helpt u bij de identiteit Hallo probleem en biedt het oplossen van problemen stappen toosolve [ Tijdelijke fouten](#troubleshoot-transient-errors) en [permanente of tijdelijke fouten](#troubleshoot-persistent-errors). 

Als u problemen met de Hallo ondervindt, kunt u Hallo oplossen stappen die worden beschreven in dit artikel.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Oorzaak
Problemen met de verbinding kunnen worden veroorzaakt door een van de volgende Hallo:

* Fout tooapply best practices en ontwerprichtlijnen tijdens ontwerpproces Hallo-toepassing.  Zie [overzicht voor ontwikkelaars van SQL Database](sql-database-develop-overview.md) tooget gestart.
* Herconfiguratie van Azure SQL Database
* Firewallinstellingen
* Verbindingstime-out
* Onjuiste aanmeldingsgegevens
* Maximum aantal is bereikt op sommige Azure SQL Database-resources

In het algemeen verbinding problemen tooAzure SQL-Database kunt als volgt worden ingedeeld:

* [Tijdelijke fouten (tijdelijke of onregelmatige)](#troubleshoot-transient-errors)
* [Permanente of tijdelijke fouten (fouten regelmatig terugkerende)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Probeer het Hallo-probleemoplosser voor Azure SQL Database-verbindingsproblemen
Als u een specifieke verbindingsfout ondervindt, kunt u [dit hulpprogramma](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), die wordt waarmee u snel identiteit en het probleem kunt oplossen.

## <a name="troubleshoot-transient-errors"></a>Tijdelijke fouten oplossen

Wanneer een toepassing verbinding tooan Azure SQL database maakt, ontvangen Hallo volgende foutbericht weergegeven:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Dit foutbericht wordt gewoonlijk tijdelijk (tijdelijke).
> 
> 

Deze fout treedt op wanneer hello Azure-database wordt verplaatst (of opnieuw geconfigureerd) en uw toepassing verliest de verbinding toohello SQL-database. SQL database-herconfiguratie gebeurtenissen optreden vanwege een geplande gebeurtenis (bijvoorbeeld een software-upgrade) of een niet-geplande gebeurtenis (bijvoorbeeld een proces crash of taakverdeling). De meeste herconfiguratie van gebeurtenissen in het algemeen tijdelijke zijn en moeten worden voltooid in minder dan 60 seconden maximaal. Deze gebeurtenissen kunnen echter van tijd tot tijd langer toofinish, zoals wanneer een grote transactie zorgt een herstelbewerking langlopende dat overnemen.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Stappen tooresolve tijdelijke verbindingsproblemen

1. Controleer de Hallo [servicedashboard van Microsoft Azure](https://azure.microsoft.com/status) voor eventuele bekende uitval die is opgetreden tijdens het Hallo-tijd gedurende welke Hallo fouten zijn gemeld door de toepassing hello.
2. Toepassingen die verbinding maken met cloudservice tooa zoals Azure SQL Database moet periodieke herconfiguratie gebeurtenissen verwachten en implementeren probeer logica toohandle deze fouten in plaats van deze toepassing fouten toousers halen. Bekijk Hallo [tijdelijke fouten](sql-database-connectivity-issues.md) sectie en Hallo best practices en richtlijnen op [overzicht voor ontwikkelaars van SQL Database](sql-database-develop-overview.md) voor meer informatie en algemene probeer strategieën. Ga vervolgens naar codevoorbeelden op [Verbindingsbibliotheken voor SQL-Database en SQL Server](sql-database-libraries.md) voor details.
3. Als een database limieten voor de nadert, lijkt het alsof toobe een tijdelijk verbindingsprobleem. Zie [het oplossen van prestatieproblemen](sql-database-troubleshoot-performance.md).
4. Een aanvraag voor de ondersteuning van Azure als connectiviteitsproblemen gaan, of als hello duur waarvoor uw toepassing hello-fout optreedt 60 seconden overschrijdt of als u meerdere exemplaren van Hallo fout in een bepaalde dag ziet, het bestand door het selecteren van **ophalenondersteunen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors"></a>Permanente fouten oplossen
Als de toepassing hello permanent tooconnect tooAzure SQL-Database mislukt, dit geeft meestal aan dat een probleem met een van de volgende Hallo:

* Firewall-configuratie. Hello Azure SQL database of de client firewall blokkeert verbindingen tooAzure SQL-Database.
* Nieuwe configuratie aan clientzijde Hallo netwerk: bijvoorbeeld een nieuw IP-adres of een proxyserver.
* Gebruikersfout: bijvoorbeeld verbindingsparameters, zoals Hallo-servernaam in de verbindingsreeks Hallo een typefout gemaakt.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Stappen tooresolve permanente verbindingsproblemen
1. Instellen van [firewall-regels](sql-database-configure-firewall-settings.md) tooallow Hallo client-IP-adres. Voor tijdelijke voor testdoeleinden, stelt u een firewallregel 0.0.0.0 als Hallo starten van IP-adresbereik en 255.255.255.255 gebruiken als Hallo eind-IP-adresbereik gebruiken. Hiermee opent u Hallo tooall IP-adressen. Als dit het connectiviteitsprobleem is opgelost, verwijdert u deze regel en een firewallregel voor een op de juiste wijze beperkt IP-adres of -adresbereik maken. 
2. Zorg dat de poort 1433 geopend voor uitgaande verbindingen is op alle firewalls tussen Hallo-client en Hallo Internet. Bekijk [Hallo Windows Firewall tooAllow toegang tot de SQL-Server configureren](https://msdn.microsoft.com/library/cc646023.aspx) en [hybride identiteit nodig poorten en protocollen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) voor aanvullende verwijzingen verwante tooadditional poorten die u moet tooopen voor Azure Active Directory-verificatie.
3. Controleer of de verbindingsreeks en andere instellingen. Zie sectie van de verbindingsreeks in Hallo Hallo [connectiviteit problemen onderwerp](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Controleer de servicestatus van de in Hallo-dashboard. Als u denkt dat er is een regionale uitval, Zie [herstellen van een storing](sql-database-disaster-recovery.md) voor stappen toorecover tooa nieuwe regio.

## <a name="next-steps"></a>Volgende stappen
* [Prestatieproblemen Azure SQL Database oplossen](sql-database-troubleshoot-performance.md)
* [Hallo-documentatie op Microsoft Azure Search](http://azure.microsoft.com/search/documentation/)
* [Weergave Hallo updates meest recente toohello Azure SQL Database-service](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Aanvullende bronnen
* [Overzicht van SQL Database-ontwikkeling](sql-database-develop-overview.md)
* [Algemene richtlijnen voor tijdelijke afhandeling van fouten](../best-practices-retry-general.md)
* [Verbindingsbibliotheken voor SQL-Database en SQL Server](sql-database-libraries.md)

