---
title: Gebruikers toewijzen aan een aangepast domein in Azure Active Directory | Microsoft Docs
description: Klik hier voor meer informatie over het vullen van een aangepast domein in Azure Active Directory met een gebruikersaccount.
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="62052-103">Gebruikers toewijzen aan een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="62052-103">Assign users to a custom domain</span></span>
<span data-ttu-id="62052-104">Nadat u uw aangepaste domein aan Azure Active Directory hebt toegevoegd, moet u de gebruikersaccounts voor dit domein toevoegen zodat u kunt beginnen met het verifiëren van deze.</span><span class="sxs-lookup"><span data-stu-id="62052-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62052-105">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="62052-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="62052-106">Voor informatie over het beheren van uw domeinnamen in de Azure AD-beheercentrum, Zie [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="62052-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="62052-107">Gebruikers synchroniseren met een on-premises adreslijst</span><span class="sxs-lookup"><span data-stu-id="62052-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="62052-108">Als u hebt al een verbinding ingesteld tussen uw on-premises Active Directory en Azure Active Directory, kan de synchronisatie van de accounts invullen.</span><span class="sxs-lookup"><span data-stu-id="62052-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="62052-109">Zie voor meer informatie over het synchroniseren van Azure Active Directory met uw lokale Active Directory [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="62052-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="62052-110">Gebruikers toegevoegd en beheerd in de cloud</span><span class="sxs-lookup"><span data-stu-id="62052-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="62052-111">Het domein voor een bestaand gebruikersaccount wijzigen:</span><span class="sxs-lookup"><span data-stu-id="62052-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="62052-112">Open de klassieke Azure portal met een account dat is een globale beheerder of de beheerder van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="62052-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="62052-113">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="62052-113">Open your directory.</span></span>
3. <span data-ttu-id="62052-114">Selecteer de tab **Gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="62052-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="62052-115">Selecteer de gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="62052-115">Select the user from the list.</span></span>
5. <span data-ttu-id="62052-116">Het domein voor de gebruiker te wijzigen en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="62052-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="62052-117">Dit kan ook worden gedaan met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of de [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="62052-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="62052-118">Een aangepast domein selecteert bij het maken van een nieuwe gebruiker</span><span class="sxs-lookup"><span data-stu-id="62052-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="62052-119">Open de klassieke Azure portal met een account dat is een globale beheerder of de beheerder van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="62052-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="62052-120">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="62052-120">Open your directory.</span></span>
3. <span data-ttu-id="62052-121">Selecteer de tab **Gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="62052-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="62052-122">Selecteer in de opdrachtbalk **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="62052-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="62052-123">Wanneer u de gebruikersnaam toevoegt, kiest u het aangepaste domein in de domeinlijst.</span><span class="sxs-lookup"><span data-stu-id="62052-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="62052-124">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="62052-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62052-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62052-125">Next steps</span></span>
* [<span data-ttu-id="62052-126">Met behulp van aangepaste domeinnamen voor het vereenvoudigen van de aanmeldingservaring voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="62052-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="62052-127">Aangepaste domeinnamen beheren</span><span class="sxs-lookup"><span data-stu-id="62052-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="62052-128">Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD</span><span class="sxs-lookup"><span data-stu-id="62052-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

