---
title: 'Azure Active Directory B2C: overschakelen naar een B2C-tenant | Microsoft Docs'
description: Overschakelen naar de context van uw Active Directory B2C-tenant
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="9faa9-103">Overschakelen naar uw Azure AD B2C-tenant</span><span class="sxs-lookup"><span data-stu-id="9faa9-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="9faa9-104">U moet zich in de context van uw Azure AD B2C-tenant bevinden om Azure AD B2C te configureren.</span><span class="sxs-lookup"><span data-stu-id="9faa9-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="9faa9-105">Aanmelden bij de Azure AD B2C-tenant</span><span class="sxs-lookup"><span data-stu-id="9faa9-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="9faa9-106">U moet bij Azure Portal zijn aangemeld als een globale beheerder van de Azure AD B2C-tenant om naar uw Azure AD B2C-tenant te gaan.</span><span class="sxs-lookup"><span data-stu-id="9faa9-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="9faa9-107">Meld u aan bij de [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9faa9-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="9faa9-108">Schakel tenants over door te klikken op uw e-mailadres of afbeelding in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="9faa9-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="9faa9-109">In de `Directory`-lijst die wordt weergegeven selecteert u de Azure AD B2C-tenant die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="9faa9-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="9faa9-110">Azure Portal wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="9faa9-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="9faa9-111">U bent nu aangemeld bij Azure Portal in de context van uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="9faa9-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="9faa9-112">Ga naar de blade B2C-functies</span><span class="sxs-lookup"><span data-stu-id="9faa9-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="9faa9-113">Klik op **Bladeren** in de navigatiebalk aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="9faa9-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="9faa9-114">Klik op **> Meer services** en zoek vervolgens naar `Azure AD B2C` in het linker navigatievenster.</span><span class="sxs-lookup"><span data-stu-id="9faa9-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="9faa9-115">(Als u het aan het Startboard links wilt vastmaken, klikt u op de ster aan de linkerkant van Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="9faa9-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="9faa9-116">Klik op **Azure AD B2C** voor toegang tot de blade B2C-functies.</span><span class="sxs-lookup"><span data-stu-id="9faa9-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Schermafbeelding van bladeren naar de blade B2C-functies](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="9faa9-118">U moet een globale beheerder van de B2C-tenant zijn om de blade B2C-functies te kunnen openen.</span><span class="sxs-lookup"><span data-stu-id="9faa9-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="9faa9-119">Een globale beheerder van andere tenant of een gebruiker van een tenant heeft hiertoe geen toegang.</span><span class="sxs-lookup"><span data-stu-id="9faa9-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="9faa9-120">U kunt overschakelen naar uw B2C-tenant met behulp van de tenantwisselaar in de rechterbovenhoek van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9faa9-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
