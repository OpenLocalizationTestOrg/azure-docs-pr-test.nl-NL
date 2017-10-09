---
title: aaaData bronnen ondersteund in Azure Analysis Services | Microsoft Docs
description: Beschrijft de gegevensbronnen die worden ondersteund voor gegevensmodellen in Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Gegevensbronnen die worden ondersteund in Azure Analysis Services
Azure Analysis Services-servers die ondersteuning voor verbindende toodata bronnen in Hallo cloud en on-premises in uw organisatie. Extra ondersteunde gegevensbronnen worden alle Hallo tijd toegevoegd. Terugkomen vaak. 

Hallo volgende gegevensbronnen worden momenteel ondersteund:

| Cloud  |
|---|
| Azure Blob Storage *  |
| Azure SQL Database  |
| Azure datawarehouse |


| On-premises  |   |   |   |
|---|---|---|---|
| Access-Database  | Map * | Oracle Database  | Teradata Database |
| Active Directory *  | JSON-document *  | Postgre SQL Database *  |XML-tabel * |
| Analysis Services  | Regels uit binair *  | SAP HANA *  |
| Analytics Platform System  | MySQL-database  | SAP Business Warehouse *  | |
| Dynamics CRM *  | OData-Feed *  | SharePoint *  |
| Excel-werkmap  | ODBC-query  | SQL Database  |
| Exchange *  | OLE DB  | Sybase-Database  |

\*1400-modellen in tabelvorm alleen. 

> [!IMPORTANT]
> Verbinding maken met tooon-premises gegevens gegevensbronnen vereisen een [On-premises gegevensgateway](analysis-services-gateway.md) geïnstalleerd op een computer in uw omgeving.

## <a name="data-providers"></a>Gegevensproviders

Gegevensmodellen in Azure Analysis Services moet mogelijk verschillende gegevensproviders verbinding te maken met gegevensbronnen toocertain. In sommige gevallen mogelijk modellen in tabelvorm toodata bronnen systeemeigen providers zoals SQL Server Native Client (SQLNCLI11) met een fout geretourneerd.

Gegevensbron voor gegevensmodellen die verbinding maken met de cloudgegevens tooa zoals Azure SQL Database, als u native providers dan SQLOLEDB gebruikt, ziet u mogelijk foutbericht: **'hello provider 'SQLNCLI11.1' is niet geregistreerd.'** Of, als er een DirectQuery model verbindende tooon-premises gegevensbronnen, als u native providers u foutbericht weergegeven: **"Fout bij het maken van de OLE DB-rijenset. Onjuiste syntaxis bij 'LIMIET' '**.

Hallo na datasource-providers worden ondersteund voor in het geheugen of de DirectQuery-modellen voor gegevens wanneer verbindende toodata in Hallo cloud of on-premises gegevensbronnen:

### <a name="cloud"></a>Cloud
| **Gegevensbron** | **In het geheugen** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL Data Warehouse |.NET framework Data Provider voor SQL Server |.NET framework Data Provider voor SQL Server |
| Azure SQL Database |.NET framework Data Provider voor SQL Server |.NET framework Data Provider voor SQL Server | |

### <a name="on-premises-via-gateway"></a>On-premises (via de Gateway)
|**Gegevensbron** | **In het geheugen** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |.NET framework Data Provider voor SQL Server |
| SQL Server |Microsoft OLE DB-Provider voor SQL Server |.NET framework Data Provider voor SQL Server | |
| SQL Server |.NET framework Data Provider voor SQL Server |.NET framework Data Provider voor SQL Server | |
| Oracle |Microsoft OLE DB-Provider voor Oracle |Oracle-gegevensprovider voor .NET | |
| Oracle |Oracle-gegevensprovider voor .NET |Oracle-gegevensprovider voor .NET | |
| Teradata |OLE DB-Provider voor Teradata |Teradata-gegevensprovider voor .NET | |
| Teradata |Teradata-gegevensprovider voor .NET |Teradata-gegevensprovider voor .NET | |
| Analytics Platform System |.NET framework Data Provider voor SQL Server |.NET framework Data Provider voor SQL Server | |

> [!NOTE]
> Zorg ervoor dat op 64-bits providers zijn geïnstalleerd bij gebruik van On-premises gateway.
> 
> 

Wanneer een lokale SQL Server Analysis Services model in tabelvorm tooAzure Analysis Services wordt gemigreerd, kan het benodigde toochange Hallo provider zijn.

**toospecify een datasource-provider**

1. In SSDT > **Tabellaire Model Explorer** > **gegevensbronnen**, met de rechtermuisknop op een gegevensbronverbinding en klik vervolgens op **gegevensbron bewerken**.
2. In **verbinding bewerken**, klikt u op **Geavanceerd** tooopen Hallo geavanceerde eigenschappenvenster.
3. In **geavanceerde eigenschappen instellen** > **Providers**, en selecteer de juiste provider Hallo.

## <a name="impersonation"></a>Imitatie
In sommige gevallen kan het benodigde toospecify een andere imitatieaccount zijn. Imitatieaccount kan worden opgegeven in SSDT of SSMS.

Voor on-premises gegevensbronnen:

* Als SQL-verificatie wordt gebruikt, moet de imitatie-serviceaccount.
* Als Windows-verificatie wordt gebruikt, moet u Windows-gebruiker/wachtwoord instellen. Voor SQL Server, wordt Windows-verificatie met een specifieke imitatie-account alleen ondersteund voor modellen van gegevens in het geheugen.

Voor cloud-gegevensbronnen:

* Als SQL-verificatie wordt gebruikt, moet de imitatie-serviceaccount.

## <a name="next-steps"></a>Volgende stappen
Als u on-premises gegevensbronnen hebt, moet u ervoor dat tooinstall hello [On-premises gateway](analysis-services-gateway.md).   
toolearn meer informatie over het beheren van uw server in SSDT of SSMS, Zie [beheren van uw server](analysis-services-manage.md).

