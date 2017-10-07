---
title: 'Azure Active Directory B2C: Een Azure Active Directory B2C-tenant maken | Microsoft Docs'
description: In dit artikel hoe toocreate een Azure Active Directory B2C-tenant
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="cee9e-103">Een Azure Active Directory B2C-tenant maken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="cee9e-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="cee9e-104">Door Sipi bewerkt.</span><span class="sxs-lookup"><span data-stu-id="cee9e-104">Edited by Sipi.</span></span>

<span data-ttu-id="cee9e-105">Deze snelstartgids kunt u een Microsoft Azure Active Directory (Azure AD) B2C-tenant maken in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="cee9e-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="cee9e-106">Wanneer u klaar bent, hebt u een B2C-tenant toouse voor het registreren van de B2C-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cee9e-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cee9e-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cee9e-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="cee9e-108">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="cee9e-108">Log in tooAzure</span></span>

<span data-ttu-id="cee9e-109">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cee9e-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="cee9e-110">Een Azure AD B2C-tenant maken</span><span class="sxs-lookup"><span data-stu-id="cee9e-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="cee9e-111">B2C-functies kunnen niet worden ingeschakeld in uw bestaande tenants.</span><span class="sxs-lookup"><span data-stu-id="cee9e-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="cee9e-112">U moet toocreate een Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="cee9e-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="cee9e-113">Gefeliciteerd, u hebt een Azure Active Directory B2C-tenant gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cee9e-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="cee9e-114">Bent u een globale beheerder van Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="cee9e-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="cee9e-115">U kunt naar believen hoofdbeheerders toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cee9e-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="cee9e-116">tooswitch tooyour nieuwe tenant, klikt u op Hallo *beheren van uw nieuwe koppeling van de tenant*.</span><span class="sxs-lookup"><span data-stu-id="cee9e-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Uw nieuwe koppeling van de tenant beheren](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="cee9e-118">Als u van plan bent toouse een B2C-tenant voor een productie-app, leest u Hallo-artikel op [productie-scale versus B2C preview tenants](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="cee9e-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="cee9e-119">Er zijn bekende problemen bij het verwijderen van een bestaande B2C-tenant en opnieuw maken met de Hallo dezelfde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="cee9e-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="cee9e-120">U moet toocreate een B2C-tenant met een andere domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="cee9e-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="cee9e-121">Uw tenant tooyour abonnement koppelen</span><span class="sxs-lookup"><span data-stu-id="cee9e-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="cee9e-122">U moet toolink uw Azure AD B2C tenant tooyour Azure-abonnement tooenable alle B2C-functies en hiervoor te betalen voor gebruikskosten.</span><span class="sxs-lookup"><span data-stu-id="cee9e-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="cee9e-123">toolearn meer lezen [in dit artikel](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="cee9e-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="cee9e-124">Als u uw Azure AD B2C-tenant tooyour Azure-abonnement niet koppelt, bepaalde functionaliteit is geblokkeerd en ziet u een waarschuwing ('geen abonnement gekoppelde toothis B2C-tenant of Hallo abonnement vereist uw aandacht.') in Hallo B2C-instellingen.</span><span class="sxs-lookup"><span data-stu-id="cee9e-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="cee9e-125">Het is belangrijk dat u deze stap uitvoeren voordat u uw apps naar de productie verzendt.</span><span class="sxs-lookup"><span data-stu-id="cee9e-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="cee9e-126">Eenvoudige toegang toosettings</span><span class="sxs-lookup"><span data-stu-id="cee9e-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="cee9e-127">U kunt Hallo blade ook openen door te voeren `Azure AD B2C` in **zoeken bronnen** Hallo boven aan het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="cee9e-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="cee9e-128">Selecteer in de lijst met resultaten Hallo **Azure AD B2C** tooaccess Hallo blade B2C-instellingen.</span><span class="sxs-lookup"><span data-stu-id="cee9e-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cee9e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cee9e-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cee9e-130">Uw B2C-toepassing registreren in een B2C-tenant</span><span class="sxs-lookup"><span data-stu-id="cee9e-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
