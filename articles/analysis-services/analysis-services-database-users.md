---
title: aaaManage rollen en gebruikers in Azure Analysis Services-database | Microsoft Docs
description: Meer informatie over hoe toomanage rollen en gebruikers op een Analysis Services-server in Azure-database.
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="d7b53-103">Databaserollen en gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="d7b53-103">Manage database roles and users</span></span>

<span data-ttu-id="d7b53-104">Op databaseniveau Hallo-model, moeten alle gebruikers tooa rol behoren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="d7b53-105">Gebruikers met bepaalde machtigingen voor de modeldatabase Hallo definiëren rollen</span><span class="sxs-lookup"><span data-stu-id="d7b53-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="d7b53-106">Een gebruiker of beveiligingsgroep groep toegevoegd tooa rol moet een account in een Azure AD-tenant in Hallo hebben hetzelfde abonnement als Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="d7b53-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="d7b53-107">Andere afhankelijk van Hallo hulpprogramma waarmee u hoe u rollen definiëren is, maar Hallo effect is dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7b53-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="d7b53-108">Rolmachtigingen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="d7b53-108">Role permissions include:</span></span>
*  <span data-ttu-id="d7b53-109">**Beheerder** -gebruikers volledige machtigingen voor Hallo database hebben.</span><span class="sxs-lookup"><span data-stu-id="d7b53-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="d7b53-110">Databaserollen met Administrator-machtigingen zijn anders dan serverbeheerders.</span><span class="sxs-lookup"><span data-stu-id="d7b53-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="d7b53-111">**Proces** -gebruikers verbinding kunnen maken van tooand proces bewerkingen uitvoeren op database Hallo en analyseren van gegevens van de database model.</span><span class="sxs-lookup"><span data-stu-id="d7b53-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="d7b53-112">**Lees** -gebruikers kunnen gebruiken een client toepassing tooconnect tooand analyseren modelgegevens van de database.</span><span class="sxs-lookup"><span data-stu-id="d7b53-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="d7b53-113">Wanneer een model in tabelvorm-project maakt, kunt u rollen maken en gebruikers of groepen toothose functies toevoegen met rolbeheer in SSDT.</span><span class="sxs-lookup"><span data-stu-id="d7b53-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="d7b53-114">Wanneer geïmplementeerde tooa server kunt u gebruiken om SSMS, [Analysis Services-PowerShell-cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), of [Tabellaire Model scripttaal](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) of verwijderen van rollen en leden van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d7b53-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="d7b53-115">tooadd of beheren van rollen en gebruikers in SSDT</span><span class="sxs-lookup"><span data-stu-id="d7b53-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="d7b53-116">In SSDT > **Tabellaire Model Explorer**, met de rechtermuisknop op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="d7b53-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="d7b53-117">Klik in **Role Manager** op **New**.</span><span class="sxs-lookup"><span data-stu-id="d7b53-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="d7b53-118">Typ een naam voor de rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7b53-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="d7b53-119">Standaard wordt Hallo-naam van Hallo standaardrol incrementeel genummerd voor elke nieuwe rol.</span><span class="sxs-lookup"><span data-stu-id="d7b53-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="d7b53-120">Het raadzaam typt u een naam die duidelijk aangeeft Hallo lidtype, bijvoorbeeld Financiën Managers of specialisten Human Resources.</span><span class="sxs-lookup"><span data-stu-id="d7b53-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="d7b53-121">Selecteer een van de volgende machtigingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="d7b53-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="d7b53-122">Machtiging</span><span class="sxs-lookup"><span data-stu-id="d7b53-122">Permission</span></span>|<span data-ttu-id="d7b53-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7b53-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="d7b53-124">**Geen**</span><span class="sxs-lookup"><span data-stu-id="d7b53-124">**None**</span></span>|<span data-ttu-id="d7b53-125">Leden Hallo modelschema kunnen niet worden gewijzigd en kunnen gegevens niet opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="d7b53-126">**Lezen**</span><span class="sxs-lookup"><span data-stu-id="d7b53-126">**Read**</span></span>|<span data-ttu-id="d7b53-127">Leden kunnen een query over gegevens (op basis van rijfilters) maar Hallo modelschema niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="d7b53-128">**Lees- en**</span><span class="sxs-lookup"><span data-stu-id="d7b53-128">**Read and Process**</span></span>|<span data-ttu-id="d7b53-129">Leden query gegevens (op basis van rijniveau filters) en voer proces en proces alle bewerkingen, maar kunnen het modelschema Hallo niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="d7b53-130">**Proces**</span><span class="sxs-lookup"><span data-stu-id="d7b53-130">**Process**</span></span>|<span data-ttu-id="d7b53-131">Leden kunnen proces en proces alle bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="d7b53-132">Hallo modelschema kan niet worden gewijzigd en kan gegevens niet opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="d7b53-133">**Beheerder**</span><span class="sxs-lookup"><span data-stu-id="d7b53-133">**Administrator**</span></span>|<span data-ttu-id="d7b53-134">Leden kunnen Hallo modelschema wijzigen en alle gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="d7b53-135">Als het Hallo-rol zijn maken heeft lees- of de machtigingen lezen en proces, kunt u rijfilters toevoegen met behulp van een DAX-formule.</span><span class="sxs-lookup"><span data-stu-id="d7b53-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="d7b53-136">Klik op Hallo **rijfilters** tabblad Selecteer een tabel vervolgens, klikt u op Hallo **DAX-Filter** veld en typ vervolgens een DAX-formule.</span><span class="sxs-lookup"><span data-stu-id="d7b53-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="d7b53-137">Klik op **leden** > **extern toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d7b53-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="d7b53-138">In **extern lid toevoegen**, gebruikers of groepen opgeven in uw Azure AD-tenant op e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="d7b53-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="d7b53-139">Nadat u op OK en rolbeheer sluit, rollen en leden van een rol worden weergegeven in de Tabellaire Model Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7b53-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Rollen en gebruikers in de Tabellaire Model Explorer](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="d7b53-141">Tooyour Azure Analysis Services-server implementeren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="d7b53-142">tooadd of beheren van rollen en gebruikers in SSMS</span><span class="sxs-lookup"><span data-stu-id="d7b53-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="d7b53-143">tooadd rollen en gebruikers tooa modeldatabase geïmplementeerd, moet u de server verbonden toohello als serverbeheerder of wordt al een databaserol met administrator-machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="d7b53-144">Met de rechtermuisknop in Verkenner-Object, **rollen** > **nieuwe rol**.</span><span class="sxs-lookup"><span data-stu-id="d7b53-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="d7b53-145">In **rol maken**, een role-naam en beschrijving opgeven.</span><span class="sxs-lookup"><span data-stu-id="d7b53-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="d7b53-146">Selecteer een machtiging.</span><span class="sxs-lookup"><span data-stu-id="d7b53-146">Select a permission.</span></span>
   |<span data-ttu-id="d7b53-147">Machtiging</span><span class="sxs-lookup"><span data-stu-id="d7b53-147">Permission</span></span>|<span data-ttu-id="d7b53-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7b53-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="d7b53-149">**Volledig beheer (beheerder)**</span><span class="sxs-lookup"><span data-stu-id="d7b53-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="d7b53-150">Leden kunnen wijzigen Hallo modelschema, verwerken en alle gegevens kunt opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="d7b53-151">**Proces-database**</span><span class="sxs-lookup"><span data-stu-id="d7b53-151">**Process database**</span></span>|<span data-ttu-id="d7b53-152">Leden kunnen proces en proces alle bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="d7b53-153">Hallo modelschema kan niet worden gewijzigd en kan gegevens niet opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="d7b53-154">**Lezen**</span><span class="sxs-lookup"><span data-stu-id="d7b53-154">**Read**</span></span>|<span data-ttu-id="d7b53-155">Leden kunnen een query over gegevens (op basis van rijfilters) maar Hallo modelschema niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="d7b53-156">Klik op **lidmaatschap**, voert u een gebruiker of groep in uw Azure AD-tenant op e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="d7b53-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Gebruiker toevoegen](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="d7b53-158">Als het Hallo-rol die u maakt is de machtiging lezen, kunt u rijfilters toevoegen met behulp van een DAX-formule.</span><span class="sxs-lookup"><span data-stu-id="d7b53-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="d7b53-159">Klik op **rijfilters**, selecteer een tabel en typ vervolgens een DAX-formule in Hallo **DAX-Filter** veld.</span><span class="sxs-lookup"><span data-stu-id="d7b53-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="d7b53-160">tooadd rollen en gebruikers met een script TMSL</span><span class="sxs-lookup"><span data-stu-id="d7b53-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="d7b53-161">U kunt een TMSL-script uitvoeren in Hallo XMLA-venster in SSMS of met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7b53-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="d7b53-162">Gebruik Hallo [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) opdracht en Hallo [rollen](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span><span class="sxs-lookup"><span data-stu-id="d7b53-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="d7b53-163">**Voorbeeldscript TMSL**</span><span class="sxs-lookup"><span data-stu-id="d7b53-163">**Sample TMSL script**</span></span>

<span data-ttu-id="d7b53-164">In dit voorbeeld wordt een externe gebruiker B2B en een groep toohello analist rol met machtigingen voor lezen voor Hallo SalesBI database toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d7b53-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="d7b53-165">Beide Hallo externe gebruiker en groep moet in dezelfde Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d7b53-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="d7b53-166">tooadd rollen en gebruikers met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7b53-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="d7b53-167">Hallo [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module biedt taakspecifieke database management-cmdlets en Hallo algemeen Invoke ASCmd cmdlet die een Tabellair Model Scripting Language (TMSL) query of script accepteert.</span><span class="sxs-lookup"><span data-stu-id="d7b53-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="d7b53-168">Hallo volgende cmdlets worden gebruikt voor databaserollen en gebruikers beheren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="d7b53-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="d7b53-169">Cmdlet</span></span>|<span data-ttu-id="d7b53-170">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7b53-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="d7b53-171">Voeg RoleMember</span><span class="sxs-lookup"><span data-stu-id="d7b53-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="d7b53-172">Toevoegen van een lid tooa-databaserol.</span><span class="sxs-lookup"><span data-stu-id="d7b53-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="d7b53-173">Verwijder RoleMember</span><span class="sxs-lookup"><span data-stu-id="d7b53-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="d7b53-174">Een lid verwijderen uit een databaserol.</span><span class="sxs-lookup"><span data-stu-id="d7b53-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="d7b53-175">Aanroepen ASCmd</span><span class="sxs-lookup"><span data-stu-id="d7b53-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="d7b53-176">Een script TMSL uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7b53-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="d7b53-177">Rijfilters</span><span class="sxs-lookup"><span data-stu-id="d7b53-177">Row filters</span></span>  
<span data-ttu-id="d7b53-178">Rijfilters definiëren welke rijen in een tabel door leden van een bepaalde rol kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="d7b53-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="d7b53-179">Rijfilters zijn gedefinieerd voor elke tabel in een model met DAX formules.</span><span class="sxs-lookup"><span data-stu-id="d7b53-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="d7b53-180">Rijfilters alleen voor rollen met lees- en kunnen worden gedefinieerd en proces machtigingen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="d7b53-181">Standaard, als een rijfilter is niet gedefinieerd voor een bepaalde tabel kunnen leden opvragen alle rijen in de tabel Hallo tenzij cross-filtering is van toepassing van een andere tabel.</span><span class="sxs-lookup"><span data-stu-id="d7b53-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="d7b53-182">Rijfilters vereisen een DAX-formule, die moet worden geëvalueerd tooa TRUE/FALSE-waarde, toodefine Hallo rijen die door leden van die bepaalde rol kunnen worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="d7b53-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="d7b53-183">Rijen niet opgenomen in Hallo DAX-formule, kunnen niet worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="d7b53-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="d7b53-184">Tabel Klanten bijvoorbeeld Hallo Hello rij filters expressie, na *= klanten [Country] = "VS"*, klanten in de Verenigde Staten Hallo alleen de leden van de rol van Hallo verkoop kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="d7b53-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="d7b53-185">Rijfilters toepassen toohello opgegeven rijen en de gerelateerde rijen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="d7b53-186">Wanneer een tabel meerdere relaties heeft, toepassing filters beveiliging voor Hallo-relatie die actief is.</span><span class="sxs-lookup"><span data-stu-id="d7b53-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="d7b53-187">Rijfilters beginnen en eindigen met een andere rij filers gedefinieerd voor de gerelateerde tabellen, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d7b53-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="d7b53-188">Tabel</span><span class="sxs-lookup"><span data-stu-id="d7b53-188">Table</span></span>|<span data-ttu-id="d7b53-189">DAX-expressie</span><span class="sxs-lookup"><span data-stu-id="d7b53-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="d7b53-190">Regio</span><span class="sxs-lookup"><span data-stu-id="d7b53-190">Region</span></span>|<span data-ttu-id="d7b53-191">= Regio [Country] = "VS"</span><span class="sxs-lookup"><span data-stu-id="d7b53-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="d7b53-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="d7b53-192">ProductCategory</span></span>|<span data-ttu-id="d7b53-193">= ProductCategory [Name] = "Fietsen"</span><span class="sxs-lookup"><span data-stu-id="d7b53-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="d7b53-194">Transacties</span><span class="sxs-lookup"><span data-stu-id="d7b53-194">Transactions</span></span>|<span data-ttu-id="d7b53-195">= Transacties [jaar] = 2016</span><span class="sxs-lookup"><span data-stu-id="d7b53-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="d7b53-196">Hallo netto effect is leden gegevensrijen waarbij Hallo klant is in de Verenigde Staten hello, Hallo productcategorie voor fietsen en Hallo jaar voor 2016 kunnen opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="d7b53-197">Gebruikers kunnen geen transacties buiten de Verenigde Staten hello, transacties die niet fietsen of transacties niet 2016 tenzij ze deel uitmaken van een andere functie die deze machtigingen verleent opvragen.</span><span class="sxs-lookup"><span data-stu-id="d7b53-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="d7b53-198">Hallo-filter, kunt u *=FALSE()*, toodeny toegang tooall rijen voor een hele tabel.</span><span class="sxs-lookup"><span data-stu-id="d7b53-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b53-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7b53-199">Next steps</span></span>
  <span data-ttu-id="d7b53-200">[Serverbeheerders beheren](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="d7b53-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="d7b53-201">Azure analyseservices met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="d7b53-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="d7b53-202">Scripting Language (TMSL) Reference Model in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="d7b53-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

