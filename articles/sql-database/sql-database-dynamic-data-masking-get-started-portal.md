---
title: 'Azure-portal: SQL-Database dynamische-gegevensmaskering | Microsoft Docs'
description: Hoe tooget gestart met de SQL-Database dynamische-gegevensmaskering in hello Azure Portal
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="4ad0d-103">Aan de slag met SQL-Database dynamische-gegevensmaskering Hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4ad0d-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="4ad0d-104">Dit onderwerp leest u hoe tooimplement [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md) Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="4ad0d-105">U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of Hallo [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ad0d-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="4ad0d-106">Dynamische gegevens maskeren voor de database met de Hallo Azure Portal instellen</span><span class="sxs-lookup"><span data-stu-id="4ad0d-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="4ad0d-107">Start de Azure-Portal op Hallo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ad0d-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4ad0d-108">Blade voor toohello-instellingen van Hallo-database waarin Hallo gevoelige gegevens die u wilt dat toomask navigeren.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="4ad0d-109">Klik op Hallo **dynamische-Gegevensmaskering** tegel die Hallo Start **dynamische-Gegevensmaskering** configuratie blade.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="4ad0d-110">U kunt ook kunt u omlaag schuiven toohello **Operations** sectie en klik op **dynamische-Gegevensmaskering**.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="4ad0d-112">In Hallo **dynamische-Gegevensmaskering** configuratie blade ziet u mogelijk enkele databasekolommen die Hallo aanbevelingen-engine is gemarkeerd voor maskering.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="4ad0d-113">In volgorde tooaccept Hallo aanbevelingen, klikt u op **masker toevoegen** voor een of meer kolommen en een masker wordt gemaakt op basis van het standaardtype Hallo voor deze kolom.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="4ad0d-114">Hallo gegevensmaskeringsfunctie door te klikken op Hallo maskeringsregel en bewerken van Hallo dat maskering veld indeling tooa andere indeling van uw keuze, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="4ad0d-115">Ervoor tooclick worden **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="4ad0d-117">tooadd een masker voor elke kolom in de database, boven Hallo Hallo **dynamische-Gegevensmaskering** configuratie blade Klik **masker toevoegen** tooopen hello **maskeren regel toevoegen** configuratie-blade</span><span class="sxs-lookup"><span data-stu-id="4ad0d-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="4ad0d-119">Selecteer Hallo **Schema**, **tabel** en **kolom** toodefine Hallo aangewezen veld dat wordt gemaskeerd.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="4ad0d-120">Kies een **maskeren veldindeling** uit de lijst Hallo met gevoelige gegevens maskeren categorieën.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="4ad0d-122">Klik op **opslaan** in het maskeren van blade tooupdate Hallo regelset van de regels in Hallo dynamische-gegevensmaskering beleid maskeren Hallo van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="4ad0d-123">Type Hallo SQL-gebruikers of AAD-identiteiten die moeten worden uitgesloten van maskering en hebben toegang tot toohello ontmaskerd gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="4ad0d-124">Dit moet een door puntkomma's gescheiden lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="4ad0d-125">Houd er rekening mee dat gebruikers met beheerdersrechten altijd toegang tot toohello oorspronkelijke toegankelijk gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="4ad0d-127">toomake deze dus toepassingslaag Hallo kunnen gevoelige gegevens voor beschermde toepassingsgebruikers weergeven, Hallo SQL-gebruiker toevoegen of AAD-identiteit Hallo toepassing tooquery Hallo database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="4ad0d-128">Het is raadzaam dat deze lijst een minimum aantal bevoegde gebruikers toominimize blootstelling van Hallo gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="4ad0d-129">Klik op **opslaan** in Hallo gegevens maskeren blade toosave Hallo nieuwe of bijgewerkte maskering configuratiebeleid.</span><span class="sxs-lookup"><span data-stu-id="4ad0d-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ad0d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ad0d-130">Next steps</span></span>

* <span data-ttu-id="4ad0d-131">Zie voor een overzicht van dynamische gegevensmaskering [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ad0d-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="4ad0d-132">U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of Hallo [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ad0d-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
