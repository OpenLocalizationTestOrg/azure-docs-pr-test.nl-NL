---
title: Ontwerp van uw eerste Azure SQL database - C# | Microsoft Docs
description: Informatie over het ontwerpen van uw eerste Azure SQL database en verbinding maken met een C#-programma ADO.NET gebruiken.
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="a748d-103">Ontwerp van een Azure SQL database en verbinding maken met C & #x23; en ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a748d-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="a748d-104">Azure SQL-Database is een relationele database als een service (DBaaS) in de Microsoft-Cloud ('Azure').</span><span class="sxs-lookup"><span data-stu-id="a748d-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="a748d-105">In deze zelfstudie leert u hoe de Azure-portal en ADO.NET met Visual Studio te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a748d-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a748d-106">Maak een database in de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a748d-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="a748d-107">Een firewallregel op serverniveau in de Azure portal instellen</span><span class="sxs-lookup"><span data-stu-id="a748d-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="a748d-108">Verbinding maken met de database met ADO.NET en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a748d-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="a748d-109">Tabellen maken met ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a748d-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="a748d-110">Invoegen, bijwerken en verwijderen van gegevens met ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a748d-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="a748d-111">Querygegevens ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a748d-111">Query data ADO.NET</span></span>

<span data-ttu-id="a748d-112">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="a748d-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a748d-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a748d-113">Prerequisites</span></span>

<span data-ttu-id="a748d-114">Een installatie van [Visual Studio Community 2017, Visual Studio Professional 2017 of Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a748d-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="a748d-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a748d-115">Next steps</span></span>

<span data-ttu-id="a748d-116">In deze zelfstudie hebt u geleerd basic databasetaken, zoals een database en tabellen maken, laden en een query over gegevens en de database naar een eerder tijdstip herstellen.</span><span class="sxs-lookup"><span data-stu-id="a748d-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="a748d-117">U leert hoe naar:</span><span class="sxs-lookup"><span data-stu-id="a748d-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a748d-118">Een database maken</span><span class="sxs-lookup"><span data-stu-id="a748d-118">Create a database</span></span>
> * <span data-ttu-id="a748d-119">Een firewallregel instellen</span><span class="sxs-lookup"><span data-stu-id="a748d-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="a748d-120">Verbinding maken met de database met [Visual Studio en C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="a748d-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="a748d-121">Tabellen maken</span><span class="sxs-lookup"><span data-stu-id="a748d-121">Create tables</span></span>
> * <span data-ttu-id="a748d-122">Invoegen, bijwerken en verwijderen van gegevens</span><span class="sxs-lookup"><span data-stu-id="a748d-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="a748d-123">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="a748d-123">Query data</span></span>

<span data-ttu-id="a748d-124">Ga naar de volgende zelfstudie voor meer informatie over het migreren van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="a748d-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="a748d-125">De SQL Server-database migreren naar Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a748d-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

