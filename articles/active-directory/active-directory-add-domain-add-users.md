---
title: aaaAssign gebruikers tooa aangepast domein in Azure Active Directory | Microsoft Docs
description: Hoe toopopulate een aangepast domein in Azure Active Directory met een gebruikersaccount.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="fcd79-103">Gebruikers tooa aangepast domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="fcd79-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="fcd79-104">Nadat u uw aangepaste domein tooAzure Active Directory hebt toegevoegd, moet u de gebruikersaccounts Hallo voor dit domein toevoegen zodat u kunt beginnen met het verifiëren van deze.</span><span class="sxs-lookup"><span data-stu-id="fcd79-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcd79-105">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fcd79-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="fcd79-106">Zie voor hoe toomanage uw in hello Azure AD-beheercentrum domeinnamen, [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fcd79-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="fcd79-107">Gebruikers synchroniseren met een on-premises adreslijst</span><span class="sxs-lookup"><span data-stu-id="fcd79-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="fcd79-108">Als u hebt al een verbinding ingesteld tussen uw on-premises Active Directory en Azure Active Directory, kan de synchronisatie Hallo accounts invullen.</span><span class="sxs-lookup"><span data-stu-id="fcd79-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="fcd79-109">Voor meer informatie over hoe toosynchronize Azure Active Directory met uw lokale Active Directory, Zie [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="fcd79-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="fcd79-110">Gebruikers toegevoegd en beheerd in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="fcd79-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="fcd79-111">toochange hello domein voor een bestaand gebruikersaccount:</span><span class="sxs-lookup"><span data-stu-id="fcd79-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="fcd79-112">Open Hallo klassieke Azure-portal met een account dat is een globale beheerder of de beheerder van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fcd79-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="fcd79-113">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="fcd79-113">Open your directory.</span></span>
3. <span data-ttu-id="fcd79-114">Selecteer Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fcd79-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="fcd79-115">Hallo-gebruiker in Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="fcd79-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="fcd79-116">Hallo-domein voor Hallo gebruiker te wijzigen en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fcd79-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="fcd79-117">Dit kan ook worden gedaan met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of Hallo [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="fcd79-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="fcd79-118">Een aangepast domein selecteert bij het maken van een nieuwe gebruiker</span><span class="sxs-lookup"><span data-stu-id="fcd79-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="fcd79-119">Open Hallo klassieke Azure-portal met een account dat is een globale beheerder of de beheerder van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fcd79-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="fcd79-120">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="fcd79-120">Open your directory.</span></span>
3. <span data-ttu-id="fcd79-121">Selecteer Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fcd79-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="fcd79-122">Selecteer in de opdrachtbalk Hallo **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fcd79-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="fcd79-123">Wanneer u de naam van de gebruiker Hallo toevoegt, kiest u Hallo aangepast domein uit Hallo Domeinlijst.</span><span class="sxs-lookup"><span data-stu-id="fcd79-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="fcd79-124">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fcd79-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcd79-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcd79-125">Next steps</span></span>
* [<span data-ttu-id="fcd79-126">Met behulp van aangepast domein namen toosimplify hello aanmeldingservaring voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="fcd79-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="fcd79-127">Aangepaste domeinnamen beheren</span><span class="sxs-lookup"><span data-stu-id="fcd79-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="fcd79-128">Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcd79-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

