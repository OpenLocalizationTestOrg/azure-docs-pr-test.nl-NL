---
title: aaaAdd taalspecifieke huisstijl tooyour aanmeldingspagina in hello Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een specifieke taal tooadd bedrijf huisstijl afbeeldingen en tekst tooan Azure aanmelden pagina
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="c94de-103">Tooyour aanmeldingspagina in hello Azure Active Directory voor taalspecifieke huisstijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="c94de-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="c94de-104">tooavoid verwarring, willen veel bedrijven tooapply een consistent uiterlijk voor alle Hallo websites en services die ze beheren.</span><span class="sxs-lookup"><span data-stu-id="c94de-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="c94de-105">Azure Active Directory biedt deze mogelijkheid doordat u toocustomize Hallo vormgeving van Hallo aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen.</span><span class="sxs-lookup"><span data-stu-id="c94de-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c94de-106">Hallo-aanmeldingspagina is Hallo-pagina waarop wordt weergegeven wanneer u zich aanmeldt tooOffice 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="c94de-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c94de-107">U communiceren met deze pagina tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="c94de-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="c94de-108">Hallo-aanmeldingspagina voor een andere taal aanpassen</span><span class="sxs-lookup"><span data-stu-id="c94de-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="c94de-109">U kunt de taalspecifieke elementen tooyour aangepaste aanmeldingspagina toevoegen alleen als u een aangepaste aanmeldingspagina al hebt gemaakt zoals beschreven in [tooyour-aanmeldingspagina huisstijl toevoegen](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c94de-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="c94de-110">U kunt een aanmeldingspagina per directory configureren met een standaardset aanpasbare elementen.</span><span class="sxs-lookup"><span data-stu-id="c94de-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="c94de-111">Nadat u de standaardset Hallo van pagina-elementen hebt geconfigureerd, kunt u meer versies voor verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="c94de-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="c94de-112">U kunt ook een combinatie van verschillende elementen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c94de-112">You can also mix and match various elements.</span></span> <span data-ttu-id="c94de-113">U kunt bijvoorbeeld het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c94de-113">For example, you could:</span></span>

* <span data-ttu-id="c94de-114">Maken van een standaard **aanmelden pagina-afbeelding** dat werkt voor alle culturen en afzonderlijke versies maken voor de Engelse en Franse.</span><span class="sxs-lookup"><span data-stu-id="c94de-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="c94de-115">Bij het instellen van uw tooone browsers van die twee talen Hallo taalspecifieke afbeelding wordt weergegeven, terwijl de standaardafbeelding hello wordt weergegeven voor alle andere talen.</span><span class="sxs-lookup"><span data-stu-id="c94de-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="c94de-116">Voor uw organisatie verschillende logo's configureren (bijvoorbeeld een Japanse en een Hebreeuwse versie).</span><span class="sxs-lookup"><span data-stu-id="c94de-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="c94de-117">We adviseren dat u Hallo aantal taal variaties lage omwille van onderhoud en prestaties.</span><span class="sxs-lookup"><span data-stu-id="c94de-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="c94de-118">**tooadd bedrijf huisstijl tooyour map:**</span><span class="sxs-lookup"><span data-stu-id="c94de-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="c94de-119">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c94de-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c94de-120">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c94de-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="c94de-122">Op Hallo **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.</span><span class="sxs-lookup"><span data-stu-id="c94de-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c94de-123">Op Hallo **gebruikers en groepen - bedrijf huisstijl** blade, selecteer Hallo **taal toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="c94de-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![De huisstijl elementen taalspecifieke toevoegen](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="c94de-125">Hallo-elementen die u wilt dat toocustomize wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c94de-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="c94de-126">Alle elementen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="c94de-126">All elements are optional.</span></span>
6. <span data-ttu-id="c94de-127">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c94de-127">Click **Save**.</span></span>

<span data-ttu-id="c94de-128">Het kan tooan uur duren voor u de wijzigingen toohello aanmelden pagina huisstijl tooappear.</span><span class="sxs-lookup"><span data-stu-id="c94de-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c94de-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c94de-129">Next steps</span></span>
[<span data-ttu-id="c94de-130">De aanmeldingspagina tooyour huisstijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="c94de-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
