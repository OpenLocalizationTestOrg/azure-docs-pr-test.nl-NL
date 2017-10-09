---
title: Transparent Data Encryption voor Stretch Database - Azure aaaEnable | Microsoft Docs
description: Transparante gegevensversleuteling (TDE) voor SQL Server Stretch Database in Azure inschakelen
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="7d81b-103">Transparante gegevensversleuteling (TDE) inschakelen voor Stretch Database in Azure</span><span class="sxs-lookup"><span data-stu-id="7d81b-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d81b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7d81b-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="7d81b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="7d81b-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="7d81b-106">Transparent Data Encryption (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door het uitvoeren van realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogboekbestanden in rust zonder wijzigingen toohello de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7d81b-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="7d81b-107">TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel.</span><span class="sxs-lookup"><span data-stu-id="7d81b-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="7d81b-108">Hallo databaseversleutelingssleutel is beveiligd met een ingebouwde servercertificaat.</span><span class="sxs-lookup"><span data-stu-id="7d81b-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="7d81b-109">ingebouwde Hallo-servercertificaat is uniek voor elke Azure-server.</span><span class="sxs-lookup"><span data-stu-id="7d81b-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="7d81b-110">Microsoft draait automatisch deze certificaten ten minste om de 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="7d81b-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="7d81b-111">Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="7d81b-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="7d81b-112">Codering inschakelen</span><span class="sxs-lookup"><span data-stu-id="7d81b-112">Enabling Encryption</span></span>
<span data-ttu-id="7d81b-113">tooenable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d81b-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="7d81b-114">Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7d81b-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="7d81b-115">Klik op Hallo databaseblade Hallo **instellingen** knop</span><span class="sxs-lookup"><span data-stu-id="7d81b-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="7d81b-116">Selecteer Hallo **transparante gegevensversleuteling** optie![][1]</span><span class="sxs-lookup"><span data-stu-id="7d81b-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="7d81b-117">Selecteer Hallo **op** instelling en selecteer vervolgens **opslaan**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="7d81b-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="7d81b-118">Codering uitschakelen</span><span class="sxs-lookup"><span data-stu-id="7d81b-118">Disabling Encryption</span></span>
<span data-ttu-id="7d81b-119">toodisable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d81b-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="7d81b-120">Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7d81b-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="7d81b-121">Klik op Hallo databaseblade Hallo **instellingen** knop</span><span class="sxs-lookup"><span data-stu-id="7d81b-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="7d81b-122">Selecteer Hallo **transparante gegevensversleuteling** optie</span><span class="sxs-lookup"><span data-stu-id="7d81b-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="7d81b-123">Selecteer Hallo **uit** instelling en selecteer vervolgens **opslaan**</span><span class="sxs-lookup"><span data-stu-id="7d81b-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
