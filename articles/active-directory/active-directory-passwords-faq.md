---
title: 'Veelgestelde vragen over: Azure AD SSPR | Microsoft Docs'
description: Veelgestelde vragen over Azure AD zelf uw wachtwoord opnieuw instellen
services: active-directory
keywords: Wachtwoordbeheer Active directory, wachtwoordbeheer, Azure AD self service voor wachtwoordherstel
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="a008e-104">Veelgestelde vragen over wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="a008e-104">Password management frequently asked questions</span></span>

<span data-ttu-id="a008e-105">Hier volgen enkele veelgestelde vragen voor alle bewerkingen die betrekking hebben op wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="a008e-106">Als er een algemene vraag over Azure AD en zelf uw wachtwoord opnieuw instellen, die niet wordt beantwoord hier, kunt u vragen de community om hulp op de [Azure Ad-forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="a008e-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="a008e-107">Leden van de community opnemen Engineers, Product Managers, MVP's en fellow IT-Professionals.</span><span class="sxs-lookup"><span data-stu-id="a008e-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="a008e-108">Deze Veelgestelde vragen wordt opgedeeld in de volgende secties:</span><span class="sxs-lookup"><span data-stu-id="a008e-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="a008e-109">**Vragen over het registreren voor wachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="a008e-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="a008e-110">**Vragen over wachtwoordherstel**</span><span class="sxs-lookup"><span data-stu-id="a008e-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="a008e-111">**Vragen over het wijzigen van wachtwoorden**</span><span class="sxs-lookup"><span data-stu-id="a008e-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="a008e-112">**Rapporten voor vragen over wachtwoordbeheer**</span><span class="sxs-lookup"><span data-stu-id="a008e-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="a008e-113">**Vragen over Write-back van wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="a008e-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="a008e-114">Registratie voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="a008e-114">Password reset registration</span></span>
* <span data-ttu-id="a008e-115">**V: kunnen mijn gebruikers registreren hun eigen wachtwoord opnieuw instellen van gegevens?**</span><span class="sxs-lookup"><span data-stu-id="a008e-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="a008e-116">**A:** Ja, zoals wachtwoord opnieuw instellen is ingeschakeld en worden ze in licentie gegeven, kunnen ze naar de portal van de registratie voor wachtwoord opnieuw instellen op http://aka.ms/ssprsetup registreren hun verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="a008e-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="a008e-117">Gebruikers kunnen ook registreren door te gaan naar het toegangspaneel bij http://myapps.microsoft.com, te klikken op het profieltabblad en te klikken op het Register voor de optie wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="a008e-118">**V: kan ik wachtwoord opnieuw instellen van gegevens definiëren namens mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="a008e-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="a008e-119">**A:** Ja, u kunt dit doen met Azure AD Connect, PowerShell, de [Azure-portal](https://portal.azure.com), of de beheerder van Office-portal.</span><span class="sxs-lookup"><span data-stu-id="a008e-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="a008e-120">Zie voor meer informatie het artikel [gegevens die worden gebruikt door Azure AD selfservice voor wachtwoordherstel](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="a008e-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="a008e-121">**V: kan ik gegevens voor vragen over de beveiliging van on-premises synchroniseren?**</span><span class="sxs-lookup"><span data-stu-id="a008e-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="a008e-122">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="a008e-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="a008e-123">**V: kunnen mijn gebruikers gegevens registreren zodanig dat deze gegevens door andere gebruikers niet zien?**</span><span class="sxs-lookup"><span data-stu-id="a008e-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="a008e-124">**A:** Ja, wanneer gebruikers zich registreren voor gegevens met behulp van de Wachtwoordregistratieportal opnieuw instellen dat het wordt opgeslagen in persoonlijke verificatie velden die alleen zichtbaar voor globale beheerders en de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a008e-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="a008e-125">Als een **Azure Administrator-account** registreert hun telefoonnummer verificatie deze ook worden ingevuld in het veld mobiele telefoon en zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="a008e-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="a008e-126">**V: Mijn gebruikers hoeft te worden geregistreerd voordat ze kunnen voor wachtwoordherstel gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="a008e-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="a008e-127">**A:** Nee, als u onvoldoende verificatiegegevens namens hen definieert, gebruikers niet hoeven te registreren.</span><span class="sxs-lookup"><span data-stu-id="a008e-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="a008e-128">Wachtwoord opnieuw moet worden ingesteld als u hebt opgeslagen gegevens in de juiste velden in de map juist opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="a008e-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="a008e-129">**V: kan ik synchroniseren of instellen van de telefoon voor authenticatie, authenticatie-e-mailadres of andere telefoon voor authenticatie velden namens mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="a008e-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="a008e-130">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="a008e-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="a008e-131">**V: hoe de portal voor wachtwoordregistratie weet welke opties mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="a008e-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="a008e-132">**A:** de registratieportal voor wachtwoordherstel alleen ziet u de opties die u hebt ingeschakeld voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a008e-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="a008e-133">Deze opties zijn gevonden onder de sectie gebruiker opnieuw instellen wachtwoordbeleid van uw directory configureren tabblad.</span><span class="sxs-lookup"><span data-stu-id="a008e-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="a008e-134">Dit betekent bijvoorbeeld dat als u vragen over de beveiliging niet inschakelt, klikt u vervolgens gebruikers zich niet kunnen registreren voor die optie.</span><span class="sxs-lookup"><span data-stu-id="a008e-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="a008e-135">**V: wanneer een gebruiker als beschouwd ingeschreven?**</span><span class="sxs-lookup"><span data-stu-id="a008e-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="a008e-136">**A:** een gebruiker wordt beschouwd geregistreerd voor SSPR, wanneer zij hebben geregistreerd ten minste de **aantal methoden die zijn vereist om in te stellen** die u hebt ingesteld in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a008e-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="a008e-137">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="a008e-137">Password reset</span></span>
* <span data-ttu-id="a008e-138">**V: hoe lang moet ik wachten om te ontvangen van een e-mail, SMS of telefoongesprek van wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="a008e-139">**A:** SMS-berichten, e-mailadres en telefoongesprekken moet binnenkomen in onder één minuut, met het normale geval wordt de 5-20 seconden.</span><span class="sxs-lookup"><span data-stu-id="a008e-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="a008e-140">Als u de melding niet binnen deze tijd ontvangt:</span><span class="sxs-lookup"><span data-stu-id="a008e-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="a008e-141">Controleer de map Ongewenste e-mail.</span><span class="sxs-lookup"><span data-stu-id="a008e-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="a008e-142">Controleer het nummer of de e-mailadres waarmee contact wordt opgenomen is die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="a008e-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="a008e-143">Controleer dat de verificatiegegevens in de map is juist opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="a008e-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="a008e-144">Voorbeeld: "+ 1 4255551234' of 'user@contoso.com'</span><span class="sxs-lookup"><span data-stu-id="a008e-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="a008e-145">**V: welke talen worden ondersteund door het wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="a008e-146">**A:** -gebruikersinterface voor het wachtwoord opnieuw instellen van SMS-berichten en telefoongesprekken in dezelfde talen worden ondersteund in Office 365 worden gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="a008e-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="a008e-147">**V: welke onderdelen van de ervaring van wachtwoord opnieuw instellen wanneer ik ingesteld organisatie huisstijl in mijn directory ophalen huisstijl het tabblad configureren?**</span><span class="sxs-lookup"><span data-stu-id="a008e-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="a008e-148">**A:** de portal voor wachtwoord opnieuw instellen, ziet u het logo van uw organisatie en kunt u configureren van de contact op met uw beheerder koppeling om te verwijzen naar een aangepaste e-mailadres of URL.</span><span class="sxs-lookup"><span data-stu-id="a008e-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="a008e-149">Een e-mailbericht dat wordt verzonden door het wachtwoord opnieuw instellen van uw organisatie logo, de kleuren, de naam in de hoofdtekst van het e-mailbericht bevat en aangepast met de naam van.</span><span class="sxs-lookup"><span data-stu-id="a008e-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="a008e-150">**V: hoe kan ik mijn gebruikers opleiden waar u om hun wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="a008e-151">**A:** kunt u uw gebruikers rechtstreeks naar https://passwordreset.microsoftonline.com verzenden of u kunt de opdracht op te geven de **heeft geen toegang tot uw accountkoppeling** gevonden op eventuele werk of School-aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="a008e-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="a008e-152">U kunt deze koppelingen ook publiceren op een locatie die gemakkelijk toegankelijk is voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a008e-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="a008e-153">**V: kan ik deze pagina vanaf een mobiel apparaat gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="a008e-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="a008e-154">**A:** Ja, deze pagina werkt op mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="a008e-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="a008e-155">**V: ondersteund ontgrendelen lokale active directory-accounts wanneer gebruikers hun wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="a008e-156">**A:** Ja, als hun wachtwoord opnieuw instellen van een gebruiker en wachtwoord terugschrijven is geïmplementeerd met Azure AD Connect, die gebruikersaccount is automatisch ontgrendeld wanneer ze hun wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="a008e-157">**V: hoe kan ik wachtwoordherstel rechtstreeks in mijn gebruiker aanmelden Bureaubladervaring worden geïntegreerd?**</span><span class="sxs-lookup"><span data-stu-id="a008e-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="a008e-158">**A:** als u een Azure AD Premium-klant bent, kunt u Microsoft Identity Manager installeren zonder extra kosten en implementeren van de on-premises-oplossing wachtwoord opnieuw instellen om te voldoen aan deze vereiste.</span><span class="sxs-lookup"><span data-stu-id="a008e-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="a008e-159">**V: kan ik andere beveiligingsvragen voor verschillende talen instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="a008e-160">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="a008e-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="a008e-161">**V: hoe zoveel mogelijk vragen kunnen we configureren voor de verificatie-optie beveiligingsvragen**</span><span class="sxs-lookup"><span data-stu-id="a008e-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="a008e-162">**A:** kunt u maximaal 20 aangepaste beveiligingsvragen in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a008e-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="a008e-163">**V: hoe lang mogelijk beveiligingsvragen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="a008e-164">**A:** beveiligingsvragen mogelijk tussen 3 en 200 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="a008e-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="a008e-165">**V: hoe lang mogelijk antwoorden op beveiligingsvragen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="a008e-166">**A:** antwoorden mogelijk 3 tot 40 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="a008e-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="a008e-167">**V: zijn dubbele antwoorden op beveiligingsvragen afgewezen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="a008e-168">**A:** Ja, er dubbele antwoorden op beveiligingsvragen afwijzen.</span><span class="sxs-lookup"><span data-stu-id="a008e-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="a008e-169">**V: kan registreren van een gebruiker de dezelfde beveiligingsvraag het meer dan één keer?**</span><span class="sxs-lookup"><span data-stu-id="a008e-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="a008e-170">**A:** Nee, wanneer een gebruiker zich registreert voor een bepaald criterium, ze kunnen niet worden geregistreerd voor deze vraag een tweede keer.</span><span class="sxs-lookup"><span data-stu-id="a008e-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="a008e-171">**V: is het mogelijk is de ondergrens van beveiligingsvragen voor registratie instellen en resetten?**</span><span class="sxs-lookup"><span data-stu-id="a008e-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="a008e-172">**A:** Ja, een limiet kan worden ingesteld voor registratie en een andere voor het opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="a008e-173">3-5-beveiligingsvragen mogelijk zijn vereist voor inschrijving en 3-5 mogelijk zijn vereist voor opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="a008e-174">**V: als een gebruiker meer dan het maximum aantal vragen dat vereist is om in te stellen is geregistreerd, hoe beveiligingsvragen geselecteerd tijdens het opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="a008e-175">**A:** N beveiligingsvragen willekeurig geselecteerd van het totale aantal vragen dat een gebruiker is geregistreerd, waarbij N staat voor de **aantal vragen dat vereist is om in te stellen**.</span><span class="sxs-lookup"><span data-stu-id="a008e-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="a008e-176">Bijvoorbeeld, als een gebruiker 5 beveiligingsvragen geregistreerd heeft, maar alleen 3 nodig zijn om in te stellen, zijn 3 van de 5 willekeurig geselecteerd en gepresenteerd op opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="a008e-177">Als de gebruiker de antwoorden op de vragen verkeerde ontvangt, wordt het selectieproces om te voorkomen dat vraag hammering optreedt.</span><span class="sxs-lookup"><span data-stu-id="a008e-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="a008e-178">**V: heb u voorkomen dat gebruikers vaak in een korte periode voor wachtwoordherstel probeert?**</span><span class="sxs-lookup"><span data-stu-id="a008e-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="a008e-179">**A:** Ja, er zijn ingebouwd in het wachtwoord opnieuw instellen om te beveiligen tegen misbruik beveiligingsfuncties.</span><span class="sxs-lookup"><span data-stu-id="a008e-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="a008e-180">Gebruikers kunnen alleen proberen opnieuw instellen van 5 wachtwoordpogingen binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="a008e-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="a008e-181">Gebruikers kunnen alleen proberen te valideren een telefoonnummer 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="a008e-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="a008e-182">Gebruikers kunnen alleen een één verificatiemethode proberen 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="a008e-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="a008e-183">**V: voor hoe lang de e-mail en SMS eenmalige wachtwoordcode geldig zijn?**</span><span class="sxs-lookup"><span data-stu-id="a008e-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="a008e-184">**A:** de levensduur van de sessie voor wachtwoordherstel is 105 minuten.</span><span class="sxs-lookup"><span data-stu-id="a008e-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="a008e-185">Vanaf het begin van de bewerking van wachtwoord opnieuw instellen van heeft de gebruiker 105 minuten hun wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="a008e-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="a008e-186">De e-mail en SMS eenmalige wachtwoordcode zijn ongeldig nadat deze periode is verstreken.</span><span class="sxs-lookup"><span data-stu-id="a008e-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="a008e-187">Wachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="a008e-187">Password change</span></span>
* <span data-ttu-id="a008e-188">**V: waar moeten Mijn gebruikers hun wachtwoord moeten wijzigen gaan?**</span><span class="sxs-lookup"><span data-stu-id="a008e-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="a008e-189">**A:** gebruikers kunnen hun wachtwoord wijzigen waar ze hun profielfoto of pictogram ziet (zoals in de rechterbovenhoek van hun [Office 365](https://portal.office.com) of [Toegangspaneel](https://myapps.microsoft.com) optreedt.</span><span class="sxs-lookup"><span data-stu-id="a008e-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="a008e-190">Gebruikers kunnen hun wachtwoorden op wijzigen de [Toegangspaneel profielpagina](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="a008e-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="a008e-191">Gebruikers kunnen ook worden gevraagd hun wachtwoord moeten wijzigen automatisch op de Azure AD in het scherm als hun wachtwoord is verlopen.</span><span class="sxs-lookup"><span data-stu-id="a008e-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="a008e-192">Ten slotte gebruikers mogelijk gaat u naar de [Azure AD-wachtwoord wijzigen Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) rechtstreeks als ze willen hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a008e-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="a008e-193">**V: kunnen mijn gebruikers worden gewaarschuwd in de Office-Portal wanneer hun on-premises wachtwoord is verlopen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="a008e-194">**A:** dit vandaag is mogelijk als u AD FS gebruikt door de volgende instructies te volgen: [wachtwoord beleid Claims verzenden met AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="a008e-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="a008e-195">Als u synchronisatie van wachtwoordhash, is dit niet mogelijk vandaag.</span><span class="sxs-lookup"><span data-stu-id="a008e-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="a008e-196">Dit is omdat we niet wachtwoordbeleid van on-premises synchroniseren zodat het is niet mogelijk om te posten verlopen-meldingen naar cloud ervaringen.</span><span class="sxs-lookup"><span data-stu-id="a008e-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="a008e-197">In beide gevallen is het ook mogelijk te [Waarschuw gebruikers waarvan de wachtwoorden bijna verlopen zijn met behulp van PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="a008e-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="a008e-198">Wachtwoord-rapporten</span><span class="sxs-lookup"><span data-stu-id="a008e-198">Password management reports</span></span>
* <span data-ttu-id="a008e-199">**V: hoe lang duurt het voor de gegevens worden weergegeven op de wachtwoord-rapporten?**</span><span class="sxs-lookup"><span data-stu-id="a008e-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="a008e-200">**A:** gegevens op de wachtwoord-rapporten moet worden weergegeven in 5-10 minuten.</span><span class="sxs-lookup"><span data-stu-id="a008e-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="a008e-201">Deze sommige gevallen is het een uur duren kan om te worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a008e-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="a008e-202">**V: hoe kan ik de wachtwoord-rapporten filteren?**</span><span class="sxs-lookup"><span data-stu-id="a008e-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="a008e-203">**A:** kunt u de wachtwoord-rapporten filteren door te klikken op het Vergrootglas kleine uiterst rechts van de kolomlabels boven aan het rapport.</span><span class="sxs-lookup"><span data-stu-id="a008e-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="a008e-204">Als u doen uitgebreidere filteren wilt, kunt u het rapport naar excel en maak een draaitabel kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="a008e-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="a008e-205">**V: Wat is het maximum aantal gebeurtenissen in de wachtwoord-rapporten worden opgeslagen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="a008e-206">**A:** maximaal 75.000 wachtwoord opnieuw instellen of het wachtwoord opnieuw instellen van inschrijving gebeurtenissen worden opgeslagen in de wachtwoord-rapporten, back-spanning maximaal 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="a008e-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="a008e-207">We werken als u dit aantal zodanig dat meer gebeurtenissen wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="a008e-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="a008e-208">**V: hoe ver terug de wachtwoordbeheer rapporten gaan doen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="a008e-209">**A:** de wachtwoordbeheer rapporten weergeven-bewerkingen plaatsvinden in de afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="a008e-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="a008e-210">Op dit moment als u nodig hebt om deze gegevens te archiveren kunt u periodiek de rapporten downloaden en opslaan op een andere locatie.</span><span class="sxs-lookup"><span data-stu-id="a008e-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="a008e-211">**V: is er een maximale aantal rijen dat kan worden weergegeven op de wachtwoord-rapporten?**</span><span class="sxs-lookup"><span data-stu-id="a008e-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="a008e-212">**A:** Ja, maximaal 75.000 rijen kan worden weergegeven op een van de wachtwoord-rapporten, of ze worden weergegeven in de gebruikersinterface of wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="a008e-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="a008e-213">**V: is er een API voor toegang tot het wachtwoord opnieuw instellen of de registratie rapportagegegevens?**</span><span class="sxs-lookup"><span data-stu-id="a008e-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="a008e-214">**A:** Ja, Zie de volgende documentatie voor meer informatie over hoe u toegang hebt tot de rapportage van de gegevensstroom voor wachtwoordherstel.</span><span class="sxs-lookup"><span data-stu-id="a008e-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="a008e-215">[Informatie over wachtwoordherstel rapportages programmatisch toegang tot](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="a008e-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="a008e-216">Wachtwoord terugschrijven</span><span class="sxs-lookup"><span data-stu-id="a008e-216">Password writeback</span></span>
* <span data-ttu-id="a008e-217">**V: hoe werkt wachtwoord terugschrijven achter de schermen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="a008e-218">**A:** Zie [de werking van wachtwoord terugschrijven](active-directory-passwords-writeback.md) voor een uitleg van wat er gebeurt als u terugschrijven van wachtwoord en hoe gegevens via het systeem loopt terug naar uw on-premises-omgeving inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a008e-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="a008e-219">**V: hoe lang duurt wachtwoord terugschrijven voordat werken?  Is er een vertraging synchronisatie zoals met wachtwoordhashsynchronisatie?**</span><span class="sxs-lookup"><span data-stu-id="a008e-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="a008e-220">**A:** wachtwoord terugschrijven is snel.</span><span class="sxs-lookup"><span data-stu-id="a008e-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="a008e-221">Het is een synchrone pijplijn die fundamenteel anders dan de synchronisatie van wachtwoordhash werkt.</span><span class="sxs-lookup"><span data-stu-id="a008e-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="a008e-222">Wachtwoord terugschrijven kan gebruikers realtime feedback over het succes van hun wachtwoord opnieuw instellen of wijzigen van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="a008e-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="a008e-223">De gemiddelde tijd voor een geslaagde write-back van een wachtwoord is onder 500 ms.</span><span class="sxs-lookup"><span data-stu-id="a008e-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="a008e-224">**V: hoe wordt mijn account/toegang tot de cloud getroffen als mijn lokale account is uitgeschakeld?**</span><span class="sxs-lookup"><span data-stu-id="a008e-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="a008e-225">**A:** als uw lokale ID is uitgeschakeld, uw cloud-ID/access worden ook uitgeschakeld op de volgende synchronisatie-interval via AAD Connect byt standaard is dit elke 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="a008e-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="a008e-226">**V: als mijn lokale account wordt beperkt door een beleid on-premises Active Directory-wachtwoord, houdt SSPR zich aan dit beleid wanneer ik het wachtwoord wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="a008e-227">**A:** Ja, SSPR is afhankelijk van en houdt zich aan de on-premises AD-wachtwoordbeleid, met inbegrip van typische wachtwoordbeleid van de AD-domein, evenals alle fijnmazige wachtwoordbeleid dat is bestemd voor een bepaalde gebruiker gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a008e-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="a008e-228">**V: wat typen accounts werkt wachtwoord terugschrijven voor?**</span><span class="sxs-lookup"><span data-stu-id="a008e-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="a008e-229">**A:** wachtwoord terugschrijven is geschikt voor gebruikers van federatieve en het wachtwoord-Hash gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a008e-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="a008e-230">**V: bevat wachtwoord terugschrijven mijn domein wachtwoordbeleid afdwingen?**</span><span class="sxs-lookup"><span data-stu-id="a008e-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="a008e-231">**A:** Ja, wachtwoord terugschrijven worden afgedwongen wachtwoord leeftijd, geschiedenis, complexiteit, filters en eventuele andere beperkingen die u in plaats van wachtwoorden in uw lokale domein kan plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a008e-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="a008e-232">**V: wachtwoord terugschrijven veilig is?  Hoe kan ik dat ik won't ingebroken zijn?**</span><span class="sxs-lookup"><span data-stu-id="a008e-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="a008e-233">**A:** Ja, Write-back van wachtwoord is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="a008e-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="a008e-234">Bekijk meer informatie over de vier beveiligingslagen geïmplementeerd door de service van de Write-back van wachtwoord, de [wachtwoord terugschrijven beveiligingsmodel](active-directory-passwords-writeback.md#password-writeback-security-model) sectie in de werking van wachtwoord terugschrijven.</span><span class="sxs-lookup"><span data-stu-id="a008e-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="a008e-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a008e-235">Next steps</span></span>

<span data-ttu-id="a008e-236">De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="a008e-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="a008e-237">[**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="a008e-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="a008e-238">[**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren</span><span class="sxs-lookup"><span data-stu-id="a008e-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="a008e-239">[**Gegevens**](active-directory-passwords-data.md): informatie over de gegevens die nodig zijn en hoe deze worden gebruikt voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="a008e-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="a008e-240">[**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie</span><span class="sxs-lookup"><span data-stu-id="a008e-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="a008e-241">[**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="a008e-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="a008e-242">[**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken</span><span class="sxs-lookup"><span data-stu-id="a008e-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="a008e-243">[**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen</span><span class="sxs-lookup"><span data-stu-id="a008e-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="a008e-244">[**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory</span><span class="sxs-lookup"><span data-stu-id="a008e-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="a008e-245">[**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="a008e-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="a008e-246">[**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel</span><span class="sxs-lookup"><span data-stu-id="a008e-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
