---
title: De huisstijl specifieke taal zijn gebonden aan de aanmeldingspagina in Azure Active Directory toevoegen | Microsoft Docs
description: Informatie over het toevoegen van een specifieke taal-bedrijf huisstijl afbeeldingen en tekst naar een Azure-aanmeldingspagina
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
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="16d71-103">De huisstijl specifieke taal zijn gebonden aan de aanmeldingspagina in Azure Active Directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="16d71-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="16d71-104">Om verwarring te voorkomen, willen veel bedrijven een consistente look gebruiken voor alle websites en services die ze beheren.</span><span class="sxs-lookup"><span data-stu-id="16d71-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="16d71-105">Azure Active Directory biedt deze mogelijkheid doordat u pas het uiterlijk van de aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen.</span><span class="sxs-lookup"><span data-stu-id="16d71-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="16d71-106">De aanmeldingspagina is de pagina die wordt weergegeven wanneer u zich aanmeldt bij Office 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="16d71-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="16d71-107">U communiceert met deze pagina uw referenties in te voeren.</span><span class="sxs-lookup"><span data-stu-id="16d71-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="16d71-108">De aanmeldingspagina voor een andere taal aanpassen</span><span class="sxs-lookup"><span data-stu-id="16d71-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="16d71-109">U kunt specifieke taal zijn gebonden elementen toevoegen aan uw aangepaste pagina aanmelden alleen als u een aangepaste aanmeldingspagina al hebt gemaakt zoals beschreven in [toevoegen aan uw aanmeldingspagina huisstijl van uw bedrijf](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16d71-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="16d71-110">U kunt een aanmeldingspagina per directory configureren met een standaardset aanpasbare elementen.</span><span class="sxs-lookup"><span data-stu-id="16d71-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="16d71-111">Nadat u de standaardset van pagina-elementen hebt geconfigureerd, kunt u meer versies voor verschillende talen.</span><span class="sxs-lookup"><span data-stu-id="16d71-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="16d71-112">U kunt ook een combinatie van verschillende elementen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16d71-112">You can also mix and match various elements.</span></span> <span data-ttu-id="16d71-113">U kunt bijvoorbeeld het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="16d71-113">For example, you could:</span></span>

* <span data-ttu-id="16d71-114">Maken van een standaard **aanmelden pagina-afbeelding** dat werkt voor alle culturen en afzonderlijke versies maken voor de Engelse en Franse.</span><span class="sxs-lookup"><span data-stu-id="16d71-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="16d71-115">Als u een browser op een van deze twee talen instelt, de taalspecifieke afbeelding wordt weergegeven, terwijl de standaardafbeelding voor alle andere talen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16d71-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="16d71-116">Voor uw organisatie verschillende logo's configureren (bijvoorbeeld een Japanse en een Hebreeuwse versie).</span><span class="sxs-lookup"><span data-stu-id="16d71-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="16d71-117">We adviseren dat u het aantal variaties taal lage omwille van onderhoud en prestaties.</span><span class="sxs-lookup"><span data-stu-id="16d71-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="16d71-118">**Toevoegen aan uw directory huisstijl van uw bedrijf:**</span><span class="sxs-lookup"><span data-stu-id="16d71-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="16d71-119">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="16d71-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="16d71-120">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="16d71-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="16d71-122">Op de **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.</span><span class="sxs-lookup"><span data-stu-id="16d71-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="16d71-123">Op de **gebruikers en groepen - bedrijf huisstijl** blade, selecteer de **taal toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="16d71-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![De huisstijl elementen taalspecifieke toevoegen](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="16d71-125">Wijzig de elementen die u wilt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="16d71-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="16d71-126">Alle elementen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="16d71-126">All elements are optional.</span></span>
6. <span data-ttu-id="16d71-127">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="16d71-127">Click **Save**.</span></span>

<span data-ttu-id="16d71-128">Dit kan een uur duren voor alle wijzigingen naar de pagina aanmeldingspagina met huisstijl weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16d71-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16d71-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16d71-129">Next steps</span></span>
[<span data-ttu-id="16d71-130">Huisstijl aan uw aanmeldingspagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="16d71-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
