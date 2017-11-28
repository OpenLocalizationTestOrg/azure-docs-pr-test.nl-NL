---
title: aaaDesign uw eerste Azure SQL database - C# | Microsoft Docs
description: Informatie over toodesign uw eerste Azure SQL database en tooit verbinden met een C#-programma ADO.NET gebruiken.
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
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="bee62-103">Ontwerp van een Azure SQL database en verbinding maken met C & #x23; en ADO.NET</span><span class="sxs-lookup"><span data-stu-id="bee62-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="bee62-104">Azure SQL-Database is een relationele database als een service (DBaaS) in Hallo Microsoft Cloud ('Azure').</span><span class="sxs-lookup"><span data-stu-id="bee62-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="bee62-105">In deze zelfstudie leert u hoe toouse hello Azure portal en ADO.NET met Visual Studio aan:</span><span class="sxs-lookup"><span data-stu-id="bee62-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bee62-106">Maak een database in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="bee62-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="bee62-107">Een firewallregel op serverniveau in hello Azure-portal instellen</span><span class="sxs-lookup"><span data-stu-id="bee62-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="bee62-108">Verbinding maken met toohello database met ADO.NET en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bee62-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="bee62-109">Tabellen maken met ADO.NET</span><span class="sxs-lookup"><span data-stu-id="bee62-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="bee62-110">Invoegen, bijwerken en verwijderen van gegevens met ADO.NET</span><span class="sxs-lookup"><span data-stu-id="bee62-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="bee62-111">Querygegevens ADO.NET</span><span class="sxs-lookup"><span data-stu-id="bee62-111">Query data ADO.NET</span></span>

<span data-ttu-id="bee62-112">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="bee62-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bee62-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bee62-113">Prerequisites</span></span>

<span data-ttu-id="bee62-114">Een installatie van [Visual Studio Community 2017, Visual Studio Professional 2017 of Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bee62-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="bee62-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bee62-115">Next steps</span></span>

<span data-ttu-id="bee62-116">In deze zelfstudie hebt u geleerd basic databasetaken, zoals een database en tabellen maken, laden en gegevens opvragen en tijdstip Hallo database tooa eerder punt herstellen.</span><span class="sxs-lookup"><span data-stu-id="bee62-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="bee62-117">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="bee62-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="bee62-118">Een database maken</span><span class="sxs-lookup"><span data-stu-id="bee62-118">Create a database</span></span>
> * <span data-ttu-id="bee62-119">Een firewallregel instellen</span><span class="sxs-lookup"><span data-stu-id="bee62-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="bee62-120">Verbinding maken met de database toohello met [Visual Studio en C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="bee62-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="bee62-121">Tabellen maken</span><span class="sxs-lookup"><span data-stu-id="bee62-121">Create tables</span></span>
> * <span data-ttu-id="bee62-122">Invoegen, bijwerken en verwijderen van gegevens</span><span class="sxs-lookup"><span data-stu-id="bee62-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="bee62-123">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="bee62-123">Query data</span></span>

<span data-ttu-id="bee62-124">Ga toohello volgende zelfstudie toolearn over het migreren van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="bee62-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="bee62-125">Migreren van uw SQL Server-database tooAzure SQL-Database</span><span class="sxs-lookup"><span data-stu-id="bee62-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

