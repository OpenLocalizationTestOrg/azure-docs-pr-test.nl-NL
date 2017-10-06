---
title: aaaAccess rapportage - Azure RBAC | Microsoft Docs
description: Genereer een rapport dat een lijst met alle wijzigingen in de tooyour voor toegang tot Azure-abonnementen met op rollen gebaseerde toegangsbeheer via Hallo afgelopen 90 dagen.
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
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="268d8-103">Een access-rapport maken voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="268d8-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="268d8-104">Elk gewenst moment iemand verleent of trekt u toegang binnen uw abonnementen worden Hallo wijzigingen geregistreerd in Azure gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="268d8-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="268d8-105">U kunt maken toegang wijzigen geschiedenis rapporten toosee alle wijzigingen voor Hallo afgelopen 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="268d8-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="268d8-106">Een rapport maken met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="268d8-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="268d8-107">toocreate een toegang wijzigen geschiedenisrapport in PowerShell gebruik Hallo [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) opdracht.</span><span class="sxs-lookup"><span data-stu-id="268d8-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="268d8-108">Wanneer u deze opdracht aanroept, kunt u opgeven welke eigenschap van de gewenste weergegeven, met inbegrip van de volgende Hallo Hallo-toewijzingen:</span><span class="sxs-lookup"><span data-stu-id="268d8-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="268d8-109">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="268d8-109">Property</span></span> | <span data-ttu-id="268d8-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="268d8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="268d8-111">**Actie**</span><span class="sxs-lookup"><span data-stu-id="268d8-111">**Action**</span></span> |<span data-ttu-id="268d8-112">Hiermee wordt aangegeven of toegang is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="268d8-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="268d8-113">**Aanroeper**</span><span class="sxs-lookup"><span data-stu-id="268d8-113">**Caller**</span></span> |<span data-ttu-id="268d8-114">Hallo-eigenaar die verantwoordelijk is voor Hallo toegang wijzigen</span><span class="sxs-lookup"><span data-stu-id="268d8-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="268d8-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="268d8-115">**PrincipalId**</span></span> | <span data-ttu-id="268d8-116">de unieke id van het Hallo-gebruiker, groep of toepassing die is toegewezen rol Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="268d8-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="268d8-117">**Primaire naam**</span><span class="sxs-lookup"><span data-stu-id="268d8-117">**PrincipalName**</span></span> |<span data-ttu-id="268d8-118">Hallo-naam van het Hallo-gebruiker, groep of toepassing</span><span class="sxs-lookup"><span data-stu-id="268d8-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="268d8-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="268d8-119">**PrincipalType**</span></span> |<span data-ttu-id="268d8-120">Hiermee wordt aangegeven of Hallo-toewijzing voor een gebruiker, groep of toepassing is</span><span class="sxs-lookup"><span data-stu-id="268d8-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="268d8-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="268d8-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="268d8-122">Hallo GUID van het Hallo-rol die is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="268d8-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="268d8-123">**Rolnaam**</span><span class="sxs-lookup"><span data-stu-id="268d8-123">**RoleName**</span></span> |<span data-ttu-id="268d8-124">Hallo-rol die is toegekend of ingetrokken</span><span class="sxs-lookup"><span data-stu-id="268d8-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="268d8-125">**Bereik**</span><span class="sxs-lookup"><span data-stu-id="268d8-125">**Scope**</span></span> | <span data-ttu-id="268d8-126">Hallo unieke id van Hallo abonnement, resourcegroep of resource die Hallo toewijzing is van toepassing te</span><span class="sxs-lookup"><span data-stu-id="268d8-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="268d8-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="268d8-127">**ScopeName**</span></span> |<span data-ttu-id="268d8-128">Hallo-naam van het Hallo-abonnement, resourcegroep of resource</span><span class="sxs-lookup"><span data-stu-id="268d8-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="268d8-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="268d8-129">**ScopeType**</span></span> |<span data-ttu-id="268d8-130">Hiermee wordt aangegeven of Hallo-toewijzing is op het Hallo-abonnement, resourcegroep of resource bereik</span><span class="sxs-lookup"><span data-stu-id="268d8-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="268d8-131">**Tijdstempel**</span><span class="sxs-lookup"><span data-stu-id="268d8-131">**Timestamp**</span></span> |<span data-ttu-id="268d8-132">Hallo-datum en tijd waarop de toegang is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="268d8-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="268d8-133">Deze opdracht worden alle toegang wijzigingen in het abonnement voor Hallo Hallo afgelopen zeven dagen:</span><span class="sxs-lookup"><span data-stu-id="268d8-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - schermafbeelding](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="268d8-135">Een rapport maken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="268d8-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="268d8-136">een geschiedenisrapport voor gewijzigde van toegang in hello Azure-opdrachtregelinterface (CLI) toocreate gebruiken Hallo `azure role assignment changelog list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="268d8-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="268d8-137">Werkblad tooa exporteren</span><span class="sxs-lookup"><span data-stu-id="268d8-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="268d8-138">toosave rapport Hallo of Hallo gegevens bewerken, export Hallo toegang verandert in een CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="268d8-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="268d8-139">U kunt vervolgens Hallo rapport weergeven in een werkblad voor controle.</span><span class="sxs-lookup"><span data-stu-id="268d8-139">You can then view hello report in a spreadsheet for review.</span></span>

![Changelog weergegeven als werkblad - schermafbeelding](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="268d8-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="268d8-141">Next steps</span></span>
* <span data-ttu-id="268d8-142">Werken met [aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="268d8-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="268d8-143">Meer informatie over hoe toomanage [Azure RBAC met powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="268d8-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

