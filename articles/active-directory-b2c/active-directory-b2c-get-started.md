---
title: 'Azure Active Directory B2C: Een Azure Active Directory B2C-tenant maken | Microsoft Docs'
description: In dit artikel wordt beschreven hoe u een Azure Active Directory B2C-tenant kunt maken
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="f4c6e-103">Een Azure Active Directory B2C-tenant maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="f4c6e-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="f4c6e-104">Door Sipi bewerkt.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-104">Edited by Sipi.</span></span>

<span data-ttu-id="f4c6e-105">Deze snelstartgids kunt u een Microsoft Azure Active Directory (Azure AD) B2C-tenant maken in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="f4c6e-106">Wanneer u klaar bent, hebt u een B2C-tenant te gebruiken voor het registreren van de B2C-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4c6e-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4c6e-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="f4c6e-108">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-108">Log in to Azure</span></span>

<span data-ttu-id="f4c6e-109">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f4c6e-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="f4c6e-110">Een Azure AD B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="f4c6e-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="f4c6e-111">B2C-functies kunnen niet worden ingeschakeld in uw bestaande tenants.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="f4c6e-112">U moet een Azure AD B2C-tenant maken.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="f4c6e-113">Gefeliciteerd, u hebt een Azure Active Directory B2C-tenant gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="f4c6e-114">Bent u een globale beheerder van de tenant.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="f4c6e-115">U kunt naar believen hoofdbeheerders toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="f4c6e-116">Als u wilt overschakelen naar de nieuwe tenant, klikt u op de *beheren van uw nieuwe koppeling van de tenant*.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Uw nieuwe koppeling van de tenant beheren](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="f4c6e-118">Als u van plan bent te gebruiken van een B2C-tenant voor een productie-app, lees het artikel op [productie-scale versus B2C preview tenants](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="f4c6e-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="f4c6e-119">Er zijn bekende problemen wanneer u een bestaande B2C-tenant verwijderen en opnieuw met dezelfde domeinnaam maken.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="f4c6e-120">U moet een B2C-tenant maken met een andere domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="f4c6e-121">Uw tenant te koppelen aan uw abonnement</span><span class="sxs-lookup"><span data-stu-id="f4c6e-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="f4c6e-122">U moet uw Azure AD B2C-tenant koppelen aan uw Azure-abonnement alle B2C-functies inschakelen en betaalt voor gebruikskosten.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="f4c6e-123">Voor meer informatie lezen [in dit artikel](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="f4c6e-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="f4c6e-124">Als u niet uw Azure AD B2C-tenant koppeling naar uw Azure-abonnement, bepaalde functionaliteit is geblokkeerd en ziet u een waarschuwing ('geen abonnement is gekoppeld aan deze B2C-tenant of de abonnement-behoeften uw aandacht.') in de B2C-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="f4c6e-125">Het is belangrijk dat u deze stap uitvoeren voordat u uw apps naar de productie verzendt.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="f4c6e-126">Eenvoudig toegang krijgen tot instellingen</span><span class="sxs-lookup"><span data-stu-id="f4c6e-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="f4c6e-127">U kunt de blade ook openen door te voeren `Azure AD B2C` in **zoeken bronnen** aan de bovenkant van de portal.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="f4c6e-128">Selecteer in de lijst met resultaten **Azure AD B2C** voor toegang tot de blade B2C-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f4c6e-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4c6e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4c6e-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4c6e-130">Uw B2C-toepassing registreren in een B2C-tenant</span><span class="sxs-lookup"><span data-stu-id="f4c6e-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
