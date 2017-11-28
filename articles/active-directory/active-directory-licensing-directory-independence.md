---
title: aaaCharacteristics van Azure Active Directory-tenant intercaction | Microsoft Docs
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
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="884f5-103">Begrijpen hoe meerdere tenants van Azure Active Directory gebruiken</span><span class="sxs-lookup"><span data-stu-id="884f5-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="884f5-104">In Azure Active Directory (Azure AD), is elke tenant een volledig onafhankelijke resource: een peer die is logisch onafhankelijk van andere tenants die u beheert Hallo.</span><span class="sxs-lookup"><span data-stu-id="884f5-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="884f5-105">Er is geen bovenliggende / onderliggende relatie tussen de tenants.</span><span class="sxs-lookup"><span data-stu-id="884f5-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="884f5-106">Deze onafhankelijkheid tussen de tenants bevat resourceonafhankelijkheid, beheeronafhankelijkheid en synchronisatieonafhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="884f5-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="884f5-107">Resourceonafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="884f5-107">Resource independence</span></span>
* <span data-ttu-id="884f5-108">Als u maken of verwijderen van een resource in een tenant, heeft dit geen invloed op alle bronnen in een andere tenant, met de Hallo gedeeltelijke uitzondering van externe gebruikers.</span><span class="sxs-lookup"><span data-stu-id="884f5-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="884f5-109">Als u een van uw domeinnamen met een tenant gebruikt, wordt deze niet gebruikt met een andere tenant.</span><span class="sxs-lookup"><span data-stu-id="884f5-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="884f5-110">Beheeronafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="884f5-110">Administrative independence</span></span>
<span data-ttu-id="884f5-111">Als een beheergebruiker van de tenant 'Contoso' een testtenant 'Test' vervolgens maakt:</span><span class="sxs-lookup"><span data-stu-id="884f5-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="884f5-112">Hallo-gebruiker die een tenant maakt wordt standaard toegevoegd als een externe gebruiker in die nieuwe tenant en de globale beheerdersrol toegewezen Hallo in deze tenant.</span><span class="sxs-lookup"><span data-stu-id="884f5-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="884f5-113">Beheerders van de tenant 'Contoso' Hallo hebben geen directe beheerdersrechten tootenant 'Test', tenzij de beheerder van 'Test' specifiek hun deze rechten verleent.</span><span class="sxs-lookup"><span data-stu-id="884f5-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="884f5-114">Echter, 'Contoso' kunnen beheerders toegang tootenant 'Test' als ze bepalen Hallo-gebruikersaccount die gemaakt van 'Test'.</span><span class="sxs-lookup"><span data-stu-id="884f5-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="884f5-115">Als u toevoegen/verwijderen een beheerdersrol voor een gebruiker in een tenant, Hallo wijzigen heeft geen invloed op Hallo beheerdersrollen die Hallo gebruiker heeft in een andere tenant.</span><span class="sxs-lookup"><span data-stu-id="884f5-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="884f5-116">Synchronisatieonafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="884f5-116">Synchronization independence</span></span>
<span data-ttu-id="884f5-117">U kunt elke Azure AD onafhankelijk tooget gegevens worden gesynchroniseerd vanuit één exemplaar van een tenant:</span><span class="sxs-lookup"><span data-stu-id="884f5-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="884f5-118">Hello Azure AD Connect-hulpprogramma, toosynchronize gegevens met één AD-forest.</span><span class="sxs-lookup"><span data-stu-id="884f5-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="884f5-119">Hallo van Azure Active-tenant Connector voor Forefront Identity Manager, toosynchronize gegevens met een of meer on-premises forests en/of niet-Azure AD-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="884f5-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="884f5-120">Toevoegen van een Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="884f5-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="884f5-121">tooadd een Azure AD-tenant in hello Azure-portal, meld u aan te[hello Azure-portal](https://portal.azure.com) met een account dat een globale beheerder van Azure AD, en aan de linkerkant hello, selecteert u **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="884f5-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="884f5-122">In tegenstelling tot andere Azure-resources zijn uw tenants niet onderliggende resources van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="884f5-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="884f5-123">Als uw Azure-abonnement is geannuleerd of verlopen, kunt u nog steeds toegang tot uw tenant-gegevens met Azure PowerShell of Azure Graph API Hallo Hallo Office 365-beheercentrum.</span><span class="sxs-lookup"><span data-stu-id="884f5-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="884f5-124">U kunt ook een ander abonnement koppelen aan Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="884f5-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="884f5-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="884f5-125">Next steps</span></span>
<span data-ttu-id="884f5-126">Zie voor een breed overzicht van Azure AD-licentieverlening problemen en aanbevolen procedures [wat is Azure Active-tenant-licentieverlening?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="884f5-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
