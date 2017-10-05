---
title: Kenmerken van Azure Active Directory-tenant intercaction | Microsoft Docs
description: Uw Azure Active-tenant tenants inzicht hebt in uw tenants als volledig onafhankelijke resource beheren
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="50229-103">Begrijpen hoe meerdere tenants van Azure Active Directory gebruiken</span><span class="sxs-lookup"><span data-stu-id="50229-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="50229-104">In Azure Active Directory (Azure AD), is elke tenant een volledig onafhankelijke resource: een peer die logisch onafhankelijk van andere tenants die u beheert.</span><span class="sxs-lookup"><span data-stu-id="50229-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="50229-105">Er is geen bovenliggende / onderliggende relatie tussen de tenants.</span><span class="sxs-lookup"><span data-stu-id="50229-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="50229-106">Deze onafhankelijkheid tussen de tenants bevat resourceonafhankelijkheid, beheeronafhankelijkheid en synchronisatieonafhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="50229-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="50229-107">Resourceonafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="50229-107">Resource independence</span></span>
* <span data-ttu-id="50229-108">Als u maken of verwijderen van een resource in een tenant, heeft dit geen invloed op alle bronnen in een andere tenant, met de gedeeltelijke uitzondering van externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="50229-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="50229-109">Als u een van uw domeinnamen met een tenant gebruikt, wordt deze niet gebruikt met een andere tenant.</span><span class="sxs-lookup"><span data-stu-id="50229-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="50229-110">Beheeronafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="50229-110">Administrative independence</span></span>
<span data-ttu-id="50229-111">Als een beheergebruiker van de tenant 'Contoso' een testtenant 'Test' vervolgens maakt:</span><span class="sxs-lookup"><span data-stu-id="50229-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="50229-112">Standaard wordt de gebruiker die een tenant maakt toegevoegd als een externe gebruiker in deze nieuwe tenant en de rol globale beheerder in deze tenant toegewezen.</span><span class="sxs-lookup"><span data-stu-id="50229-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="50229-113">De beheerders van de tenant 'Contoso' hebben geen directe beheerdersrechten voor de tenant 'Test', tenzij de beheerder van 'Test' specifiek hun deze rechten verleent.</span><span class="sxs-lookup"><span data-stu-id="50229-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="50229-114">Echter, 'Contoso' kunnen beheerders toegang tot de tenant 'Test' als ze bepalen dat het gebruikersaccount dat wordt gemaakt van 'Test'.</span><span class="sxs-lookup"><span data-stu-id="50229-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="50229-115">Als u toevoegen/verwijderen een beheerdersrol voor een gebruiker in een tenant, heeft deze wijziging geen invloed op de beheerdersrollen die de gebruiker in een andere tenant heeft.</span><span class="sxs-lookup"><span data-stu-id="50229-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="50229-116">Synchronisatieonafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="50229-116">Synchronization independence</span></span>
<span data-ttu-id="50229-117">U kunt elke Azure AD-tenant onafhankelijk zodanig gegevens worden gesynchroniseerd vanuit één exemplaar van een configureren:</span><span class="sxs-lookup"><span data-stu-id="50229-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="50229-118">Het hulpprogramma Azure AD Connect om gegevens te synchroniseren met één AD-forest.</span><span class="sxs-lookup"><span data-stu-id="50229-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="50229-119">De Azure Active tenant Connector voor Forefront Identity Manager, om gegevens te synchroniseren met een of meer on-premises-forests en/of niet-Azure AD-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="50229-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="50229-120">Toevoegen van een Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="50229-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="50229-121">Als u wilt toevoegen van een Azure AD-tenant in de Azure portal, moet u zich aanmelden bij [de Azure-portal](https://portal.azure.com) met een account dat een globale beheerder van Azure AD, en aan de linkerkant, selecteert u **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="50229-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="50229-122">In tegenstelling tot andere Azure-resources zijn uw tenants niet onderliggende resources van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="50229-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="50229-123">Als uw Azure-abonnement is geannuleerd of verlopen, kunt u nog steeds toegang tot uw tenant-gegevens met Azure PowerShell, de Azure Graph API of Office 365-beheercentrum.</span><span class="sxs-lookup"><span data-stu-id="50229-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="50229-124">U kunt ook een ander abonnement koppelen aan de tenant.</span><span class="sxs-lookup"><span data-stu-id="50229-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="50229-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50229-125">Next steps</span></span>
<span data-ttu-id="50229-126">Zie voor een breed overzicht van Azure AD-licentieverlening problemen en aanbevolen procedures [wat is Azure Active-tenant-licentieverlening?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="50229-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
