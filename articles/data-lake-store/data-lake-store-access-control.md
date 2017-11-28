---
title: aaaOverview van toegangsbeheer in Data Lake Store | Microsoft Docs
description: Begrijpen hoe toegangsbeheer werkt in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="c3938-103">Toegangsbeheer in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c3938-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="c3938-104">Azure Data Lake Store implementeert een model voor toegangsbeheer die is afgeleid van HDFS die op zijn beurt is afgeleid van Hallo POSIX model voor toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="c3938-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="c3938-105">In dit artikel bevat een overzicht van Hallo basisprincipes van Hallo model voor toegangsbeheer voor Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="c3938-106">toolearn meer informatie over Hallo HDFS model voor toegangsbeheer, Zie [HDFS machtigingen handleiding](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="c3938-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="c3938-107">Toegangsbeheerlijsten voor bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="c3938-107">Access control lists on files and folders</span></span>

<span data-ttu-id="c3938-108">Er zijn twee soorten toegangsbeheerlijsten (ACL's): **Toegangs-ACL's** en **Standaard-ACL's**.</span><span class="sxs-lookup"><span data-stu-id="c3938-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="c3938-109">**Toegang tot de ACL's**: deze control toegang tooan-object.</span><span class="sxs-lookup"><span data-stu-id="c3938-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="c3938-110">Bestanden en mappen hebben Toegangs-ACL's.</span><span class="sxs-lookup"><span data-stu-id="c3938-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="c3938-111">**ACL's standaard**: een 'sjabloon' van ACL's die zijn gekoppeld aan een map die bepalen Hallo toegang ACL's voor alle onderliggende items die in die map worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3938-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="c3938-112">Bestanden hebben geen Standaard-ACL's.</span><span class="sxs-lookup"><span data-stu-id="c3938-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="c3938-114">Zowel toegang ACL's en standaard ACL's hebben Hallo dezelfde structuur.</span><span class="sxs-lookup"><span data-stu-id="c3938-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="c3938-116">Veranderende Hallo ACL standaard op een bovenliggende heeft geen invloed op Hallo ACL Access of standaard ACL van onderliggende items die al bestaan.</span><span class="sxs-lookup"><span data-stu-id="c3938-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="c3938-117">Gebruikers en identiteiten</span><span class="sxs-lookup"><span data-stu-id="c3938-117">Users and identities</span></span>

<span data-ttu-id="c3938-118">Alle bestanden en mappen beschikken over verschillende machtigingen voor de volgende identiteiten:</span><span class="sxs-lookup"><span data-stu-id="c3938-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="c3938-119">Hallo die eigenaar is van de gebruiker van Hallo-bestand</span><span class="sxs-lookup"><span data-stu-id="c3938-119">hello owning user of hello file</span></span>
* <span data-ttu-id="c3938-120">Hallo eigenaar groep</span><span class="sxs-lookup"><span data-stu-id="c3938-120">hello owning group</span></span>
* <span data-ttu-id="c3938-121">Benoemde gebruikers</span><span class="sxs-lookup"><span data-stu-id="c3938-121">Named users</span></span>
* <span data-ttu-id="c3938-122">Benoemde groepen</span><span class="sxs-lookup"><span data-stu-id="c3938-122">Named groups</span></span>
* <span data-ttu-id="c3938-123">Alle andere gebruikers</span><span class="sxs-lookup"><span data-stu-id="c3938-123">All other users</span></span>

<span data-ttu-id="c3938-124">Hallo-identiteit van gebruikers en groepen zijn identiteiten met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3938-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="c3938-125">Dus tenzij anders vermeld, ', ' in de context van Data Lake Store Hallo kan de gebruiker: een Azure AD-gebruiker of een Azure AD-beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="c3938-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="c3938-126">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="c3938-126">Permissions</span></span>

<span data-ttu-id="c3938-127">Hallo-machtigingen voor een bestandssysteemobject zijn **lezen**, **schrijven**, en **Execute**, en ze kunnen worden gebruikt voor bestanden en mappen zoals weergegeven in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="c3938-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="c3938-128">File</span><span class="sxs-lookup"><span data-stu-id="c3938-128">File</span></span>     |   <span data-ttu-id="c3938-129">Map</span><span class="sxs-lookup"><span data-stu-id="c3938-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="c3938-130">**Lezen (L)**</span><span class="sxs-lookup"><span data-stu-id="c3938-130">**Read (R)**</span></span> | <span data-ttu-id="c3938-131">Hallo-inhoud van een bestand kan worden gelezen</span><span class="sxs-lookup"><span data-stu-id="c3938-131">Can read hello contents of a file</span></span> | <span data-ttu-id="c3938-132">Vereist **lezen** en **Execute** toolist Hallo inhoud van Hallo-map</span><span class="sxs-lookup"><span data-stu-id="c3938-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="c3938-133">**Schrijven (S)**</span><span class="sxs-lookup"><span data-stu-id="c3938-133">**Write (W)**</span></span> | <span data-ttu-id="c3938-134">Kan schrijven of tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3938-134">Can write or append tooa file</span></span> | <span data-ttu-id="c3938-135">Vereist **schrijven** en **Execute** toocreate onderliggende items in een map</span><span class="sxs-lookup"><span data-stu-id="c3938-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="c3938-136">**Uitvoeren (U)**</span><span class="sxs-lookup"><span data-stu-id="c3938-136">**Execute (X)**</span></span> | <span data-ttu-id="c3938-137">Betekent niet dat iets in de context Hallo van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c3938-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="c3938-138">Vereiste tootraverse Hallo onderliggende items van een map</span><span class="sxs-lookup"><span data-stu-id="c3938-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="c3938-139">Korte formulieren voor machtigingen</span><span class="sxs-lookup"><span data-stu-id="c3938-139">Short forms for permissions</span></span>

<span data-ttu-id="c3938-140">**RWX** gebruikte tooindicate is **lezen + schrijven + uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="c3938-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="c3938-141">Er bestaat een meer compacte numerieke vorm waarin **lezen = 4**, **schrijven = 2**, en **Execute = 1**, Hallo som waarvan vertegenwoordigt Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="c3938-142">Hier volgen enkele voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c3938-142">Following are some examples.</span></span>

| <span data-ttu-id="c3938-143">Numerieke vorm</span><span class="sxs-lookup"><span data-stu-id="c3938-143">Numeric form</span></span> | <span data-ttu-id="c3938-144">Verkorte vorm</span><span class="sxs-lookup"><span data-stu-id="c3938-144">Short form</span></span> |      <span data-ttu-id="c3938-145">Wat het betekent</span><span class="sxs-lookup"><span data-stu-id="c3938-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="c3938-146">7</span><span class="sxs-lookup"><span data-stu-id="c3938-146">7</span></span>            | <span data-ttu-id="c3938-147">LSU</span><span class="sxs-lookup"><span data-stu-id="c3938-147">RWX</span></span>        | <span data-ttu-id="c3938-148">Lezen + Schrijven + Uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c3938-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="c3938-149">5</span><span class="sxs-lookup"><span data-stu-id="c3938-149">5</span></span>            | <span data-ttu-id="c3938-150">L-U</span><span class="sxs-lookup"><span data-stu-id="c3938-150">R-X</span></span>        | <span data-ttu-id="c3938-151">Lezen + Uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c3938-151">Read + Execute</span></span>         |
| <span data-ttu-id="c3938-152">4</span><span class="sxs-lookup"><span data-stu-id="c3938-152">4</span></span>            | <span data-ttu-id="c3938-153">L--</span><span class="sxs-lookup"><span data-stu-id="c3938-153">R--</span></span>        | <span data-ttu-id="c3938-154">Lezen</span><span class="sxs-lookup"><span data-stu-id="c3938-154">Read</span></span>                   |
| <span data-ttu-id="c3938-155">0</span><span class="sxs-lookup"><span data-stu-id="c3938-155">0</span></span>            | ---        | <span data-ttu-id="c3938-156">Geen machtigingen</span><span class="sxs-lookup"><span data-stu-id="c3938-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="c3938-157">Machtigingen worden niet overgenomen</span><span class="sxs-lookup"><span data-stu-id="c3938-157">Permissions do not inherit</span></span>

<span data-ttu-id="c3938-158">Hallo POSIX-stijl-model dat wordt gebruikt door de Data Lake Store, zijn machtigingen voor een item opgeslagen in Hallo item zelf.</span><span class="sxs-lookup"><span data-stu-id="c3938-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="c3938-159">Met andere woorden, kunnen niet de machtigingen voor een item worden overgenomen van Hallo bovenliggende items.</span><span class="sxs-lookup"><span data-stu-id="c3938-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="c3938-160">Algemene scenario's gerelateerde toopermissions</span><span class="sxs-lookup"><span data-stu-id="c3938-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="c3938-161">Hieronder volgen enkele algemene scenario's toohelp u weten welke machtigingen zijn vereist tooperform bepaalde bewerkingen op een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c3938-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="c3938-162">Machtigingen nodig tooread een bestand</span><span class="sxs-lookup"><span data-stu-id="c3938-162">Permissions needed tooread a file</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="c3938-164">Hallo aanroeper behoeften voor Hallo bestand toobe lezen, **lezen** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="c3938-165">Voor alle mappen in de mapstructuur Hallo die Hallo-bestand bevatten hello, Hallo aanroeper behoeften **Execute** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="c3938-166">Machtigingen nodig tooappend tooa bestand</span><span class="sxs-lookup"><span data-stu-id="c3938-166">Permissions needed tooappend tooa file</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="c3938-168">Voor Hallo bestand toobe toegevoegd aan, Hallo aanroeper behoeften **schrijven** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="c3938-169">Voor alle mappen met Hallo bestand hello, Hallo aanroeper behoeften **Execute** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="c3938-170">Machtigingen nodig toodelete een bestand</span><span class="sxs-lookup"><span data-stu-id="c3938-170">Permissions needed toodelete a file</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="c3938-172">Voor de bovenliggende map Hallo Hallo aanroeper behoeften **schrijven + uitvoeren** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="c3938-173">Voor alle andere mappen in Hallo bestandspad hello, Hallo aanroeper behoeften **Execute** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="c3938-174">Schrijven machtigingen op Hallo-bestand zijn niet vereist toodelete deze zolang Hallo van de vorige twee voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="c3938-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="c3938-175">Machtigingen nodig tooenumerate een map</span><span class="sxs-lookup"><span data-stu-id="c3938-175">Permissions needed tooenumerate a folder</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="c3938-177">Hallo aanroeper behoeften voor Hallo map tooenumerate, **lezen + Execute** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="c3938-178">Voor alle bovenliggende mappen hello, Hallo aanroeper behoeften **Execute** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="c3938-179">Machtigingen weergeven in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c3938-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="c3938-180">Van Hallo **Data Explorer** blade Hallo Data Lake Store-account, klikt u op **toegang** toosee Hallo ACL's voor een bestand of map.</span><span class="sxs-lookup"><span data-stu-id="c3938-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="c3938-181">Klik op **toegang** toosee Hallo ACL's voor Hallo **catalogus** map onder Hallo **mydatastore** account.</span><span class="sxs-lookup"><span data-stu-id="c3938-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="c3938-183">Op deze blade geeft de bovenste gedeelte Hallo een overzicht van Hallo machtigingen die u hebt.</span><span class="sxs-lookup"><span data-stu-id="c3938-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="c3938-184">(In Hallo schermafbeelding is Hallo gebruiker Bob.) Hierna Hallo toegangsmachtigingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c3938-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="c3938-185">Daarna van Hallo **toegang** blade, klikt u op **eenvoudige weergave** toosee Hallo eenvoudiger weergave.</span><span class="sxs-lookup"><span data-stu-id="c3938-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="c3938-187">Klik op **geavanceerde weergave** toosee Hallo meer geavanceerde weergave, waarbij Hallo concepten van standaard ACL's, masker en supergebruiker worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c3938-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="c3938-189">Hallo supergebruiker</span><span class="sxs-lookup"><span data-stu-id="c3938-189">hello super-user</span></span>

<span data-ttu-id="c3938-190">Een supergebruiker heeft Hallo meeste rechten van gebruikers met alle Hallo in Hallo Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="c3938-191">Een supergebruiker:</span><span class="sxs-lookup"><span data-stu-id="c3938-191">A super-user:</span></span>

* <span data-ttu-id="c3938-192">RWX machtigingen te heeft**alle** bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="c3938-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="c3938-193">Kunt Hallo-machtigingen op een bestand of map wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3938-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="c3938-194">Kunt Hallo eigendom van gebruiker of groep van een bestand of map eigenaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3938-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="c3938-195">In Azure heeft een Data Lake Store-account meerdere Azure-rollen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="c3938-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="c3938-196">Eigenaren</span><span class="sxs-lookup"><span data-stu-id="c3938-196">Owners</span></span>
* <span data-ttu-id="c3938-197">Inzenders</span><span class="sxs-lookup"><span data-stu-id="c3938-197">Contributors</span></span>
* <span data-ttu-id="c3938-198">Lezers</span><span class="sxs-lookup"><span data-stu-id="c3938-198">Readers</span></span>

<span data-ttu-id="c3938-199">Iedereen in Hallo **eigenaars** rol voor een Data Lake Store-account wordt automatisch een supergebruiker voor dat account.</span><span class="sxs-lookup"><span data-stu-id="c3938-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="c3938-200">toolearn meer, Zie [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c3938-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="c3938-201">Als u wilt dat toocreate een aangepaste rol-gebaseerd-toegangsbeheer (RBAC)-functie die supergebruiker machtigingen heeft, moet deze toohave Hallo volgende machtigingen:</span><span class="sxs-lookup"><span data-stu-id="c3938-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="c3938-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="c3938-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="c3938-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="c3938-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="c3938-204">Hallo eigenaar gebruiker</span><span class="sxs-lookup"><span data-stu-id="c3938-204">hello owning user</span></span>

<span data-ttu-id="c3938-205">Hallo-gebruiker die Hallo-item gemaakt is automatisch Hallo eigendom van gebruiker Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="c3938-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="c3938-206">Een gebruiker die eigenaar is kan:</span><span class="sxs-lookup"><span data-stu-id="c3938-206">An owning user can:</span></span>

* <span data-ttu-id="c3938-207">Hallo-machtigingen van een bestand dat eigendom is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c3938-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="c3938-208">Hallo die eigenaar is van de groep van een bestand dat eigendom is zolang Hallo eigenaar gebruiker deel uitmaakt van de doelgroep Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3938-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="c3938-209">Hallo eigendom van gebruiker *kan niet* Hallo die eigenaar is van de gebruiker van een ander in eigendom van bestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3938-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="c3938-210">Alleen absoluut gebruikers kunnen Hallo die eigenaar is van de gebruiker van een bestand of map wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3938-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="c3938-211">Hallo eigenaar groep</span><span class="sxs-lookup"><span data-stu-id="c3938-211">hello owning group</span></span>

<span data-ttu-id="c3938-212">Hallo POSIX-ACL's, elke gebruiker is gekoppeld aan een "primaire groep'.</span><span class="sxs-lookup"><span data-stu-id="c3938-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="c3938-213">Gebruiker 'Els' kan bijvoorbeeld toohello 'Financiën' groep behoren.</span><span class="sxs-lookup"><span data-stu-id="c3938-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="c3938-214">Els mogelijk ook toomultiple groepen behoren, maar één groep altijd is aangewezen als haar primaire groep.</span><span class="sxs-lookup"><span data-stu-id="c3938-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="c3938-215">In het POSIX, wanneer een bestand, Alice maakt is Hallo die eigenaar is van de groep van het bestand ingesteld tooher primaire groep, die in dit geval 'Financiën'.</span><span class="sxs-lookup"><span data-stu-id="c3938-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="c3938-216">Wanneer een nieuw bestandssysteem item is gemaakt, toegewezen Data Lake Store een waarde toohello die eigenaar is van groep.</span><span class="sxs-lookup"><span data-stu-id="c3938-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="c3938-217">**Voorbeeld 1**: hoofdmap Hallo '/'.</span><span class="sxs-lookup"><span data-stu-id="c3938-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="c3938-218">Deze map wordt gemaakt wanneer een Data Lake Store-account wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3938-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="c3938-219">Hallo eigenaar groep ingesteld in dit geval toohello gebruiker Hallo-account hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3938-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="c3938-220">**Voorbeeld 2** (alle andere gevallen): wanneer een nieuw item is gemaakt, Hallo eigenaar groep wordt gekopieerd van Hallo bovenliggende map.</span><span class="sxs-lookup"><span data-stu-id="c3938-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="c3938-221">Hallo eigenaar groep kan worden gewijzigd door:</span><span class="sxs-lookup"><span data-stu-id="c3938-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="c3938-222">Alle supergebruikers.</span><span class="sxs-lookup"><span data-stu-id="c3938-222">Any super-users.</span></span>
* <span data-ttu-id="c3938-223">Hallo eigendom van gebruiker, als Hallo eigenaar gebruiker deel uitmaakt van de doelgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3938-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="c3938-224">Algoritme voor toegangscontrole</span><span class="sxs-lookup"><span data-stu-id="c3938-224">Access check algorithm</span></span>

<span data-ttu-id="c3938-225">Hallo volgende illustratie vertegenwoordigt Hallo toegang selectievakje algoritme voor het Data Lake Store-accounts.</span><span class="sxs-lookup"><span data-stu-id="c3938-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algoritme voor Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="c3938-227">Hallo masker en "effectieve machtigingen"</span><span class="sxs-lookup"><span data-stu-id="c3938-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="c3938-228">Hallo **masker** is een RWX waarde die is gebruikt toolimit toegang voor **benoemde gebruikers**, Hallo **die eigenaar is van groep**, en **benoemde groepen** wanneer u klaar Hallo toegang selectievakje algoritme uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c3938-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="c3938-229">Hier vindt u belangrijke concepten voor Hallo masker Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3938-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="c3938-230">Hallo masker maakt "effectieve machtigingen."</span><span class="sxs-lookup"><span data-stu-id="c3938-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="c3938-231">Dat wil zeggen, wijzigt de machtigingen Hallo Hallo gelijktijdig met toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="c3938-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="c3938-232">Hallo masker kan rechtstreeks worden bewerkt met Hallo bestandseigenaar en eventuele absoluut gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c3938-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="c3938-233">Hallo masker kunt machtigingen toocreate Hallo effectieve machtiging te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c3938-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="c3938-234">Hallo masker *kan niet* machtigingen toohello effectieve machtiging toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c3938-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="c3938-235">We bekijken enkele voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c3938-235">Let's look at some examples.</span></span> <span data-ttu-id="c3938-236">In Hallo voorbeeld te volgen, Hallo masker te ingesteld**RWX**, wat betekent dat masker Hallo machtigingen niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c3938-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="c3938-237">Hallo effectieve machtigingen van Hallo benoemde gebruiker, groep eigenaar en de naam van de groep niet worden gewijzigd tijdens het Hallo-toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="c3938-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="c3938-239">In Hallo voorbeeld te volgen, Hallo masker te ingesteld**R X**.</span><span class="sxs-lookup"><span data-stu-id="c3938-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="c3938-240">Dit betekent dat deze **wordt uitgeschakeld Hallo schrijfmachtigingen** voor **benoemde gebruiker**, **die eigenaar is van groep**, en **groep** gelijktijdig Hallo met toegang Controleer.</span><span class="sxs-lookup"><span data-stu-id="c3938-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="c3938-242">Ter referentie: dit is waar Hallo masker aan voor een bestand of map wordt weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c3938-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="c3938-244">Voor een nieuwe Data Lake Store-account, Hallo masker voor Hallo ACL Access en standaard ACL van hoofd-Hallo standaard map ('/') tooRWX.</span><span class="sxs-lookup"><span data-stu-id="c3938-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="c3938-245">Machtigingen voor nieuwe bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="c3938-245">Permissions on new files and folders</span></span>

<span data-ttu-id="c3938-246">Wanneer een nieuw bestand of map wordt gemaakt onder een bestaande map, bepaalt Hallo standaard ACL op Hallo bovenliggende map:</span><span class="sxs-lookup"><span data-stu-id="c3938-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="c3938-247">De Standaard-ACL en Toegangs-ACL voor een onderliggende map.</span><span class="sxs-lookup"><span data-stu-id="c3938-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="c3938-248">De Toegangs-ACL van een onderliggend bestand (bestanden beschikken niet over een Standaard-ACL).</span><span class="sxs-lookup"><span data-stu-id="c3938-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="c3938-249">Hallo ACL Access van een onderliggend bestand of map</span><span class="sxs-lookup"><span data-stu-id="c3938-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="c3938-250">Wanneer een onderliggend bestand of map wordt gemaakt, wordt als Hallo ACL Access van Hallo onderliggende bestand of map van het bovenliggende Hallo standaard ACL gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="c3938-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="c3938-251">Ook als **andere** gebruiker RWX machtigingen in van het bovenliggende Hallo standaard ACL heeft, wordt deze verwijderd uit de ACL Access Hallo onderliggend item.</span><span class="sxs-lookup"><span data-stu-id="c3938-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="c3938-253">In de meeste gevallen is Hallo voorgaande informatie moet alle u tooknow over hoe een onderliggend item toegang ACL wordt bepaald.</span><span class="sxs-lookup"><span data-stu-id="c3938-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="c3938-254">Echter, als u bekend met POSIX-systemen en gewenste toounderstand diepgaande hoe deze transformatie wordt voldaan bent, raadpleegt u Hallo sectie [Umask van rol bij het maken van Hallo toegang ACL voor nieuwe bestanden en mappen](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c3938-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="c3938-255">De Standaard-ACL voor een onderliggende map</span><span class="sxs-lookup"><span data-stu-id="c3938-255">A child folder's Default ACL</span></span>

<span data-ttu-id="c3938-256">Als een onderliggende map onder de bovenliggende map wordt gemaakt, wordt Hallo bovenliggende map standaard ACL wordt gekopieerd via omdat toohello onderliggende map standaard ACL.</span><span class="sxs-lookup"><span data-stu-id="c3938-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="c3938-258">Geavanceerde onderwerpen om ACL's in de Data Lake Store te begrijpen</span><span class="sxs-lookup"><span data-stu-id="c3938-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="c3938-259">Hier volgen enkele geavanceerde onderwerpen toohelp dat u begrijpt hoe de ACL's voor Data Lake Store-bestanden of mappen zijn bepaald.</span><span class="sxs-lookup"><span data-stu-id="c3938-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="c3938-260">Rol van Umask Hallo toegang ACL voor nieuwe bestanden en mappen maken</span><span class="sxs-lookup"><span data-stu-id="c3938-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="c3938-261">In een POSIX-compatibele systeem Hallo algemeen concept is dat umask is een 9-bits waarde op Hallo bovenliggende map die is gebruikt tootransform Hallo machtiging voor **eigendom van gebruiker**, **die eigenaar is van groep**, en  **andere** op Hallo ACL Access van een nieuw onderliggend bestand of map.</span><span class="sxs-lookup"><span data-stu-id="c3938-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="c3938-262">Hallo bits van een umask identificeren welke tooturn bits uitschakelen in de ACL Access Hallo onderliggend item.</span><span class="sxs-lookup"><span data-stu-id="c3938-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="c3938-263">Dus Hiermee tooselectively te voorkomen dat Hallo doorgifte van machtigingen voor **eigendom van gebruiker**, **die eigenaar is van groep**, en **andere**.</span><span class="sxs-lookup"><span data-stu-id="c3938-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="c3938-264">Hallo umask is in een HDFS-systeem, meestal een configuratieoptie op de hele site, die wordt beheerd door beheerders.</span><span class="sxs-lookup"><span data-stu-id="c3938-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="c3938-265">Data Lake Store gebruikt een **umask voor het hele account** die niet kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c3938-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="c3938-266">Hallo volgende tabel toont Hallo maskeren voor Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="c3938-267">Gebruikersgroep</span><span class="sxs-lookup"><span data-stu-id="c3938-267">User group</span></span>  | <span data-ttu-id="c3938-268">Instelling</span><span class="sxs-lookup"><span data-stu-id="c3938-268">Setting</span></span> | <span data-ttu-id="c3938-269">Invloed op de Toegangs-ACL van het nieuwe onderliggende item</span><span class="sxs-lookup"><span data-stu-id="c3938-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="c3938-270">Gebruiker die eigenaar is</span><span class="sxs-lookup"><span data-stu-id="c3938-270">Owning user</span></span> | ---     | <span data-ttu-id="c3938-271">Geen effect</span><span class="sxs-lookup"><span data-stu-id="c3938-271">No effect</span></span>                             |
| <span data-ttu-id="c3938-272">Groep die eigenaar is</span><span class="sxs-lookup"><span data-stu-id="c3938-272">Owning group</span></span>| ---     | <span data-ttu-id="c3938-273">Geen effect</span><span class="sxs-lookup"><span data-stu-id="c3938-273">No effect</span></span>                             |
| <span data-ttu-id="c3938-274">Overige</span><span class="sxs-lookup"><span data-stu-id="c3938-274">Other</span></span>       | <span data-ttu-id="c3938-275">LSU</span><span class="sxs-lookup"><span data-stu-id="c3938-275">RWX</span></span>     | <span data-ttu-id="c3938-276">Lezen + Schrijven + Uitvoeren verwijderen</span><span class="sxs-lookup"><span data-stu-id="c3938-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="c3938-277">Hallo volgende afbeelding ziet deze umask in actie.</span><span class="sxs-lookup"><span data-stu-id="c3938-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="c3938-278">Hallo netto effect is tooremove **lezen + schrijven + uitvoeren** voor **andere** gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c3938-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="c3938-279">Omdat Hallo umask is niet opgegeven voor bits voor **eigendom van gebruiker** en **die eigenaar is van groep**, deze machtigingen niet worden getransformeerd.</span><span class="sxs-lookup"><span data-stu-id="c3938-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL’s](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="c3938-281">een tijdelijke Hallo-bits</span><span class="sxs-lookup"><span data-stu-id="c3938-281">hello sticky bit</span></span>

<span data-ttu-id="c3938-282">een tijdelijke Hallo-bit is een geavanceerde functie van een POSIX-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="c3938-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="c3938-283">In de context van de Hallo van Data Lake Store is het onwaarschijnlijk dat een tijdelijke bits Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="c3938-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="c3938-284">Hallo volgende tabel ziet u de werking van een tijdelijke bits Hallo in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="c3938-285">Gebruikersgroep</span><span class="sxs-lookup"><span data-stu-id="c3938-285">User group</span></span>         | <span data-ttu-id="c3938-286">File</span><span class="sxs-lookup"><span data-stu-id="c3938-286">File</span></span>    | <span data-ttu-id="c3938-287">Map</span><span class="sxs-lookup"><span data-stu-id="c3938-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="c3938-288">Vergrendelde bit **UIT**</span><span class="sxs-lookup"><span data-stu-id="c3938-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="c3938-289">Geen effect</span><span class="sxs-lookup"><span data-stu-id="c3938-289">No effect</span></span>   | <span data-ttu-id="c3938-290">Geen effect.</span><span class="sxs-lookup"><span data-stu-id="c3938-290">No effect.</span></span>           |
| <span data-ttu-id="c3938-291">Vergrendelde bit **AAN**</span><span class="sxs-lookup"><span data-stu-id="c3938-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="c3938-292">Geen effect</span><span class="sxs-lookup"><span data-stu-id="c3938-292">No effect</span></span>   | <span data-ttu-id="c3938-293">Voorkomen dat iemand behalve **absoluut gebruikers** en Hallo **eigendom van gebruiker** van een onderliggend item van het verwijderen of hernoemen van onderliggende item.</span><span class="sxs-lookup"><span data-stu-id="c3938-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="c3938-294">een tijdelijke bits Hallo wordt niet weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c3938-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="c3938-295">Veelgestelde vragen over ACL's in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c3938-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="c3938-296">Hier volgen enkele vragen die vaak worden gesteld over ACL's in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="c3938-297">Heb ik tooenable ondersteuning voor de ACL's?</span><span class="sxs-lookup"><span data-stu-id="c3938-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="c3938-298">Nee.</span><span class="sxs-lookup"><span data-stu-id="c3938-298">No.</span></span> <span data-ttu-id="c3938-299">Toegangsbeheer via de ACL's is altijd ingeschakeld voor een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c3938-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="c3938-300">Welke machtigingen zijn vereist toorecursively het verwijderen van een map en de inhoud ervan?</span><span class="sxs-lookup"><span data-stu-id="c3938-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="c3938-301">Hallo bovenliggende map moet hebben **schrijven + uitvoeren** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="c3938-302">Hallo map toobe verwijderd en vereist dat elke map erin **lezen + schrijven + uitvoeren** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="c3938-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="c3938-303">U hoeft geen schrijfmachtigingen toodelete bestanden in mappen.</span><span class="sxs-lookup"><span data-stu-id="c3938-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="c3938-304">Bovendien hoofdmap Hallo ' / ' kunnen **nooit** worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c3938-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="c3938-305">Wie is eigenaar van een bestand of map Hallo?</span><span class="sxs-lookup"><span data-stu-id="c3938-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="c3938-306">Hallo maker van een bestand of map wordt Hallo eigenaar.</span><span class="sxs-lookup"><span data-stu-id="c3938-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="c3938-307">Welke groep is ingesteld als Hallo die eigenaar is van een bestand of map bij het maken van groep?</span><span class="sxs-lookup"><span data-stu-id="c3938-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="c3938-308">Hallo eigenaar groep wordt gekopieerd van Hallo die eigenaar is van de groep van Hallo bovenliggende map onder welke Hallo nieuw bestand of map wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3938-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="c3938-309">Ik ben Hallo die eigenaar is van de gebruiker van een bestand, maar ik heb Hallo RWX machtigingen die ik nodig.</span><span class="sxs-lookup"><span data-stu-id="c3938-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="c3938-310">Wat moet ik doen?</span><span class="sxs-lookup"><span data-stu-id="c3938-310">What do I do?</span></span>

<span data-ttu-id="c3938-311">Hallo eigenaar gebruiker kunt Hallo machtigingen wijzigen van Hallo bestand toogive zelf alle RWX machtigingen die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="c3938-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="c3938-312">Wanneer ik Kijk ACL's in Azure-portal Hallo Zie ik gebruikersnamen, maar via API's, Zie GUID's, waarom is dat?</span><span class="sxs-lookup"><span data-stu-id="c3938-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="c3938-313">Vermeldingen in het Hallo-ACL's worden opgeslagen als GUID's die overeenkomen met toousers in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3938-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="c3938-314">Hallo API's retourneren Hallo GUID's is.</span><span class="sxs-lookup"><span data-stu-id="c3938-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="c3938-315">Hello Azure-portal probeert toomake ACL's eenvoudiger toouse door vertalen Hallo GUID's naar beschrijvende namen indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="c3938-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="c3938-316">Waarom kan ik soms zien GUID's in Hallo ACL's bij gebruik van hello Azure-portal?</span><span class="sxs-lookup"><span data-stu-id="c3938-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="c3938-317">Een GUID wordt weergegeven wanneer het Hallo-gebruiker in Azure AD meer bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="c3938-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="c3938-318">Dit gebeurt meestal wanneer de gebruiker Hallo Hallo bedrijf heeft verlaten of als hun account in Azure AD is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c3938-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="c3938-319">Biedt Data Lake Store ondersteuning voor overname van ACL's?</span><span class="sxs-lookup"><span data-stu-id="c3938-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="c3938-320">Nee.</span><span class="sxs-lookup"><span data-stu-id="c3938-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="c3938-321">Wat is Hallo verschil tussen het masker en umask?</span><span class="sxs-lookup"><span data-stu-id="c3938-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="c3938-322">masker</span><span class="sxs-lookup"><span data-stu-id="c3938-322">mask</span></span> | <span data-ttu-id="c3938-323">umask</span><span class="sxs-lookup"><span data-stu-id="c3938-323">umask</span></span>|
|------|------|
| <span data-ttu-id="c3938-324">Hallo **masker** -eigenschap is beschikbaar op alle bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="c3938-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="c3938-325">Hallo **umask** is een eigenschap van Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c3938-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="c3938-326">Er is daarom alleen een enkele umask in Hallo Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c3938-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="c3938-327">Hallo masker eigenschap op een bestand of map kan worden gewijzigd door Hallo eigendom van gebruiker of groep van een bestand of een absoluut gebruiker die eigenaar is.</span><span class="sxs-lookup"><span data-stu-id="c3938-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="c3938-328">Hallo umask eigenschap kan niet worden gewijzigd door een gebruiker, zelfs supergebruiker.</span><span class="sxs-lookup"><span data-stu-id="c3938-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="c3938-329">Het is een onveranderbare, constante waarde.</span><span class="sxs-lookup"><span data-stu-id="c3938-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="c3938-330">de eigenschap mask Hello wordt gebruikt tijdens Hallo toegang selectievakje algoritme op runtime toodetermine of de gebruiker de juiste tooperform Hallo op de bewerking op een bestand of map is.</span><span class="sxs-lookup"><span data-stu-id="c3938-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="c3938-331">Hallo-rol van Hallo masker is toocreate 'effectieve machtigingen' Hallo gelijktijdig met toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="c3938-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="c3938-332">Hallo umask wordt niet gebruikt tijdens toegangscontrole helemaal.</span><span class="sxs-lookup"><span data-stu-id="c3938-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="c3938-333">Hallo umask is gebruikte toodetermine Hallo toegang ACL van nieuwe onderliggende items van een map.</span><span class="sxs-lookup"><span data-stu-id="c3938-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="c3938-334">Hallo-masker is een 3-bits RWX-waarde die toonamed gebruiker, benoemde groep en gebruiker die eigenaar is van toepassing op Hallo moment toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="c3938-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="c3938-335">Hallo umask is een 9-bits waarde die van toepassing eigendom van gebruiker is, groep eigenaar toohello en **andere** van een nieuw onderliggend.</span><span class="sxs-lookup"><span data-stu-id="c3938-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="c3938-336">Waar kan ik meer informatie over het POSIX-model voor toegangsbeheer?</span><span class="sxs-lookup"><span data-stu-id="c3938-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="c3938-337">POSIX met behulp van toegangsbeheerlijsten op Linux</span><span class="sxs-lookup"><span data-stu-id="c3938-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="c3938-338">Handleiding voor HDFS-machtigingen</span><span class="sxs-lookup"><span data-stu-id="c3938-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="c3938-339">Veelgestelde vragen over POSIX</span><span class="sxs-lookup"><span data-stu-id="c3938-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="c3938-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="c3938-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="c3938-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="c3938-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="c3938-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="c3938-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="c3938-343">POSIX ACL in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c3938-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="c3938-344">ACL met behulp van toegangsbeheerlijsten op Linux</span><span class="sxs-lookup"><span data-stu-id="c3938-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="c3938-345">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c3938-345">See also</span></span>

* [<span data-ttu-id="c3938-346">Overzicht van Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c3938-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
