---
title: aaaConfigure SaaS-apps voor B2B-samenwerking in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="aa1f4-103">SaaS-apps voor B2B-samenwerking configureren</span><span class="sxs-lookup"><span data-stu-id="aa1f4-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="aa1f4-104">Azure Active Directory (Azure AD) B2B-samenwerking werkt met de meeste apps die zijn geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="aa1f4-105">In deze sectie doorlopen we instructies voor het configureren van een aantal populaire SaaS-apps voor gebruik met Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="aa1f4-106">Voordat u de instructies van de app-specifiek bekijkt, hier een aantal regels van miniatuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa1f4-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="aa1f4-107">Voor de meeste Hallo apps moet gebruikersinstellingen toohappen handmatig.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="aa1f4-108">Dat wil zeggen, moeten gebruikers handmatig in Hallo app ook worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="aa1f4-109">Voor apps die ondersteuning bieden voor automatische installatie, zoals Dropbox, worden afzonderlijke inschrijvingen van Hallo-apps gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="aa1f4-110">Gebruikers ervoor tooaccept elke uitnodiging moet zijn.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="aa1f4-111">In gebruikerskenmerken hello, eventuele problemen met vervormde gebruikersprofielschijf (UDP) in gastgebruikers, toomitigate altijd ingesteld **gebruikers-id** te**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="aa1f4-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="aa1f4-112">Dropbox Business</span></span>

<span data-ttu-id="aa1f4-113">tooenable gebruikers toosign met hun organisatieaccount, moet u handmatig configureren Dropbox Business toouse Azure AD als een id-provider Security Assertion Markup Language (SAML).</span><span class="sxs-lookup"><span data-stu-id="aa1f4-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="aa1f4-114">Als Dropbox Business geconfigureerde toodo niet is dus kan het vragen of anders toestaan dat gebruikers toosign in met behulp van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="aa1f4-115">tooadd hello Dropbox-Business-app in Azure AD, selecteer **bedrijfstoepassingen** in het linkerdeelvenster Hallo en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![Hallo "Toevoegen" knop op de pagina met toepassingen Hallo Enterprise](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="aa1f4-117">In Hallo **een toepassing toevoegen** venster invoeren **dropbox** in het zoekvak Hallo en selecteer vervolgens **Dropbox voor bedrijven** in de lijst met resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Zoek naar 'dropbox' op Hallo-toepassingspagina voor een toevoegen](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="aa1f4-119">Op Hallo **eenmalige aanmelding** pagina **eenmalige aanmelding** in het linkerdeelvenster Hallo en voer vervolgens **user.mail** in Hallo **gebruikers-id** vak.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="aa1f4-120">(Het ingesteld als de UPN standaard.)</span><span class="sxs-lookup"><span data-stu-id="aa1f4-120">(It's set as UPN by default.)</span></span>

  ![Eenmalige aanmelding voor Hallo app configureren](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="aa1f4-122">toodownload hello certificaat toouse voor configuratie van Dropbox, selecteer **DropBox configureren**, en selecteer vervolgens **SAML aanmelding op Service-URL met eenmalige** in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Hallo-certificaat voor de configuratie van Dropbox downloaden](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="aa1f4-124">Aanmelden tooDropbox Hello aanmelding URL uit Hallo **eenmalige aanmelding** pagina.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![Hallo aanmeldingspagina Dropbox-pagina](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="aa1f4-126">Selecteer Hallo menu **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-126">On hello menu, select **Admin Console**.</span></span>

  ![Hallo 'Admin Console' koppeling op Hallo Dropbox menu](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="aa1f4-128">In Hallo **verificatie** dialoogvenster, **meer**, Hallo-certificaat uploaden en klik vervolgens op Hallo **aanmelden URL** Voer Hallo eenmalige aanmelding SAML-URL.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Hallo ' ' link in het dialoogvenster verificatie Hallo samengevouwen](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hallo 'Aanmelding in URL' in hello uitgevouwen dialoogvenster verificatie](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="aa1f4-131">Automatische gebruikersinstellingen tooconfigure in hello Azure-portal, selecteer **inrichten** selecteren in het linkerdeelvenster Hallo **automatische** in Hallo **modus inrichting** vak en selecteer vervolgens **Autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Automatisch gebruikers inrichten in hello Azure-portal configureren](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="aa1f4-133">Nadat de gast of lid gebruikers zijn ingesteld in Hallo Dropbox-app, ontvangen ze een uitnodiging voor een afzonderlijke van Dropbox.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="aa1f4-134">toouse eenmalige aanmelding Dropbox genodigden moeten Hallo uitnodiging accepteren door te klikken op een koppeling in het.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="aa1f4-135">Box</span><span class="sxs-lookup"><span data-stu-id="aa1f4-135">Box</span></span>
<span data-ttu-id="aa1f4-136">U kunt gebruikers tooauthenticate vak gastgebruikers met hun Azure AD-account inschakelen met behulp van de federatieserver die gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="aa1f4-137">In deze procedure moet u metagegevens tooBox.com uploaden.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="aa1f4-138">Hallo-Box-app uit Hallo zakelijke apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="aa1f4-139">Eenmalige aanmelding in volgorde Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="aa1f4-139">Configure single sign-on in hello following order:</span></span>

  ![Eenmalige aanmelding vak configureren](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="aa1f4-141">a.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-141">a.</span></span> <span data-ttu-id="aa1f4-142">In Hallo **aanmelden URL** Zorg dat Hallo aanmeldings-URL juist is ingesteld voor Box in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="aa1f4-143">Deze URL is Hallo-URL van uw tenant Box.com.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="aa1f4-144">Deze moet voldoen aan de naamgevingsconventie Hallo *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="aa1f4-145">Hallo **id** toothis is niet van toepassing app, maar nog steeds wordt weergegeven als een verplicht veld.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="aa1f4-146">b.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-146">b.</span></span> <span data-ttu-id="aa1f4-147">In Hallo **gebruikers-id** Voer **user.mail** (voor eenmalige aanmelding voor gastaccounts).</span><span class="sxs-lookup"><span data-stu-id="aa1f4-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="aa1f4-148">c.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-148">c.</span></span> <span data-ttu-id="aa1f4-149">Onder **SAML-certificaat voor ondertekening van**, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="aa1f4-150">d.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-150">d.</span></span> <span data-ttu-id="aa1f4-151">uw Box.com tenant toouse Azure AD configureren als een id-provider toobegin Hallo metagegevensbestand downloaden en sla vervolgens tooyour lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="aa1f4-152">e.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-152">e.</span></span> <span data-ttu-id="aa1f4-153">Doorsturen Hallo metagegevens bestand toohello vak ondersteuningsteam, eenmalige aanmelding voor u te configureren.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="aa1f4-154">Selecteer voor Azure AD automatische gebruikersinstellingen, in het linkerdeelvenster Hallo **inrichten**, en selecteer vervolgens **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Azure AD tooconnect tooBox autoriseren](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="aa1f4-156">Zoals Dropbox-genodigden moeten vak genodigden gebruikmaken van hun uitnodiging van Hallo Box-app.</span><span class="sxs-lookup"><span data-stu-id="aa1f4-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa1f4-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa1f4-157">Next steps</span></span>

<span data-ttu-id="aa1f4-158">Zie Hallo artikelen over Azure AD B2B-samenwerking te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa1f4-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="aa1f4-159">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="aa1f4-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="aa1f4-160">Gebruikerseigenschappen B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="aa1f4-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="aa1f4-161">B2B-samenwerking tooa gebruikersrol toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa1f4-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="aa1f4-162">B2B-samenwerking uitnodigingen delegeren</span><span class="sxs-lookup"><span data-stu-id="aa1f4-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="aa1f4-163">Dynamische groepen en B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="aa1f4-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="aa1f4-164">B2B-samenwerking code en PowerShell-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="aa1f4-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="aa1f4-165">B2B-samenwerking gebruikerstokens</span><span class="sxs-lookup"><span data-stu-id="aa1f4-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="aa1f4-166">Gebruikersclaims voor B2B-samenwerking toewijzing</span><span class="sxs-lookup"><span data-stu-id="aa1f4-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="aa1f4-167">Office 365 extern delen</span><span class="sxs-lookup"><span data-stu-id="aa1f4-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="aa1f4-168">Huidige beperkingen voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="aa1f4-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
