---
title: Azure SQL-Databases met behulp van Azure Automation beheren | Microsoft Docs
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van Azure SQL-databases op grote schaal.
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
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="92fa7-103">Azure SQL-Databases met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="92fa7-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="92fa7-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van beheer van uw Azure SQL-databases.</span><span class="sxs-lookup"><span data-stu-id="92fa7-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="92fa7-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="92fa7-105">What is Azure Automation?</span></span>
<span data-ttu-id="92fa7-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="92fa7-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="92fa7-107">Met behulp van Azure Automation, worden langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken geautomatiseerd om betrouwbaarheid, efficiëntie en tijd voor de waarde voor uw organisatie te verhogen.</span><span class="sxs-lookup"><span data-stu-id="92fa7-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="92fa7-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar is om te voldoen aan de behoeften van uw wanneer uw organisatie groeit.</span><span class="sxs-lookup"><span data-stu-id="92fa7-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="92fa7-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="92fa7-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="92fa7-110">Lagere operationele overhead en vrijmaken IT / DevOps-personeel te concentreren op het werk dat zakelijke voegt waarde door uw cloud-beheertaken automatisch wordt uitgevoerd door Azure Automation te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="92fa7-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="92fa7-111">Hoe kan Azure Automation helpen Azure SQL-databases beheren?</span><span class="sxs-lookup"><span data-stu-id="92fa7-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="92fa7-112">Azure SQL Database in Azure Automation kunnen worden beheerd met behulp van de [Azure SQL Database PowerShell-cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) die beschikbaar zijn in de [hulpprogramma's van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="92fa7-112">Azure SQL Database can be managed in Azure Automation by using the [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in the [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="92fa7-113">Azure Automation heeft deze Azure SQL Database PowerShell-cmdlets beschikbaar gebruiksklaar, zodat u al uw taken voor het beheer van SQL-database in de service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="92fa7-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of the box, so that you can perform all of your SQL DB management tasks within the service.</span></span> <span data-ttu-id="92fa7-114">U kunt ook deze cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en 3e systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="92fa7-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="92fa7-115">Azure Automation heeft ook de mogelijkheid om te communiceren met de SQL-servers rechtstreeks, door uitgifte van SQL-opdrachten met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92fa7-115">Azure Automation also has the ability to communicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="92fa7-116">De [galerie van Azure Automation-runbook](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) bevat een verscheidenheid aan product team en community runbooks om te beginnen met het automatiseren van beheer van Azure SQL-Databases, andere Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="92fa7-116">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="92fa7-117">Galerie-runbooks zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="92fa7-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="92fa7-118">SQL-query's uitvoeren op een SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="92fa7-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="92fa7-119">(Omhoog of omlaag) verticaal te schalen een Azure SQL Database volgens een schema</span><span class="sxs-lookup"><span data-stu-id="92fa7-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="92fa7-120">Een SQL-tabel afkappen als de database de maximale grootte nadert</span><span class="sxs-lookup"><span data-stu-id="92fa7-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="92fa7-121">Indexeren van tabellen in een Azure SQL Database als ze zijn sterk gefragmenteerd zijn</span><span class="sxs-lookup"><span data-stu-id="92fa7-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="92fa7-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92fa7-122">Next steps</span></span>
<span data-ttu-id="92fa7-123">Nu dat u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van Azure SQL-databases hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="92fa7-123">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure SQL databases, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="92fa7-124">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="92fa7-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="92fa7-125">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="92fa7-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="92fa7-126">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="92fa7-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="92fa7-127">Azure Automation: Uw SQL-Agent in de Cloud</span><span class="sxs-lookup"><span data-stu-id="92fa7-127">Azure Automation: Your SQL Agent in the Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

