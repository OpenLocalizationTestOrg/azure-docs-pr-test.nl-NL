---
title: Toegang tot rapportage - Azure RBAC | Microsoft Docs
description: Genereer een rapport met een lijst met alle wijzigingen in de toegang tot uw Azure-abonnementen met toegangsbeheer op basis van rollen gedurende de afgelopen 90 dagen.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="55042-103">Een access-rapport maken voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="55042-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="55042-104">Elk gewenst moment iemand verleent of trekt u toegang binnen uw abonnementen, worden de wijzigingen geregistreerd in Azure gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="55042-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="55042-105">U kunt toegang tot Geschiedenisrapporten om te zien alle wijzigingen voor de afgelopen negentig dagen maken.</span><span class="sxs-lookup"><span data-stu-id="55042-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="55042-106">Een rapport maken met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="55042-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="55042-107">Gebruik voor het maken van een geschiedenisrapport voor gewijzigde van toegang in PowerShell de [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) opdracht.</span><span class="sxs-lookup"><span data-stu-id="55042-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="55042-108">Wanneer u deze opdracht aanroept, kunt u opgeven welke eigenschap van de toewijzingen die u weergegeven, inclusief het volgende wilt:</span><span class="sxs-lookup"><span data-stu-id="55042-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="55042-109">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="55042-109">Property</span></span> | <span data-ttu-id="55042-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="55042-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55042-111">**Actie**</span><span class="sxs-lookup"><span data-stu-id="55042-111">**Action**</span></span> |<span data-ttu-id="55042-112">Hiermee wordt aangegeven of toegang is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="55042-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="55042-113">**Aanroeper**</span><span class="sxs-lookup"><span data-stu-id="55042-113">**Caller**</span></span> |<span data-ttu-id="55042-114">De eigenaar die verantwoordelijk is voor de wijziging toegang</span><span class="sxs-lookup"><span data-stu-id="55042-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="55042-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="55042-115">**PrincipalId**</span></span> | <span data-ttu-id="55042-116">De unieke id van de gebruiker, groep of toepassing die de rol is toegewezen</span><span class="sxs-lookup"><span data-stu-id="55042-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="55042-117">**Primaire naam**</span><span class="sxs-lookup"><span data-stu-id="55042-117">**PrincipalName**</span></span> |<span data-ttu-id="55042-118">De naam van de gebruiker, groep of toepassing</span><span class="sxs-lookup"><span data-stu-id="55042-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="55042-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="55042-119">**PrincipalType**</span></span> |<span data-ttu-id="55042-120">Hiermee wordt aangegeven of de toewijzing voor een gebruiker, groep of toepassing is</span><span class="sxs-lookup"><span data-stu-id="55042-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="55042-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="55042-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="55042-122">De GUID van de rol die is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="55042-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="55042-123">**Rolnaam**</span><span class="sxs-lookup"><span data-stu-id="55042-123">**RoleName**</span></span> |<span data-ttu-id="55042-124">De rol die is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="55042-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="55042-125">**Bereik**</span><span class="sxs-lookup"><span data-stu-id="55042-125">**Scope**</span></span> | <span data-ttu-id="55042-126">De unieke id van het abonnement, resourcegroep of resource die de toewijzing is van toepassing op</span><span class="sxs-lookup"><span data-stu-id="55042-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="55042-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="55042-127">**ScopeName**</span></span> |<span data-ttu-id="55042-128">De naam van het abonnement, resourcegroep of resource</span><span class="sxs-lookup"><span data-stu-id="55042-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="55042-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="55042-129">**ScopeType**</span></span> |<span data-ttu-id="55042-130">Hiermee wordt aangegeven of de toewijzing is op het abonnement, resourcegroep of resource-bereik</span><span class="sxs-lookup"><span data-stu-id="55042-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="55042-131">**Tijdstempel**</span><span class="sxs-lookup"><span data-stu-id="55042-131">**Timestamp**</span></span> |<span data-ttu-id="55042-132">De datum en tijd op dat toegang is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="55042-132">The date and time that access was changed</span></span> |

<span data-ttu-id="55042-133">Deze opdracht worden alle wijzigingen in het abonnement voor de afgelopen zeven dagen:</span><span class="sxs-lookup"><span data-stu-id="55042-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - schermafbeelding](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="55042-135">Een rapport maken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="55042-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="55042-136">Gebruik voor het maken van een access-geschiedenisrapport van wijziging in de Azure-opdrachtregelinterface (CLI) de `azure role assignment changelog list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="55042-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="55042-137">Naar een spreadsheet exporteren</span><span class="sxs-lookup"><span data-stu-id="55042-137">Export to a spreadsheet</span></span>
<span data-ttu-id="55042-138">Als u het rapport opslaan of manipuleren van de gegevens, de toegang wijzigingen in een CSV-bestand wilt exporteren.</span><span class="sxs-lookup"><span data-stu-id="55042-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="55042-139">U kunt vervolgens het rapport weergeven in een werkblad voor revisie.</span><span class="sxs-lookup"><span data-stu-id="55042-139">You can then view the report in a spreadsheet for review.</span></span>

![Changelog weergegeven als werkblad - schermafbeelding](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="55042-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55042-141">Next steps</span></span>
* <span data-ttu-id="55042-142">Werken met [aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="55042-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="55042-143">Meer informatie over het beheren van [Azure RBAC met powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="55042-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

