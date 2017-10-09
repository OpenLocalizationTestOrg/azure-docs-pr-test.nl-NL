---
title: onderwerpen over aaaAll voor de service SQL Data Warehouse | Microsoft Docs
description: Tabel met alle onderwerpen voor hello Azure-service de naam van SQL Data Warehouse die aanwezig zijn op http://azure.microsoft.com/documentation/articles/, titel en beschrijving.
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Alle onderwerpen voor Azure SQL Data Warehouse-service
Dit onderwerp vindt u elk onderwerp die van toepassing rechtstreeks toohello is **SQL Data Warehouse** service van Azure. U kunt deze webpagina voor trefwoorden zoeken met behulp van **Ctrl + F**, toofind Hallo onderwerpen van huidige belang.

## <a name="new"></a>Nieuw
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 1 |[Back-ups van SQL Data Warehouse](sql-data-warehouse-backups.md) |Meer informatie over SQL Data Warehouse ingebouwde databaseback-ups die u in staat toorestore stellen een herstelpunt voor Azure SQL Data Warehouse tooa of een andere geografische regio. |

## <a name="updated-articles-sql-data-warehouse"></a>Bijgewerkte artikelen, SQL Data Warehouse
Deze sectie vindt u artikelen die onlangs zijn bijgewerkt, waarin Hallo bijwerken is groot of belangrijke. Voor elk bijgewerkte artikel toegevoegd een ruwe codefragment Hallo markdown-tekst wordt weergegeven. Hallo artikelen zijn bijgewerkt binnen de datumbereik Hallo van **2016-08-22** te**2016-10-05**.

| &nbsp; | Artikel | Bijgewerkte tekst, codefragment | Wanneer bijgewerkt |
| ---:|:--- |:--- |:--- |
| 2 |[Gegevens uit Azure blob-opslag laden in SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |/ tootrack bytes en bestanden selecteren r.command, s.request_id, r.status, count (afzonderlijke input_name) als nbr_files, som (s.bytes_processed) / 1024/1024 als gb_processed van sys.dm_pdw_exec_requests r inner join sys.dm_pdw_dms_external_work s op r.request_id s.request_id = waar r. label = ' CTAS: Load cso. DimProduct ' of r. label = ' CTAS: Load cso. De FactOnlineSales GROUP BY r.command, s.request_id, r.status ORDER BY nbr_files desc, gb_processed desc; |2016-09-07 |
| 3 |[SQL Data Warehouse terugzetten](sql-data-warehouse-restore-database-overview.md) |** Kan ik een onderbroken datawarehouse terugzetten? ** toorestore een datawarehouse die is onderbroken, moet u toofirst weer online brengen. Nadat het Hallo-datawarehouse weer online is, hebt u zeven dagen van terugzetten punten toochoose uit. ** Herstellen tooa geografisch redundante regio ** als u Hallo geografisch redundante opslag gebruikt, kunt u herstellen Hallo datawarehouse tooyour gekoppeld datacenter in een andere geografische regio. Hallo-datawarehouse wordt teruggezet vanuit Hallo laatste dagelijkse back-up. ** Herstellen tijdlijn ** kunt u een database tooany herstelpunt binnen Hallo afgelopen zeven dagen herstellen. Momentopnamen elke vier uur voor tooeight start en zijn beschikbaar voor de zeven dagen. Wanneer een momentopname ouder dan zeven dagen is, het verloopt en het herstelpunt is niet meer beschikbaar. ** Herstellen kosten ** Hallo opslag kosten voor het datawarehouse Hallo hersteld snelheid hello Azure Premium-opslag wordt gefactureerd. Als u een herstelde datawarehouse onderbreekt, wordt u in rekening gebracht voor opslag snelheid hello Azure Premium-opslag. Hallo voordeel van het onderbreken is dat u niet bent kosten |2016-09-29 |

## <a name="get-started"></a>Aan de slag
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 4 |[Verificatie tooAzure SQL Data Warehouse](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) en SQL Server-verificatie tooAzure SQL Data Warehouse. |
| 5 |[Aanbevolen procedures voor Azure SQL Data Warehouse](sql-data-warehouse-best-practices.md) |Aanbevelingen en aanbevolen procedures voor het ontwikkelen van oplossingen voor Azure SQL Data Warehouse. Deze helpen u goede resultaten te bereiken. |
| 6 |[Stuurprogramma's voor Azure SQL datawarehouse](sql-data-warehouse-connection-strings.md) |Verbindingsreeksen en stuurprogramma's voor SQL Data Warehouse |
| 7 |[Verbinding maken met SQL Data Warehouse tooAzure](sql-data-warehouse-connect-overview.md) |Hoe toofind Hallo-servernaam en verbinding met de tekenreeks van uw tooAzure SQL Data Warehouse |
| 8 |[Gegevens analyseren met Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Gebruik toobuild Azure Machine Learning een Voorspellend machine learning-model op basis van gegevens die zijn opgeslagen in Azure SQL Data Warehouse. |
| 9 |[Query uitvoeren op Azure SQL Data Warehouse (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Azure SQL Data Warehouse met Hallo sqlcmd-opdrachtregelprogramma opvragen. |
| 10 |[Een SQL Data Warehouse-database maken met behulp van Transact-SQL (TSQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Meer informatie over hoe toocreate een Azure SQL Data Warehouse met TSQL |
| 11 |[Hoe toocreate een ondersteuning voor SQL Data Warehouse-ticket](sql-data-warehouse-get-started-create-support-ticket.md) |Hoe ticket toocreate een ondersteuningsaanvraag in Azure SQL Data Warehouse. |
| 12 |[Gegevens laden met Azure Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Meer informatie over tooload gegevens met Azure Data Factory |
| 13 |[Gegevens laden met PolyBase in SQL Data Warehouse](sql-data-warehouse-get-started-load-with-polybase.md) |Meer informatie over wat PolyBase is en hoe toouse voor datawarehousescenario's. |
| 14 |[Een Azure SQL datawarehouse maken](sql-data-warehouse-get-started-provision.md) |Meer informatie over hoe toocreate een Azure SQL Data Warehouse in hello Azure-portal |
| 15 |[SQL Data Warehouse met behulp van PowerShell maken](sql-data-warehouse-get-started-provision-powershell.md) |SQL Data Warehouse maken met Powershell |
| 16 |[Gegevens visualiseren met Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |SQL Data Warehouse-gegevens visualiseren met Power BI |
| 17 |[Query’s uitvoeren bij Azure SQL Data Warehouse (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Query’s uitvoeren bij SQL Data Warehouse met Visual Studio. |

## <a name="develop"></a>Ontwikkelen
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 18 |[Optimaliseren van transacties voor SQL Data Warehouse](sql-data-warehouse-develop-best-practices-transactions.md) |Aanbevolen procedurerichtlijn over het schrijven van efficiënte transactie-updates in Azure SQL Data Warehouse |
| 19 |[Beheer van gelijktijdigheid van taken en de belasting in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md) |Begrijpen en de belasting van gelijktijdigheid management in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 20 |[Table As Select (CTAS) in SQL datawarehouse maken](sql-data-warehouse-develop-ctas.md) |Tips voor het coderen van Hello maken tabel selecteert u de instructie (CTAS) in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 21 |[Dynamische SQL in SQL datawarehouse](sql-data-warehouse-develop-dynamic-sql.md) |Tips voor het gebruik van dynamische SQL in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 22 |[Groeperen op opties in SQL Data Warehouse](sql-data-warehouse-develop-group-by-options.md) |Tips voor het implementeren van de groep door de opties in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 23 |[Labels tooinstrument query's in SQL Data Warehouse gebruiken](sql-data-warehouse-develop-label.md) |Tips voor het gebruik van labels tooinstrument query's in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 24 |[Lussen in SQL datawarehouse](sql-data-warehouse-develop-loops.md) |Tips voor de Transact-SQL-lussen en vervang cursors in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 25 |[Opgeslagen procedures in SQL Data Warehouse](sql-data-warehouse-develop-stored-procedures.md) |Tips voor het implementeren van opgeslagen procedures in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 26 |[Transacties in SQL datawarehouse](sql-data-warehouse-develop-transactions.md) |Tips voor het implementeren van transacties in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 27 |[Gebruiker gedefinieerde schema's in SQL Data Warehouse](sql-data-warehouse-develop-user-defined-schemas.md) |Tips voor het gebruik van Transact-SQL-schema's in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 28 |[Variabelen in SQL Data Warehouse toewijzen](sql-data-warehouse-develop-variable-assignment.md) |Tips voor het toewijzen van Transact-SQL-variabelen in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 29 |[Weergaven in SQL datawarehouse](sql-data-warehouse-develop-views.md) |Tips voor het gebruik van Transact-SQL-weergaven in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 30 |[Ontwerpbeslissingen en codering technieken voor SQL Data Warehouse](sql-data-warehouse-overview-develop.md) |Concepten voor ontwikkeling, ontwerpbeslissingen, aanbevelingen en codering technieken voor SQL Data Warehouse. |

## <a name="manage"></a>Beheren
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 31 |[De rekencapaciteit in Azure SQL Data Warehouse (overzicht) beheren](sql-data-warehouse-manage-compute-overview.md) |Prestaties scale-out mogelijkheden in Azure SQL Data Warehouse. Uitbreiden door dwu's aan te passen of onderbreken en hervatten van compute resources toosave kosten. |
| 32 |[Beheren van de rekencapaciteit in Azure SQL Data Warehouse (Azure-portal)](sql-data-warehouse-manage-compute-portal.md) |Azure portal taken toomanage rekenkracht. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten compute-bronnen toosave kosten. |
| 33 |[De rekencapaciteit in Azure SQL Data Warehouse (PowerShell) beheren](sql-data-warehouse-manage-compute-powershell.md) |PowerShell taken toomanage rekenkracht. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten compute-bronnen toosave kosten. |
| 34 |[Rekencapaciteit in Azure SQL Data Warehouse (REST) beheren](sql-data-warehouse-manage-compute-rest-api.md) |PowerShell taken toomanage rekenkracht. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten compute-bronnen toosave kosten. |
| 35 |[Beheren van de rekencapaciteit in Azure SQL Data Warehouse (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) taken tooscale-out-prestaties door dwu's aan te passen. Kosten besparen door te schalen tijdens de niet-piekuren. |
| 36 |[Uw workload controleren met DMV's](sql-data-warehouse-manage-monitor.md) |Meer informatie over hoe toomonitor uw werkbelasting via DMV's. |
| 37 |[Databases in Azure SQL Data Warehouse beheren](sql-data-warehouse-overview-manage.md) |Overzicht van het beheren van databases in SQL Data Warehouse. Beheerhulpprogramma's voor dwu's en scale-out-prestaties queryprestaties tot stand brengen van goede beveiligingsbeleid en het herstellen van een database van beschadigde gegevens of van een regionale uitval probleemoplossing bevat. |
| 38 |[Monitor gebruiker query's in Azure SQL Data Warehouse](sql-data-warehouse-overview-manage-user-queries.md) |Overzicht van Hallo overwegingen, best practices en taken voor het controleren van de gebruiker query's in Azure SQL Data Warehouse |
| 39 |[SQL Data Warehouse terugzetten](sql-data-warehouse-restore-database-overview.md) |Overzicht van opties voor Hallo database terugzetten voor het herstellen van een database in Azure SQL Data Warehouse. |
| 40 |[Herstellen van een Azure SQL datawarehouse (Portal)](sql-data-warehouse-restore-database-portal.md) |Azure portal taken voor het herstellen van een Azure SQL Data Warehouse. |
| 41 |[Herstellen van een Azure SQL datawarehouse (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |PowerShell-taken voor het herstellen van een Azure SQL Data Warehouse. |
| 42 |[Herstellen van een Azure SQL datawarehouse (REST-API)](sql-data-warehouse-restore-database-rest-api.md) |REST-API-taken voor het herstellen van een Azure SQL Data Warehouse. |

## <a name="tables-and-indexes"></a>Tabellen en indexen
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 43 |[Gegevenstypen voor tabellen in SQL Data Warehouse](sql-data-warehouse-tables-data-types.md) |Aan de slag met gegevenstypen voor Azure SQL Data Warehouse-tabellen. |
| 44 |[Distributie van tabellen in SQL Data Warehouse](sql-data-warehouse-tables-distribute.md) |Aan de slag met het distribueren van tabellen in Azure SQL Data Warehouse. |
| 45 |[Indexeren van tabellen in SQL Data Warehouse](sql-data-warehouse-tables-index.md) |Aan de slag met de tabel in Azure SQL Data Warehouse te indexeren. |
| 46 |[Overzicht van tabellen in SQL Data Warehouse](sql-data-warehouse-tables-overview.md) |Aan de slag met Azure SQL Data Warehouse-tabellen. |
| 47 |[Tabellen in SQL Data Warehouse partitioneren](sql-data-warehouse-tables-partition.md) |Aan de slag met Tabelpartities in Azure SQL Data Warehouse. |
| 48 |[Het beheren van statistieken over tabellen in SQL Data Warehouse](sql-data-warehouse-tables-statistics.md) |Aan de slag met statistieken over tabellen in Azure SQL Data Warehouse. |
| 49 |[Tijdelijke tabellen in SQL Data Warehouse](sql-data-warehouse-tables-temporary.md) |Aan de slag met tijdelijke tabellen in Azure SQL Data Warehouse. |

## <a name="integrate"></a>Integreren
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 50 |[Azure Data Factory gebruiken met SQL datawarehouse](sql-data-warehouse-integrate-azure-data-factory.md) |Tips voor het gebruik van Azure Data Factory (ADF) met Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 51 |[Gebruik Azure Machine Learning met SQL datawarehouse](sql-data-warehouse-integrate-azure-machine-learning.md) |Zelfstudie voor het gebruik van Azure Machine Learning met Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 52 |[Azure Stream Analytics gebruiken met SQL datawarehouse](sql-data-warehouse-integrate-azure-stream-analytics.md) |Tips voor het gebruik van Azure Stream Analytics met Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 53 |[Power BI gebruiken met SQL datawarehouse](sql-data-warehouse-integrate-power-bi.md) |Tips voor het gebruik van Power BI met Azure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 54 |[Gebruikmaken van andere services met SQL Data Warehouse](sql-data-warehouse-overview-integrate.md) |Hulpprogramma's en partners met oplossingen die zijn geïntegreerd met SQL Data Warehouse. |

## <a name="load"></a>Belasting
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 55 |[Gegevens uit Azure blob-opslag laden in Azure SQL Data Warehouse (Azure Data Factory)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Meer informatie over tooload gegevens met Azure Data Factory |
| 56 |[Gegevens uit Azure blob-opslag laden in SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Meer informatie over hoe toouse PolyBase tooload gegevens van Azure blob-opslag in SQL Data Warehouse. Enkele tabellen uit openbare gegevens laden in Hallo Contoso Retail Data Warehouse-schema. |
| 57 |[Gegevens uit SQL Server laden in Azure SQL Data Warehouse (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Gebruikt bcp tooexport gegevens uit SQL Server tooflat bestanden, AZCopy tooimport gegevens tooAzure blob storage en PolyBase tooingest Hallo gegevens in Azure SQL Data Warehouse. |
| 58 |[Gegevens uit SQL Server laden in Azure SQL Data Warehouse (platte bestanden)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Voor kleine gegevenssets gebruikt bcp tooexport gegevens uit SQL Server tooflat bestanden en importeren Hallo rechtstreeks in Azure SQL Data Warehouse. |
| 59 |[Laden van gegevens uit SQL Server in Azure SQL Data Warehouse (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Ziet u hoe toocreate SQL Server Integration Services (SSIS) toomove pakketgegevens uit een scala aan gegevensbronnen tooSQL Data Warehouse. |
| 60 |[Gegevens laden met PolyBase in SQL Data Warehouse](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Gebruikt bcp tooexport gegevens uit SQL Server tooflat bestanden, AZCopy tooimport gegevens tooAzure blob storage en PolyBase tooingest Hallo gegevens in Azure SQL Data Warehouse. |
| 61 |[Handleiding voor het gebruik van PolyBase in SQL Data Warehouse](sql-data-warehouse-load-polybase-guide.md) |Richtlijnen en aanbevelingen voor het gebruik van PolyBase in SQL Data Warehouse-scenario's. |
| 62 |[Voorbeeldgegevens laden in SQL Data Warehouse](sql-data-warehouse-load-sample-databases.md) |Voorbeeldgegevens laden in SQL Data Warehouse |
| 63 |[Gegevens laden met bcp](sql-data-warehouse-load-with-bcp.md) |Meer informatie over welke BCP en hoe toouse voor datawarehousescenario's. |
| 64 |[Load data into Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) (Gegevens laden in Azure SQL Data Warehouse) |Meer informatie over Hallo algemene scenario's om gegevens te laden in SQL Data Warehouse. Deze omvatten het gebruik van PolyBase, Azure blob-opslag, platte bestanden en back-ups van schijf. U kunt ook hulpprogramma's van derden gebruiken. |

## <a name="migrate"></a>Migreren
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 65 |[Uw code tooSQL voor SQL Data Warehouse migreren](sql-data-warehouse-migrate-code.md) |Tips voor het migreren van uw SQL-code tooAzure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 66 |[Uw gegevens migreren](sql-data-warehouse-migrate-data.md) |Tips voor het migreren van uw gegevens tooAzure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 67 |[Datawarehouse migratiehulpprogramma (Preview)](sql-data-warehouse-migrate-migration-utility.md) |TooSQL Data Warehouse migreren. |
| 68 |[Uw schema tooSQL Data Warehouse migreren](sql-data-warehouse-migrate-schema.md) |Tips voor het migreren van uw schema tooAzure SQL Data Warehouse om oplossingen te ontwikkelen. |
| 69 |[Uw oplossing tooSQL Data Warehouse migreren](sql-data-warehouse-overview-migrate.md) |Migratie-instructies voor uw oplossing tooAzure SQL Data Warehouse-platform te brengen. |

## <a name="partners"></a>Partners
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 70 |[SQL Data Warehouse business intelligence-partners](sql-data-warehouse-partner-business-intelligence.md) |Lijsten van derden business intelligence partners met oplossingen die ondersteuning bieden voor SQL Data Warehouse. |
| 71 |[SQL Data Warehouse gegevens integratiepartners](sql-data-warehouse-partner-data-integration.md) |Lijsten met partners van derden met oplossingen voor integratie die ondersteuning bieden voor Azure SQL Data Warehouse. |
| 72 |[SQL Data Warehouse data management partners](sql-data-warehouse-partner-data-management.md) |Lijsten met gegevens van derden management partners met oplossingen die ondersteuning bieden voor SQL Data Warehouse. |

## <a name="reference"></a>Naslaginformatie
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 73 |[Naslaginformatie voor SQL Data Warehouse](sql-data-warehouse-overview-reference.md) |Inhoud koppelingen met naslaginformatie voor SQL Data Warehouse. |
| 74 |[PowerShell-cmdlets en REST-API's voor SQL Data Warehouse](sql-data-warehouse-reference-powershell-cmdlets.md) |Hallo bovenste PowerShell-cmdlets voor Azure SQL Data Warehouse vinden met inbegrip van hoe toopause en hervatten van een database. |
| 75 |[Elementen van de taal](sql-data-warehouse-reference-tsql-language-elements.md) |Lijst met koppelingen tooreference inhoud voor Hallo Transact-SQL elementen van de taal gebruikt voor SQL Data Warehouse. |
| 76 |[Transact-SQL-onderwerpen](sql-data-warehouse-reference-tsql-statements.md) |Koppelingen tooreference inhoud voor Hallo Transact-SQL-onderwerpen die worden gebruikt door SQL Data Warehouse. |
| 77 |[Systeemweergaven](sql-data-warehouse-reference-tsql-system-views.md) |Koppelingen toosystem weergaven inhoud voor SQL Data Warehouse. |

## <a name="security"></a>Beveiliging
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 78 |[Ondersteuning voor SQL datawarehouse - Downlevel-clients voor controle en dynamische Gegevensmaskering](sql-data-warehouse-auditing-downlevel-clients.md) |Meer informatie over SQL Data Warehouse-ondersteuning voor downlevel-clients voor het controleren van gegevens |
| 79 |[Controle van Azure SQL datawarehouse](sql-data-warehouse-auditing-overview.md) |Aan de slag met Azure SQL Data Warehouse controle |
| 80 |[Aan de slag met Transparent Data Encryption (TDE) in SQL Data Warehouse](sql-data-warehouse-encryption-tde.md) |Transparante gegevensversleuteling (TDE) in SQL datawarehouse |
| 81 |[Aan de slag met Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Transparante gegevensversleuteling (TDE) in SQL datawarehouse (T-SQL) |
| 82 |[Een database in SQL Data Warehouse beveiligen](sql-data-warehouse-overview-manage-security.md) |Tips voor het beveiligen van een database in Azure SQL Data Warehouse om oplossingen te ontwikkelen. |

## <a name="miscellaneous"></a>Diversen
| &nbsp; | Titel | Beschrijving |
| ---:|:--- |:--- |
| 83 |[Visual Studio en SSDT voor SQL datawarehouse installeren](sql-data-warehouse-install-visual-studio.md) |Visual Studio en SQL Server Development Tools (SSDT) voor Azure SQL Data Warehouse installeren |
| 84 |[Migratie tooPremium opslaggroep](sql-data-warehouse-migrate-to-premium-storage.md) |Instructies voor het migreren van een bestaande SQL Data Warehouse toopremium opslag |
| 85 |[Aan de slag met detectie van dreigingen](sql-data-warehouse-security-threat-detection.md) |Hoe tooget de slag met detectie van dreigingen |
| 86 |[SQL Data Warehouse Capaciteitslimieten](sql-data-warehouse-service-capacity-limits.md) |Maximale waarden voor verbindingen, databases, tabellen en query's voor SQL Data Warehouse. |
| 87 |[Het oplossen van Azure SQL datawarehouse](sql-data-warehouse-troubleshoot.md) |Het oplossen van Azure SQL datawarehouse. |

