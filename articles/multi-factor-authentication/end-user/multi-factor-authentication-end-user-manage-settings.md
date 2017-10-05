---
title: De verificatie in twee stappen instellingen beheren | Microsoft Docs
description: Beheren hoe u Azure multi-factor Authentication, inclusief het aanpassen van uw contactgegevens of configureren van uw apparaten gebruiken.
services: multi-factor-authentication
keywords: multifactor-verificatie-client, verificatieprobleem, correlatie-ID
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="4e412-104">De instellingen voor verificatie in twee stappen beheren</span><span class="sxs-lookup"><span data-stu-id="4e412-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="4e412-105">In dit artikel antwoorden op vragen over het bijwerken van de instellingen voor de verificatie of meervoudige verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="4e412-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="4e412-106">Als u problemen die zijn aangemeld bij uw account hebt, raadpleegt u [problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md) voor hulp bij probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="4e412-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="4e412-107">Waar vind ik de instellingenpagina</span><span class="sxs-lookup"><span data-stu-id="4e412-107">Where to find the settings page</span></span>
<span data-ttu-id="4e412-108">Afhankelijk van hoe uw bedrijf van Azure multi-factor Authentication instellen, zijn er enkele locaties waar u uw instellingen zoals uw telefoonnummer wijzigen kunt.</span><span class="sxs-lookup"><span data-stu-id="4e412-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="4e412-109">Als uw IT-beheerder verzonden een specifieke URL of de stappen voor het beheren van verificatie in twee stappen, volgt u deze instructies.</span><span class="sxs-lookup"><span data-stu-id="4e412-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="4e412-110">Anders moeten de volgende instructies werken voor alle andere.</span><span class="sxs-lookup"><span data-stu-id="4e412-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="4e412-111">Als u deze stappen maar dezelfde opties niet ziet, betekent dit dat uw werk of school hun eigen portal wordt aangepast.</span><span class="sxs-lookup"><span data-stu-id="4e412-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="4e412-112">Vraag uw beheerder voor de koppeling naar de Azure multi-factor Authentication-portal.</span><span class="sxs-lookup"><span data-stu-id="4e412-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="4e412-113">Aanmelden bij [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="4e412-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="4e412-114">Selecteer de accountnaam van uw in de rechterbovenhoek en selecteer vervolgens **profiel**.</span><span class="sxs-lookup"><span data-stu-id="4e412-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="4e412-115">Selecteer **aanvullende beveiligingsverificatie**.</span><span class="sxs-lookup"><span data-stu-id="4e412-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="4e412-117">De pagina extra beveiliging verificatie wordt geladen met uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="4e412-117">The Additional security verification page loads with your settings.</span></span>

    ![Proofup](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="4e412-119">Ik wil mijn telefoonnummer wijzigen of toevoegen van een secundaire getal</span><span class="sxs-lookup"><span data-stu-id="4e412-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="4e412-120">Het is belangrijk voor het configureren van een telefoonnummer van de secundaire verificatie.</span><span class="sxs-lookup"><span data-stu-id="4e412-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="4e412-121">Omdat je primaire telefoonnummer en uw mobiele app waarschijnlijk op de dezelfde telefoon zijn, is de tweede telefoonnummer de enige manier waarop u zich weer toegang te krijgen tot je account als uw telefoon is kwijtgeraakt of gestolen.</span><span class="sxs-lookup"><span data-stu-id="4e412-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="4e412-122">Als u geen toegang tot uw primaire telefoonnummer hebben en aan uw account in hulp nodig hebt, raadpleegt u onze help-onderwerpen in [problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="4e412-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="4e412-123">**Het primaire telefoonnummer wijzigen:**</span><span class="sxs-lookup"><span data-stu-id="4e412-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="4e412-124">Klik op de pagina aanvullende beveiligingsinstellingen verificatie selecteren in het tekstvak met uw huidige telefoonnummer en met uw nieuwe telefoonnummer te bewerken.</span><span class="sxs-lookup"><span data-stu-id="4e412-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="4e412-125">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e412-125">Select **Save**.</span></span>  
3. <span data-ttu-id="4e412-126">Als dit het aantal die u voor uw voorkeursoptie voor verificatie-optie gebruikt is, hebt u het nieuwe nummer controleren voordat u deze kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="4e412-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="4e412-127">**Een tweede telefoonnummer toevoegen:**</span><span class="sxs-lookup"><span data-stu-id="4e412-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="4e412-128">Op de pagina aanvullende beveiligingsinstellingen verificatie, schakel het selectievakje in naast **telefoon voor alternatieve authenticatie.**</span><span class="sxs-lookup"><span data-stu-id="4e412-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="4e412-129">Voer uw secundaire telefoonnummer in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="4e412-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="4e412-130">Selecteer **opslaan** en uw wijzigingen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="4e412-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="4e412-131">Verificatie in twee stappen opnieuw op een apparaat dat u hebt gemarkeerd als vertrouwd vereisen</span><span class="sxs-lookup"><span data-stu-id="4e412-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="4e412-132">Afhankelijk van de instellingen van uw organisatie, moet u wellicht een selectievakje met de tekst ' niet opnieuw vragen voor **X** dagen ' wanneer u verificatie in twee stappen uitvoeren op uw browser.</span><span class="sxs-lookup"><span data-stu-id="4e412-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="4e412-133">Als u dit selectievakje inschakelt en uw apparaat kwijtraakt of denkt dat uw account is geknoeid, moet u verificatie in twee stappen weer naar al uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="4e412-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="4e412-134">Selecteer op de pagina controle van extra beveiliging **multi factor authentication herstellen op eerder vertrouwde apparaten**.</span><span class="sxs-lookup"><span data-stu-id="4e412-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="4e412-135">De volgende keer dat u zich op elk apparaat aanmelden, wordt u gevraagd een verificatie in twee stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4e412-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="4e412-136">Hoe ik Microsoft Authenticator opschonen van mijn oude apparaat en verplaatsen naar een nieuwe?</span><span class="sxs-lookup"><span data-stu-id="4e412-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="4e412-137">Wanneer u de app van uw apparaat verwijderen of het apparaat opnieuw instelt, wordt de activering op de back-end niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4e412-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="4e412-138">Zie voor meer informatie [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4e412-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e412-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e412-139">Next steps</span></span>
* <span data-ttu-id="4e412-140">Problemen oplossen met tips en help op [problemen hebt met verificatie in twee stappen](multi-factor-authentication-end-user-troubleshoot.md)</span><span class="sxs-lookup"><span data-stu-id="4e412-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="4e412-141">Instellen van [app-wachtwoorden](multi-factor-authentication-end-user-app-passwords.md) voor alle apps die verificatie in twee stappen niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="4e412-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>
