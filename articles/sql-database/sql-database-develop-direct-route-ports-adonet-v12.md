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
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="259d3-104">Poorten buiten 1433 voor ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="259d3-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="259d3-105">Dit onderwerp beschrijft hello Azure SQL Database Verbindingsgedrag voor clients die gebruikmaken van ADO.NET 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="259d3-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="259d3-106">Zie voor meer informatie over de architectuur van de connectiviteit [Azure SQL Database connectivity architectuur](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="259d3-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="259d3-107">Externe tegenover binnen</span><span class="sxs-lookup"><span data-stu-id="259d3-107">Outside vs inside</span></span>
<span data-ttu-id="259d3-108">Voor verbindingen tooAzure SQL-Database, moet eerst vragen we uw clientprogramma wordt uitgevoerd of *buiten* of *binnen* hello Azure-cloud grens.</span><span class="sxs-lookup"><span data-stu-id="259d3-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="259d3-109">Hallo subsecties worden de twee algemene scenario's besproken.</span><span class="sxs-lookup"><span data-stu-id="259d3-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="259d3-110">*Buiten:* Client wordt uitgevoerd op uw computer</span><span class="sxs-lookup"><span data-stu-id="259d3-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="259d3-111">Poort 1433 is Hallo enige poort die moet worden geopend op uw bureaublad computer die als host fungeert voor uw clienttoepassing SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="259d3-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="259d3-112">*Binnen:* Client wordt uitgevoerd op Azure</span><span class="sxs-lookup"><span data-stu-id="259d3-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="259d3-113">Wanneer de client wordt uitgevoerd binnen een grens van hello Azure-cloud, gebruikt het kunt zogeheten een *direct route* toointeract met Hallo SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="259d3-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="259d3-114">Nadat een verbinding tot stand is gebracht, hebben geen proxy middleware betrekking op verdere interacties tussen Hallo-client en de database.</span><span class="sxs-lookup"><span data-stu-id="259d3-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="259d3-115">Hallo-reeks is als volgt:</span><span class="sxs-lookup"><span data-stu-id="259d3-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="259d3-116">ADO.NET 4.5 (of hoger) initieert een korte interactie met hello Azure-cloud en ontvangt een dynamisch geïdentificeerde poortnummer.</span><span class="sxs-lookup"><span data-stu-id="259d3-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="259d3-117">Hallo dynamisch geïdentificeerd-poortnummer is binnen het bereik van 11000 11999 of 14000 14999 Hallo.</span><span class="sxs-lookup"><span data-stu-id="259d3-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="259d3-118">ADO.NET maakt vervolgens verbinding toohello SQL Database-server rechtstreeks met geen middleware ertussen.</span><span class="sxs-lookup"><span data-stu-id="259d3-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="259d3-119">Query's rechtstreeks toohello database worden verzonden en resultaten rechtstreeks toohello client worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="259d3-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="259d3-120">Zorg ervoor dat Hallo poort bereiken van 11000 11999 en 14000-14999 op uw Azure-client-computer beschikbaar voor ADO.NET 4.5 client interactie met de SQL-Database blijven.</span><span class="sxs-lookup"><span data-stu-id="259d3-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="259d3-121">In het bijzonder moeten poorten in Hallo bereik andere uitgaande blockers gratis.</span><span class="sxs-lookup"><span data-stu-id="259d3-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="259d3-122">Op de virtuele machine van Azure Hallo **Windows Firewall met geavanceerde beveiliging** besturingselementen Hallo poortinstellingen.</span><span class="sxs-lookup"><span data-stu-id="259d3-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="259d3-123">Kunt u Hallo [gebruikersinterface van de firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd een regel die u Hallo opgeeft **TCP** protocol samen met een poortbereik met Hallo-syntaxis, zoals **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="259d3-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="259d3-124">Versie verduidelijkingen</span><span class="sxs-lookup"><span data-stu-id="259d3-124">Version clarifications</span></span>
<span data-ttu-id="259d3-125">Deze sectie wordt uitleg gegeven over Hallo monikers die tooproduct versies verwijzen.</span><span class="sxs-lookup"><span data-stu-id="259d3-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="259d3-126">Het bevat ook enkele koppelingen tussen versies tussen producten.</span><span class="sxs-lookup"><span data-stu-id="259d3-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="259d3-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="259d3-127">ADO.NET</span></span>
* <span data-ttu-id="259d3-128">ADO.NET 4.0 ondersteunt Hallo 7.3 TDS-protocol, maar niet 7.4.</span><span class="sxs-lookup"><span data-stu-id="259d3-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="259d3-129">ADO.NET 4.5 en hoger ondersteunt Hallo 7.4 TDS-protocol.</span><span class="sxs-lookup"><span data-stu-id="259d3-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="259d3-130">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="259d3-130">Related links</span></span>
* <span data-ttu-id="259d3-131">ADO.NET 4.6 is uitgebracht op 20 juli 2015.</span><span class="sxs-lookup"><span data-stu-id="259d3-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="259d3-132">Er is een aankondiging blog van Hallo .NET-team beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="259d3-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="259d3-133">ADO.NET 4.5 is uitgebracht op 15 augustus 2012.</span><span class="sxs-lookup"><span data-stu-id="259d3-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="259d3-134">Er is een aankondiging blog van Hallo .NET-team beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="259d3-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="259d3-135">Er is een blogbericht over ADO.NET 4.5.1 beschikbaar [hier](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="259d3-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="259d3-136">Lijst met de versie van de TDS-protocol</span><span class="sxs-lookup"><span data-stu-id="259d3-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="259d3-137">Overzicht van SQL Database-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="259d3-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="259d3-138">Azure SQL Database-firewall</span><span class="sxs-lookup"><span data-stu-id="259d3-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="259d3-139">Procedure: firewall-instellingen configureren op de SQL-Database</span><span class="sxs-lookup"><span data-stu-id="259d3-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

