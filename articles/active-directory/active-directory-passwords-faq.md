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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="025dc-104">Veelgestelde vragen over wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="025dc-104">Password management frequently asked questions</span></span>

<span data-ttu-id="025dc-105">Hallo na worden enkele veelgestelde vragen voor alle bewerkingen die betrekking hebben toopassword opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="025dc-106">Als er een algemene vraag over Azure AD en zelf uw wachtwoord opnieuw instellen, die niet wordt beantwoord hier, kunt u vragen Hallo community om hulp op Hallo [Azure Ad-forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="025dc-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="025dc-107">Leden van de community Hallo opnemen Engineers, Product Managers, MVP's en fellow IT-Professionals.</span><span class="sxs-lookup"><span data-stu-id="025dc-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="025dc-108">Deze Veelgestelde vragen opgesplitst Hallo uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="025dc-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="025dc-109">**Vragen over het registreren voor wachtwoord opnieuw instellen**</span><span class="sxs-lookup"><span data-stu-id="025dc-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="025dc-110">**Vragen over wachtwoordherstel**</span><span class="sxs-lookup"><span data-stu-id="025dc-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="025dc-111">**Vragen over het wijzigen van wachtwoorden**</span><span class="sxs-lookup"><span data-stu-id="025dc-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="025dc-112">**Rapporten voor vragen over wachtwoordbeheer**</span><span class="sxs-lookup"><span data-stu-id="025dc-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="025dc-113">**Vragen over Write-back van wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="025dc-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="025dc-114">Registratie voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="025dc-114">Password reset registration</span></span>
* <span data-ttu-id="025dc-115">**V: kunnen mijn gebruikers registreren hun eigen wachtwoord opnieuw instellen van gegevens?**</span><span class="sxs-lookup"><span data-stu-id="025dc-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="025dc-116">**A:** Ja, zoals wachtwoord opnieuw instellen is ingeschakeld en worden ze in licentie gegeven, kunnen ze toohello registratie voor wachtwoord opnieuw instellen-portal op http://aka.ms/ssprsetup tooregister hun verificatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="025dc-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="025dc-117">Gebruikers kunnen ook registreren door toohello-Toegangsvenster gaan bij http://myapps.microsoft.com, tabblad Hallo-profiel en Hallo registreren voor wachtwoordherstel optie klikken.</span><span class="sxs-lookup"><span data-stu-id="025dc-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="025dc-118">**V: kan ik wachtwoord opnieuw instellen van gegevens definiëren namens mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="025dc-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="025dc-119">**A:** Ja, u kunt dit doen met Azure AD Connect PowerShell Hallo [Azure-portal](https://portal.azure.com), of Hallo beheerder van Office-portal.</span><span class="sxs-lookup"><span data-stu-id="025dc-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="025dc-120">Zie voor meer informatie artikel Hallo [gegevens die worden gebruikt door Azure AD selfservice voor wachtwoordherstel](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="025dc-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="025dc-121">**V: kan ik gegevens voor vragen over de beveiliging van on-premises synchroniseren?**</span><span class="sxs-lookup"><span data-stu-id="025dc-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="025dc-122">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="025dc-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="025dc-123">**V: kunnen mijn gebruikers gegevens registreren zodanig dat deze gegevens door andere gebruikers niet zien?**</span><span class="sxs-lookup"><span data-stu-id="025dc-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="025dc-124">**A:** Ja, wanneer gebruikers zich registreren voor gegevens met behulp van Hallo opnieuw instellen-Portal voor Wachtwoordregistratie is opgeslagen in persoonlijke verificatie velden die alleen zichtbaar zijn door de gebruiker globale beheerders en Hallo.</span><span class="sxs-lookup"><span data-stu-id="025dc-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="025dc-125">Als een **Azure Administrator-account** registreert hun telefoonnummer verificatie deze ook worden ingevuld in het veld van de mobiele telefoon Hallo en zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="025dc-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="025dc-126">**V: Mijn gebruikers hebt toobe geregistreerd voordat ze kunnen voor wachtwoordherstel gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="025dc-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="025dc-127">**A:** Nee, als u onvoldoende verificatiegegevens namens hen definieert, gebruikers hebben geen tooregister.</span><span class="sxs-lookup"><span data-stu-id="025dc-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="025dc-128">Wachtwoord opnieuw moet worden ingesteld als u hebt opgeslagen gegevens in de juiste velden in de map Hallo Hallo juist opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="025dc-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="025dc-129">**V: kan ik synchroniseren of instellen van de telefoon voor authenticatie, authenticatie E-mail of andere telefoon voor authenticatie velden Hallo namens mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="025dc-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="025dc-130">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="025dc-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="025dc-131">**V: hoe Hallo-portal voor wachtwoordregistratie weet welke opties tooshow Mijn gebruikers?**</span><span class="sxs-lookup"><span data-stu-id="025dc-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="025dc-132">**A:** Hallo wachtwoordherstel registratieportal alleen toont Hallo opties die u hebt ingeschakeld voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="025dc-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="025dc-133">Deze opties zijn gevonden onder de sectie van de gebruiker opnieuw instellen wachtwoordbeleid van uw directory configureren tabblad Hallo. Dit betekent bijvoorbeeld dat als u vragen over de beveiliging niet inschakelt, klikt u vervolgens gebruikers zich niet kunnen tooregister voor die optie.</span><span class="sxs-lookup"><span data-stu-id="025dc-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="025dc-134">**V: wanneer een gebruiker als beschouwd ingeschreven?**</span><span class="sxs-lookup"><span data-stu-id="025dc-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="025dc-135">**A:** een gebruiker wordt beschouwd geregistreerd voor SSPR, wanneer zij hebben geregistreerd ten minste Hallo **aantal methoden vereist tooreset** die u hebt ingesteld in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="025dc-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="025dc-136">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="025dc-136">Password reset</span></span>
* <span data-ttu-id="025dc-137">**V: hoe lang moet ik tooreceive wachten een e-mail, SMS of telefoongesprek van wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="025dc-138">**A:** SMS-berichten, e-mailadres en telefoongesprekken moet binnenkomen in onder één minuut aan normale Hallo-aanvraag wordt 5-20 seconden.</span><span class="sxs-lookup"><span data-stu-id="025dc-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="025dc-139">Als u hiervan geen melding voor Hallo binnen deze tijd:</span><span class="sxs-lookup"><span data-stu-id="025dc-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="025dc-140">Controleer de map Ongewenste e-mail.</span><span class="sxs-lookup"><span data-stu-id="025dc-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="025dc-141">Hallo nummer of e-mailbericht waarmee contact wordt opgenomen is Hallo een die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="025dc-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="025dc-142">Controleer Hallo verificatiegegevens in de directory Hallo is juist opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="025dc-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="025dc-143">Voorbeeld: "+ 1 4255551234' of 'user@contoso.com'</span><span class="sxs-lookup"><span data-stu-id="025dc-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="025dc-144">**V: welke talen worden ondersteund door het wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="025dc-145">**A:** Hallo wachtwoordherstel gebruikersinterface SMS-berichten en stem aanroepen zijn gelokaliseerd in Hallo dezelfde talen die worden ondersteund in Office 365.</span><span class="sxs-lookup"><span data-stu-id="025dc-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="025dc-146">**V: welke onderdelen van Hallo wachtwoord opnieuw instellen van ervaring ophalen huisstijl wanneer ik ingesteld organisatie huisstijl in mijn directory het tabblad configureren?**</span><span class="sxs-lookup"><span data-stu-id="025dc-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="025dc-147">**A:** hello wachtwoordresetportal ziet u het logo van uw organisatie en kunt u tooconfigure Hallo Neem contact op met uw beheerder koppeling toopoint tooa aangepaste e-mailadres of URL.</span><span class="sxs-lookup"><span data-stu-id="025dc-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="025dc-148">Een e-mailbericht dat wordt verzonden door het wachtwoord opnieuw instellen van uw organisatie logo, de kleuren, de naam bevat in Hallo hoofdtekst van e-mail Hallo en aangepast met de naam van.</span><span class="sxs-lookup"><span data-stu-id="025dc-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="025dc-149">**V: hoe kan ik mijn moet u gebruikers informeren over waar toogo tooreset hun wachtwoorden?**</span><span class="sxs-lookup"><span data-stu-id="025dc-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="025dc-150">**A:** kunt u uw gebruikers toohttps://passwordreset.microsoftonline.com rechtstreeks verzenden, of u kunt opgeven dat ze tooclick hello **heeft geen toegang tot uw accountkoppeling** gevonden op eventuele werk of School-aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="025dc-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="025dc-151">U kunt deze koppelingen ook publiceren in een plaats eenvoudig toegankelijk tooyour gebruikers.</span><span class="sxs-lookup"><span data-stu-id="025dc-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="025dc-152">**V: kan ik deze pagina vanaf een mobiel apparaat gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="025dc-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="025dc-153">**A:** Ja, deze pagina werkt op mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="025dc-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="025dc-154">**V: ondersteund ontgrendelen lokale active directory-accounts wanneer gebruikers hun wachtwoord opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="025dc-155">**A:** Ja, als hun wachtwoord opnieuw instellen van een gebruiker en wachtwoord terugschrijven is geïmplementeerd met Azure AD Connect, die gebruikersaccount is automatisch ontgrendeld wanneer ze hun wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="025dc-156">**V: hoe kan ik wachtwoordherstel rechtstreeks in mijn gebruiker aanmelden Bureaubladervaring worden geïntegreerd?**</span><span class="sxs-lookup"><span data-stu-id="025dc-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="025dc-157">**A:** als u een Azure AD Premium-klant bent, kunt u Microsoft Identity Manager installeren zonder extra kosten en implementeren van Hallo lokale wachtwoord opnieuw instellen van oplossing toomeet deze vereiste.</span><span class="sxs-lookup"><span data-stu-id="025dc-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="025dc-158">**V: kan ik andere beveiligingsvragen voor verschillende talen instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="025dc-159">**A:** dit niet mogelijk is vandaag de dag.</span><span class="sxs-lookup"><span data-stu-id="025dc-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="025dc-160">**V: hoe zoveel mogelijk vragen kunt we voor Hallo beveiligingsvragen verificatieoptie configureren?**</span><span class="sxs-lookup"><span data-stu-id="025dc-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="025dc-161">**A:** kunt u aangepaste beveiligingsvragen too20 in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="025dc-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="025dc-162">**V: hoe lang mogelijk beveiligingsvragen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="025dc-163">**A:** beveiligingsvragen mogelijk tussen 3 en 200 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="025dc-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="025dc-164">**V: hoe lang mogelijk antwoorden toosecurity vragen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="025dc-165">**A:** antwoorden mogelijk 3 too40 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="025dc-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="025dc-166">**V: zijn afgewezen dubbele antwoorden toosecurity vragen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="025dc-167">**A:** Ja, er dubbele antwoorden toosecurity vragen afwijzen.</span><span class="sxs-lookup"><span data-stu-id="025dc-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="025dc-168">**V: kan Hallo het registreren van een gebruiker dezelfde beveiligingsvraag het meer dan één keer?**</span><span class="sxs-lookup"><span data-stu-id="025dc-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="025dc-169">**A:** Nee, wanneer een gebruiker zich registreert voor een bepaald criterium, ze kunnen niet worden geregistreerd voor deze vraag een tweede keer.</span><span class="sxs-lookup"><span data-stu-id="025dc-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="025dc-170">**V: is het mogelijk tooset de ondergrens van beveiligingsvragen voor registratie en opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="025dc-171">**A:** Ja, een limiet kan worden ingesteld voor registratie en een andere voor het opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="025dc-172">3-5-beveiligingsvragen mogelijk zijn vereist voor inschrijving en 3-5 mogelijk zijn vereist voor opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="025dc-173">**V: als een gebruiker meer dan het maximum aantal vragen vereist tooreset Hallo is geregistreerd, hoe beveiligingsvragen geselecteerd tijdens het opnieuw instellen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="025dc-174">**A:** N beveiliging vragen willekeurig geselecteerd uit Hallo kunt u het totaal aantal vragen een gebruiker is geregistreerd, waarbij N staat voor Hallo **aantal vragen vereist tooreset**.</span><span class="sxs-lookup"><span data-stu-id="025dc-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="025dc-175">Bijvoorbeeld, als een gebruiker 5 beveiligingsvragen geregistreerd heeft, maar alleen 3 vereiste tooreset zijn, zijn 3 Hallo 5 willekeurig geselecteerd en gepresenteerd op opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="025dc-176">Als het Hallo-gebruiker afkomstig Hallo-antwoorden toohello vragen verkeerde, optreedt Hallo selectieproces tooprevent vraag hammering.</span><span class="sxs-lookup"><span data-stu-id="025dc-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="025dc-177">**V: heb u voorkomen dat gebruikers vaak in een korte periode voor wachtwoordherstel probeert?**</span><span class="sxs-lookup"><span data-stu-id="025dc-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="025dc-178">**A:** Ja, er zijn ingebouwd in het wachtwoord opnieuw instellen van tooprotect tegen misbruik beveiligingsfuncties.</span><span class="sxs-lookup"><span data-stu-id="025dc-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="025dc-179">Gebruikers kunnen alleen proberen opnieuw instellen van 5 wachtwoordpogingen binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="025dc-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="025dc-180">Gebruikers kunnen toovalidate een telefoonnummer alleen proberen 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="025dc-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="025dc-181">Gebruikers kunnen alleen een één verificatiemethode proberen 5 maal binnen een uur voordat ze worden geblokkeerd voor 24 uur.</span><span class="sxs-lookup"><span data-stu-id="025dc-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="025dc-182">**V: voor hoe lang Hallo e-mail en SMS eenmalige wachtwoordcode geldig zijn?**</span><span class="sxs-lookup"><span data-stu-id="025dc-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="025dc-183">**A:** Hallo levensduur van de sessie voor wachtwoordherstel is 105 minuten.</span><span class="sxs-lookup"><span data-stu-id="025dc-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="025dc-184">Vanaf Hallo Hallo wachtwoordherstel bewerking, Hallo gebruiker 105 minuten tooreset hun wachtwoord heeft.</span><span class="sxs-lookup"><span data-stu-id="025dc-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="025dc-185">Hallo zijn e-mail en SMS eenmalige wachtwoordcode ongeldig nadat deze periode is verstreken.</span><span class="sxs-lookup"><span data-stu-id="025dc-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="025dc-186">Wachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="025dc-186">Password change</span></span>
* <span data-ttu-id="025dc-187">**V: waar moeten Mijn gebruikers gaan toochange hun wachtwoorden?**</span><span class="sxs-lookup"><span data-stu-id="025dc-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="025dc-188">**A:** gebruikers kunnen hun wachtwoord wijzigen waar ze hun profielfoto of pictogram ziet (zoals in Hallo rechterbovenhoek van hun [Office 365](https://portal.office.com) of [Toegangspaneel](https://myapps.microsoft.com) optreedt.</span><span class="sxs-lookup"><span data-stu-id="025dc-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="025dc-189">Gebruikers kunnen hun wachtwoord wijzigen vanaf Hallo [Toegangspaneel profielpagina](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="025dc-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="025dc-190">Gebruikers kunnen ook worden toochange gevraagd hun wachtwoord automatisch hello Azure AD in het scherm als hun wachtwoord is verlopen.</span><span class="sxs-lookup"><span data-stu-id="025dc-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="025dc-191">Ten slotte gebruikers toohello kunnen navigeren [Azure AD-wachtwoord wijzigen Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) rechtstreeks desgewenst toochange hun wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="025dc-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="025dc-192">**V: kunnen mijn gebruikers worden gewaarschuwd in Office-Portal Hallo wanneer hun on-premises wachtwoord is verlopen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="025dc-193">**A:** dit vandaag is mogelijk als u van AD FS gebruikmaakt door hier Hallo-instructies te volgen: [wachtwoord beleid Claims verzenden met AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="025dc-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="025dc-194">Als u synchronisatie van wachtwoordhash, is dit niet mogelijk vandaag.</span><span class="sxs-lookup"><span data-stu-id="025dc-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="025dc-195">Dit is omdat we synchroniseert geen wachtwoordbeleid van on-premises, zodat het is niet mogelijk voor ons toopost verlopen-meldingen toocloud optreedt.</span><span class="sxs-lookup"><span data-stu-id="025dc-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="025dc-196">In beide gevallen is het ook mogelijk te[Waarschuw gebruikers waarvan de wachtwoorden over tooexpire worden met behulp van PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="025dc-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="025dc-197">Wachtwoord-rapporten</span><span class="sxs-lookup"><span data-stu-id="025dc-197">Password management reports</span></span>
* <span data-ttu-id="025dc-198">**V: hoe lang duurt het voor gegevens tooshow up op Hallo wachtwoord-rapporten?**</span><span class="sxs-lookup"><span data-stu-id="025dc-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="025dc-199">**A:** gegevens op Hallo wachtwoord-rapporten moet worden weergegeven in 5-10 minuten.</span><span class="sxs-lookup"><span data-stu-id="025dc-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="025dc-200">Het aantal exemplaren het tooappear van tooan uur kan duren.</span><span class="sxs-lookup"><span data-stu-id="025dc-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="025dc-201">**V: hoe kan ik Hallo wachtwoord-rapporten filteren?**</span><span class="sxs-lookup"><span data-stu-id="025dc-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="025dc-202">**A:** kunt u Hallo wachtwoord-rapporten filteren op Hallo kleine Vergrootglas toohello uiterst rechts van de kolomlabels hello, aan de bovenkant Hallo van Hallo-rapport te klikken.</span><span class="sxs-lookup"><span data-stu-id="025dc-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="025dc-203">Als u toodo uitgebreidere filteren wilt, kunt u downloaden Hallo rapport tooexcel en een draaitabel maken.</span><span class="sxs-lookup"><span data-stu-id="025dc-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="025dc-204">**V: wat Hallo kunt u het maximum aantal gebeurtenissen is in Hallo wachtwoord-rapporten worden opgeslagen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="025dc-205">**A:** Up too75, 000 wachtwoord opnieuw instellen of het wachtwoord opnieuw instellen van registratie gebeurtenissen worden opgeslagen in Hallo wachtwoord-rapporten, maakt u een back-up van too30 dagen-spanning.</span><span class="sxs-lookup"><span data-stu-id="025dc-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="025dc-206">We werken tooexpand dit nummer tooinclude meer gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="025dc-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="025dc-207">**V: hoe ver terug Hallo wachtwoord-rapporten gaan?**</span><span class="sxs-lookup"><span data-stu-id="025dc-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="025dc-208">**A:** Hallo wachtwoordbeheer rapporten weergeven bewerkingen plaatsvinden binnen Hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="025dc-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="025dc-209">Op dit moment als u deze gegevens tooarchive moet kunt u downloaden Hallo rapporten periodiek en deze opslaan op een andere locatie.</span><span class="sxs-lookup"><span data-stu-id="025dc-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="025dc-210">**V: is er een maximale aantal rijen dat kan worden weergegeven op Hallo wachtwoord-rapporten?**</span><span class="sxs-lookup"><span data-stu-id="025dc-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="025dc-211">**A:** Ja, maximaal 75.000 rijen kan worden weergegeven op een van de Hallo wachtwoord-rapporten of worden ze weergegeven Hallo UI of wordt gedownload.</span><span class="sxs-lookup"><span data-stu-id="025dc-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="025dc-212">**V: is er een API-tooaccess Hallo wachtwoord opnieuw instellen of registratie rapportagegegevens?**</span><span class="sxs-lookup"><span data-stu-id="025dc-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="025dc-213">**A:** Ja, Zie Hallo na documentatie toolearn reporting gegevensstroom hoe u toegang hebt tot Hallo-wachtwoord instellen.</span><span class="sxs-lookup"><span data-stu-id="025dc-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="025dc-214">[Meer informatie over hoe tooaccess wachtwoordherstel rapportagegebeurtenissen programmatisch](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="025dc-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="025dc-215">Wachtwoord terugschrijven</span><span class="sxs-lookup"><span data-stu-id="025dc-215">Password writeback</span></span>
* <span data-ttu-id="025dc-216">**V: hoe werkt wachtwoord terugschrijven achter de schermen Hallo?**</span><span class="sxs-lookup"><span data-stu-id="025dc-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="025dc-217">**A:** Zie [de werking van wachtwoord terugschrijven](active-directory-passwords-writeback.md) voor een uitleg van wat er gebeurt als u terugschrijven van wachtwoord en hoe gegevens loopt via Hallo systeem terug naar uw on-premises-omgeving inschakelen.</span><span class="sxs-lookup"><span data-stu-id="025dc-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="025dc-218">**V: hoe lang duurt wachtwoord terugschrijven toowork  Is er een vertraging synchronisatie zoals met wachtwoordhashsynchronisatie?**</span><span class="sxs-lookup"><span data-stu-id="025dc-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="025dc-219">**A:** wachtwoord terugschrijven is snel.</span><span class="sxs-lookup"><span data-stu-id="025dc-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="025dc-220">Het is een synchrone pijplijn die fundamenteel anders dan de synchronisatie van wachtwoordhash werkt.</span><span class="sxs-lookup"><span data-stu-id="025dc-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="025dc-221">Wachtwoord terugschrijven kan gebruikers tooget realtime feedback over geslaagde Hallo van hun wachtwoord opnieuw instellen of wijzigen van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="025dc-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="025dc-222">Hallo gemiddelde tijd voor een geslaagde write-back van een wachtwoord is onder 500 ms.</span><span class="sxs-lookup"><span data-stu-id="025dc-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="025dc-223">**V: hoe wordt mijn account/toegang tot de cloud getroffen als mijn lokale account is uitgeschakeld?**</span><span class="sxs-lookup"><span data-stu-id="025dc-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="025dc-224">**A:** als uw lokale ID is uitgeschakeld, uw cloud-ID/access worden ook uitgeschakeld op de volgende synchronisatie-interval Hallo via AAD Connect byt standaard is dit elke 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="025dc-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="025dc-225">**V: als mijn lokale account wordt beperkt door een beleid on-premises Active Directory-wachtwoord, houdt SSPR zich aan dit beleid wanneer ik Hallo wachtwoord wijzigen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="025dc-226">**A:** Ja, SSPR is afhankelijk van en houdt zich aan Hallo lokale AD-wachtwoordbeleid, met inbegrip van AD-domein wachtwoord standaardbeleid, evenals alle gedefinieerde fijnmazige wachtwoordbeleid gericht tooa toegekend.</span><span class="sxs-lookup"><span data-stu-id="025dc-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="025dc-227">**V: wat typen accounts werkt wachtwoord terugschrijven voor?**</span><span class="sxs-lookup"><span data-stu-id="025dc-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="025dc-228">**A:** wachtwoord terugschrijven is geschikt voor gebruikers van federatieve en het wachtwoord-Hash gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="025dc-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="025dc-229">**V: bevat wachtwoord terugschrijven mijn domein wachtwoordbeleid afdwingen?**</span><span class="sxs-lookup"><span data-stu-id="025dc-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="025dc-230">**A:** Ja, wachtwoord terugschrijven worden afgedwongen wachtwoord leeftijd, geschiedenis, complexiteit, filters en eventuele andere beperkingen die u in plaats van wachtwoorden in uw lokale domein kan plaatsen.</span><span class="sxs-lookup"><span data-stu-id="025dc-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="025dc-231">**V: wachtwoord terugschrijven veilig is?  Hoe kan ik dat ik won't ingebroken zijn?**</span><span class="sxs-lookup"><span data-stu-id="025dc-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="025dc-232">**A:** Ja, Write-back van wachtwoord is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="025dc-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="025dc-233">tooread meer informatie over Hallo vier beveiligingslagen die door Hallo wachtwoord terugschrijven service is geïmplementeerd, bekijk Hallo [wachtwoord terugschrijven beveiligingsmodel](active-directory-passwords-writeback.md#password-writeback-security-model) sectie in de werking van wachtwoord terugschrijven.</span><span class="sxs-lookup"><span data-stu-id="025dc-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="025dc-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="025dc-234">Next steps</span></span>

<span data-ttu-id="025dc-235">Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="025dc-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="025dc-236">[**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="025dc-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="025dc-237">[**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren</span><span class="sxs-lookup"><span data-stu-id="025dc-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="025dc-238">[**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="025dc-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="025dc-239">[**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden</span><span class="sxs-lookup"><span data-stu-id="025dc-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="025dc-240">[**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.</span><span class="sxs-lookup"><span data-stu-id="025dc-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="025dc-241">[**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken</span><span class="sxs-lookup"><span data-stu-id="025dc-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="025dc-242">[**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen</span><span class="sxs-lookup"><span data-stu-id="025dc-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="025dc-243">[**Write-back van wachtwoord**](active-directory-passwords-writeback.md): hoe werkt write-back van wachtwoord met uw on-premises directory</span><span class="sxs-lookup"><span data-stu-id="025dc-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="025dc-244">[**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="025dc-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="025dc-245">[**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR</span><span class="sxs-lookup"><span data-stu-id="025dc-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
