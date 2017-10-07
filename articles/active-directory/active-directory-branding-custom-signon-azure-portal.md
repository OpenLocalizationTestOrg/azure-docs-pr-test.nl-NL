---
title: aaaCustomize pagina bent aangemeld in hello Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een bedrijf huisstijl toohello Azure aanmelden pagina tooadd
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="c5ff4-103">Huisstijl tooyour aanmeldingspagina in hello Azure Active Directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="c5ff4-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="c5ff4-104">tooavoid verwarring, willen veel bedrijven tooapply een consistent uiterlijk voor alle Hallo websites en services die ze beheren.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="c5ff4-105">Azure Active Directory biedt deze mogelijkheid doordat u toocustomize Hallo vormgeving van Hallo aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c5ff4-106">Hallo-aanmeldingspagina is Hallo-pagina waarop wordt weergegeven wanneer u zich aanmeldt tooOffice 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c5ff4-107">U communiceren met deze pagina tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="c5ff4-108">Als u tooshow uw bedrijfsmerk en -kleuren en andere aanpasbare elementen op deze pagina wilt, Zie Hallo installatiekopieën toounderstand Hallo verschil tussen de twee ervaringen hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="c5ff4-109">Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **voordat** het aanpassen:</span><span class="sxs-lookup"><span data-stu-id="c5ff4-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![De Office 365-aanmeldingspagina vóór het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="c5ff4-111">Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **nadat** het aanpassen:</span><span class="sxs-lookup"><span data-stu-id="c5ff4-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![De Office 365-aanmeldingspagina na het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="c5ff4-113">Hallo-aanmeldingspagina aanpassen</span><span class="sxs-lookup"><span data-stu-id="c5ff4-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="c5ff4-114">Als u nodig hebt voor toegang op basis van een browser tooyour cloud-apps en services die uw organisatie op is geabonneerd, gebruikt u doorgaans de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="c5ff4-115">Als u wijzigingen tooyour aanmeldingspagina hebt toegepast, kan het Hallo wijzigingen tooappear tooan uur duren.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="c5ff4-116">Er wordt alleen een aanmeldingspagina met huisstijl weergegeven wanneer u een service opent met een tenantspecifieke URL, zoals https://outlook.com/**contoso**.com of https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="c5ff4-117">Wanneer u een service gebruikt met niet-tenantspecifieke URL’s (bijvoorbeeld https://mail.office365.com), wordt er een aanmeldingspagina zonder huisstijl weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="c5ff4-118">In dat geval wordt uw huisstijl weergegeven zodra u uw gebruikers-id hebt ingevoerd of een gebruikerstegel hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="c5ff4-119">Uw domeinnaam moet worden weergegeven als 'Actief' in hello **domeinen** gedeelte van hello Azure portal waarin u de huisstijl hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="c5ff4-120">Zie voor meer informatie [toevoegen van aangepaste domeinnamen](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c5ff4-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="c5ff4-121">Aanmeldingspagina huisstijl niet meegenomen toohello consumenten zich op de pagina van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="c5ff4-122">Als u zich met een Microsoft-account aanmeldt, wordt er een reeks wordt door Azure AD gebruikerstegels met, maar Hallo huisstijl van uw organisatie aanmeldingspagina van Microsoft toohello niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="c5ff4-123">Op de aanmeldingspagina Hallo **aangemeld blijven** selectievakje kunt u een tooremain gebruiker is aangemeld wanneer ze sluiten en opnieuw hun browser openen.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="c5ff4-125">Dit heeft geen invloed op de levensduur van de sessie.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-125">It does not effect session lifetime.</span></span> <span data-ttu-id="c5ff4-126">U kunt Hallo selectievakje op Hallo Azure Active Directory-aanmeldingspagina verbergen.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="c5ff4-127">Hiermee wordt aangegeven of Hallo selectievakje wordt weergegeven, hangt af van Hallo-instelling van **aangemeld uitgeschakeld blijven**.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="c5ff4-129">toohide Hallo selectievakje, configureer deze instelling te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="c5ff4-130">Sommige functies van Office 2010 en SharePoint Online, is afhankelijk van gebruikers kunnen toocheck wordt dit selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="c5ff4-131">Als u deze instelling toohidden configureert, kunnen aanvullende en onverwachte prompts toosign in uw gebruikers te zien.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="c5ff4-132">**tooadd bedrijf huisstijl tooyour map:**</span><span class="sxs-lookup"><span data-stu-id="c5ff4-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="c5ff4-133">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c5ff4-134">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="c5ff4-136">Op Hallo **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c5ff4-137">Op Hallo **gebruikers en groepen - bedrijf huisstijl** blade, selecteer Hallo **bewerken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Aangepaste huisstijl bewerken](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="c5ff4-139">Hallo-elementen die u wilt dat toocustomize wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="c5ff4-140">Alle elementen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-140">All elements are optional.</span></span>
6. <span data-ttu-id="c5ff4-141">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-141">Click **Save**.</span></span>

<span data-ttu-id="c5ff4-142">Het kan tooan uur duren voor u de wijzigingen toohello aanmelden pagina huisstijl tooappear.</span><span class="sxs-lookup"><span data-stu-id="c5ff4-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5ff4-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5ff4-143">Next steps</span></span>
[<span data-ttu-id="c5ff4-144">Taalspecifieke huisstijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="c5ff4-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
