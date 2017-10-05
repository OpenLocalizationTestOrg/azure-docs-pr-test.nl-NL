---
title: Ondersteuning voor SQL Data Warehouse downlevel-clients voor het controleren van de gegevens | Microsoft Docs
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
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="0793b-103">Ondersteuning voor SQL datawarehouse - Downlevel-clients voor controle en dynamische Gegevensmaskering</span><span class="sxs-lookup"><span data-stu-id="0793b-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="0793b-104">[Controle](sql-data-warehouse-auditing-overview.md) werkt met SQL-clients die ondersteuning bieden voor omleiden van TDS.</span><span class="sxs-lookup"><span data-stu-id="0793b-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="0793b-105">Omleiding moet ook ondersteuning voor elke client waarmee de TDS-7.4 wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0793b-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="0793b-106">Uitzonderingen op deze omvatten JDBC 4.0 waarin de functie voor omleiding wordt niet volledig ondersteund en Tedious voor Node.JS in welke omleiding is niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0793b-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="0793b-107">Voor 'Downlevel-clients', moet dat wil zeggen welke ondersteuning TDS 7.3 en hieronder - de FQDN-naam van de server in de verbinding versietekenreeks worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="0793b-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="0793b-108">Oorspronkelijke server FQDN-naam in de verbindingsreeks: <*servernaam*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="0793b-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="0793b-109">Gewijzigde FQDN van de server in de verbindingsreeks: <*servernaam*> .database. **beveiligde**. windows.net</span><span class="sxs-lookup"><span data-stu-id="0793b-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="0793b-110">Een gedeeltelijke lijst met 'Downlevel-clients' omvat:</span><span class="sxs-lookup"><span data-stu-id="0793b-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="0793b-111">.NET 4.0 en lager,</span><span class="sxs-lookup"><span data-stu-id="0793b-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="0793b-112">ODBC-10.0 en lager.</span><span class="sxs-lookup"><span data-stu-id="0793b-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="0793b-113">JDBC (Hoewel JDBC TDS 7.4 ondersteunt, de TDS-omleiding-functie is niet volledig ondersteund)</span><span class="sxs-lookup"><span data-stu-id="0793b-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="0793b-114">Omslachtig (voor Node.JS)</span><span class="sxs-lookup"><span data-stu-id="0793b-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="0793b-115">**Opmerking:** de bovenstaande server FDQN wijziging mogelijk handig ook voor het toepassen van een beleid voor controle van SQL Server op zonder behoefte aan een configuratie stap in elke database (tijdelijke risicobeperking).</span><span class="sxs-lookup"><span data-stu-id="0793b-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

