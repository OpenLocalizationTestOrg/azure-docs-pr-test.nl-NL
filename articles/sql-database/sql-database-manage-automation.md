---
title: aaaManage Azure SQL-Databases met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure SQL-databases op grote schaal kan worden.
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Azure SQL-Databases met behulp van Azure Automation beheren
Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van uw Azure SQL-databases kan zijn.

## <a name="what-is-azure-automation"></a>Wat is Azure Automation?
[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen. Met behulp van Azure Automation, kunnen langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.

Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar toomeet wanneer uw organisatie groeit uw behoeften. In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.

Lagere operationele overhead en vrijmaken IT / DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Hoe kan Azure Automation helpen Azure SQL-databases beheren?
Azure SQL Database in Azure Automation kunnen worden beheerd met behulp van Hallo [Azure SQL Database PowerShell-cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) die beschikbaar zijn in Hallo [hulpprogramma's van Azure PowerShell](/powershell/azure/overview). Azure Automation heeft deze Azure SQL Database PowerShell-cmdlets beschikbaar out of box hello, zodat u alle van uw SQL-database beheertaken in Hallo service kunt uitvoeren. U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.

Azure Automation heeft ook Hallo mogelijkheid toocommunicate met SQL-servers rechtstreeks, door uitgifte van SQL-opdrachten met behulp van PowerShell.

Hallo [galerie van Azure Automation-runbook](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) bevat een verscheidenheid aan product team en community runbooks tooget gestart met het automatiseren van beheer van Azure SQL-Databases, andere Azure-services en 3e systemen van derden. Galerie-runbooks zijn onder andere:

* [SQL-query's uitvoeren op een SQL Server-database](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [(Omhoog of omlaag) verticaal te schalen een Azure SQL Database volgens een schema](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Een SQL-tabel afkappen als de database de maximale grootte nadert](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Indexeren van tabellen in een Azure SQL Database als ze zijn sterk gefragmenteerd zijn](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure SQL-databases hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.

* [Overzicht van Azure Automation](../automation/automation-intro.md)
* [Mijn eerste runbook](../automation/automation-first-runbook-graphical.md)
* [Azure Automation-leeroverzicht](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Azure Automation: De SQL Agent Hallo Cloud](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

