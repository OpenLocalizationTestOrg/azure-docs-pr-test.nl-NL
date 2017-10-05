---
title: SaaS-apps voor B2B-samenwerking configureren in Azure Active Directory | Microsoft Docs
description: Voorbeelden van code en PowerShell voor Azure Active Directory B2B-samenwerking
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="eba9a-103">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="eba9a-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="eba9a-104">Azure Active Directory (Azure AD) B2B-samenwerking werkt met de meeste apps die zijn geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eba9a-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="eba9a-105">In deze sectie doorlopen we instructies voor het configureren van een aantal populaire SaaS-apps voor gebruik met Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="eba9a-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="eba9a-106">Voordat u de instructies van de app-specifiek bekijkt, hier een aantal regels van miniatuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="eba9a-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="eba9a-107">Voor de meeste van de apps moet gebruikersinstellingen handmatig gebeuren.</span><span class="sxs-lookup"><span data-stu-id="eba9a-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="eba9a-108">Dat wil zeggen, moeten gebruikers handmatig in de app ook worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eba9a-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="eba9a-109">Voor apps die ondersteuning bieden voor automatische installatie, zoals Dropbox, worden afzonderlijke uitnodigingen gemaakt vanuit apps.</span><span class="sxs-lookup"><span data-stu-id="eba9a-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="eba9a-110">Gebruikers moeten ervoor dat elke uitnodiging te accepteren.</span><span class="sxs-lookup"><span data-stu-id="eba9a-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="eba9a-111">In de kenmerken van de gebruiker om te beperken eventuele problemen met vervormde gebruikersprofielschijf (UDP) in gastgebruikers, altijd ingesteld **gebruikers-id** naar **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="eba9a-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="eba9a-112">Dropbox Business</span></span>

<span data-ttu-id="eba9a-113">Om gebruikers aan te melden met hun organisatie, moet u handmatig Business Dropbox voor het gebruik van Azure AD als een id-provider Security Assertion Markup Language (SAML) configureren.</span><span class="sxs-lookup"><span data-stu-id="eba9a-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="eba9a-114">Als Dropbox bedrijven is niet geconfigureerd om dit te doen, kan deze vragen of anders kunnen gebruikers zich aanmelden bij het gebruik van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eba9a-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="eba9a-115">Selecteer om de Dropbox-Business-app met Azure AD toe **bedrijfstoepassingen** in het linkerdeelvenster en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![De knop "Toevoegen" op de pagina van de Enterprise-toepassingen](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="eba9a-117">In de **een toepassing toevoegen** venster invoeren **dropbox** in het zoekvak en selecteer vervolgens **Dropbox voor bedrijven** in de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="eba9a-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Zoeken naar 'dropbox' op het toevoegen van een toepassingspagina](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="eba9a-119">Op de **eenmalige aanmelding** pagina **eenmalige aanmelding** in het linkerdeelvenster en voer vervolgens **user.mail** in de **gebruikers-id** vak.</span><span class="sxs-lookup"><span data-stu-id="eba9a-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="eba9a-120">(Het ingesteld als de UPN standaard.)</span><span class="sxs-lookup"><span data-stu-id="eba9a-120">(It's set as UPN by default.)</span></span>

  ![Eenmalige aanmelding voor de app configureren](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="eba9a-122">Selecteer voor het downloaden van het certificaat moet worden gebruikt voor de configuratie van Dropbox, **DropBox configureren**, en selecteer vervolgens **SAML aanmelding op Service-URL met eenmalige** in de lijst.</span><span class="sxs-lookup"><span data-stu-id="eba9a-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Downloaden van het certificaat voor Dropbox-configuratie](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="eba9a-124">Aanmelden bij Dropbox met de aanmeldings-URL van de **eenmalige aanmelding** pagina.</span><span class="sxs-lookup"><span data-stu-id="eba9a-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![De aanmeldingspagina Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="eba9a-126">Selecteer in het menu **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-126">On the menu, select **Admin Console**.</span></span>

  ![De koppeling 'Admin Console' in het menu Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="eba9a-128">In de **verificatie** dialoogvenster, **meer**, upload het certificaat en klik vervolgens op de **aanmelden URL** Voer het SAML één aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="eba9a-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![De koppeling 'Meer' in het dialoogvenster voor samengevouwen verificatie](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![De 'aanmelden URL' in het dialoogvenster voor uitgebreide verificatie](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="eba9a-131">Voor het configureren van automatische gebruikersinstellingen in de Azure portal, selecteer **inrichten** selecteren in het linkerdeelvenster **automatische** in de **modus inrichting** vak en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Automatisch gebruikers inrichten in de Azure portal configureren](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="eba9a-133">Nadat de gast of lid gebruikers zijn ingesteld in de app Dropbox, ontvangen ze een uitnodiging voor een afzonderlijke van Dropbox.</span><span class="sxs-lookup"><span data-stu-id="eba9a-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="eba9a-134">Voor het gebruik van eenmalige aanmelding Dropbox, moeten de genodigden de uitnodiging accepteren door te klikken op een koppeling in het.</span><span class="sxs-lookup"><span data-stu-id="eba9a-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="eba9a-135">Box</span><span class="sxs-lookup"><span data-stu-id="eba9a-135">Box</span></span>
<span data-ttu-id="eba9a-136">U kunt gebruikers vak Gast om gebruikers te verifiëren met hun Azure AD-account met behulp van de federatieserver die gebaseerd op het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="eba9a-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="eba9a-137">In deze procedure kunt u metagegevens uploaden naar Box.com.</span><span class="sxs-lookup"><span data-stu-id="eba9a-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="eba9a-138">De Box-app uit de zakelijke apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="eba9a-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="eba9a-139">Eenmalige aanmelding configureren in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="eba9a-139">Configure single sign-on in the following order:</span></span>

  ![Eenmalige aanmelding vak configureren](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="eba9a-141">a.</span><span class="sxs-lookup"><span data-stu-id="eba9a-141">a.</span></span> <span data-ttu-id="eba9a-142">In de **aanmelden URL** Zorg dat de aanmeldings-URL juist is ingesteld voor het selectievakje in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eba9a-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="eba9a-143">Deze URL is de URL van uw tenant Box.com.</span><span class="sxs-lookup"><span data-stu-id="eba9a-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="eba9a-144">Deze naam moet voldoen aan de naamgevingsconventie *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="eba9a-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="eba9a-145">De **id** geldt niet voor deze app maar nog steeds wordt weergegeven als een verplicht veld.</span><span class="sxs-lookup"><span data-stu-id="eba9a-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="eba9a-146">b.</span><span class="sxs-lookup"><span data-stu-id="eba9a-146">b.</span></span> <span data-ttu-id="eba9a-147">In de **gebruikers-id** Voer **user.mail** (voor eenmalige aanmelding voor gastaccounts).</span><span class="sxs-lookup"><span data-stu-id="eba9a-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="eba9a-148">c.</span><span class="sxs-lookup"><span data-stu-id="eba9a-148">c.</span></span> <span data-ttu-id="eba9a-149">Onder **SAML-certificaat voor ondertekening van**, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="eba9a-150">d.</span><span class="sxs-lookup"><span data-stu-id="eba9a-150">d.</span></span> <span data-ttu-id="eba9a-151">Om te beginnen met het configureren van uw tenant Box.com voor het gebruik van Azure AD als id-provider, downloadt u het metagegevensbestand en vervolgens opslaan in de lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="eba9a-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="eba9a-152">e.</span><span class="sxs-lookup"><span data-stu-id="eba9a-152">e.</span></span> <span data-ttu-id="eba9a-153">Het metagegevensbestand aan het vak ondersteuning doorsturen team eenmalige aanmelding voor u te configureren.</span><span class="sxs-lookup"><span data-stu-id="eba9a-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="eba9a-154">Selecteer voor Azure AD automatische gebruikersinstellingen, in het linkerdeelvenster **inrichten**, en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="eba9a-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Azure AD verbinding maken met het selectievakje toestaan](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="eba9a-156">Zoals Dropbox genodigden, moeten het selectievakje genodigden hun uitnodiging van de app vak inwisselen.</span><span class="sxs-lookup"><span data-stu-id="eba9a-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eba9a-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eba9a-157">Next steps</span></span>

<span data-ttu-id="eba9a-158">Zie de volgende artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="eba9a-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="eba9a-159">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="eba9a-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="eba9a-160">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="eba9a-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="eba9a-161">Een B2B-samenwerking-gebruiker toe te voegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="eba9a-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="eba9a-162">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="eba9a-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="eba9a-163">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="eba9a-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="eba9a-164">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="eba9a-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="eba9a-165">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="eba9a-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="eba9a-166">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="eba9a-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="eba9a-167">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="eba9a-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="eba9a-168">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="eba9a-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
