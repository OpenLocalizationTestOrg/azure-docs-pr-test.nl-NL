---
title: aaaHow tooconnect toodata bronnen | Microsoft Docs
description: Hoe-tooarticle hoe tooconnect toodata bronnen gedetecteerd met Azure Data Catalog is gemarkeerd.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Hoe tooconnect toodata bronnen
## <a name="introduction"></a>Inleiding
**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert. Met andere woorden, **Azure Data Catalog** wordt alle informatie over mensen helpen detecteren, begrijpen en gebruiken van gegevensbronnen en helpt organisaties tooget meer waarde van hun bestaande gegevens. Een belangrijk aspect van dit scenario Hallo gegevensbron – wanneer een gebruiker een gegevens detecteert en begrijpt van het doel gebruikt, kan de volgende stap Hallo is tooconnect toohello gegevensbron tooput de toouse gegevens.

## <a name="data-source-locations"></a>Gegevensbronlocaties
Tijdens de registratie van gegevensbron, **Azure Data Catalog** ontvangt de metagegevens over Hallo-gegevensbron. Deze metagegevens bevat Hallo details van de locatie Hallo van de gegevensbron. Hallo-details van Hallo-locatie van gegevensbron bron toodata verschilt, maar bevat altijd tooconnect van Hallo informatie die nodig is. Bijvoorbeeld, Hallo voor een tabel met SQL Server omvat ook Hallo-servernaam, databasenaam, de naam van schema en tabelnaam, terwijl het Hallo-locatie voor een SQL Server Reporting Services-rapport bevat Hallo-servernaam en Hallo pad toohello rapport. Andere typen gegevensbronnen hebben locaties die overeenkomen met Hallo structuur en mogelijkheden van het bronsysteem Hallo.

## <a name="integrated-client-tools"></a>Geïntegreerde clienthulpprogramma 's
Hallo eenvoudigste manier tooconnect tooa gegevensbron is toouse Hallo "openen in... ' menu in Hallo **Azure Data Catalog** portal. Dit menu geeft een lijst met opties voor het verbinden van de geselecteerde gegevensasset toohello weer.
Wanneer u de standaardweergave tegel hello, dit menu is beschikbaar op Hallo van elke tegel.

 ![Het openen van een SQL Server-tabel in Excel van Hallo gegevens asset tegel](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Wanneer u de lijstweergave hello, is Hallo menu beschikbaar in de zoekbalk Hallo Hallo boven aan het portalvenster Hallo.

 ![Openen van een SQL Server Reporting Services-rapport in Report Manager van Hallo zoekbalk](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Ondersteunde Client-toepassingen
Wanneer u Hallo "openen in... ' menu voor gegevens in Azure Data Catalog-portal Hallo gegevensbronnen, Hallo juiste client-toepassing moet worden geïnstalleerd op de clientcomputer Hallo.

| Open in de toepassing | Extensie / protocol | Versies van de ondersteunde toepassing |
| --- | --- | --- |
| Excel |.odc |Excel 2010 of hoger |
| Excel (Top 1000) |.odc |Excel 2010 of hoger |
| Power Query |.xlsx |Excel 2016 of Excel 2010 of Excel 2013 Hello Power Query voor Excel-invoegtoepassing geïnstalleerd |
| Power BI Desktop |pbix |Power BI Desktop juli 2016 of hoger |
| SQL Server Data Tools |vsweb: / / |Visual Studio 2013 Update 4 of hoger met SQL Server tooling geïnstalleerd |
| Rapportbeheer |http:// |Zie [Browservereisten voor het SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Uw gegevens, de hulpprogramma 's
Hallo-opties die beschikbaar zijn in het menu Hallo hangt Hallo-type van de geselecteerde gegevensasset. Natuurlijk niet alle mogelijke hulpprogramma's worden opgenomen in Hallo "openen in... ' menu, maar is nog steeds eenvoudig tooconnect toohello-gegevensbron met behulp van een clienthulpprogramma. Wanneer een gegevensasset is geselecteerd in Hallo **Azure Data Catalog** portal Hallo voltooid locatie wordt weergegeven in het eigenschappendeelvenster Hallo.

 ![Verbindingsgegevens voor een SQL Server-databasetabel](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

Hallo-verbindingsgegevens details zullen verschillen van type toodata bron gegevensbrontype, maar Hallo informatie is opgenomen in de portal Hallo krijgt u alles wat dat u moet tooconnect toohello gegevensbron in een clienthulpprogramma. Gebruikers kunnen kopiëren Hallo Verbindingsdetails voor Hallo gegevensbronnen die ze hebben gedetecteerd via **Azure Data Catalog**, waardoor ze toowork met Hallo-gegevens in een hulpprogramma naar keuze.

## <a name="connecting-and-data-source-permissions"></a>Verbinding maken en gegevens bron machtigingen
Hoewel **Azure Data Catalog** maakt gegevensbronnen kunnen worden gedetecteerd, toegang toohello gegevens zelf blijft onder het Hallo-beheer van Hallo data source-eigenaar of beheerder. Detectie van een gegevensbron in **Azure Data Catalog** geeft geen een gebruiker een gegevensbron van machtigingen tooaccess Hallo zelf.

toomake het gemakkelijker voor gebruikers die een data detecteren bron, maar hebben geen toestemming tooaccess gegevens, gebruikers kunnen bieden informatie in Hallo eigenschap toegang aanvragen bij de aantekeningen maken van een gegevensbron. Informatie die hier wordt beschreven, waaronder koppelingen toohello proces of contactpunt voor toegang tot de gegevensbron – wordt weergegeven naast Hallo locatie gegevensbroninformatie in Hallo-portal.

 ![Verbindingsgegevens met aanvraag toegang instructies](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Samenvatting
Registreren van een gegevensbron met **Azure Data Catalog** maakt die gegevens kunnen worden gedetecteerd door te kopiëren structurele en beschrijvende metagegevens uit de gegevensbron Hallo naar Hallo Catalog-service. Als een gegevensbron is geregistreerd en gedetecteerd, gebruikers verbinding kunnen maken toohello gegevensbron Hallo **Azure Data Catalog** portal "openen in..." " menu of met hun data tools van keuze.

## <a name="see-also"></a>Zie ook
* [Aan de slag met Azure Data Catalog](data-catalog-get-started.md) zelfstudie voor stapsgewijze informatie over het tooconnect toodata bronnen.
