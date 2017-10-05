---
title: De elementen van het e-mailbericht van Azure Active Directory B2B-samenwerking uitnodiging | Microsoft Docs
description: Azure Active Directory B2B-samenwerking uitnodiging voor een e-mailsjabloon
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="fd336-103">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="fd336-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="fd336-104">Een uitnodiging voor e-mailberichten zijn een essentieel onderdeel op te zetten van partners aan boord als B2B-samenwerking gebruikers in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd336-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="fd336-105">U kunt deze gebruiken om te verhogen van de geadresseerde vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="fd336-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="fd336-106">u kunt legitimiteit toevoegen en sociale bewijs in de e-mail om te controleren of de ontvanger werkt bekendheid met het selecteren van de **aan de slag** knop de uitnodiging te accepteren.</span><span class="sxs-lookup"><span data-stu-id="fd336-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="fd336-107">Deze vertrouwensrelatie is dat een sleutel betekent dat u wilt delen wrijving verminderen.</span><span class="sxs-lookup"><span data-stu-id="fd336-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="fd336-108">En u wilt er ook voor het e-mailadres er fantastisch uitzien!</span><span class="sxs-lookup"><span data-stu-id="fd336-108">And you also want to make the email look great!</span></span>

![Azure AD B2b-uitnodigingsmail](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="fd336-110">Het e-mailbericht waarin wordt uitgelegd</span><span class="sxs-lookup"><span data-stu-id="fd336-110">Explaining the email</span></span>
<span data-ttu-id="fd336-111">Bekijk enkele elementen van het e-mailadres zodat u hoe het beste weet hun mogelijkheden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fd336-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="fd336-112">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="fd336-112">Subject</span></span>
<span data-ttu-id="fd336-113">Het onderwerp van het e-mailbericht volgt u de volgende notatie: U bent uitgenodigd voor de &lt;tenantname&gt; organisatie</span><span class="sxs-lookup"><span data-stu-id="fd336-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="fd336-114">Van-adres</span><span class="sxs-lookup"><span data-stu-id="fd336-114">From address</span></span>
<span data-ttu-id="fd336-115">We gebruiken een LinkedIn patroon voor het adres van de afzender.</span><span class="sxs-lookup"><span data-stu-id="fd336-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="fd336-116">U moet wissen die afzender van de uitnodiging is en waaruit de bedrijfsportal en ook verduidelijken dat het e-mailbericht afkomstig is van een Microsoft e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="fd336-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="fd336-117">De indeling is: &lt;weergavenaam van de uitnodiging antwoorden&gt; van &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="fd336-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="fd336-118">Beantwoorden</span><span class="sxs-lookup"><span data-stu-id="fd336-118">Reply To</span></span>
<span data-ttu-id="fd336-119">Het antwoord aan e-mailbericht is ingesteld op van de afzender van de uitnodiging e indien beschikbaar, zodat u het e-mailbericht beantwoordt een e-mailbericht teruggestuurd naar de uitnodiging antwoorden wordt.</span><span class="sxs-lookup"><span data-stu-id="fd336-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="fd336-120">De huisstijl</span><span class="sxs-lookup"><span data-stu-id="fd336-120">Branding</span></span>
<span data-ttu-id="fd336-121">De uitnodiging voor een e-mailberichten van uw gebruik van de tenant de huisstijl die u mogelijk hebt ingesteld voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="fd336-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="fd336-122">Als u wilt profiteren van deze mogelijkheid [hier](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) vindt u de details over het configureren van deze.</span><span class="sxs-lookup"><span data-stu-id="fd336-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="fd336-123">Het logo in banner wordt weergegeven in het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="fd336-123">The banner logo appears in the email.</span></span> <span data-ttu-id="fd336-124">Voer de grootte van de installatiekopie en kwaliteit instructies [hier](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) voor de beste resultaten.</span><span class="sxs-lookup"><span data-stu-id="fd336-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="fd336-125">Bovendien de bedrijfsnaam wordt ook weergegeven in de aanroep aan de actie.</span><span class="sxs-lookup"><span data-stu-id="fd336-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="fd336-126">Aanroep van bewerking</span><span class="sxs-lookup"><span data-stu-id="fd336-126">Call to action</span></span>
<span data-ttu-id="fd336-127">De aanroep van bewerking bestaat uit twee delen: waarin wordt uitgelegd waarom de ontvanger het e-mailbericht heeft ontvangen en wat de ontvanger is wordt gevraagd om u te doen.</span><span class="sxs-lookup"><span data-stu-id="fd336-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="fd336-128">De sectie 'Waarom' kan worden aangepakt met behulp van het volgende patroon volgen: U bent uitgenodigd voor toegang tot toepassingen in de &lt;tenantname&gt; organisatie</span><span class="sxs-lookup"><span data-stu-id="fd336-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="fd336-129">En de 'wat u wordt gevraagd om te doen' sectie wordt aangegeven door de aanwezigheid van de **aan de slag** knop.</span><span class="sxs-lookup"><span data-stu-id="fd336-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="fd336-130">Als de ontvanger zonder de noodzaak van uitnodigingen is toegevoegd, weergegeven deze knop niet.</span><span class="sxs-lookup"><span data-stu-id="fd336-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="fd336-131">De uitnodiging antwoorden informatie</span><span class="sxs-lookup"><span data-stu-id="fd336-131">Inviter's information</span></span>
<span data-ttu-id="fd336-132">Weergavenaam van de afzender van de uitnodiging is opgenomen in het e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="fd336-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="fd336-133">En daarnaast als u een profielfoto voor uw Azure AD-account hebt ingesteld, het uitnodigen e-mailbericht omvatten ook afbeelding.</span><span class="sxs-lookup"><span data-stu-id="fd336-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="fd336-134">Beide zijn bedoeld om meer vertrouwen in de e-mail van de geadresseerde.</span><span class="sxs-lookup"><span data-stu-id="fd336-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="fd336-135">Als u nog uw profielfoto niet hebt ingesteld, wordt een pictogram met de initialen van de afzender van de uitnodiging in plaats van de afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="fd336-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![Initialen van de afzender van de uitnodiging weergeven](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="fd336-137">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="fd336-137">Body</span></span>
<span data-ttu-id="fd336-138">De hoofdtekst van bevat het bericht dat de afzender van de uitnodiging stelt het bericht of wordt doorgegeven aan de uitnodiging API.</span><span class="sxs-lookup"><span data-stu-id="fd336-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="fd336-139">Het is een tekstgebied, zodat deze geen HTML-tags uit veiligheidsoverwegingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="fd336-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="fd336-140">Voettekstsectie</span><span class="sxs-lookup"><span data-stu-id="fd336-140">Footer section</span></span>
<span data-ttu-id="fd336-141">De voettekst bevat van de Microsoft-bedrijfsmerk en stelt de ontvanger weten of het e-mailbericht is verzonden vanaf een niet-bewaakte alias.</span><span class="sxs-lookup"><span data-stu-id="fd336-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="fd336-142">Speciale gevallen:</span><span class="sxs-lookup"><span data-stu-id="fd336-142">Special cases:</span></span>

- <span data-ttu-id="fd336-143">De uitnodiging antwoorden geen een e-mailadres in de uitnodiging tenancymodus</span><span class="sxs-lookup"><span data-stu-id="fd336-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![afbeelding van uitnodiging antwoorden geen een e-mailadres in de uitnodiging tenancymodus](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="fd336-145">De ontvanger hoeft niet te nemen van de uitnodiging</span><span class="sxs-lookup"><span data-stu-id="fd336-145">The recipient doesn't need to redeem the invitation</span></span>

  ![Wanneer de ontvanger niet hoeft te uitnodiging inwisselen](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="fd336-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fd336-147">Next steps</span></span>

<span data-ttu-id="fd336-148">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="fd336-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="fd336-149">Wat is Azure AD B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="fd336-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="fd336-150">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="fd336-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="fd336-151">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="fd336-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="fd336-152">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="fd336-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="fd336-153">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="fd336-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="fd336-154">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="fd336-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="fd336-155">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="fd336-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="fd336-156">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="fd336-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="fd336-157">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="fd336-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="fd336-158">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="fd336-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="fd336-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="fd336-159">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
