---
title: aaaClient bibliotheken die vereist zijn voor het verbinden van tooAzure Analysis Services | Microsoft Docs
description: Beschrijft de clientbibliotheken vereist is voor client toepassingen en hulpprogramma's tooconnect Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Clientbibliotheken voor het verbinden van tooAzure Analysis Services

Clientbibliotheken zijn nodig voor client-toepassingen en hulpprogramma's tooconnect tooAnalysis Services-servers. 

Analyseservices gebruikmaken van drie clientbibliotheken. ADOMD.NET en Analysis Services Management Objects (AMO), zijn beheerde clientbibliotheken. Hallo Analysis Services OLE DB-provider (MSOLAP DLL) is een native clientbibliotheek. Normaal gesproken alle drie worden geïnstalleerd op Hallo hetzelfde moment. Azure Analysis Services is de meest recente versies Hallo vereist. 

Microsoft-clienttoepassingen, zoals Power BI Desktop- en Excel installeren alle drie clientbibliotheken. Echter, afhankelijk van het Hallo-versie of -frequentie van updates, clientbibliotheken mogelijk niet de nieuwste versies Hallo vereist door Azure Analysis Services. Hallo geldt toocustom toepassingen of andere interfaces zoals AsCmd, aangepaste, ADOMD.NET. Deze toepassingen vereisen Hallo tapewisselaars handmatig te installeren. Hallo-clientbibliotheken voor handmatige installatie zijn opgenomen in SQL Server featurepacks die als pakketten te distribueren. Deze clientbibliotheken zijn echter gebonden toohello SQL Server-versie en zijn mogelijk niet Hallo meest recente.  

Clientbibliotheken voor clientverbindingen zijn anders dan data providers vereist tooconnect uit een Azure Analysis Services server tooa-gegevensbron. toolearn meer informatie over de datasource-verbindingen, Zie [Datasource verbindingen](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Download de meest recente clientbibliotheken Hallo  
Gebruik Hallo clientbibliotheken volgen als u in een productieomgeving en volledig vrijgegeven en ondersteunde versies vereist.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Volgende stappen
[Verbinding maken met Excel](analysis-services-connect-excel.md)    
[Verbinden met Power BI](analysis-services-connect-pbi.md)
