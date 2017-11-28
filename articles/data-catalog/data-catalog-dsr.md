---
title: de gegevensbronnen aaaSupported in Azure Data Catalog | Microsoft Docs
description: Dit artikel worden de specificaties van gegevensbronnen Hallo momenteel niet ondersteund.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="a2af8-103">Ondersteunde gegevensbronnen in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="a2af8-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="a2af8-104">U kunt metagegevens publiceren met behulp van een openbare API of een klik-eenmaal hulpprogramma voor registratie of door het handmatig invoeren van gegevens rechtstreeks toohello Azure Data Catalog web-portal.</span><span class="sxs-lookup"><span data-stu-id="a2af8-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="a2af8-105">Hallo volgende tabel geeft een overzicht van alle gegevensbronnen die worden ondersteund door de catalogus Hallo vandaag en Hallo publishing mogelijkheden voor elk.</span><span class="sxs-lookup"><span data-stu-id="a2af8-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="a2af8-106">Ook vermeld zijn Hallo hulpprogramma's voor externe gegevens die elke gegevensbron uit onze ervaring portal 'open-in' kan starten.</span><span class="sxs-lookup"><span data-stu-id="a2af8-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="a2af8-107">de tweede tabel Hallo bevat een meer technische specificatie van elke gegevensbron verbinding-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a2af8-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="a2af8-108">Lijst met ondersteunde gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="a2af8-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="a2af8-109"><b>Gegevensbronobject</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="a2af8-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="a2af8-111"><b>Handmatige invoer</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="a2af8-112"><b>Hulpprogramma voor registratie</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="a2af8-113"><b>Open in hulpprogramma 's</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="a2af8-114"><b>Opmerkingen bij de</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-115">Azure Data Lake Store-map</span><span class="sxs-lookup"><span data-stu-id="a2af8-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="a2af8-116">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-116">✓</span></span></td>
      <td><span data-ttu-id="a2af8-117">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-117">✓</span></span></td>
      <td><span data-ttu-id="a2af8-118">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-119">Azure Data Lake Store-bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="a2af8-120">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-120">✓</span></span></td>
      <td><span data-ttu-id="a2af8-121">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-121">✓</span></span></td>
      <td><span data-ttu-id="a2af8-122">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-123">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a2af8-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="a2af8-124">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-124">✓</span></span></td>
      <td><span data-ttu-id="a2af8-125">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-125">✓</span></span></td>
      <td><span data-ttu-id="a2af8-126">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-126">✓</span></span></td>
      <td><span data-ttu-id="a2af8-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-128">Azure-opslagmap</span><span class="sxs-lookup"><span data-stu-id="a2af8-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="a2af8-129">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-129">✓</span></span></td>
      <td><span data-ttu-id="a2af8-130">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-130">✓</span></span></td>
      <td><span data-ttu-id="a2af8-131">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-131">✓</span></span></td>
      <td><span data-ttu-id="a2af8-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-133">Azure Storage-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="a2af8-134">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-134">✓</span></span></td>
      <td><span data-ttu-id="a2af8-135">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-135">✓</span></span></td>
      <td><span data-ttu-id="a2af8-136">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-137">HDFS-directory</span><span class="sxs-lookup"><span data-stu-id="a2af8-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="a2af8-138">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-138">✓</span></span></td>
      <td><span data-ttu-id="a2af8-139">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-139">✓</span></span></td>
      <td><span data-ttu-id="a2af8-140">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-141">HDFS-bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-141">HDFS file</span></span></td>
      <td><span data-ttu-id="a2af8-142">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-142">✓</span></span></td>
      <td><span data-ttu-id="a2af8-143">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-143">✓</span></span></td>
      <td><span data-ttu-id="a2af8-144">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-145">Hive-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-145">Hive table</span></span></td>
      <td><span data-ttu-id="a2af8-146">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-146">✓</span></span></td>
      <td><span data-ttu-id="a2af8-147">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-147">✓</span></span></td>
      <td><span data-ttu-id="a2af8-148">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-148">✓</span></span></td>
      <td><span data-ttu-id="a2af8-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-150">Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-150">Hive view</span></span></td>
      <td><span data-ttu-id="a2af8-151">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-151">✓</span></span></td>
      <td><span data-ttu-id="a2af8-152">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-152">✓</span></span></td>
      <td><span data-ttu-id="a2af8-153">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-153">✓</span></span></td>
      <td><span data-ttu-id="a2af8-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-155">MySQL-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-155">MySQL table</span></span></td>
      <td><span data-ttu-id="a2af8-156">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-156">✓</span></span></td>
      <td><span data-ttu-id="a2af8-157">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-157">✓</span></span></td>
      <td><span data-ttu-id="a2af8-158">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-158">✓</span></span></td>
      <td><span data-ttu-id="a2af8-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-160">MySQL-weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-160">MySQL view</span></span></td>
      <td><span data-ttu-id="a2af8-161">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-161">✓</span></span></td>
      <td><span data-ttu-id="a2af8-162">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-162">✓</span></span></td>
      <td><span data-ttu-id="a2af8-163">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-163">✓</span></span></td>
      <td><span data-ttu-id="a2af8-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-165">Oracle-databasetabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="a2af8-166">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-166">✓</span></span></td>
      <td><span data-ttu-id="a2af8-167">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-167">✓</span></span></td>
      <td><span data-ttu-id="a2af8-168">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-168">✓</span></span></td>
      <td><span data-ttu-id="a2af8-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-170">Weergave van de Oracle-Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="a2af8-171">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-171">✓</span></span></td>
      <td><span data-ttu-id="a2af8-172">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-172">✓</span></span></td>
      <td><span data-ttu-id="a2af8-173">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-173">✓</span></span></td>
      <td><span data-ttu-id="a2af8-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-175">Andere (algemene actief)</span><span class="sxs-lookup"><span data-stu-id="a2af8-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="a2af8-176">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-176">✓</span></span></td>
      <td><span data-ttu-id="a2af8-177">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-178">Azure SQL Data Warehouse-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="a2af8-179">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-179">✓</span></span></td>
      <td><span data-ttu-id="a2af8-180">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-180">✓</span></span></td>
      <td><span data-ttu-id="a2af8-181">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-181">✓</span></span></td>
      <td><span data-ttu-id="a2af8-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-183">SQL Data Warehouse weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="a2af8-184">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-184">✓</span></span></td>
      <td><span data-ttu-id="a2af8-185">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-185">✓</span></span></td>
      <td><span data-ttu-id="a2af8-186">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-186">✓</span></span></td>
      <td><span data-ttu-id="a2af8-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-188">SQL Server Analysis Services-dimensie</span><span class="sxs-lookup"><span data-stu-id="a2af8-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="a2af8-189">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-189">✓</span></span></td>
      <td><span data-ttu-id="a2af8-190">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-190">✓</span></span></td>
      <td><span data-ttu-id="a2af8-191">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-191">✓</span></span></td>
      <td><span data-ttu-id="a2af8-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-193">SQL Server analyseservices KPI</span><span class="sxs-lookup"><span data-stu-id="a2af8-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="a2af8-194">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-194">✓</span></span></td>
      <td><span data-ttu-id="a2af8-195">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-195">✓</span></span></td>
      <td><span data-ttu-id="a2af8-196">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-196">✓</span></span></td>
      <td><span data-ttu-id="a2af8-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-198">SQL Server Analysis Services-meting</span><span class="sxs-lookup"><span data-stu-id="a2af8-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="a2af8-199">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-199">✓</span></span></td>
      <td><span data-ttu-id="a2af8-200">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-200">✓</span></span></td>
      <td><span data-ttu-id="a2af8-201">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-201">✓</span></span></td>
      <td><span data-ttu-id="a2af8-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-203">Tabel met SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a2af8-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="a2af8-204">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-204">✓</span></span></td>
      <td><span data-ttu-id="a2af8-205">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-205">✓</span></span></td>
      <td><span data-ttu-id="a2af8-206">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-206">✓</span></span></td>
      <td><span data-ttu-id="a2af8-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-208">SQL Server Reporting Services-rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="a2af8-209">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-209">✓</span></span></td>
      <td><span data-ttu-id="a2af8-210">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-210">✓</span></span></td>
      <td><span data-ttu-id="a2af8-211">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-211">✓</span></span></td>
      <td><span data-ttu-id="a2af8-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="a2af8-213"><font size=2>Native modus servers. SharePoint-modus wordt niet ondersteund.</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-214">SQL Server-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="a2af8-215">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-215">✓</span></span></td>
      <td><span data-ttu-id="a2af8-216">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-216">✓</span></span></td>
      <td><span data-ttu-id="a2af8-217">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-217">✓</span></span></td>
      <td><span data-ttu-id="a2af8-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-219">Weergave van SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="a2af8-220">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-220">✓</span></span></td>
      <td><span data-ttu-id="a2af8-221">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-221">✓</span></span></td>
      <td><span data-ttu-id="a2af8-222">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-222">✓</span></span></td>
      <td><span data-ttu-id="a2af8-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-224">Tabel voor Teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-224">Teradata table</span></span></td>
      <td><span data-ttu-id="a2af8-225">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-225">✓</span></span></td>
      <td><span data-ttu-id="a2af8-226">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-226">✓</span></span></td>
      <td><span data-ttu-id="a2af8-227">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-227">✓</span></span></td>
      <td><span data-ttu-id="a2af8-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-229">Weergave voor Teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-229">Teradata view</span></span></td>
      <td><span data-ttu-id="a2af8-230">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-230">✓</span></span></td>
      <td><span data-ttu-id="a2af8-231">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-231">✓</span></span></td>
      <td><span data-ttu-id="a2af8-232">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-232">✓</span></span></td>
      <td><span data-ttu-id="a2af8-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-234">SAP HANA-weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="a2af8-235">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-235">✓</span></span></td>
      <td><span data-ttu-id="a2af8-236">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-236">✓</span></span></td>
      <td><span data-ttu-id="a2af8-237">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-237">✓</span></span></td>
      <td><span data-ttu-id="a2af8-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-239">DB2-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-239">DB2 table</span></span></td>
      <td><span data-ttu-id="a2af8-240">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-240">✓</span></span></td>
      <td><span data-ttu-id="a2af8-241">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-241">✓</span></span></td>
      <td><span data-ttu-id="a2af8-242">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-243">DB2 weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-243">DB2 view</span></span></td>
      <td><span data-ttu-id="a2af8-244">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-244">✓</span></span></td>
      <td><span data-ttu-id="a2af8-245">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-245">✓</span></span></td>
      <td><span data-ttu-id="a2af8-246">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-247">Bestandssysteem bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-247">File system file</span></span></td>
      <td><span data-ttu-id="a2af8-248">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-249">FTP-map</span><span class="sxs-lookup"><span data-stu-id="a2af8-249">FTP directory</span></span></td>
      <td><span data-ttu-id="a2af8-250">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-250">✓</span></span></td>
      <td><span data-ttu-id="a2af8-251">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-251">✓</span></span></td>
      <td><span data-ttu-id="a2af8-252">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-253">FTP-bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-253">FTP file</span></span></td>
      <td><span data-ttu-id="a2af8-254">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-254">✓</span></span></td>
      <td><span data-ttu-id="a2af8-255">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-255">✓</span></span></td>
      <td><span data-ttu-id="a2af8-256">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-257">HTTP-rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-257">HTTP report</span></span></td>
      <td><span data-ttu-id="a2af8-258">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-259">HTTP-eindpunt</span><span class="sxs-lookup"><span data-stu-id="a2af8-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="a2af8-260">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-261">HTTP-bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-261">HTTP file</span></span></td>
      <td><span data-ttu-id="a2af8-262">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-263">OData-entiteitset</span><span class="sxs-lookup"><span data-stu-id="a2af8-263">OData entity set</span></span></td>
      <td><span data-ttu-id="a2af8-264">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-265">OData-functie</span><span class="sxs-lookup"><span data-stu-id="a2af8-265">OData function</span></span></td>
      <td><span data-ttu-id="a2af8-266">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-267">PostgreSQL-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="a2af8-268">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-268">✓</span></span></td>
      <td><span data-ttu-id="a2af8-269">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-269">✓</span></span></td>
      <td><span data-ttu-id="a2af8-270">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-271">PostgreSQL weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="a2af8-272">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-272">✓</span></span></td>
      <td><span data-ttu-id="a2af8-273">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-273">✓</span></span></td>
      <td><span data-ttu-id="a2af8-274">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-275">SAP HANA-weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="a2af8-276">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="a2af8-277">SalesForce-object</span><span class="sxs-lookup"><span data-stu-id="a2af8-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="a2af8-278">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-278">✓</span></span></td>
      <td><span data-ttu-id="a2af8-279">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-279">✓</span></span></td>
      <td><span data-ttu-id="a2af8-280">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-281">SharePoint-lijst</span><span class="sxs-lookup"><span data-stu-id="a2af8-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="a2af8-282">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-283">Azure DB Cosmos-verzameling</span><span class="sxs-lookup"><span data-stu-id="a2af8-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="a2af8-284">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-284">✓</span></span></td>
      <td><span data-ttu-id="a2af8-285">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-285">✓</span></span></td>
      <td><span data-ttu-id="a2af8-286">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-287">Algemene ODBC-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="a2af8-288">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-288">✓</span></span></td>
      <td><span data-ttu-id="a2af8-289">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-289">✓</span></span></td>
      <td><span data-ttu-id="a2af8-290">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-291">Algemene ODBC-weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="a2af8-292">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-292">✓</span></span></td>
      <td><span data-ttu-id="a2af8-293">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-293">✓</span></span></td>
      <td><span data-ttu-id="a2af8-294">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-295">Cassandra tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="a2af8-296">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-296">✓</span></span></td>
      <td><span data-ttu-id="a2af8-297">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-297">✓</span></span></td>
      <td><span data-ttu-id="a2af8-298">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="a2af8-299"><font size=2>Als een algemene ODBC-asset publiceren</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-300">Cassandra weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="a2af8-301">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-301">✓</span></span></td>
      <td><span data-ttu-id="a2af8-302">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-302">✓</span></span></td>
      <td><span data-ttu-id="a2af8-303">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="a2af8-304"><font size=2>Als een algemene ODBC-asset publiceren</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-305">Sybase-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-305">Sybase table</span></span></td>
      <td><span data-ttu-id="a2af8-306">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-306">✓</span></span></td>
      <td><span data-ttu-id="a2af8-307">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-307">✓</span></span></td>
      <td><span data-ttu-id="a2af8-308">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-309">Sybase weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-309">Sybase view</span></span></td>
      <td><span data-ttu-id="a2af8-310">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-310">✓</span></span></td>
      <td><span data-ttu-id="a2af8-311">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-311">✓</span></span></td>
      <td><span data-ttu-id="a2af8-312">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-313">MongoDB-tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="a2af8-314">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-314">✓</span></span></td>
      <td><span data-ttu-id="a2af8-315">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-315">✓</span></span></td>
      <td><span data-ttu-id="a2af8-316">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="a2af8-317"><font size=2>Als een algemene ODBC-asset publiceren</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-318">MongoDB weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="a2af8-319">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-319">✓</span></span></td>
      <td><span data-ttu-id="a2af8-320">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-320">✓</span></span></td>
      <td><span data-ttu-id="a2af8-321">✓</span><span class="sxs-lookup"><span data-stu-id="a2af8-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="a2af8-322"><font size=2>Als een algemene ODBC-asset publiceren</font></span><span class="sxs-lookup"><span data-stu-id="a2af8-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="a2af8-323">Als u ondersteuning voor aanvullende bronnen nodig, een functie aanvraag toohello indienen [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a2af8-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="a2af8-324">Gegevensbron Verwijzingsspecificatie</span><span class="sxs-lookup"><span data-stu-id="a2af8-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="a2af8-325">Hallo **DSL structuur** kolom in de volgende tabel Hallo bevat alleen Hallo verbindingseigenschappen voor 'adres' eigenschappenverzameling die worden gebruikt door Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="a2af8-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="a2af8-326">Dat wil zeggen, mag 'adres' eigenschappenverzameling andere eigenschappen van Hallo-gegevensbron waarmee Azure Data Catalog zich blijft voordoen, maar maakt geen gebruik van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a2af8-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="a2af8-327"><b>Type gegevensbron</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="a2af8-328"><b>Activatype</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="a2af8-329"><b>Objecttypen</b></span><span class="sxs-lookup"><span data-stu-id="a2af8-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="a2af8-330"><b>DSL-structuur<b></span><span class="sxs-lookup"><span data-stu-id="a2af8-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a2af8-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="a2af8-332">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-332">Container</span></span></td>
      <td><span data-ttu-id="a2af8-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="a2af8-333">Data Lake</span></span></td>
      <td><span data-ttu-id="a2af8-334">
        <font size=2>Protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="a2af8-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="a2af8-335">Verificatie: {basis, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="a2af8-336">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-336">Address:</span></span> <br><span data-ttu-id="a2af8-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a2af8-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="a2af8-339">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-339">Table</span></span></td>
      <td><span data-ttu-id="a2af8-340">Map, bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-340">Directory, file</span></span></td>
      <td><span data-ttu-id="a2af8-341">
        <font size=2>Protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="a2af8-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="a2af8-342">Verificatie: {basis, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="a2af8-343">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-343">Address:</span></span> <br><span data-ttu-id="a2af8-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-345">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a2af8-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="a2af8-346">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-346">Container</span></span></td>
      <td><span data-ttu-id="a2af8-347">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-347">Container</span></span></td>
      <td><span data-ttu-id="a2af8-348">
        <font size=2>Protocol: azure-BLOB 's</span><span class="sxs-lookup"><span data-stu-id="a2af8-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="a2af8-349">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-350">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-350">Address:</span></span> <br><span data-ttu-id="a2af8-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domein</span><span class="sxs-lookup"><span data-stu-id="a2af8-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="a2af8-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;account</span><span class="sxs-lookup"><span data-stu-id="a2af8-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="a2af8-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;container</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-354">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a2af8-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="a2af8-355">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-355">Table</span></span></td>
      <td><span data-ttu-id="a2af8-356">BLOB, directory</span><span class="sxs-lookup"><span data-stu-id="a2af8-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="a2af8-357">
        <font size=2>Protocol: azure-BLOB 's</span><span class="sxs-lookup"><span data-stu-id="a2af8-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="a2af8-358">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-359">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-359">Address:</span></span> <br><span data-ttu-id="a2af8-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domein</span><span class="sxs-lookup"><span data-stu-id="a2af8-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="a2af8-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;account</span><span class="sxs-lookup"><span data-stu-id="a2af8-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="a2af8-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;container</span><span class="sxs-lookup"><span data-stu-id="a2af8-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="a2af8-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;naam</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-364">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a2af8-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="a2af8-365">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-365">Container</span></span></td>
      <td><span data-ttu-id="a2af8-366">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-366">Container</span></span></td>
      <td><span data-ttu-id="a2af8-367">
        <font size=2>Protocol: azure-tabellen</span><span class="sxs-lookup"><span data-stu-id="a2af8-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="a2af8-368">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-369">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-369">Address:</span></span> <br><span data-ttu-id="a2af8-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domein</span><span class="sxs-lookup"><span data-stu-id="a2af8-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="a2af8-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;account</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-372">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a2af8-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="a2af8-373">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-373">Table</span></span></td>
      <td><span data-ttu-id="a2af8-374">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-374">Table</span></span></td>
      <td><span data-ttu-id="a2af8-375">
        <font size=2>Protocol: azure-tabellen</span><span class="sxs-lookup"><span data-stu-id="a2af8-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="a2af8-376">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-377">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-377">Address:</span></span> <br><span data-ttu-id="a2af8-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;domein</span><span class="sxs-lookup"><span data-stu-id="a2af8-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="a2af8-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;account</span><span class="sxs-lookup"><span data-stu-id="a2af8-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="a2af8-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;naam</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="a2af8-381">Cosmos</span></span></td>
      <td><span data-ttu-id="a2af8-382">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-382">Container</span></span></td>
      <td><span data-ttu-id="a2af8-383">Virtueel cluster</span><span class="sxs-lookup"><span data-stu-id="a2af8-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="a2af8-384">
        <font size=2>Protocol: cosmos</span><span class="sxs-lookup"><span data-stu-id="a2af8-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="a2af8-385">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-386">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-386">Address:</span></span> <br><span data-ttu-id="a2af8-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="a2af8-388">Cosmos</span></span></td>
      <td><span data-ttu-id="a2af8-389">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-389">Table</span></span></td>
      <td><span data-ttu-id="a2af8-390">Stream, stream is ingesteld, weergeven</span><span class="sxs-lookup"><span data-stu-id="a2af8-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="a2af8-391">
        <font size=2>Protocol: cosmos</span><span class="sxs-lookup"><span data-stu-id="a2af8-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="a2af8-392">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-393">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-393">Address:</span></span> <br><span data-ttu-id="a2af8-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="a2af8-395">Datazen</span></span></td>
      <td><span data-ttu-id="a2af8-396">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-396">Container</span></span></td>
      <td><span data-ttu-id="a2af8-397">Site</span><span class="sxs-lookup"><span data-stu-id="a2af8-397">Site</span></span></td>
      <td><span data-ttu-id="a2af8-398">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-399">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-400">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-400">Address:</span></span> <br><span data-ttu-id="a2af8-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="a2af8-402">Datazen</span></span></td>
      <td><span data-ttu-id="a2af8-403">Rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-403">Report</span></span></td>
      <td><span data-ttu-id="a2af8-404">Rapport, dashboard</span><span class="sxs-lookup"><span data-stu-id="a2af8-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="a2af8-405">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-406">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-407">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-407">Address:</span></span> <br><span data-ttu-id="a2af8-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-409">DB2</span><span class="sxs-lookup"><span data-stu-id="a2af8-409">DB2</span></span></td>
      <td><span data-ttu-id="a2af8-410">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-410">Container</span></span></td>
      <td><span data-ttu-id="a2af8-411">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-411">Database</span></span></td>
      <td><span data-ttu-id="a2af8-412">
        <font size=2>Protocol: db2</span><span class="sxs-lookup"><span data-stu-id="a2af8-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="a2af8-413">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-414">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-414">Address:</span></span> <br><span data-ttu-id="a2af8-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-417">DB2</span><span class="sxs-lookup"><span data-stu-id="a2af8-417">DB2</span></span></td>
      <td><span data-ttu-id="a2af8-418">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-418">Table</span></span></td>
      <td><span data-ttu-id="a2af8-419">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-419">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-420">
        <font size=2>Protocol: db2</span><span class="sxs-lookup"><span data-stu-id="a2af8-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="a2af8-421">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-422">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-422">Address:</span></span> <br><span data-ttu-id="a2af8-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-427">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="a2af8-427">File system</span></span></td>
      <td><span data-ttu-id="a2af8-428">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-428">Table</span></span></td>
      <td><span data-ttu-id="a2af8-429">File</span><span class="sxs-lookup"><span data-stu-id="a2af8-429">File</span></span></td>
      <td><span data-ttu-id="a2af8-430">
        <font size=2>Protocol: bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="a2af8-431">Verificatie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="a2af8-432">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-432">Address:</span></span> <br><span data-ttu-id="a2af8-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pad</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-434">FTP</span><span class="sxs-lookup"><span data-stu-id="a2af8-434">FTP</span></span></td>
      <td><span data-ttu-id="a2af8-435">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-435">Table</span></span></td>
      <td><span data-ttu-id="a2af8-436">Map, bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-436">Directory, file</span></span></td>
      <td><span data-ttu-id="a2af8-437">
        <font size=2>Protocol: ftp</span><span class="sxs-lookup"><span data-stu-id="a2af8-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="a2af8-438">Verificatie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="a2af8-439">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-439">Address:</span></span> <br><span data-ttu-id="a2af8-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="a2af8-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="a2af8-442">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-442">Container</span></span></td>
      <td><span data-ttu-id="a2af8-443">Cluster</span><span class="sxs-lookup"><span data-stu-id="a2af8-443">Cluster</span></span></td>
      <td><span data-ttu-id="a2af8-444">
        <font size=2>Protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="a2af8-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="a2af8-445">Verificatie: {basis, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="a2af8-446">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-446">Address:</span></span> <br><span data-ttu-id="a2af8-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="a2af8-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="a2af8-449">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-449">Table</span></span></td>
      <td><span data-ttu-id="a2af8-450">Map, bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-450">Directory, file</span></span></td>
      <td><span data-ttu-id="a2af8-451">
        <font size=2>Protocol: webhdfs</span><span class="sxs-lookup"><span data-stu-id="a2af8-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="a2af8-452">Verificatie: {basis, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="a2af8-453">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-453">Address:</span></span> <br><span data-ttu-id="a2af8-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-455">Hive</span><span class="sxs-lookup"><span data-stu-id="a2af8-455">Hive</span></span></td>
      <td><span data-ttu-id="a2af8-456">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-456">Container</span></span></td>
      <td><span data-ttu-id="a2af8-457">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-457">Database</span></span></td>
      <td><span data-ttu-id="a2af8-458">
        <font size=2>Protocol: hive</span><span class="sxs-lookup"><span data-stu-id="a2af8-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="a2af8-459">Verificatie: {HDInsight, basic, username, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="a2af8-460">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-460">Address:</span></span> <br><span data-ttu-id="a2af8-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="a2af8-463">connectionProperties:</span></span> <br><span data-ttu-id="a2af8-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-465">Hive</span><span class="sxs-lookup"><span data-stu-id="a2af8-465">Hive</span></span></td>
      <td><span data-ttu-id="a2af8-466">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-466">Table</span></span></td>
      <td><span data-ttu-id="a2af8-467">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-467">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-468">
        <font size=2>Protocol: hive</span><span class="sxs-lookup"><span data-stu-id="a2af8-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="a2af8-469">Verificatie: {HDInsight, basic, username, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="a2af8-470">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-470">Address:</span></span> <br><span data-ttu-id="a2af8-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="a2af8-474">connectionProperties:</span></span> <br><span data-ttu-id="a2af8-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;serverProtocol: {hive2}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="a2af8-476">HTTP</span></span></td>
      <td><span data-ttu-id="a2af8-477">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-477">Container</span></span></td>
      <td><span data-ttu-id="a2af8-478">Site</span><span class="sxs-lookup"><span data-stu-id="a2af8-478">Site</span></span></td>
      <td><span data-ttu-id="a2af8-479">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-480">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-481">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-481">Address:</span></span> <br><span data-ttu-id="a2af8-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="a2af8-483">HTTP</span></span></td>
      <td><span data-ttu-id="a2af8-484">Rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-484">Report</span></span></td>
      <td><span data-ttu-id="a2af8-485">Rapport, dashboard</span><span class="sxs-lookup"><span data-stu-id="a2af8-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="a2af8-486">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-487">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-488">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-488">Address:</span></span> <br><span data-ttu-id="a2af8-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="a2af8-490">HTTP</span></span></td>
      <td><span data-ttu-id="a2af8-491">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-491">Table</span></span></td>
      <td><span data-ttu-id="a2af8-492">Eindpunt, bestand</span><span class="sxs-lookup"><span data-stu-id="a2af8-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="a2af8-493">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-494">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-495">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-495">Address:</span></span> <br><span data-ttu-id="a2af8-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="a2af8-497">MySQL</span></span></td>
      <td><span data-ttu-id="a2af8-498">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-498">Container</span></span></td>
      <td><span data-ttu-id="a2af8-499">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-499">Database</span></span></td>
      <td><span data-ttu-id="a2af8-500">
        <font size=2>Protocol: mysql</span><span class="sxs-lookup"><span data-stu-id="a2af8-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="a2af8-501">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-502">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-502">Address:</span></span> <br><span data-ttu-id="a2af8-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="a2af8-505">MySQL</span></span></td>
      <td><span data-ttu-id="a2af8-506">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-506">Table</span></span></td>
      <td><span data-ttu-id="a2af8-507">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-507">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-508">
        <font size=2>Protocol: mysql</span><span class="sxs-lookup"><span data-stu-id="a2af8-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="a2af8-509">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-510">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-510">Address:</span></span> <br><span data-ttu-id="a2af8-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-514">OData</span><span class="sxs-lookup"><span data-stu-id="a2af8-514">OData</span></span></td>
      <td><span data-ttu-id="a2af8-515">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-515">Container</span></span></td>
      <td><span data-ttu-id="a2af8-516">Entiteitscontainer</span><span class="sxs-lookup"><span data-stu-id="a2af8-516">Entity container</span></span></td>
      <td><span data-ttu-id="a2af8-517">
        <font size=2>Protocol: odata</span><span class="sxs-lookup"><span data-stu-id="a2af8-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="a2af8-518">Verificatie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="a2af8-519">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-519">Address:</span></span> <br><span data-ttu-id="a2af8-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-521">OData</span><span class="sxs-lookup"><span data-stu-id="a2af8-521">OData</span></span></td>
      <td><span data-ttu-id="a2af8-522">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-522">Table</span></span></td>
      <td><span data-ttu-id="a2af8-523">Entiteitset, functie</span><span class="sxs-lookup"><span data-stu-id="a2af8-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="a2af8-524">
        <font size=2>Protocol: odata</span><span class="sxs-lookup"><span data-stu-id="a2af8-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="a2af8-525">Verificatie: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="a2af8-526">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-526">Address:</span></span> <br><span data-ttu-id="a2af8-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</span><span class="sxs-lookup"><span data-stu-id="a2af8-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="a2af8-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;resource</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-529">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="a2af8-530">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-530">Container</span></span></td>
      <td><span data-ttu-id="a2af8-531">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-531">Database</span></span></td>
      <td><span data-ttu-id="a2af8-532">
        <font size=2>Protocol: oracle</span><span class="sxs-lookup"><span data-stu-id="a2af8-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="a2af8-533">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-534">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-534">Address:</span></span> <br><span data-ttu-id="a2af8-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-537">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="a2af8-538">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-538">Table</span></span></td>
      <td><span data-ttu-id="a2af8-539">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-539">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-540">
        <font size=2>Protocol: oracle</span><span class="sxs-lookup"><span data-stu-id="a2af8-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="a2af8-541">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-542">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-542">Address:</span></span> <br><span data-ttu-id="a2af8-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a2af8-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="a2af8-548">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-548">Container</span></span></td>
      <td><span data-ttu-id="a2af8-549">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-549">Database</span></span></td>
      <td><span data-ttu-id="a2af8-550">
        <font size=2>Protocol: postgresql</span><span class="sxs-lookup"><span data-stu-id="a2af8-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="a2af8-551">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-552">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-552">Address:</span></span> <br><span data-ttu-id="a2af8-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a2af8-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="a2af8-556">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-556">Table</span></span></td>
      <td><span data-ttu-id="a2af8-557">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-557">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-558">
        <font size=2>Protocol: postgresql</span><span class="sxs-lookup"><span data-stu-id="a2af8-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="a2af8-559">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-560">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-560">Address:</span></span> <br><span data-ttu-id="a2af8-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="a2af8-565">Power BI</span></span></td>
      <td><span data-ttu-id="a2af8-566">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-566">Container</span></span></td>
      <td><span data-ttu-id="a2af8-567">Site</span><span class="sxs-lookup"><span data-stu-id="a2af8-567">Site</span></span></td>
      <td><span data-ttu-id="a2af8-568">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-569">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-570">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-570">Address:</span></span> <br><span data-ttu-id="a2af8-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="a2af8-572">Power BI</span></span></td>
      <td><span data-ttu-id="a2af8-573">Rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-573">Report</span></span></td>
      <td><span data-ttu-id="a2af8-574">Rapport, dashboard</span><span class="sxs-lookup"><span data-stu-id="a2af8-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="a2af8-575">
        <font size=2>Protocol: http</span><span class="sxs-lookup"><span data-stu-id="a2af8-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="a2af8-576">Verificatie: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="a2af8-577">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-577">Address:</span></span> <br><span data-ttu-id="a2af8-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="a2af8-579">Power Query</span></span></td>
      <td><span data-ttu-id="a2af8-580">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-580">Table</span></span></td>
      <td><span data-ttu-id="a2af8-581">Gegevens mashup</span><span class="sxs-lookup"><span data-stu-id="a2af8-581">Data mashup</span></span></td>
      <td><span data-ttu-id="a2af8-582">
        <font size=2>Protocol: power-query</span><span class="sxs-lookup"><span data-stu-id="a2af8-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="a2af8-583">Verificatie: {oauth}</span><span class="sxs-lookup"><span data-stu-id="a2af8-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="a2af8-584">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-584">Address:</span></span> <br><span data-ttu-id="a2af8-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-586">SalesForce</span><span class="sxs-lookup"><span data-stu-id="a2af8-586">Salesforce</span></span></td>
      <td><span data-ttu-id="a2af8-587">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-587">Table</span></span></td>
      <td><span data-ttu-id="a2af8-588">Object</span><span class="sxs-lookup"><span data-stu-id="a2af8-588">Object</span></span></td>
      <td><span data-ttu-id="a2af8-589">
        <font size=2>Protocol: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="a2af8-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="a2af8-590">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-591">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-591">Address:</span></span> <br><span data-ttu-id="a2af8-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loginServer</span><span class="sxs-lookup"><span data-stu-id="a2af8-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="a2af8-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;klasse</span><span class="sxs-lookup"><span data-stu-id="a2af8-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="a2af8-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;itemName</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a2af8-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="a2af8-596">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-596">Container</span></span></td>
      <td><span data-ttu-id="a2af8-597">Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-597">Server</span></span></td>
      <td><span data-ttu-id="a2af8-598">
        <font size=2>Protocol: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="a2af8-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="a2af8-599">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-600">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-600">Address:</span></span> <br><span data-ttu-id="a2af8-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a2af8-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="a2af8-603">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-603">Table</span></span></td>
      <td><span data-ttu-id="a2af8-604">Weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-604">View</span></span></td>
      <td><span data-ttu-id="a2af8-605">
        <font size=2>Protocol: sap hana-sql</span><span class="sxs-lookup"><span data-stu-id="a2af8-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="a2af8-606">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-607">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-607">Address:</span></span> <br><span data-ttu-id="a2af8-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2af8-611">SharePoint</span></span></td>
      <td><span data-ttu-id="a2af8-612">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-612">Table</span></span></td>
      <td><span data-ttu-id="a2af8-613">Lijst</span><span class="sxs-lookup"><span data-stu-id="a2af8-613">List</span></span></td>
      <td><span data-ttu-id="a2af8-614">
        <font size=2>Protocollen: sharepoint-lijst</span><span class="sxs-lookup"><span data-stu-id="a2af8-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="a2af8-615">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-616">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-616">Address:</span></span> <br><span data-ttu-id="a2af8-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a2af8-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="a2af8-619">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a2af8-619">Command</span></span></td>
      <td><span data-ttu-id="a2af8-620">Opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="a2af8-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="a2af8-621">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-622">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-623">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-623">Address:</span></span> <br><span data-ttu-id="a2af8-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-628">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a2af8-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="a2af8-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="a2af8-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="a2af8-630">Functie met tabelwaarden</span><span class="sxs-lookup"><span data-stu-id="a2af8-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="a2af8-631">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-632">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-633">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-633">Address:</span></span> <br><span data-ttu-id="a2af8-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-638">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a2af8-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="a2af8-639">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-639">Container</span></span></td>
      <td><span data-ttu-id="a2af8-640">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-640">Database</span></span></td>
      <td><span data-ttu-id="a2af8-641">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-642">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-643">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-643">Address:</span></span> <br><span data-ttu-id="a2af8-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-646">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a2af8-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="a2af8-647">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-647">Table</span></span></td>
      <td><span data-ttu-id="a2af8-648">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-648">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-649">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-650">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-651">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-651">Address:</span></span> <br><span data-ttu-id="a2af8-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-656">SQL Server</span></span></td>
      <td><span data-ttu-id="a2af8-657">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a2af8-657">Command</span></span></td>
      <td><span data-ttu-id="a2af8-658">Opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="a2af8-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="a2af8-659">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-660">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-661">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-661">Address:</span></span> <br><span data-ttu-id="a2af8-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-666">SQL Server</span></span></td>
      <td><span data-ttu-id="a2af8-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="a2af8-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="a2af8-668">Functie met tabelwaarden</span><span class="sxs-lookup"><span data-stu-id="a2af8-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="a2af8-669">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-670">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-671">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-671">Address:</span></span> <br><span data-ttu-id="a2af8-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-676">SQL Server</span></span></td>
      <td><span data-ttu-id="a2af8-677">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-677">Container</span></span></td>
      <td><span data-ttu-id="a2af8-678">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-678">Database</span></span></td>
      <td><span data-ttu-id="a2af8-679">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-680">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-681">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-681">Address:</span></span> <br><span data-ttu-id="a2af8-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-684">SQL Server</span></span></td>
      <td><span data-ttu-id="a2af8-685">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-685">Table</span></span></td>
      <td><span data-ttu-id="a2af8-686">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-686">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-687">
        <font size=2>Protocol: tds</span><span class="sxs-lookup"><span data-stu-id="a2af8-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="a2af8-688">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-689">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-689">Address:</span></span> <br><span data-ttu-id="a2af8-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-694">SQL Server Analysis Services multidimensionale</span><span class="sxs-lookup"><span data-stu-id="a2af8-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="a2af8-695">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-695">Container</span></span></td>
      <td><span data-ttu-id="a2af8-696">Model</span><span class="sxs-lookup"><span data-stu-id="a2af8-696">Model</span></span></td>
      <td><span data-ttu-id="a2af8-697">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-698">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-699">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-699">Address:</span></span> <br><span data-ttu-id="a2af8-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-703">SQL Server Analysis Services multidimensionale</span><span class="sxs-lookup"><span data-stu-id="a2af8-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="a2af8-704">KPI</span><span class="sxs-lookup"><span data-stu-id="a2af8-704">KPI</span></span></td>
      <td><span data-ttu-id="a2af8-705">KPI</span><span class="sxs-lookup"><span data-stu-id="a2af8-705">KPI</span></span></td>
      <td><span data-ttu-id="a2af8-706">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-707">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-708">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-708">Address:</span></span> <br><span data-ttu-id="a2af8-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-714">SQL Server Analysis Services multidimensionale</span><span class="sxs-lookup"><span data-stu-id="a2af8-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="a2af8-715">meting</span><span class="sxs-lookup"><span data-stu-id="a2af8-715">Measure</span></span></td>
      <td><span data-ttu-id="a2af8-716">meting</span><span class="sxs-lookup"><span data-stu-id="a2af8-716">Measure</span></span></td>
      <td><span data-ttu-id="a2af8-717">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-718">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-719">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-719">Address:</span></span> <br><span data-ttu-id="a2af8-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-725">SQL Server Analysis Services multidimensionale</span><span class="sxs-lookup"><span data-stu-id="a2af8-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="a2af8-726">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-726">Table</span></span></td>
      <td><span data-ttu-id="a2af8-727">Dimensie</span><span class="sxs-lookup"><span data-stu-id="a2af8-727">Dimension</span></span></td>
      <td><span data-ttu-id="a2af8-728">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-729">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-730">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-730">Address:</span></span> <br><span data-ttu-id="a2af8-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {dimensie}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-736">SQL Server Analysis Services in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="a2af8-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="a2af8-737">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-737">Container</span></span></td>
      <td><span data-ttu-id="a2af8-738">Model</span><span class="sxs-lookup"><span data-stu-id="a2af8-738">Model</span></span></td>
      <td><span data-ttu-id="a2af8-739">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-740">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-741">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-741">Address:</span></span> <br><span data-ttu-id="a2af8-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-745">SQL Server Analysis Services in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="a2af8-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="a2af8-746">KPI</span><span class="sxs-lookup"><span data-stu-id="a2af8-746">KPI</span></span></td>
      <td><span data-ttu-id="a2af8-747">KPI</span><span class="sxs-lookup"><span data-stu-id="a2af8-747">KPI</span></span></td>
      <td><span data-ttu-id="a2af8-748">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-749">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-750">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-750">Address:</span></span> <br><span data-ttu-id="a2af8-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {KPI}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-756">SQL Server Analysis Services in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="a2af8-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="a2af8-757">meting</span><span class="sxs-lookup"><span data-stu-id="a2af8-757">Measure</span></span></td>
      <td><span data-ttu-id="a2af8-758">meting</span><span class="sxs-lookup"><span data-stu-id="a2af8-758">Measure</span></span></td>
      <td><span data-ttu-id="a2af8-759">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-760">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-761">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-761">Address:</span></span> <br><span data-ttu-id="a2af8-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {Measure}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-767">SQL Server Analysis Services in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="a2af8-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="a2af8-768">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-768">Table</span></span></td>
      <td><span data-ttu-id="a2af8-769">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-769">Table</span></span></td>
      <td><span data-ttu-id="a2af8-770">
        <font size=2>Protocol: analyseservices</span><span class="sxs-lookup"><span data-stu-id="a2af8-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="a2af8-771">Verificatie: {windows, basic, anoniem, geen}</span><span class="sxs-lookup"><span data-stu-id="a2af8-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="a2af8-772">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-772">Address:</span></span> <br><span data-ttu-id="a2af8-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;objectType: {Table}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="a2af8-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="a2af8-779">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-779">Container</span></span></td>
      <td><span data-ttu-id="a2af8-780">Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-780">Server</span></span></td>
      <td><span data-ttu-id="a2af8-781">
        <font size=2>Protocol: reporting services</span><span class="sxs-lookup"><span data-stu-id="a2af8-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="a2af8-782">Verificatie: {windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-782">Authentication: {windows}</span></span> <br><span data-ttu-id="a2af8-783">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-783">Address:</span></span> <br><span data-ttu-id="a2af8-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;versie: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="a2af8-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="a2af8-787">Rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-787">Report</span></span></td>
      <td><span data-ttu-id="a2af8-788">Rapport</span><span class="sxs-lookup"><span data-stu-id="a2af8-788">Report</span></span></td>
      <td><span data-ttu-id="a2af8-789">
        <font size=2>Protocol: reporting services</span><span class="sxs-lookup"><span data-stu-id="a2af8-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="a2af8-790">Verificatie: {windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-790">Authentication: {windows}</span></span> <br><span data-ttu-id="a2af8-791">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-791">Address:</span></span> <br><span data-ttu-id="a2af8-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pad</span><span class="sxs-lookup"><span data-stu-id="a2af8-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="a2af8-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;versie: {ReportingService2010}</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-795">Teradata</span></span></td>
      <td><span data-ttu-id="a2af8-796">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-796">Container</span></span></td>
      <td><span data-ttu-id="a2af8-797">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-797">Database</span></span></td>
      <td><span data-ttu-id="a2af8-798">
        <font size=2>Protocol: teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="a2af8-799">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-800">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-800">Address:</span></span> <br><span data-ttu-id="a2af8-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-803">Teradata</span></span></td>
      <td><span data-ttu-id="a2af8-804">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-804">Table</span></span></td>
      <td><span data-ttu-id="a2af8-805">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-805">Table, view</span></span></td>
      <td><span data-ttu-id="a2af8-806">
        <font size=2>Protocol: teradata</span><span class="sxs-lookup"><span data-stu-id="a2af8-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="a2af8-807">Verificatie: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="a2af8-808">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-808">Address:</span></span> <br><span data-ttu-id="a2af8-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="a2af8-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="a2af8-813">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-813">Container</span></span></td>
      <td><span data-ttu-id="a2af8-814">Model</span><span class="sxs-lookup"><span data-stu-id="a2af8-814">Model</span></span></td>
      <td><span data-ttu-id="a2af8-815">
        <font size="2">Protocol: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="a2af8-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="a2af8-816">Verificatie: {windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-816">Authentication: {windows}</span></span> <br><span data-ttu-id="a2af8-817">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-817">Address:</span></span> <br><span data-ttu-id="a2af8-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</span><span class="sxs-lookup"><span data-stu-id="a2af8-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="a2af8-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Versie</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="a2af8-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="a2af8-822">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-822">Table</span></span></td>
      <td><span data-ttu-id="a2af8-823">Entiteit</span><span class="sxs-lookup"><span data-stu-id="a2af8-823">Entity</span></span></td>
      <td><span data-ttu-id="a2af8-824">
        <font size="2">Protocol: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="a2af8-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="a2af8-825">Verificatie: {windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-825">Authentication: {windows}</span></span> <br><span data-ttu-id="a2af8-826">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-826">Address:</span></span> <br><span data-ttu-id="a2af8-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</span><span class="sxs-lookup"><span data-stu-id="a2af8-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="a2af8-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model</span><span class="sxs-lookup"><span data-stu-id="a2af8-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="a2af8-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Versie</span><span class="sxs-lookup"><span data-stu-id="a2af8-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="a2af8-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;entiteit</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a2af8-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="a2af8-832">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-832">Container</span></span></td>
      <td><span data-ttu-id="a2af8-833">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-833">Database</span></span></td>
      <td><span data-ttu-id="a2af8-834">
        <font size=2>Protocol: document-db</span><span class="sxs-lookup"><span data-stu-id="a2af8-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="a2af8-835">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-836">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-836">Address:</span></span> <br><span data-ttu-id="a2af8-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</span><span class="sxs-lookup"><span data-stu-id="a2af8-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="a2af8-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a2af8-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="a2af8-840">Verzameling</span><span class="sxs-lookup"><span data-stu-id="a2af8-840">Collection</span></span></td>
      <td><span data-ttu-id="a2af8-841">Verzameling</span><span class="sxs-lookup"><span data-stu-id="a2af8-841">Collection</span></span></td>
      <td><span data-ttu-id="a2af8-842">
        <font size=2>Protocol: document-db</span><span class="sxs-lookup"><span data-stu-id="a2af8-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="a2af8-843">Verificatie: {azure--toegangssleutel}</span><span class="sxs-lookup"><span data-stu-id="a2af8-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="a2af8-844">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-844">Address:</span></span> <br><span data-ttu-id="a2af8-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;URL</span><span class="sxs-lookup"><span data-stu-id="a2af8-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="a2af8-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;verzameling</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-848">Algemene ODBC</span><span class="sxs-lookup"><span data-stu-id="a2af8-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="a2af8-849">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-849">Container</span></span></td>
      <td><span data-ttu-id="a2af8-850">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-850">Database</span></span></td>
      <td><span data-ttu-id="a2af8-851">
        <font size=2>Protocol: odbc</span><span class="sxs-lookup"><span data-stu-id="a2af8-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="a2af8-852">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-853">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-853">Address:</span></span> <br><span data-ttu-id="a2af8-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opties</span><span class="sxs-lookup"><span data-stu-id="a2af8-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="a2af8-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-856">Algemene ODBC</span><span class="sxs-lookup"><span data-stu-id="a2af8-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="a2af8-857">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-857">Table</span></span></td>
      <td><span data-ttu-id="a2af8-858">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-858">Table, View</span></span></td>
      <td><span data-ttu-id="a2af8-859">
        <font size=2>Protocol: odbc</span><span class="sxs-lookup"><span data-stu-id="a2af8-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="a2af8-860">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-861">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-861">Address:</span></span> <br><span data-ttu-id="a2af8-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Opties</span><span class="sxs-lookup"><span data-stu-id="a2af8-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="a2af8-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</span><span class="sxs-lookup"><span data-stu-id="a2af8-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="a2af8-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="a2af8-866">Sybase</span></span></td>
      <td><span data-ttu-id="a2af8-867">Container</span><span class="sxs-lookup"><span data-stu-id="a2af8-867">Container</span></span></td>
      <td><span data-ttu-id="a2af8-868">Database</span><span class="sxs-lookup"><span data-stu-id="a2af8-868">Database</span></span></td>
      <td><span data-ttu-id="a2af8-869">
        <font size=2>Protocol: sybase</span><span class="sxs-lookup"><span data-stu-id="a2af8-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="a2af8-870">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-871">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-871">address:</span></span> <br><span data-ttu-id="a2af8-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="a2af8-874">Sybase</span></span></td>
      <td><span data-ttu-id="a2af8-875">Tabel</span><span class="sxs-lookup"><span data-stu-id="a2af8-875">Table</span></span></td>
      <td><span data-ttu-id="a2af8-876">Tabel, weergave</span><span class="sxs-lookup"><span data-stu-id="a2af8-876">Table, View</span></span></td>
      <td><span data-ttu-id="a2af8-877">
        <font size=2>Protocol: sybase</span><span class="sxs-lookup"><span data-stu-id="a2af8-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="a2af8-878">Verificatie: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="a2af8-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="a2af8-879">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-879">address:</span></span> <br><span data-ttu-id="a2af8-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server</span><span class="sxs-lookup"><span data-stu-id="a2af8-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="a2af8-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database</span><span class="sxs-lookup"><span data-stu-id="a2af8-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="a2af8-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;schema</span><span class="sxs-lookup"><span data-stu-id="a2af8-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="a2af8-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;object</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="a2af8-884">Andere (geen Hallo hierboven)</span><span class="sxs-lookup"><span data-stu-id="a2af8-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="a2af8-885">
        <font size=2>Protocol: algemene-asset</span><span class="sxs-lookup"><span data-stu-id="a2af8-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="a2af8-886">Adres:</span><span class="sxs-lookup"><span data-stu-id="a2af8-886">Address:</span></span> <br><span data-ttu-id="a2af8-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;item-id hebt</font>
      </span><span class="sxs-lookup"><span data-stu-id="a2af8-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
