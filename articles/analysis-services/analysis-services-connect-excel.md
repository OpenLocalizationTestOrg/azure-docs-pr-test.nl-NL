---
title: Verbinding maken met Azure analyseservices met Excel | Microsoft Docs
description: Informatie over het verbinding maken met een Azure Analysis Services-server met behulp van Excel.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="4b593-103">Verbinden met Excel</span><span class="sxs-lookup"><span data-stu-id="4b593-103">Connect with Excel</span></span>

<span data-ttu-id="4b593-104">Nadat u hebt een server in Azure gemaakt en geïmplementeerd een model in tabelvorm, kunt u verbinding maken en gebruiken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4b593-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="4b593-105">Verbinding maken in Excel</span><span class="sxs-lookup"><span data-stu-id="4b593-105">Connect in Excel</span></span>

<span data-ttu-id="4b593-106">Verbinding maken met een server in Excel wordt ondersteund door ophalen van gegevens in Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="4b593-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="4b593-107">Verbinding maken met behulp van de Wizard importeren in Power Pivot wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4b593-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="4b593-108">**Verbinding maken in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="4b593-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="4b593-109">In Excel 2016, op de **gegevens** lint, klikt u op **externe gegevens ophalen** > **van andere bronnen** > **van Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="4b593-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="4b593-110">In de Wizard Gegevensverbinding in **servernaam**, voer de naam van de server waaronder het protocol en de URI.</span><span class="sxs-lookup"><span data-stu-id="4b593-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="4b593-111">Klik op **aanmeldingsreferenties**, selecteer **gebruik de volgende gebruikersnaam en wachtwoord**, en typ vervolgens de organisatie-gebruikersnaam, bijvoorbeeld nancy@adventureworks.com, en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="4b593-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Verbinding maken van Excel-aanmelding](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="4b593-113">In **Database en tabel selecteren**, de database en het model of de perspectief selecteren en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="4b593-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Verbinding maken vanaf Selecteer Excel-gegevensmodel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="4b593-115">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4b593-115">See also</span></span>
<span data-ttu-id="4b593-116">[Clientbibliotheken](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="4b593-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="4b593-117">Beheren van uw server</span><span class="sxs-lookup"><span data-stu-id="4b593-117">Manage your server</span></span>](analysis-services-manage.md)     


