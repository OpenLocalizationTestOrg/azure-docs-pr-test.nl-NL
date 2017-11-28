---
title: aaaSQL Data Warehouse downlevel-clients ondersteuning voor gegevens controle | Microsoft Docs
description: Meer informatie over SQL Data Warehouse-ondersteuning voor downlevel-clients voor het controleren van gegevens
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="01405-103">Ondersteuning voor SQL datawarehouse - Downlevel-clients voor controle en dynamische Gegevensmaskering</span><span class="sxs-lookup"><span data-stu-id="01405-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="01405-104">[Controle](sql-data-warehouse-auditing-overview.md) werkt met SQL-clients die ondersteuning bieden voor omleiden van TDS.</span><span class="sxs-lookup"><span data-stu-id="01405-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="01405-105">Omleiding moet ook ondersteuning voor elke client waarmee de TDS-7.4 wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="01405-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="01405-106">Uitzonderingen toothis omvatten JDBC 4.0 in welke functie u Hallo omleiding wordt niet volledig ondersteund en Tedious voor Node.JS waarin omleiding niet is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="01405-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="01405-107">Voor 'Downlevel-clients', moeten dat wil zeggen dat TDS-versie 7.3 ondersteunen en hieronder - FQDN van de server in de verbindingsreeks Hallo Hallo worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="01405-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="01405-108">Oorspronkelijke server FQDN-naam in de verbindingsreeks Hallo: <*servernaam*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="01405-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="01405-109">Gewijzigde FQDN van de server in de verbindingsreeks Hallo: <*servernaam*> .database. **beveiligde**. windows.net</span><span class="sxs-lookup"><span data-stu-id="01405-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="01405-110">Een gedeeltelijke lijst met 'Downlevel-clients' omvat:</span><span class="sxs-lookup"><span data-stu-id="01405-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="01405-111">.NET 4.0 en lager,</span><span class="sxs-lookup"><span data-stu-id="01405-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="01405-112">ODBC-10.0 en lager.</span><span class="sxs-lookup"><span data-stu-id="01405-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="01405-113">JDBC (Hoewel JDBC TDS 7.4, Hallo TDS-omleiding functie wordt niet volledig ondersteund ondersteunt)</span><span class="sxs-lookup"><span data-stu-id="01405-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="01405-114">Omslachtig (voor Node.JS)</span><span class="sxs-lookup"><span data-stu-id="01405-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="01405-115">**Opmerking:** Hallo hierboven server FDQN wijziging mogelijk van pas ook voor het toepassen van een beleid voor controle van SQL Server op zonder behoefte aan een configuratie stap in elke database (tijdelijke risicobeperking).</span><span class="sxs-lookup"><span data-stu-id="01405-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

