---
title: een overzicht voor de ontwikkelaars voor Azure-Database voor MySQL aaaDatabase | Microsoft Docs
description: Overwegingen bij het ontwerpen die een ontwikkelaar volgen moet bij het schrijven van toepassing code tooconnect tooAzure Database voor MySQL introduceert
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="92b25-103">Overzicht van toepassing voor ontwikkelaars voor Azure-Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="92b25-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="92b25-104">Dit artikel wordt beschreven ontwerpoverwegingen die een ontwikkelaar volgen moet bij het schrijven van toepassing code tooconnect tooAzure Database voor MySQL</span><span class="sxs-lookup"><span data-stu-id="92b25-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="92b25-105">Zie voor een zelfstudie waarin u hoe toocreate een server, een firewall op de server maken weergeven van de eigenschappen van server, database maken, verbinding maken en query uitvoert met behulp van de workbench en mysql.exe [ontwerpen van uw eerste Azure MySQL-database](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="92b25-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="92b25-106">Taal en platform</span><span class="sxs-lookup"><span data-stu-id="92b25-106">Language and platform</span></span>
<span data-ttu-id="92b25-107">Er zijn codevoorbeelden beschikbaar voor verschillende programmeertalen en platforms.</span><span class="sxs-lookup"><span data-stu-id="92b25-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="92b25-108">Vindt u koppelingen toohello codevoorbeelden op: [bibliotheken voor databaseconnectiviteit tooconnect tooAzure Database gebruikt voor MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="92b25-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="92b25-109">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="92b25-109">Tools</span></span>
<span data-ttu-id="92b25-110">Azure MySQL-Database maakt gebruik van Hallo MySQL community-versie, compatibel zijn met algemene beheerprogramma's zoals Workbench of MySQL hulpprogramma's zoals mysql.exe, MySQL [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), en andere.</span><span class="sxs-lookup"><span data-stu-id="92b25-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="92b25-111">U kunt ook hello Azure-portal, Azure CLI en toointeract REST-API's gebruiken met Hallo database-service.</span><span class="sxs-lookup"><span data-stu-id="92b25-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="92b25-112">Resourcebeperkingen</span><span class="sxs-lookup"><span data-stu-id="92b25-112">Resource limitations</span></span>
<span data-ttu-id="92b25-113">Azure MySQL-Database beheert Hallo bronnen beschikbaar tooa server met twee verschillende mechanismen:</span><span class="sxs-lookup"><span data-stu-id="92b25-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="92b25-114">Beheer van resources</span><span class="sxs-lookup"><span data-stu-id="92b25-114">Resources Governance</span></span> 
- <span data-ttu-id="92b25-115">Afdwinging van limieten.</span><span class="sxs-lookup"><span data-stu-id="92b25-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="92b25-116">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="92b25-116">Security</span></span>
<span data-ttu-id="92b25-117">Azure MySQL-Database bevat bronnen voor beperkende toegang, beschermen gegevens configureren gebruikers en rol en bewaking van activiteiten in een MySQL-Database.</span><span class="sxs-lookup"><span data-stu-id="92b25-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="92b25-118">Authentication</span><span class="sxs-lookup"><span data-stu-id="92b25-118">Authentication</span></span>
<span data-ttu-id="92b25-119">Azure MySQL-Database biedt ondersteuning voor server-verificatie van gebruikers en aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="92b25-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="92b25-120">Flexibiliteit</span><span class="sxs-lookup"><span data-stu-id="92b25-120">Resiliency</span></span>
<span data-ttu-id="92b25-121">Wanneer een tijdelijke fout optreedt tijdens het verbinden van tooMySQL Database, moet uw code Hallo-aanroep in opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="92b25-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="92b25-122">Het is raadzaam Hallo opnieuw logica gebruik uit logica, zodat deze biedt Hallo SQL-Database niet overbelast met meerdere clients tegelijkertijd opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="92b25-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="92b25-123">Codevoorbeelden: codevoorbeelden die aangeven Pogingslogica, vindt u voorbeelden voor de taal van uw keuze op Hallo: [bibliotheken voor databaseconnectiviteit tooconnect tooAzure Database gebruikt voor MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="92b25-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="92b25-124">Verbindingen beheren</span><span class="sxs-lookup"><span data-stu-id="92b25-124">Managing Connections</span></span>
<span data-ttu-id="92b25-125">Databaseverbindingen zijn een beperkte resource daarom logisch verbindingen worden gebruikt aangeraden bij het openen van uw MySQL-Database tooachieve betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="92b25-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="92b25-126">Access Hallo-database met behulp van verbindingsgroepering of permanente verbindingen.</span><span class="sxs-lookup"><span data-stu-id="92b25-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="92b25-127">Met behulp van de levensduur van een korte verbinding Access Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="92b25-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="92b25-128">Pogingslogica voor gebruik in uw toepassing bij de verbindingspoging hello, toocatch fouten vanwege tooconcurrent verbindingen Hallo Hallo maximale toegestane bereikt.</span><span class="sxs-lookup"><span data-stu-id="92b25-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="92b25-129">In Hallo Pogingslogica, een korte vertraging instellen en vervolgens wachten op een willekeurige tijd voordat de aanvullende verbindingspogingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="92b25-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
