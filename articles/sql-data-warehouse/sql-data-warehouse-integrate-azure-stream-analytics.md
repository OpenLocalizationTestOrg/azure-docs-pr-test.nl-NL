---
title: Azure Stream Analytics gebruiken met SQL datawarehouse | Microsoft Docs
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
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="b121a-103">Azure Stream Analytics gebruiken met SQL datawarehouse</span><span class="sxs-lookup"><span data-stu-id="b121a-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="b121a-104">Azure Stream Analytics is een volledig beheerde service lage latentie, maximaal beschikbare, schaalbare complexe verwerking van gebeurtenissen geven via het streamen van gegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="b121a-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="b121a-105">U kunt de basisbegrippen door te lezen [Inleiding tot Azure Stream Analytics][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="b121a-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="b121a-106">U kunt vervolgens informatie over het maken van een end-to-end-oplossing met Stream Analytics volgens de [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b121a-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="b121a-107">In dit artikel leert u hoe u uw Azure SQL Data Warehouse-database als uitvoerlocatie voor uw stoom Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="b121a-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b121a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b121a-108">Prerequisites</span></span>
<span data-ttu-id="b121a-109">Voer eerst de volgende stappen in de [aan de slag met Azure Stream Analytics] [ Get started using Azure Stream Analytics] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b121a-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="b121a-110">De invoer van een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="b121a-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="b121a-111">Configureren en starten van de gebeurtenis generator-toepassing</span><span class="sxs-lookup"><span data-stu-id="b121a-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="b121a-112">Inrichten van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="b121a-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="b121a-113">Taak invoer- en query opgeven</span><span class="sxs-lookup"><span data-stu-id="b121a-113">Specify job input and query</span></span>

<span data-ttu-id="b121a-114">Vervolgens maakt u een Azure SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="b121a-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="b121a-115">Geef de taakuitvoer: Azure SQL Data Warehouse-database</span><span class="sxs-lookup"><span data-stu-id="b121a-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="b121a-116">Stap 1</span><span class="sxs-lookup"><span data-stu-id="b121a-116">Step 1</span></span>
<span data-ttu-id="b121a-117">Klik in de Stream Analytics-taak op **uitvoer** vanaf de bovenkant van de pagina en klik vervolgens op **uitvoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b121a-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="b121a-118">Stap 2</span><span class="sxs-lookup"><span data-stu-id="b121a-118">Step 2</span></span>
<span data-ttu-id="b121a-119">Selecteer de SQL-Database en klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="b121a-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="b121a-120">Stap 3</span><span class="sxs-lookup"><span data-stu-id="b121a-120">Step 3</span></span>
<span data-ttu-id="b121a-121">Voer de volgende waarden op de volgende pagina:</span><span class="sxs-lookup"><span data-stu-id="b121a-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="b121a-122">*Uitvoer Alias*: een beschrijvende naam voor de taakuitvoer van deze.</span><span class="sxs-lookup"><span data-stu-id="b121a-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="b121a-123">*Abonnement*:</span><span class="sxs-lookup"><span data-stu-id="b121a-123">*Subscription*:</span></span>
  * <span data-ttu-id="b121a-124">Als uw SQL Data Warehouse-database zich in hetzelfde abonnement als de Stream Analytics-taak, selecteert u SQL-Database gebruiken uit het huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="b121a-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="b121a-125">Als uw database zich in een ander abonnement, selecteert u gebruik SQL Database in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="b121a-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="b121a-126">*Database*: Geef de naam van een doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="b121a-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="b121a-127">*Servernaam*: Geef de naam van de server voor de database die u zojuist hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b121a-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="b121a-128">De klassieke Azure Portal kunt u deze worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="b121a-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="b121a-129">*Gebruikersnaam*: Geef de gebruikersnaam van een account met schrijfmachtigingen voor de database.</span><span class="sxs-lookup"><span data-stu-id="b121a-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="b121a-130">*Wachtwoord*: Geef het wachtwoord op voor het opgegeven gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="b121a-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="b121a-131">*Tabel*: Geef de naam van de doeltabel in de database.</span><span class="sxs-lookup"><span data-stu-id="b121a-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="b121a-132">Stap 4</span><span class="sxs-lookup"><span data-stu-id="b121a-132">Step 4</span></span>
<span data-ttu-id="b121a-133">Klik op de knop controleren de taakuitvoer van deze toevoegen en te controleren dat Stream Analytics verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="b121a-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="b121a-134">Als de verbinding met de database is geslaagd, ziet u een melding aan de onderkant van de portal.</span><span class="sxs-lookup"><span data-stu-id="b121a-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="b121a-135">U kunt klikken op verbinding testen onderaan om de verbinding met de database te testen.</span><span class="sxs-lookup"><span data-stu-id="b121a-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b121a-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b121a-136">Next steps</span></span>
<span data-ttu-id="b121a-137">Zie voor een overzicht van de integratie van [overzicht van de integratie van SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="b121a-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="b121a-138">Zie [Overzicht van SQL Data Warehouse voor ontwikkelaars][SQL Data Warehouse development overview] voor meer tips voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b121a-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
