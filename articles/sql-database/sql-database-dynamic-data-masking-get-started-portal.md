---
title: 'Azure-portal: SQL-Database dynamische-gegevensmaskering | Microsoft Docs'
description: Hoe u aan de slag met SQL-Database dynamische gegevensmaskering in de Azure Portal
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
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="fba04-103">Aan de slag met SQL-Database dynamische-gegevensmaskering met de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fba04-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="fba04-104">Dit onderwerp leest u hoe u implementeert [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md) met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fba04-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="fba04-105">U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of de [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="fba04-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="fba04-106">Dynamische gegevens maskeren voor uw database met de Azure Portal instellen</span><span class="sxs-lookup"><span data-stu-id="fba04-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="fba04-107">Starten van de Azure Portal op [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fba04-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fba04-108">Navigeer naar de instellingenblade van de database met de gevoelige gegevens die u wilt maskeren.</span><span class="sxs-lookup"><span data-stu-id="fba04-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="fba04-109">Klik op de **dynamische-Gegevensmaskering** gestart tegel de **dynamische-Gegevensmaskering** configuratie blade.</span><span class="sxs-lookup"><span data-stu-id="fba04-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="fba04-110">U kunt ook Schuif omlaag naar de **Operations** sectie en klik op **dynamische-Gegevensmaskering**.</span><span class="sxs-lookup"><span data-stu-id="fba04-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="fba04-112">In de **dynamische-Gegevensmaskering** configuratie blade ziet u mogelijk enkele databasekolommen die voor de engine voor aanbevelingen voor maskering is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="fba04-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="fba04-113">Om de aanbevelingen hebt geaccepteerd, klikt u op **masker toevoegen** voor een of meer kolommen en een masker wordt gemaakt op basis van het standaardtype voor deze kolom.</span><span class="sxs-lookup"><span data-stu-id="fba04-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="fba04-114">U kunt de maskeringsfunctie wijzigen door te klikken op de maskeringsregel en bewerken van het maskeren veldindeling naar een andere indeling van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="fba04-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="fba04-115">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="fba04-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="fba04-117">Toevoegen van een masker voor elke kolom in de database, aan de bovenkant van de **dynamische-Gegevensmaskering** configuratie blade Klik **masker toevoegen** openen de **maskeren regel toevoegen** configuratie Blade</span><span class="sxs-lookup"><span data-stu-id="fba04-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="fba04-119">Selecteer de **Schema**, **tabel** en **kolom** voor het definiëren van het veld dat is opgegeven die wordt gemaskeerd.</span><span class="sxs-lookup"><span data-stu-id="fba04-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="fba04-120">Kies een **maskeren veldindeling** uit de lijst met gevoelige gegevens maskeren categorieën.</span><span class="sxs-lookup"><span data-stu-id="fba04-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="fba04-122">Klik op **opslaan** in de blade van de regel voor het bijwerken van de reeks regels in het beleid voor dynamische gegevensmaskering maskeren maskeren gegevens.</span><span class="sxs-lookup"><span data-stu-id="fba04-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="fba04-123">Geef de SQL-gebruikers of AAD-identiteiten die moeten worden uitgesloten van maskering en hebben toegang tot de ontmaskerd gevoelige gegevens.</span><span class="sxs-lookup"><span data-stu-id="fba04-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="fba04-124">Dit moet een door puntkomma's gescheiden lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fba04-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="fba04-125">Houd er rekening mee dat gebruikers met beheerdersrechten altijd toegang tot de oorspronkelijke gegevens toegankelijk is hebben.</span><span class="sxs-lookup"><span data-stu-id="fba04-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="fba04-127">Als u wilt ervoor zorgen dat de toepassingslaag gevoelige gegevens voor de bevoegde toepassingsgebruikers kunt weergeven, voeg de SQL-gebruiker of AAD-identiteit de toepassing wordt gebruikt om te zoeken in de database.</span><span class="sxs-lookup"><span data-stu-id="fba04-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="fba04-128">Het is raadzaam dat deze lijst een minimum aantal bevoegde gebruikers om te beperken van blootstelling van de gevoelige gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fba04-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="fba04-129">Klik op **opslaan** in de blade van de configuratie voor het opslaan van de nieuwe of bijgewerkte maskeren gegevens maskeren beleid.</span><span class="sxs-lookup"><span data-stu-id="fba04-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fba04-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fba04-130">Next steps</span></span>

* <span data-ttu-id="fba04-131">Zie voor een overzicht van dynamische gegevensmaskering [dynamische gegevensmaskering](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fba04-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="fba04-132">U kunt ook implementeren dat maskering met behulp van dynamische gegevens [cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) of de [REST-API](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="fba04-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>