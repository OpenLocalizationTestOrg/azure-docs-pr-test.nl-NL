---
title: aaaPorts buiten 1433 voor SQL-Database | Microsoft Docs
description: Clientverbindingen van ADO.NET tooAzure SQL-Database soms Hallo proxy omzeilen en rechtstreeks communiceren met de Hallo-database. Andere poorten dan poort 1433 worden belangrijk.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Poorten buiten 1433 voor ADO.NET 4.5
Dit onderwerp beschrijft hello Azure SQL Database Verbindingsgedrag voor clients die gebruikmaken van ADO.NET 4.5 of hoger. 

> [!IMPORTANT]
> Zie voor meer informatie over de architectuur van de connectiviteit [Azure SQL Database connectivity architectuur](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Externe tegenover binnen
Voor verbindingen tooAzure SQL-Database, moet eerst vragen we uw clientprogramma wordt uitgevoerd of *buiten* of *binnen* hello Azure-cloud grens. Hallo subsecties worden de twee algemene scenario's besproken.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Buiten:* Client wordt uitgevoerd op uw computer
Poort 1433 is Hallo enige poort die moet worden geopend op uw bureaublad computer die als host fungeert voor uw clienttoepassing SQL-Database.

#### <a name="inside-client-runs-on-azure"></a>*Binnen:* Client wordt uitgevoerd op Azure
Wanneer de client wordt uitgevoerd binnen een grens van hello Azure-cloud, gebruikt het kunt zogeheten een *direct route* toointeract met Hallo SQL Database-server. Nadat een verbinding tot stand is gebracht, hebben geen proxy middleware betrekking op verdere interacties tussen Hallo-client en de database.

Hallo-reeks is als volgt:

1. ADO.NET 4.5 (of hoger) initieert een korte interactie met hello Azure-cloud en ontvangt een dynamisch geïdentificeerde poortnummer.
   
   * Hallo dynamisch geïdentificeerd-poortnummer is binnen het bereik van 11000 11999 of 14000 14999 Hallo.
2. ADO.NET maakt vervolgens verbinding toohello SQL Database-server rechtstreeks met geen middleware ertussen.
3. Query's rechtstreeks toohello database worden verzonden en resultaten rechtstreeks toohello client worden geretourneerd.

Zorg ervoor dat Hallo poort bereiken van 11000 11999 en 14000-14999 op uw Azure-client-computer beschikbaar voor ADO.NET 4.5 client interactie met de SQL-Database blijven.

* In het bijzonder moeten poorten in Hallo bereik andere uitgaande blockers gratis.
* Op de virtuele machine van Azure Hallo **Windows Firewall met geavanceerde beveiliging** besturingselementen Hallo poortinstellingen.
  
  * Kunt u Hallo [gebruikersinterface van de firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd een regel die u Hallo opgeeft **TCP** protocol samen met een poortbereik met Hallo-syntaxis, zoals **11000 11999**.

## <a name="version-clarifications"></a>Versie verduidelijkingen
Deze sectie wordt uitleg gegeven over Hallo monikers die tooproduct versies verwijzen. Het bevat ook enkele koppelingen tussen versies tussen producten.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 ondersteunt Hallo 7.3 TDS-protocol, maar niet 7.4.
* ADO.NET 4.5 en hoger ondersteunt Hallo 7.4 TDS-protocol.

## <a name="related-links"></a>Verwante koppelingen
* ADO.NET 4.6 is uitgebracht op 20 juli 2015. Er is een aankondiging blog van Hallo .NET-team beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 is uitgebracht op 15 augustus 2012. Er is een aankondiging blog van Hallo .NET-team beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Er is een blogbericht over ADO.NET 4.5.1 beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Lijst met de versie van de TDS-protocol](http://www.freetds.org/userguide/tdshistory.htm)
* [Overzicht van SQL Database-ontwikkeling](sql-database-develop-overview.md)
* [Azure SQL Database-firewall](sql-database-firewall-configure.md)
* [Procedure: firewall-instellingen configureren op de SQL-Database](sql-database-configure-firewall-settings.md)

