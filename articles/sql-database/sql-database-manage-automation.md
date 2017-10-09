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
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="60f60-103">Azure SQL-Databases met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="60f60-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="60f60-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van uw Azure SQL-databases kan zijn.</span><span class="sxs-lookup"><span data-stu-id="60f60-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="60f60-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="60f60-105">What is Azure Automation?</span></span>
<span data-ttu-id="60f60-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="60f60-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="60f60-107">Met behulp van Azure Automation, kunnen langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="60f60-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="60f60-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar toomeet wanneer uw organisatie groeit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="60f60-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="60f60-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="60f60-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="60f60-110">Lagere operationele overhead en vrijmaken IT / DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="60f60-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="60f60-111">Hoe kan Azure Automation helpen Azure SQL-databases beheren?</span><span class="sxs-lookup"><span data-stu-id="60f60-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="60f60-112">Azure SQL Database in Azure Automation kunnen worden beheerd met behulp van Hallo [Azure SQL Database PowerShell-cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) die beschikbaar zijn in Hallo [hulpprogramma's van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60f60-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="60f60-113">Azure Automation heeft deze Azure SQL Database PowerShell-cmdlets beschikbaar out of box hello, zodat u alle van uw SQL-database beheertaken in Hallo service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="60f60-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="60f60-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="60f60-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="60f60-115">Azure Automation heeft ook Hallo mogelijkheid toocommunicate met SQL-servers rechtstreeks, door uitgifte van SQL-opdrachten met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60f60-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="60f60-116">Hallo [galerie van Azure Automation-runbook](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) bevat een verscheidenheid aan product team en community runbooks tooget gestart met het automatiseren van beheer van Azure SQL-Databases, andere Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="60f60-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="60f60-117">Galerie-runbooks zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="60f60-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="60f60-118">SQL-query's uitvoeren op een SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="60f60-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="60f60-119">(Omhoog of omlaag) verticaal te schalen een Azure SQL Database volgens een schema</span><span class="sxs-lookup"><span data-stu-id="60f60-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="60f60-120">Een SQL-tabel afkappen als de database de maximale grootte nadert</span><span class="sxs-lookup"><span data-stu-id="60f60-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="60f60-121">Indexeren van tabellen in een Azure SQL Database als ze zijn sterk gefragmenteerd zijn</span><span class="sxs-lookup"><span data-stu-id="60f60-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="60f60-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60f60-122">Next steps</span></span>
<span data-ttu-id="60f60-123">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure SQL-databases hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="60f60-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="60f60-124">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="60f60-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="60f60-125">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="60f60-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="60f60-126">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="60f60-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="60f60-127">Azure Automation: De SQL Agent Hallo Cloud</span><span class="sxs-lookup"><span data-stu-id="60f60-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

