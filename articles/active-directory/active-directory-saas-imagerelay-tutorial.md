---
title: 'Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en afbeelding Relay.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="0e337-103">Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay</span><span class="sxs-lookup"><span data-stu-id="0e337-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="0e337-104">In deze zelfstudie leert u hoe toointegrate installatiekopie Relay met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e337-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e337-105">Afbeelding Relay integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0e337-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e337-106">U kunt beheren in Azure AD wie toegang tot tooImage Relay heeft</span><span class="sxs-lookup"><span data-stu-id="0e337-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="0e337-107">U kunt uw gebruikers tooautomatically get aangemelde tooImage Relay (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0e337-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e337-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0e337-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e337-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e337-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e337-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e337-110">Prerequisites</span></span>

<span data-ttu-id="0e337-111">Azure AD-integratie met installatiekopie Relay tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0e337-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="0e337-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0e337-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e337-113">Een installatiekopie Relay eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0e337-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e337-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e337-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e337-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0e337-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e337-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0e337-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e337-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e337-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e337-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0e337-118">Scenario description</span></span>
<span data-ttu-id="0e337-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e337-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e337-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0e337-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e337-121">Het toevoegen van afbeelding Relay van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0e337-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="0e337-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e337-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="0e337-123">Het toevoegen van afbeelding Relay van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0e337-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="0e337-124">tooconfigure hello integratie van afbeelding Relay in Azure AD, moet u tooadd installatiekopie Relay uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0e337-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e337-125">**tooadd installatiekopie Relay via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e337-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e337-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e337-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e337-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e337-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0e337-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0e337-133">Typ in het zoekvak Hallo **installatiekopie Relay**.</span><span class="sxs-lookup"><span data-stu-id="0e337-133">In hello search box, type **Image Relay**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="0e337-135">Selecteer in het deelvenster resultaten hello, **installatiekopie Relay**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e337-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e337-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e337-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e337-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met installatiekopie Relay op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0e337-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e337-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in afbeelding Relay is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e337-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="0e337-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in afbeelding Relay toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0e337-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="0e337-141">In afbeelding Relay, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0e337-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e337-142">tooconfigure en eenmalige aanmelding Azure AD-test met installatiekopie Relay, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e337-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e337-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0e337-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e337-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e337-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e337-145">**[Maken van een installatiekopie Relay testgebruiker](#creating-an-image-relay-test-user)**  -toohave een equivalent van Britta Simon in afbeelding Relay dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0e337-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e337-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0e337-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e337-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0e337-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e337-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0e337-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e337-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw installatiekopie Relay-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e337-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="0e337-150">**Voer tooconfigure Azure AD eenmalige aanmelding met installatiekopie Relay, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e337-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e337-151">In Azure-portal op Hallo Hallo **installatiekopie Relay** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0e337-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0e337-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0e337-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="0e337-155">Op Hallo **installatiekopie Relay domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e337-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="0e337-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e337-157">a.</span></span> <span data-ttu-id="0e337-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="0e337-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="0e337-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e337-159">b.</span></span> <span data-ttu-id="0e337-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="0e337-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e337-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="0e337-161">These values are not real.</span></span> <span data-ttu-id="0e337-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="0e337-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e337-163">Neem contact op met [installatiekopie Relay Client ondersteuningsteam](http://support.imagerelay.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="0e337-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="0e337-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0e337-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="0e337-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0e337-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e337-168">Op Hallo **Image Relay-configuratie** sectie, klikt u op **installatiekopie Relay configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0e337-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e337-169">Kopiëren Hallo **Sign-Out Service URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0e337-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="0e337-171">Meld u tooyour installatiekopie Relay bedrijf site als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="0e337-172">Klik in de werkbalk van de Hallo Hallo bovenaan, op Hallo **gebruikers en machtigingen** werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="0e337-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="0e337-174">Klik op **maken van nieuwe machtiging**.</span><span class="sxs-lookup"><span data-stu-id="0e337-174">Click **Create New Permission**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="0e337-176">In Hallo **eenmalige aanmelding op instellingen** werkbelasting, selecteer Hallo **deze groep kan alleen aanmelden via eenmalige aanmelding** selectievakje en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e337-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="0e337-178">Ga te**Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-178">Go too**Account Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="0e337-180">Ga toohello **eenmalige aanmelding op instellingen** werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="0e337-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="0e337-182">Op Hallo **SAML instellingen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="0e337-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="0e337-184">a.</span><span class="sxs-lookup"><span data-stu-id="0e337-184">a.</span></span> <span data-ttu-id="0e337-185">In **aanmeldings-URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0e337-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e337-186">b.</span><span class="sxs-lookup"><span data-stu-id="0e337-186">b.</span></span> <span data-ttu-id="0e337-187">In **afmelding URL** textbox plakken Hallo-waarde van **Service-URL met eenmalige Sign-Out** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0e337-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e337-188">c.</span><span class="sxs-lookup"><span data-stu-id="0e337-188">c.</span></span> <span data-ttu-id="0e337-189">Als **indeling naam-Id**, selecteer **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="0e337-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="0e337-190">d.</span><span class="sxs-lookup"><span data-stu-id="0e337-190">d.</span></span> <span data-ttu-id="0e337-191">Als **Binding opties voor het aanvragen van Hallo serviceprovider (installatiekopie-Relay)**, selecteer **POST Binding**.</span><span class="sxs-lookup"><span data-stu-id="0e337-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="0e337-192">e.</span><span class="sxs-lookup"><span data-stu-id="0e337-192">e.</span></span> <span data-ttu-id="0e337-193">Onder **x.509-certificaat**, klikt u op **certificaat bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="0e337-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="0e337-195">f.</span><span class="sxs-lookup"><span data-stu-id="0e337-195">f.</span></span> <span data-ttu-id="0e337-196">Hallo gedownload certificaat openen in Kladblok en plak deze in Hallo x.509-certificaat textbox Hallo inhoud kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0e337-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="0e337-198">g.</span><span class="sxs-lookup"><span data-stu-id="0e337-198">g.</span></span> <span data-ttu-id="0e337-199">In **compileerprogramma gebruikersaanvragen** sectie, selecteer Hallo **compileerprogramma gebruikersaanvragen inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="0e337-201">h.</span><span class="sxs-lookup"><span data-stu-id="0e337-201">h.</span></span> <span data-ttu-id="0e337-202">Selecteer Hallo machtigingsgroep (bijvoorbeeld **SSO Basic**) dat is toegestaan toosign in alleen via eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0e337-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="0e337-204">ik.</span><span class="sxs-lookup"><span data-stu-id="0e337-204">i.</span></span> <span data-ttu-id="0e337-205">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e337-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e337-206">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0e337-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e337-207">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0e337-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e337-208">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e337-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e337-209">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0e337-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e337-210">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0e337-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0e337-212">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e337-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e337-213">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e337-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e337-215">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0e337-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e337-217">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0e337-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e337-219">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0e337-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e337-221">a.</span><span class="sxs-lookup"><span data-stu-id="0e337-221">a.</span></span> <span data-ttu-id="0e337-222">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e337-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e337-223">b.</span><span class="sxs-lookup"><span data-stu-id="0e337-223">b.</span></span> <span data-ttu-id="0e337-224">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e337-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e337-225">c.</span><span class="sxs-lookup"><span data-stu-id="0e337-225">c.</span></span> <span data-ttu-id="0e337-226">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0e337-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e337-227">d.</span><span class="sxs-lookup"><span data-stu-id="0e337-227">d.</span></span> <span data-ttu-id="0e337-228">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e337-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="0e337-229">Maken van een installatiekopie Relay testgebruiker</span><span class="sxs-lookup"><span data-stu-id="0e337-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="0e337-230">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Relay installatiekopie van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0e337-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="0e337-231">**toocreate een gebruiker Britta Simon aangeroepen in de installatiekopie Relay, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e337-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e337-232">Eenmalige aanmelding tooyour installatiekopie Relay bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0e337-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="0e337-233">Ga te**gebruikers en machtigingen** en selecteer **SSO-gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="0e337-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="0e337-235">Voer Hallo **e**, **voornaam**, **achternaam**, en **bedrijf** van Hallo gebruiker gewenste tooprovision en selecteer Hallo machtigingsgroep (bijvoorbeeld: Basic SSO) die is Hallo-groep die alleen via eenmalige aanmelding kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="0e337-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="0e337-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e337-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e337-238">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e337-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e337-239">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooImage Relay.</span><span class="sxs-lookup"><span data-stu-id="0e337-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0e337-241">**tooassign Britta Simon tooImage Relay, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0e337-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e337-242">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0e337-244">Selecteer in de lijst met de toepassingen van Hallo **installatiekopie Relay**.</span><span class="sxs-lookup"><span data-stu-id="0e337-244">In hello applications list, select **Image Relay**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="0e337-246">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0e337-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0e337-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0e337-248">Click **Add** button.</span></span> <span data-ttu-id="0e337-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0e337-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0e337-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e337-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e337-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e337-254">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e337-254">Testing single sign-on</span></span>

<span data-ttu-id="0e337-255">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="0e337-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="0e337-256">Als u op Hallo installatiekopie Relay-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour installatiekopie Relay-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e337-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0e337-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0e337-257">Additional resources</span></span>

* [<span data-ttu-id="0e337-258">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e337-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e337-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e337-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

