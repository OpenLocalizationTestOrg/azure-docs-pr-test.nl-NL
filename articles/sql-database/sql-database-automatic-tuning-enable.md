---
title: aaaEnable automatische afstemming voor Azure SQL Database | Microsoft Docs
description: U kunt inschakelen automatische afstemming op uw Azure SQL Database eenvoudig.
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="2c8a6-103">Automatisch instellen inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c8a6-103">Enable automatic tuning</span></span>

<span data-ttu-id="2c8a6-104">Azure SQL-Database is een automatisch beheerd gegevens-service die voortdurend bewaakt uw query's en identificeert Hallo actie dat u de prestaties van uw workload tooimprove kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="2c8a6-105">U kunt bekijken van aanbevelingen en handmatig toepassen of Azure SQL Database automatisch toegepast corrigerende maatregelen kunt: dit staat bekend als **automatische afstemmen modus**.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="2c8a6-106">Automatische afstemming kan worden ingeschakeld op de server voor Hallo of Hallo databaseniveau.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="2c8a6-107">Automatische afstemming op server inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c8a6-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="2c8a6-108">tooenable automatische afstemming op Azure SQL Database-server, gaat u toohello-server in Azure portal en selecteer vervolgens **automatische afstemming** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="2c8a6-109">Selecteer opties voor automatische afstemmen gewenste tooenable en selecteer Hallo **toepassen**:</span><span class="sxs-lookup"><span data-stu-id="2c8a6-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Server](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="2c8a6-111">Automatische afstemming van de opties op de server zijn toegepaste tooall databases op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="2c8a6-112">Standaard alle databases Hallo configuratie overnemen van hun bovenliggende server, maar dit kan worden genegeerd en afzonderlijk opgegeven voor elke database.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="2c8a6-113">Configureer Automatische afstemming op database</span><span class="sxs-lookup"><span data-stu-id="2c8a6-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="2c8a6-114">Hallo Azure portal kunt u tooindividually Hallo-configuratie voor automatische afstemmen op elke database opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="2c8a6-115">Hallo algemene aanbeveling is toomanage Hallo automatische afstemmen configuratie op serverniveau in dat geval Hallo dezelfde configuratie-instellingen kunnen worden toegepast op elke database automatisch.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="2c8a6-116">Configureer Automatische afstemming op een individuele database als Hallo database verschilt dat anderen op dezelfde server Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="2c8a6-117">Automatische afstemming op een individuele database tooenable toohello database in Azure-portal Hallo navigeren en vervolgens selecteert **automatische afstemming**.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="2c8a6-118">U kunt een individuele database tooinherit Hallo instellingen uit de database Hallo Hallo vinken configureren of u kunt Hallo-configuratie voor een database afzonderlijk opgeven.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Database](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="2c8a6-120">Nadat u de juiste configuratie hebt geselecteerd, klikt u op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c8a6-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c8a6-121">Next steps</span></span>
* <span data-ttu-id="2c8a6-122">Lees Hallo [automatische afstemmen artikel](sql-database-automatic-tuning.md) toolearn meer over automatische afstemming en hoe deze kan u helpen de prestaties worden verbeterd.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="2c8a6-123">Zie [prestaties aanbevelingen](sql-database-advisor.md) voor een overzicht van Azure SQL Database prestaties aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="2c8a6-124">Zie [inzichten voor queryprestaties](sql-database-query-performance.md) toolearn over het weergeven van Hallo prestatie-invloed van de meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="2c8a6-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
