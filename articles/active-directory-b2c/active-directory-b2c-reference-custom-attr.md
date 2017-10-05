---
title: 'Azure Active Directory B2C: Aangepaste kenmerken | Microsoft Docs'
description: Het gebruik van aangepaste kenmerken in Azure Active Directory B2C informatie verzamelen over uw consumenten
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
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="e4156-103">Azure Active Directory B2C: Gebruik aangepaste kenmerken voor het verzamelen van informatie over uw consumenten</span><span class="sxs-lookup"><span data-stu-id="e4156-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="e4156-104">Uw Azure Active Directory (Azure AD) B2C-directory wordt geleverd met een ingebouwde verzameling gegevens (kenmerken): voornaam, achternaam, plaats, postcode en andere kenmerken.</span><span class="sxs-lookup"><span data-stu-id="e4156-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="e4156-105">Elke consumentgerichte toepassing heeft echter unieke vereisten op welke kenmerken voor het verzamelen van consumenten.</span><span class="sxs-lookup"><span data-stu-id="e4156-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="e4156-106">Met Azure AD B2C, kunt u de set kenmerken die zijn opgeslagen op elke consumentenaccount uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="e4156-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="e4156-107">U kunt aangepaste kenmerken maken op de [Azure-portal](https://portal.azure.com/) en deze gebruiken in uw registratie-beleid, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4156-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="e4156-108">U kunt ook lezen en schrijven van deze kenmerken met behulp van de [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e4156-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e4156-109">Gebruik van aangepaste kenmerken [Azure AD Graph API Directory-Schemauitbreidingen](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4156-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="e4156-110">Een aangepast kenmerk maken</span><span class="sxs-lookup"><span data-stu-id="e4156-110">Create a custom attribute</span></span>
1. <span data-ttu-id="e4156-111">[Volg deze stappen om te navigeren naar de blade B2C-functies in de Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e4156-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e4156-112">Klik op **gebruikerskenmerken**.</span><span class="sxs-lookup"><span data-stu-id="e4156-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="e4156-113">Klik op **+Toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="e4156-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="e4156-114">Geef een **naam** voor het aangepaste kenmerk (bijvoorbeeld ' ShoeSize') en eventueel een **beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="e4156-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="e4156-115">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e4156-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4156-116">Alleen de 'tekenreeks' **gegevenstype** is momenteel beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="e4156-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="e4156-117">Het aangepaste kenmerk is nu beschikbaar in de lijst met **gebruikerskenmerken**, en voor gebruik in uw registratie-beleid.</span><span class="sxs-lookup"><span data-stu-id="e4156-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="e4156-118">Gebruik een aangepast kenmerk in het registratiebeleid</span><span class="sxs-lookup"><span data-stu-id="e4156-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="e4156-119">[Volg deze stappen om te navigeren naar de blade B2C-functies in de Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e4156-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e4156-120">Klik op **Registratiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="e4156-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="e4156-121">Klik op het registratiebeleid (bijvoorbeeld ' B2C_1_SiUp') om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="e4156-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="e4156-122">Klik op **bewerken** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="e4156-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="e4156-123">Klik op **registratiekenmerken** en selecteert u het aangepaste kenmerk (bijvoorbeeld ' ShoeSize').</span><span class="sxs-lookup"><span data-stu-id="e4156-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="e4156-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4156-124">Click **OK**.</span></span>
5. <span data-ttu-id="e4156-125">Klik op **toepassingsclaims** en selecteert u het aangepaste kenmerk.</span><span class="sxs-lookup"><span data-stu-id="e4156-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="e4156-126">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4156-126">Click **OK**.</span></span>
6. <span data-ttu-id="e4156-127">Klik op **opslaan** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="e4156-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="e4156-128">U kunt de functie 'Nu uitvoeren' op het beleid gebruiken om te controleren of de consumer-ervaring.</span><span class="sxs-lookup"><span data-stu-id="e4156-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="e4156-129">U moet nu Zie 'ShoeSize' in de lijst met kenmerken die zijn verzameld tijdens consumenten registreren en deze weergegeven in het token terug naar uw toepassing verzonden.</span><span class="sxs-lookup"><span data-stu-id="e4156-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="e4156-130">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e4156-130">Notes</span></span>
* <span data-ttu-id="e4156-131">Samen met aanmelding beleid kunnen ook aangepaste kenmerken worden gebruikt in beleid voor het registreren of aanmelden en profiel bewerken van beleid.</span><span class="sxs-lookup"><span data-stu-id="e4156-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="e4156-132">Er is een bekende beperking van aangepaste kenmerken.</span><span class="sxs-lookup"><span data-stu-id="e4156-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="e4156-133">Het is alleen de eerste keer wordt gebruikt in een beleid gemaakt en niet wanneer u deze toevoegen aan de lijst met **gebruikerskenmerken**.</span><span class="sxs-lookup"><span data-stu-id="e4156-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

