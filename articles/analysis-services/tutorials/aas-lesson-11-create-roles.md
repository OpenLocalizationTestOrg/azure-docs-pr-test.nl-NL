---
<span data-ttu-id="3f8c9-101">titel: aaa "Azure Analysis Services-zelfstudie les 11: rollen maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate rollen in Hallo zelfstudie Azure Analysis Services-project.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="3f8c9-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="3f8c9-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="3f8c9-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="3f8c9-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="3f8c9-104">Les 11: Rollen maken</span><span class="sxs-lookup"><span data-stu-id="3f8c9-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3f8c9-105">In deze les gaat u rollen maken.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-105">In this lesson, you create roles.</span></span> <span data-ttu-id="3f8c9-106">Functies bieden model object en gegevens databasebeveiliging met tooonly toegang beperken die gebruikers die deel uitmaken van de rol.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="3f8c9-107">Elke rol is gekoppeld aan één machtiging: None, Read, Read and Process, Process of Administrator.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="3f8c9-108">Rollen kunnen tijdens de ontwerpfase van het model worden gedefinieerd met behulp van Role Manager.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="3f8c9-109">Nadat een model is geïmplementeerd, kunt u rollen beheren met behulp van SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="3f8c9-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="3f8c9-110">toolearn meer, Zie [rollen](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="3f8c9-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="3f8c9-111">Rollen maken is niet nodig toocomplete in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="3f8c9-112">Standaard Hallo-account die u momenteel bent aangemeld met beheerdersrechten heeft op Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="3f8c9-113">Echter, voor andere gebruikers in uw organisatie toobrowse met behulp van een client rapporteert, moet u ten minste één rol maken met lees machtigingen en die gebruikers toevoegen als leden.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="3f8c9-114">U gaat drie rollen maken:</span><span class="sxs-lookup"><span data-stu-id="3f8c9-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="3f8c9-115">**Verkoopmanager** – deze rol kunt gebruikers in uw organisatie waarvoor u toohave lezen machtiging tooall modelobjecten en gegevens wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="3f8c9-116">**Verkoop analist VS** – deze rol kan gebruikers bevatten in uw organisatie waarvoor u wilt dat alleen toobe kunnen toobrowse gegevens gerelateerd toosales in Hallo Verenigde Staten.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="3f8c9-117">Voor deze rol die u gebruikt een DAX-formule toodefine een *rijfilter*, waardoor er minder leden toobrowse alleen gegevens voor Hallo Verenigde Staten.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="3f8c9-118">**Beheerder** – deze rol kan gebruikers waarvoor u beheerdersrechten toohave, waardoor onbeperkte toegang en machtigingen tooperform administratieve taken op Hallo modeldatabase wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="3f8c9-119">Omdat Windows-gebruikers- en groepsaccounts in uw organisatie uniek zijn, kunt u de accounts van uw organisatie bepaalde toomembers kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="3f8c9-120">Echter, voor deze zelfstudie, u kunt ook Hallo leden leeg laten.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="3f8c9-121">Hallo effect van elke rol te testen later in les 12: analyseren in Excel.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="3f8c9-122">Geschatte tijd toocomplete deze les: **15 minuten**</span><span class="sxs-lookup"><span data-stu-id="3f8c9-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3f8c9-123">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f8c9-123">Prerequisites</span></span>  
<span data-ttu-id="3f8c9-124">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3f8c9-125">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 10: partities maken](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="3f8c9-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="3f8c9-126">Rollen maken</span><span class="sxs-lookup"><span data-stu-id="3f8c9-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="3f8c9-127">een gebruikersrol Sales Manager toocreate</span><span class="sxs-lookup"><span data-stu-id="3f8c9-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="3f8c9-128">Klik in Tabular Model Explorer met de rechtermuisknop op **Roles** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="3f8c9-129">Klik in Role Manager op **New**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="3f8c9-130">Klik op de nieuwe rol hello, en klik vervolgens in Hallo **naam** kolom Hallo rol te wijzigen**Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="3f8c9-131">In Hallo **machtigingen** kolom, klikt u op Hallo vervolgkeuzelijst en selecteer vervolgens Hallo **lezen** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="3f8c9-133">Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3f8c9-134">In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="3f8c9-135">een gebruikersrol verkoop analist VS toocreate</span><span class="sxs-lookup"><span data-stu-id="3f8c9-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="3f8c9-136">Klik in Role Manager op **New**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="3f8c9-137">Wijzig de naam van de rol Hallo te**verkoop analist VS**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="3f8c9-138">Geef deze rol de machtiging **Read**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="3f8c9-139">Klikt u op Hallo rijfilters tabblad, en vervolgens voor Hallo **DimGeography** tabel alleen in Hallo DAX Filter kolom type Hallo volgende formule:</span><span class="sxs-lookup"><span data-stu-id="3f8c9-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="3f8c9-140">Tooa Booleaans (waar/onwaar)-waarde moet worden omgezet in een rijfilter formule.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="3f8c9-141">Met deze formule geeft u aan dat alleen rijen met Hallo landcode regio-waarde van 'VS' zichtbaar toohello gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="3f8c9-143">Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3f8c9-144">In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="3f8c9-145">een gebruikersrol Administrator toocreate</span><span class="sxs-lookup"><span data-stu-id="3f8c9-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="3f8c9-146">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="3f8c9-147">Wijzig de naam van de rol Hallo te**beheerder**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="3f8c9-148">Geef deze rol de machtiging **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="3f8c9-149">Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="3f8c9-150">In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="3f8c9-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="3f8c9-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f8c9-151">What's next?</span></span>
<span data-ttu-id="3f8c9-152">[Les 12: Analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="3f8c9-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
