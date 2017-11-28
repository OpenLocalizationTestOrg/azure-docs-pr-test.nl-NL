---
title: 'Azure Active Directory B2C: Aangepaste kenmerken | Microsoft Docs'
description: Hoe toouse aangepaste kenmerken in Azure Active Directory B2C toocollect informatie over uw consumenten
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="1d35f-103">Azure Active Directory B2C: Gebruik aangepaste kenmerken toocollect informatie over uw consumenten</span><span class="sxs-lookup"><span data-stu-id="1d35f-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="1d35f-104">Uw Azure Active Directory (Azure AD) B2C-directory wordt geleverd met een ingebouwde verzameling gegevens (kenmerken): voornaam, achternaam, plaats, postcode en andere kenmerken.</span><span class="sxs-lookup"><span data-stu-id="1d35f-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="1d35f-105">Elke consumentgerichte toepassing heeft echter unieke vereisten op welke toogather kenmerken van consumenten.</span><span class="sxs-lookup"><span data-stu-id="1d35f-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="1d35f-106">Met Azure AD B2C, kunt u Hallo set kenmerken die zijn opgeslagen op elke consumentenaccount uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="1d35f-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="1d35f-107">U kunt aangepaste kenmerken maken op Hallo [Azure-portal](https://portal.azure.com/) en deze gebruiken in uw registratie-beleid, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d35f-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="1d35f-108">U kunt ook lezen en schrijven van deze kenmerken met behulp van Hallo [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1d35f-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1d35f-109">Gebruik van aangepaste kenmerken [Azure AD Graph API Directory-Schemauitbreidingen](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d35f-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="1d35f-110">Een aangepast kenmerk maken</span><span class="sxs-lookup"><span data-stu-id="1d35f-110">Create a custom attribute</span></span>
1. <span data-ttu-id="1d35f-111">[Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="1d35f-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="1d35f-112">Klik op **gebruikerskenmerken**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="1d35f-113">Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="1d35f-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="1d35f-114">Geef een **naam** voor Hallo aangepast kenmerk (bijvoorbeeld ' ShoeSize') en eventueel een **beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="1d35f-115">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d35f-116">Alleen Hallo 'String' **gegevenstype** is momenteel beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1d35f-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="1d35f-117">Hallo aangepast kenmerk is nu beschikbaar in de lijst met Hallo **gebruikerskenmerken**, en voor gebruik in uw registratie-beleid.</span><span class="sxs-lookup"><span data-stu-id="1d35f-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="1d35f-118">Gebruik een aangepast kenmerk in het registratiebeleid</span><span class="sxs-lookup"><span data-stu-id="1d35f-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="1d35f-119">[Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="1d35f-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="1d35f-120">Klik op **Registratiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="1d35f-121">Klik op uw tooopen registratiebeleid (bijvoorbeeld ' B2C_1_SiUp') deze.</span><span class="sxs-lookup"><span data-stu-id="1d35f-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="1d35f-122">Klik op **bewerken** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="1d35f-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="1d35f-123">Klik op **registratiekenmerken** en selecteer Hallo aangepast kenmerk (bijvoorbeeld ' ShoeSize').</span><span class="sxs-lookup"><span data-stu-id="1d35f-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="1d35f-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-124">Click **OK**.</span></span>
5. <span data-ttu-id="1d35f-125">Klik op **toepassingsclaims** en selecteer Hallo aangepast kenmerk.</span><span class="sxs-lookup"><span data-stu-id="1d35f-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="1d35f-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-126">Click **OK**.</span></span>
6. <span data-ttu-id="1d35f-127">Klik op **opslaan** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="1d35f-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="1d35f-128">Hallo 'Nu uitvoeren' functie kunt u op Hallo beleid tooverify Hallo consumer ervaring.</span><span class="sxs-lookup"><span data-stu-id="1d35f-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="1d35f-129">U moet nu Zie 'ShoeSize' in Hallo-lijst met kenmerken die zijn verzameld tijdens consumenten registreren en deze in Hallo token verzonden back tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d35f-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="1d35f-130">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1d35f-130">Notes</span></span>
* <span data-ttu-id="1d35f-131">Samen met aanmelding beleid kunnen ook aangepaste kenmerken worden gebruikt in beleid voor het registreren of aanmelden en profiel bewerken van beleid.</span><span class="sxs-lookup"><span data-stu-id="1d35f-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="1d35f-132">Er is een bekende beperking van aangepaste kenmerken.</span><span class="sxs-lookup"><span data-stu-id="1d35f-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="1d35f-133">Het is alleen Hallo eerste keer dat deze wordt gebruikt in een beleid gemaakt en niet wanneer u deze lijst met toohello toevoegen **gebruikerskenmerken**.</span><span class="sxs-lookup"><span data-stu-id="1d35f-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

