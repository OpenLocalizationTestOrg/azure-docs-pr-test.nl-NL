---
title: 'Zelfstudie: Azure Active Directory-integratie met Kiteworks | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="17da0-103">Zelfstudie: Azure Active Directory-integratie met Kiteworks</span><span class="sxs-lookup"><span data-stu-id="17da0-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="17da0-104">In deze zelfstudie leert u hoe toointegrate Kiteworks met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17da0-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17da0-105">Kiteworks integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="17da0-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17da0-106">U kunt beheren in Azure AD die tooKiteworks toegang heeft</span><span class="sxs-lookup"><span data-stu-id="17da0-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="17da0-107">U kunt uw gebruikers tooautomatically get aangemelde tooKiteworks (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="17da0-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17da0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="17da0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17da0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17da0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17da0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="17da0-110">Prerequisites</span></span>

<span data-ttu-id="17da0-111">Azure AD-integratie met Kiteworks tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="17da0-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="17da0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="17da0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17da0-113">Een Kiteworks eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="17da0-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17da0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="17da0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17da0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="17da0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17da0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="17da0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17da0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17da0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17da0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="17da0-118">Scenario description</span></span>
<span data-ttu-id="17da0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="17da0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17da0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="17da0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17da0-121">Het toevoegen van Kiteworks van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="17da0-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="17da0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17da0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="17da0-123">Het toevoegen van Kiteworks van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="17da0-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="17da0-124">tooconfigure hello integratie van Kiteworks in Azure AD, moet u tooadd Kiteworks uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="17da0-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17da0-125">**tooadd Kiteworks via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17da0-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17da0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="17da0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17da0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17da0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17da0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17da0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="17da0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17da0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="17da0-133">Typ in het zoekvak Hallo **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="17da0-133">In hello search box, type **Kiteworks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="17da0-135">Selecteer in het deelvenster resultaten hello, **Kiteworks**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="17da0-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17da0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17da0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17da0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Kiteworks op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="17da0-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17da0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kiteworks is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17da0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="17da0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kiteworks toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="17da0-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="17da0-141">Wijs in Kiteworks, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="17da0-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17da0-142">tooconfigure en eenmalige aanmelding Azure AD-test met Kiteworks, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17da0-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17da0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="17da0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17da0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17da0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17da0-145">**[Maken van een testgebruiker Kiteworks](#creating-a-kiteworks-test-user)**  -toohave een equivalent van Britta Simon in Kiteworks die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="17da0-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17da0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="17da0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17da0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="17da0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17da0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="17da0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17da0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kiteworks configureren.</span><span class="sxs-lookup"><span data-stu-id="17da0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="17da0-150">**Azure AD tooconfigure eenmalige aanmelding met Kiteworks, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17da0-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="17da0-151">In de Azure-portal op Hallo Hallo **Kiteworks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="17da0-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="17da0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="17da0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="17da0-155">Op Hallo **Kiteworks domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17da0-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="17da0-157">a.</span><span class="sxs-lookup"><span data-stu-id="17da0-157">a.</span></span> <span data-ttu-id="17da0-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="17da0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="17da0-159">b.</span><span class="sxs-lookup"><span data-stu-id="17da0-159">b.</span></span> <span data-ttu-id="17da0-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="17da0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17da0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="17da0-161">These values are not real.</span></span> <span data-ttu-id="17da0-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="17da0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17da0-163">Neem contact op met [Kiteworks Client ondersteuningsteam](http://accellion.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="17da0-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="17da0-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="17da0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="17da0-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="17da0-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17da0-168">Op Hallo **Kiteworks configuratie** sectie, klikt u op **configureren Kiteworks** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="17da0-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17da0-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="17da0-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="17da0-171">Meld u op tooyour Kiteworks bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="17da0-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="17da0-172">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="17da0-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="17da0-174">In Hallo **verificatie en autorisatie** sectie, klikt u op **SSO Setup**.</span><span class="sxs-lookup"><span data-stu-id="17da0-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="17da0-176">Op Hallo SSO-installatiepagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17da0-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="17da0-178">a.</span><span class="sxs-lookup"><span data-stu-id="17da0-178">a.</span></span> <span data-ttu-id="17da0-179">Selecteer **verifiëren via eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="17da0-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="17da0-180">b.</span><span class="sxs-lookup"><span data-stu-id="17da0-180">b.</span></span> <span data-ttu-id="17da0-181">Selecteer **AuthnRequest initiëren**.</span><span class="sxs-lookup"><span data-stu-id="17da0-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="17da0-182">c.</span><span class="sxs-lookup"><span data-stu-id="17da0-182">c.</span></span> <span data-ttu-id="17da0-183">In Hallo **IDP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17da0-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="17da0-184">d.</span><span class="sxs-lookup"><span data-stu-id="17da0-184">d.</span></span> <span data-ttu-id="17da0-185">In Hallo **Single Sign-On Service-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17da0-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="17da0-186">e.</span><span class="sxs-lookup"><span data-stu-id="17da0-186">e.</span></span> <span data-ttu-id="17da0-187">In Hallo **Service-URL met eenmalige afmelding** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17da0-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="17da0-188">f.</span><span class="sxs-lookup"><span data-stu-id="17da0-188">f.</span></span> <span data-ttu-id="17da0-189">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **RSA-certificaat voor openbare sleutel** textbox.</span><span class="sxs-lookup"><span data-stu-id="17da0-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="17da0-190">g.</span><span class="sxs-lookup"><span data-stu-id="17da0-190">g.</span></span> <span data-ttu-id="17da0-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="17da0-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="17da0-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="17da0-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17da0-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="17da0-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17da0-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17da0-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17da0-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="17da0-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="17da0-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="17da0-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="17da0-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17da0-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17da0-199">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="17da0-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17da0-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="17da0-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17da0-203">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="17da0-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17da0-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17da0-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17da0-207">a.</span><span class="sxs-lookup"><span data-stu-id="17da0-207">a.</span></span> <span data-ttu-id="17da0-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17da0-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17da0-209">b.</span><span class="sxs-lookup"><span data-stu-id="17da0-209">b.</span></span> <span data-ttu-id="17da0-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17da0-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17da0-211">c.</span><span class="sxs-lookup"><span data-stu-id="17da0-211">c.</span></span> <span data-ttu-id="17da0-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="17da0-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17da0-213">d.</span><span class="sxs-lookup"><span data-stu-id="17da0-213">d.</span></span> <span data-ttu-id="17da0-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="17da0-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="17da0-215">Een testgebruiker Kiteworks maken</span><span class="sxs-lookup"><span data-stu-id="17da0-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="17da0-216">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Kiteworks van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="17da0-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="17da0-217">Kiteworks ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="17da0-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="17da0-218">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="17da0-218">There is no action item for you in this section.</span></span> <span data-ttu-id="17da0-219">Een nieuwe gebruiker wordt tijdens een poging tooaccess Kitewors gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="17da0-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="17da0-220">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Kiteworks ondersteuningsteam](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="17da0-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17da0-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17da0-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17da0-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKiteworks toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="17da0-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="17da0-224">**tooassign Britta Simon tooKiteworks, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17da0-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="17da0-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17da0-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="17da0-227">Selecteer in de lijst met de toepassingen van Hallo **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="17da0-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="17da0-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="17da0-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="17da0-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="17da0-231">Click **Add** button.</span></span> <span data-ttu-id="17da0-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17da0-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="17da0-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="17da0-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17da0-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17da0-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17da0-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17da0-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17da0-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17da0-237">Testing single sign-on</span></span>

<span data-ttu-id="17da0-238">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="17da0-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="17da0-239">Als u op Hallo Kiteworks-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kiteworks toepassing.</span><span class="sxs-lookup"><span data-stu-id="17da0-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17da0-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="17da0-240">Additional resources</span></span>

* [<span data-ttu-id="17da0-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17da0-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17da0-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17da0-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

