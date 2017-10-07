---
title: aaaTroubleshooting Azure SQL Data Warehouse | Microsoft Docs
description: Het oplossen van Azure SQL datawarehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Het oplossen van Azure SQL datawarehouse
Dit onderwerp worden enkele van Hallo meer veelvoorkomende vragen we graag van onze klanten.

## <a name="connecting"></a>Verbinding maken
| Probleem | Oplossing |
|:--- |:--- |
| Aanmelden is mislukt voor gebruiker 'NT AUTHORITY\ANONYMOUS aanmelden'. (Microsoft SQL Server, fout: 18456) |Deze fout treedt op wanneer een gebruiker met AAD tooconnect toohello hoofddatabase probeert, maar geen een gebruiker in master heeft.  Dit probleem opgeven toocorrect Hallo SQL Data Warehouse u wenst dat tooconnect tooat verbindingstijd of Hallo gebruiker toohello hoofddatabase toevoegen.  Zie [beveiligingsoverzicht] [ Security overview] artikel voor meer informatie. |
| Hallo server principal 'gebruik met Windows' geen is kunnen tooaccess Hallo 'master'-database in de huidige beveiligingscontext Hallo. Kan de standaarddatabase van de gebruiker niet openen. Aanmelden is mislukt. Aanmelden is mislukt voor gebruiker 'gebruik met Windows'. (Microsoft SQL Server, fout: 916) |Deze fout treedt op wanneer een gebruiker met AAD tooconnect toohello hoofddatabase probeert, maar geen een gebruiker in master heeft.  Dit probleem opgeven toocorrect Hallo SQL Data Warehouse u wenst dat tooconnect tooat verbindingstijd of Hallo gebruiker toohello hoofddatabase toevoegen.  Zie [beveiligingsoverzicht] [ Security overview] artikel voor meer informatie. |
| CTAIP fout |Deze fout kan optreden wanneer een aanmelding is gemaakt op Hallo SQL server-hoofddatabase, maar niet in Hallo SQL Data Warehouse-database.  Als u deze fout tegenkomt, bekijk Hallo [beveiligingsoverzicht] [ Security overview] artikel.  Dit artikel wordt uitgelegd hoe toocreate een gebruikersnaam en een gebruiker maken op de master en hoe toocreate een gebruiker in Hallo SQL datawarehouse-database. |
| Geblokkeerd door een Firewall |Azure SQL-databases worden beveiligd door de server en database niveau firewalls tooensure alleen bekende IP-adressen toegang tooa database hebben. Hallo firewalls zijn beveiligd door standaard, wat betekent dat moet u expliciet inschakelen en IP-adres of een bereik aan adressen dat voordat u verbinding kunt maken.  tooconfigure uw firewall om toegang te krijgen, stappen Hallo in [servertoegang firewall configureren voor uw client-IP-] [ Configure server firewall access for your client IP] in Hallo [inrichting instructies] [Provisioning instructions]. |
| Kan geen verbinding maken met het hulpprogramma of het stuurprogramma |SQL Data Warehouse raadt het gebruik van [SSMS][SSMS], [SSDT voor Visual Studio][SSDT for Visual Studio], of [sqlcmd] [ sqlcmd] tooquery uw gegevens. Zie voor meer informatie over stuurprogramma's en verbindende tooSQL Data Warehouse [stuurprogramma's voor Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] en [verbinding maken met SQL Data Warehouse tooAzure] [ Connect tooAzure SQL Data Warehouse] artikelen. |

## <a name="tools"></a>Hulpprogramma's
| Probleem | Oplossing |
|:--- |:--- |
| Visual Studio-Objectverkenner ontbreekt AAD-gebruikers |Dit is een bekend probleem.  Als tijdelijke oplossing weergeven Hallo gebruikers in [sys.database_principals][sys.database_principals].  Zie [verificatie tooAzure SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn meer over het gebruik van Azure Active Directory met SQL Data Warehouse. |
|Handmatig uitvoeren van scripts, Hallo scripting wizard te gebruiken of verbinding maakt via SSMS is traag, vastgelopen of produceren fouten| Zorg dat gebruikers in de hoofddatabase Hallo zijn gemaakt. In scriptopties, ook voor zorgen dat Hallo-engine-editie is ingesteld als 'Microsoft Azure SQL Data Warehouse Edition' en engine-type is 'Microsoft Azure SQL Database'.|

## <a name="performance"></a>Prestaties
| Probleem | Oplossing |
|:--- |:--- |
| Query-prestaties probleemoplossing |Als u een bepaalde query tootroubleshoot probeert, beginnen met een [leren hoe toomonitor uw query's][Learning how toomonitor your queries]. |
| Slechte queryprestaties en planningen is vaak een resultaat van ontbrekende statistieken |Hallo meest voorkomende oorzaak van slechte prestaties is een gebrek aan statistics voor tabellen.  Zie [tabelstatistieken onderhouden] [ Statistics] voor meer informatie over het toocreate statistieken en waarom ze essentieel tooyour prestaties zijn. |
| Lage gelijktijdigheid / query's in de wachtrij |Informatie over [werkbelasting management] [ Workload management] is hoe belangrijk in volgorde toounderstand toobalance geheugentoewijzing met gelijktijdigheid van taken. |
| Hoe tooimplement aanbevolen procedures |Hallo beste queryprestaties van plaats toostart toolearn manieren tooimprove is [aanbevolen procedures voor SQL Data Warehouse] [ SQL Data Warehouse best practices] artikel. |
| Hoe tooimprove prestaties met schalen |Hallo oplossing tooimproving prestaties is soms toosimply toevoegen meer power tooyour query's door compute [schalen van uw SQL Data Warehouse][Scaling your SQL Data Warehouse]. |
| Slechte queryprestaties als gevolg van slechte index kwaliteit |Enkele voorbeelden van momenten query's kunnen vertraging vanwege [slechte columnstore-index kwaliteit][Poor columnstore index quality].  Raadpleeg dit artikel voor meer informatie en hoe te[opnieuw geïndexeerd tooimprove segment kwaliteit][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Systeembeheer
| Probleem | Oplossing |
|:--- |:--- |
| Bericht 40847: Kan Hallo-bewerking niet uitvoeren omdat server Hallo toegestaan Database Transaction Unit quotum van 45000 zou overschrijden. |Verlaag Hallo [DWU] [ DWU] van Hallo database probeert u toocreate of [aanvragen van een verhoging van het quotum][request a quota increase]. |
| Ruimtegebruik onderzoeken |Zie [tabel grootten] [ Table sizes] toounderstand Hallo ruimtegebruik van uw systeem. |
| Het beheer van tabellen |Zie Hallo [tabel overzicht] [ Overview] artikel voor meer informatie over het beheren van uw tabellen.  In dit artikel bevat ook koppelingen naar meer gedetailleerde onderwerpen zoals [tabel gegevenstypen][Data types], [distribueren van een tabel][Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel][Partition], [tabelstatistieken onderhouden] [ Statistics] en [tijdelijke tabellen][Temporary]. |
|Transparent data encryption (TDE) voortgangsbalk wordt niet bijgewerkt in hello Azure Portal|U kunt Hallo weergavestatus van TDE via [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>PolyBase
| Probleem | Oplossing |
|:--- |:--- |
| Laden is mislukt vanwege de grote rijen |Ondersteuning voor grote rij is momenteel niet beschikbaar voor Polybase.  Dit betekent dat als de tabel VARCHAR(MAX), NVARCHAR(MAX) of VARBINARY(MAX) bevat, externe tabellen kunnen niet worden gebruikt tooload uw gegevens.  Belasting voor grote rijen is momenteel alleen ondersteund door Azure Data Factory (met BCP), Azure Stream Analytics, SSIS, BCP of Hallo SQLBulkCopy .NET-klasse. PolyBase-ondersteuning voor grote rijen wordt in een toekomstige release toegevoegd. |
| BCP belasting van de tabel met maximale-gegevenstype is mislukt |Er is een bekend probleem dat is vereist dat VARCHAR(MAX), NVARCHAR(MAX) of VARBINARY(MAX) achter Hallo Hallo-tabel in bepaalde scenario's worden geplaatst.  Verplaats het end van uw MAX kolommen toohello van Hallo tabel. |

## <a name="differences-from-sql-database"></a>Verschillen met SQL-Database
| Probleem | Oplossing |
|:--- |:--- |
| Niet-ondersteunde functies van de SQL-Database |Zie [niet-ondersteunde tabelfuncties][Unsupported table features]. |
| Niet-ondersteunde gegevenstypen van de SQL-Database |Zie [niet-ondersteunde gegevenstypen][Unsupported data types]. |
| VERWIJDEREN en beperkingen van de UPDATE |Zie [UPDATE tijdelijke oplossingen][UPDATE workarounds], [verwijderen tijdelijke oplossingen] [ DELETE workarounds] en [toowork CTAS met behulp van niet-ondersteunde update en DELETE syntaxis][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| MERGE-instructie wordt niet ondersteund. |Zie [samenvoegen tijdelijke oplossingen][MERGE workarounds]. |
| Beperkingen van de opgeslagen procedure |Zie [opgeslagen procedure beperkingen] [ Stored procedure limitations] toounderstand aantal Hallo beperkingen van opgeslagen procedures. |
| UDF's bieden geen ondersteuning voor SELECT-instructies |Dit is een beperking van onze UDF's.  Zie [CREATE FUNCTION] [ CREATE FUNCTION] Hallo-syntaxis wordt ondersteund. |

## <a name="next-steps"></a>Volgende stappen
Als u zijn toofind niet kan een probleem met de oplossing tooyour hierboven Hier volgen enkele andere resources die u kunt proberen.

* [Blogs]
* [Functieverzoeken]
* [Video's]
* [CAT-teamblogs]
* [Ondersteuningsticket maken]
* [MSDN-forum]
* [Stack Overflow-forum]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Ondersteuningsticket maken]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[CAT-teamblogs]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Functieverzoeken]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN-forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Stack Overflow-forum]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Video's]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
