---
title: aaaUse Azure Stream Analytics met SQL Data Warehouse | Microsoft Docs
description: Tips voor het gebruik van Azure Stream Analytics met Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="280c0-103">Azure Stream Analytics gebruiken met SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="280c0-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="280c0-104">Azure Stream Analytics is een volledig beheerde service lage latentie, maximaal beschikbare, schaalbare complexe verwerking van gebeurtenissen boven het streamen van gegevens in de cloud Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="280c0-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="280c0-105">U kunt basisbegrippen Hallo door te lezen [inleiding tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="280c0-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="280c0-106">Vervolgens leert u hoe een end-to-end-oplossing met Stream Analytics door toocreate Hallo [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="280c0-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="280c0-107">In dit artikel leert u hoe toouse uw Azure SQL Data Warehouse-database als uitvoerlocatie voor uw stoom Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="280c0-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="280c0-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="280c0-108">Prerequisites</span></span>
<span data-ttu-id="280c0-109">Voer eerst via de volgende stappen uit in Hallo Hallo [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="280c0-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="280c0-110">De invoer van een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="280c0-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="280c0-111">Configureren en starten van de gebeurtenis generator-toepassing</span><span class="sxs-lookup"><span data-stu-id="280c0-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="280c0-112">Inrichten van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="280c0-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="280c0-113">Taak invoer- en query opgeven</span><span class="sxs-lookup"><span data-stu-id="280c0-113">Specify job input and query</span></span>

<span data-ttu-id="280c0-114">Vervolgens maakt u een Azure SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="280c0-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="280c0-115">Geef de taakuitvoer: Azure SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="280c0-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="280c0-116">Stap 1</span><span class="sxs-lookup"><span data-stu-id="280c0-116">Step 1</span></span>
<span data-ttu-id="280c0-117">Klik in de Stream Analytics-taak op **uitvoer** vanaf de bovenkant Hallo Hallo pagina en klik vervolgens op **uitvoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="280c0-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="280c0-118">Stap 2</span><span class="sxs-lookup"><span data-stu-id="280c0-118">Step 2</span></span>
<span data-ttu-id="280c0-119">Selecteer de SQL-Database en klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="280c0-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="280c0-120">Stap 3</span><span class="sxs-lookup"><span data-stu-id="280c0-120">Step 3</span></span>
<span data-ttu-id="280c0-121">Voer de volgende waarden op de volgende pagina Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="280c0-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="280c0-122">*Uitvoer Alias*: een beschrijvende naam voor de taakuitvoer van deze.</span><span class="sxs-lookup"><span data-stu-id="280c0-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="280c0-123">*Abonnement*:</span><span class="sxs-lookup"><span data-stu-id="280c0-123">*Subscription*:</span></span>
  * <span data-ttu-id="280c0-124">Als uw SQL Data Warehouse-database in Hallo is hetzelfde abonnement als Hallo Stream Analytics-taak, selecteert u gebruik SQL Database uit het huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="280c0-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="280c0-125">Als uw database zich in een ander abonnement, selecteert u gebruik SQL Database in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="280c0-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="280c0-126">*Database*: Hallo-naam van een doeldatabase opgeven.</span><span class="sxs-lookup"><span data-stu-id="280c0-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="280c0-127">*Servernaam*: Geef de servernaam Hallo voor Hallo-database die u zojuist hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="280c0-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="280c0-128">U kunt Hallo klassieke Azure-Portal toofind deze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="280c0-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="280c0-129">*Gebruikersnaam*: Geef de gebruikersnaam op Hallo van een account met schrijfmachtigingen voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="280c0-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="280c0-130">*Wachtwoord*: bieden Hallo wachtwoord voor Hallo opgegeven gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="280c0-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="280c0-131">*Tabel*: Hallo naam opgeven van de doeltabel Hallo in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="280c0-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="280c0-132">Stap 4</span><span class="sxs-lookup"><span data-stu-id="280c0-132">Step 4</span></span>
<span data-ttu-id="280c0-133">Klik op Hallo selectievakje knop tooadd deze taakuitvoer en tooverify dat Stream Analytics verbinding toohello database maken kan.</span><span class="sxs-lookup"><span data-stu-id="280c0-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="280c0-134">Als de databaseverbinding toohello Hallo is geslaagd, ziet u een melding onderaan Hallo Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="280c0-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="280c0-135">U kunt klikken op verbinding testen op Hallo onder tootest Hallo verbinding toohello database.</span><span class="sxs-lookup"><span data-stu-id="280c0-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="280c0-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="280c0-136">Next steps</span></span>
<span data-ttu-id="280c0-137">Zie voor een overzicht van de integratie van [overzicht van de integratie van SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="280c0-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="280c0-138">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="280c0-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
