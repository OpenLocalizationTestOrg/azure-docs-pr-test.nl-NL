---
title: Aanpassen van de aanmeldingspagina in Azure Active Directory | Microsoft Docs
description: Informatie over het toevoegen van een huisstijl naar de Azure-aanmeldingspagina
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="a15b2-103">Huisstijl aan uw pagina aanmelden in de Azure Active Directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="a15b2-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="a15b2-104">Om verwarring te voorkomen, willen veel bedrijven een consistente look gebruiken voor alle websites en services die ze beheren.</span><span class="sxs-lookup"><span data-stu-id="a15b2-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="a15b2-105">Azure Active Directory biedt deze mogelijkheid doordat u pas het uiterlijk van de aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="a15b2-106">De aanmeldingspagina is de pagina die wordt weergegeven wanneer u zich aanmeldt bij Office 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="a15b2-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="a15b2-107">U communiceert met deze pagina uw referenties in te voeren.</span><span class="sxs-lookup"><span data-stu-id="a15b2-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="a15b2-108">Als u op deze pagina uw bedrijfsmerk en -kleuren en andere aanpasbare elementen wilt weergeven, bekijkt u de volgende afbeeldingen om inzicht te krijgen in het verschil tussen de twee ervaringen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="a15b2-109">In de volgende schermafbeelding ziet u een voorbeeld van de Office 365-aanmeldingspagina op een desktopcomputer **vóór** het aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a15b2-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![De Office 365-aanmeldingspagina vóór het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="a15b2-111">In de volgende schermafbeelding ziet u een voorbeeld van de Office 365-aanmeldingspagina op een desktopcomputer **na** het aanpassen:</span><span class="sxs-lookup"><span data-stu-id="a15b2-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![De Office 365-aanmeldingspagina na het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="a15b2-113">De aanmeldingspagina aanpassen</span><span class="sxs-lookup"><span data-stu-id="a15b2-113">Customizing the sign-in page</span></span>
<span data-ttu-id="a15b2-114">Als u browsertoegang nodig hebt om de cloud-apps en -services te openen waar uw organisatie op is geabonneerd, gebruikt u de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="a15b2-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="a15b2-115">Als u wijzigingen hebt aangebracht aan uw aanmeldingspagina, kan het een uur duren voordat de wijzigingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a15b2-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="a15b2-116">Er wordt alleen een aanmeldingspagina met huisstijl weergegeven wanneer u een service opent met een tenantspecifieke URL, zoals https://outlook.com/**contoso**.com of https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="a15b2-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="a15b2-117">Wanneer u een service gebruikt met niet-tenantspecifieke URL’s (bijvoorbeeld https://mail.office365.com), wordt er een aanmeldingspagina zonder huisstijl weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a15b2-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="a15b2-118">In dat geval wordt uw huisstijl weergegeven zodra u uw gebruikers-id hebt ingevoerd of een gebruikerstegel hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a15b2-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="a15b2-119">Uw domeinnaam moet worden weergegeven als 'Actief' de **domeinen** gedeelte van de Azure portal waarin u de huisstijl hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a15b2-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="a15b2-120">Zie voor meer informatie [toevoegen van aangepaste domeinnamen](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a15b2-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="a15b2-121">De huisstijl van de aanmeldingspagina wordt niet meegenomen naar de Microsoft-aanmeldingspagina voor klanten.</span><span class="sxs-lookup"><span data-stu-id="a15b2-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="a15b2-122">Als u zich met een Microsoft-account aanmeldt, wordt er een reeks wordt door Azure AD gebruikerstegels met, maar de huisstijl van uw organisatie niet van toepassing op de Microsoft-account aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="a15b2-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="a15b2-123">Op de aanmeldingspagina kunnen gebruikers er met het selectievakje **Aangemeld blijven** voor zorgen dat ze aangemeld blijven als ze hun browser sluiten en opnieuw openen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="a15b2-125">Dit heeft geen invloed op de levensduur van de sessie.</span><span class="sxs-lookup"><span data-stu-id="a15b2-125">It does not effect session lifetime.</span></span> <span data-ttu-id="a15b2-126">U kunt het selectievakje op de aanmeldingspagina van Azure Active Directory verbergen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="a15b2-127">Hiermee wordt aangegeven of het selectievakje wordt weergegeven, hangt af van de instelling van **aangemeld uitgeschakeld blijven**.</span><span class="sxs-lookup"><span data-stu-id="a15b2-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="a15b2-129">Als u wilt het selectievakje verbergen, configureert u deze instelling om te **Ja**.</span><span class="sxs-lookup"><span data-stu-id="a15b2-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="a15b2-130">Of sommige functies van SharePoint Online en Office 2010 beschikbaar zijn, hangt ervan of gebruikers dit selectievakje wel of niet kunnen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="a15b2-131">Als u deze instelling instelt op Verborgen, krijgen uw gebruikers mogelijk extra en onverwachte prompts te zien om zich aan te melden.</span><span class="sxs-lookup"><span data-stu-id="a15b2-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="a15b2-132">**Toevoegen aan uw directory huisstijl van uw bedrijf:**</span><span class="sxs-lookup"><span data-stu-id="a15b2-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="a15b2-133">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="a15b2-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a15b2-134">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a15b2-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="a15b2-136">Op de **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.</span><span class="sxs-lookup"><span data-stu-id="a15b2-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="a15b2-137">Op de **gebruikers en groepen - bedrijf huisstijl** blade, selecteer de **bewerken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a15b2-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Aangepaste huisstijl bewerken](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="a15b2-139">Wijzig de elementen die u wilt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a15b2-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="a15b2-140">Alle elementen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="a15b2-140">All elements are optional.</span></span>
6. <span data-ttu-id="a15b2-141">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a15b2-141">Click **Save**.</span></span>

<span data-ttu-id="a15b2-142">Dit kan een uur duren voor alle wijzigingen naar de pagina aanmeldingspagina met huisstijl weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a15b2-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a15b2-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a15b2-143">Next steps</span></span>
[<span data-ttu-id="a15b2-144">Taalspecifieke huisstijl toevoegen</span><span class="sxs-lookup"><span data-stu-id="a15b2-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
