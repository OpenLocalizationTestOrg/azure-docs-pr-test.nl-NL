---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="15721-103">Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="15721-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="15721-104">In deze zelfstudie leert u hoe toointegrate werkplek door Facebook met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15721-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15721-105">Werkplek door Facebook integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="15721-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="15721-106">U kunt beheren in Azure AD die toegang tooWorkplace door Facebook heeft.</span><span class="sxs-lookup"><span data-stu-id="15721-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="15721-107">U kunt uw gebruikers tooautomatically ophalen aangemeld tooWorkplace door Facebook (eenmalige aanmelding) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="15721-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="15721-108">U kunt uw accounts op één locatie beheren: hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15721-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="15721-109">Zie voor meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15721-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15721-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="15721-110">Prerequisites</span></span>

<span data-ttu-id="15721-111">Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="15721-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="15721-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="15721-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15721-113">Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="15721-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="15721-114">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="15721-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="15721-115">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="15721-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15721-116">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15721-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15721-117">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="15721-117">Scenario description</span></span>
<span data-ttu-id="15721-118">In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="15721-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="15721-119">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="15721-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15721-120">Werkplek door Facebook uit Hallo galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15721-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="15721-121">Configureren en testen eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15721-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="15721-122">Werkplek door Facebook van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="15721-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="15721-123">tooconfigure hello integratie van werkplek door Facebook in Azure AD, werkplek door Facebook uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="15721-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="15721-124">In Hallo [Azure-portal](https://portal.azure.com), linkerdeelvenster Hallo in, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15721-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="15721-126">Te bladeren**bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="15721-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="15721-128">tooadd hello nieuwe toepassing, selecteert **nieuwe toepassing** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="15721-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="15721-130">Typ in het zoekvak Hallo **werkplek door Facebook**, en selecteer **werkplek door Facebook** van resultaten.</span><span class="sxs-lookup"><span data-stu-id="15721-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="15721-131">Selecteer vervolgens **toevoegen**, tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="15721-131">Then select **Add**, tooadd hello application.</span></span>

    ![Werkplek door Facebook in de lijst met resultaten Hallo](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="15721-133">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="15721-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="15721-134">In deze sectie kunt u configureren en testen van Azure AD-SSO met werkplek door Facebook, op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="15721-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="15721-135">Voor eenmalige aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werkplek door Facebook is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15721-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="15721-136">Met andere woorden, moet een gekoppelde relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in werkplek door Facebook worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="15721-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="15721-137">Deze relatie tot stand brengen door toe te wijzen Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="15721-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="15721-138">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="15721-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="15721-139">In deze sectie kunt u Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en u eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.</span><span class="sxs-lookup"><span data-stu-id="15721-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="15721-140">In de Azure-portal op Hallo Hallo **werkplek door Facebook** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="15721-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="15721-142">In Hallo **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="15721-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="15721-144">In Hallo **werkplek Facebook-domein en URL's** sectie, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="15721-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="15721-145">a.</span><span class="sxs-lookup"><span data-stu-id="15721-145">a.</span></span> <span data-ttu-id="15721-146">In Hallo **aanmeldings-URL** tekstvak, typt u een URL die gebruikmaakt van Hallo patroon volgen:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="15721-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="15721-147">b.</span><span class="sxs-lookup"><span data-stu-id="15721-147">b.</span></span> <span data-ttu-id="15721-148">In Hallo **id** tekstvak, typt u een URL die gebruikmaakt van Hallo patroon volgen:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="15721-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="15721-149">Deze waarden zijn alleen een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="15721-149">These values are an example only.</span></span> <span data-ttu-id="15721-150">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="15721-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="15721-151">Neem contact op met Hallo [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="15721-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="15721-152">In Hallo **SAML-certificaat voor ondertekening van** sectie **certificaat (Base64)**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="15721-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="15721-154">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15721-154">Select **Save**.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="15721-156">In Hallo **werkplek door Facebook configuratie** sectie **werkplek configureren door Facebook** tooopen hello **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="15721-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="15721-157">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="15721-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Werkplek door Facebook-configuratie](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="15721-159">Meld u tooyour werkplek door Facebook bedrijf site als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="15721-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="15721-160">Als onderdeel van SAML-verificatieproces Hallo kunt werkplek queryreeksen van up too2.5 kilobytes in grootte in volgorde toopass parameters tooAzure AD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="15721-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="15721-161">In Hallo **bedrijf Dashboard**, gaat u toohello **verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="15721-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="15721-162">Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="15721-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="15721-163">Voer Hallo waarden van Hallo gekopieerd **werkplek door Facebook configuratie** sectie van de Azure-portal in de bijbehorende velden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="15721-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="15721-164">In de **SAML URL** tekstvak plakken Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15721-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="15721-165">In de **URL-verlener SAML** tekstvak plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15721-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="15721-166">In **SAML afmelding omleiden (optioneel)**, plak Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15721-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="15721-167">Open uw **base-64 gecodeerde certificaat** in Kladblok gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15721-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="15721-168">Hallo-inhoud van het kopiëren naar het Klembord en plak deze toothe **SAML certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="15721-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="15721-169">Mogelijk moet u tooenter Hallo doelgroep-URL, geadresseerde URL en ACS (Assertion Consumer-Service)-URL, die worden vermeld onder Hallo **SAML-configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="15721-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="15721-170">Schuif toohello onder aan de sectie Hallo en schakel **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="15721-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="15721-171">Een pop-upvenster wordt weergegeven, met de aanmeldingspagina hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15721-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="15721-172">tooauthenticate, Voer uw referenties als normaal.</span><span class="sxs-lookup"><span data-stu-id="15721-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="15721-173">Zorg ervoor dat Hallo e-mailadres is geretourneerd door Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="15721-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="15721-174">Als het Hallo-test is voltooid, schuift u toohello onderaan Hallo pagina en selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="15721-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="15721-175">Iedereen met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="15721-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="15721-176">U kunt een SAML afmeldings-URL die gebruikt toopoint op Afmelden hello Azure AD-pagina worden kan tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="15721-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="15721-177">Als deze instelling is ingeschakeld en geconfigureerd, wordt de gebruiker Hallo is niet langer afmelden pagina gerichte toohello werkplek.</span><span class="sxs-lookup"><span data-stu-id="15721-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="15721-178">In plaats daarvan is Hallo gebruiker omgeleid toohello-URL die is toegevoegd in Hallo SAML afmelden omleidings-instelling.</span><span class="sxs-lookup"><span data-stu-id="15721-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="15721-179">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="15721-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="15721-180">Na het toevoegen van deze app van Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteert u de Hallo **Single Sign-On** tabblad en toegang Hallo Embedded-documentatie via Hallo **configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="15721-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="15721-181">Meer informatie over Hallo embedded-documentatie-functie in Hallo [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="15721-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="15721-182">De frequentie van herauthenticatie configureren</span><span class="sxs-lookup"><span data-stu-id="15721-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="15721-183">U kunt configureren werkplek tooprompt voor een SAML-controle elke dag drie dagen één week, twee weken, één maand of nooit.</span><span class="sxs-lookup"><span data-stu-id="15721-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="15721-184">Hallo minimale waarde voor Hallo SAML-controle voor mobiele toepassingen is ingesteld tooone week.</span><span class="sxs-lookup"><span data-stu-id="15721-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="15721-185">U kunt ook een SAML opnieuw instellen voor alle gebruikers afdwingen.</span><span class="sxs-lookup"><span data-stu-id="15721-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="15721-186">toodo deze, gebruik Hallo **vereisen SAML-verificatie voor alle gebruikers nu** knop.</span><span class="sxs-lookup"><span data-stu-id="15721-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="15721-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="15721-187">Create an Azure AD test user</span></span>
<span data-ttu-id="15721-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="15721-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

1. <span data-ttu-id="15721-190">In Hallo **Azure-portal**, linkerdeelvenster Hallo in, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15721-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="15721-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en selecteer **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="15721-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="15721-194">Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15721-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="15721-196">In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="15721-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15721-198">a.</span><span class="sxs-lookup"><span data-stu-id="15721-198">a.</span></span> <span data-ttu-id="15721-199">In Hallo **naam** in het tekstvak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15721-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15721-200">b.</span><span class="sxs-lookup"><span data-stu-id="15721-200">b.</span></span> <span data-ttu-id="15721-201">In Hallo **gebruikersnaam** tekstvak, type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="15721-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="15721-202">c.</span><span class="sxs-lookup"><span data-stu-id="15721-202">c.</span></span> <span data-ttu-id="15721-203">Selecteer **wachtwoord weergeven**, en schrijf deze op.</span><span class="sxs-lookup"><span data-stu-id="15721-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="15721-204">d.</span><span class="sxs-lookup"><span data-stu-id="15721-204">d.</span></span> <span data-ttu-id="15721-205">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="15721-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="15721-206">Maken van een werkplek door Facebook testgebruiker</span><span class="sxs-lookup"><span data-stu-id="15721-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="15721-207">In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook.</span><span class="sxs-lookup"><span data-stu-id="15721-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="15721-208">Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="15721-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="15721-209">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="15721-209">There is no action for you in this section.</span></span> <span data-ttu-id="15721-210">Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u tooaccess werkplek probeert met Facebook.</span><span class="sxs-lookup"><span data-stu-id="15721-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="15721-211">Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="15721-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="15721-212">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="15721-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="15721-213">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooWorkplace door Facebook.</span><span class="sxs-lookup"><span data-stu-id="15721-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Gebruiker toewijzen][200] 

1. <span data-ttu-id="15721-215">In hello Azure weergeven portal, open Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="15721-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="15721-216">Ga toohello directory weergeven, gaat u te**bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="15721-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="15721-218">Selecteer in de lijst met de toepassingen van Hallo **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="15721-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Hallo werkplek door Facebook-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="15721-220">Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="15721-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="15721-222">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15721-222">Select **Add**.</span></span> <span data-ttu-id="15721-223">Klik op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="15721-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="15721-225">In Hallo **gebruikers en groepen** dialoogvenster, **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="15721-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="15721-226">In Hallo **gebruikers en groepen** dialoogvenster, **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="15721-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="15721-227">In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="15721-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="15721-228">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="15721-228">Test single sign-on</span></span>

<span data-ttu-id="15721-229">Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="15721-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="15721-230">Zie voor meer informatie [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15721-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="15721-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15721-231">Next steps</span></span>

* <span data-ttu-id="15721-232">Zie Hallo [lijst met zelfstudies over het SaaS-Apps met Azure Active Directory toointegrate](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="15721-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="15721-233">Lees [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15721-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="15721-234">Meer informatie over het te[configureren gebruikersaanvragen](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="15721-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

