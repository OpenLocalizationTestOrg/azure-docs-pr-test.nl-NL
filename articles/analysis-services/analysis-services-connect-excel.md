---
title: aaaConnect tooAzure Analysis Services met Excel | Microsoft Docs
description: Meer informatie over hoe tooconnect tooan Azure Analysis Services-server met behulp van Excel.
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="d784c-103">Verbinden met Excel</span><span class="sxs-lookup"><span data-stu-id="d784c-103">Connect with Excel</span></span>

<span data-ttu-id="d784c-104">Nadat u hebt gemaakt van een server in Azure en een model in tabelvorm tooit geïmplementeerd, kunt u bent klaar tooconnect en begint met het verkennen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d784c-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="d784c-105">Verbinding maken in Excel</span><span class="sxs-lookup"><span data-stu-id="d784c-105">Connect in Excel</span></span>

<span data-ttu-id="d784c-106">Tooa-server in Excel verbinding maken wordt met behulp van de gegevens ophalen in Excel 2016 ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d784c-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="d784c-107">Verbinding maken met behulp van de Wizard tabel importeren Hallo in Power Pivot wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d784c-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="d784c-108">**tooconnect in Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="d784c-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="d784c-109">In Excel 2016 op Hallo **gegevens** lint, klikt u op **externe gegevens ophalen** > **van andere bronnen** > **van Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="d784c-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="d784c-110">Hallo in de Wizard Gegevensverbinding **servernaam**, Voer Hallo servernaam waaronder het protocol en de URI.</span><span class="sxs-lookup"><span data-stu-id="d784c-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="d784c-111">Klik op **aanmeldingsreferenties**, selecteer **gebruik Hallo volgende gebruikersnaam en wachtwoord**, en typ vervolgens het organisatie-gebruikersnaam hello, bijvoorbeeld nancy@adventureworks.com, en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d784c-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Verbinding maken van Excel-aanmelding](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="d784c-113">In **Database en tabel selecteren**Hallo-database en model of perspectief selecteren en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d784c-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Verbinding maken vanaf Selecteer Excel-gegevensmodel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="d784c-115">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d784c-115">See also</span></span>
<span data-ttu-id="d784c-116">[Clientbibliotheken](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="d784c-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="d784c-117">Beheren van uw server</span><span class="sxs-lookup"><span data-stu-id="d784c-117">Manage your server</span></span>](analysis-services-manage.md)     


