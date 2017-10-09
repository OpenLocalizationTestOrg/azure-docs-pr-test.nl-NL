---
title: 'Zelfstudie: Azure Active Directory-integratie met Freshservice | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="5f50f-103">Zelfstudie: Azure Active Directory-integratie met Freshservice</span><span class="sxs-lookup"><span data-stu-id="5f50f-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="5f50f-104">In deze zelfstudie leert u hoe toointegrate Freshservice met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f50f-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f50f-105">Freshservice integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f50f-106">U kunt beheren in Azure AD die tooFreshservice toegang heeft</span><span class="sxs-lookup"><span data-stu-id="5f50f-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="5f50f-107">U kunt uw gebruikers tooautomatically get aangemelde tooFreshservice (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5f50f-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f50f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5f50f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f50f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f50f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f50f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5f50f-110">Prerequisites</span></span>

<span data-ttu-id="5f50f-111">Azure AD-integratie met Freshservice tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="5f50f-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="5f50f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5f50f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f50f-113">Een Freshservice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5f50f-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f50f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5f50f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f50f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f50f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5f50f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f50f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f50f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f50f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5f50f-118">Scenario description</span></span>
<span data-ttu-id="5f50f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5f50f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f50f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f50f-121">Het toevoegen van Freshservice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5f50f-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="5f50f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5f50f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="5f50f-123">Het toevoegen van Freshservice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5f50f-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="5f50f-124">tooconfigure hello integratie van Freshservice in Azure AD, moet u tooadd Freshservice uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5f50f-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f50f-125">**tooadd Freshservice via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5f50f-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f50f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5f50f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f50f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f50f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5f50f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5f50f-133">Typ in het zoekvak Hallo **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-133">In hello search box, type **Freshservice**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="5f50f-135">Selecteer in het deelvenster resultaten hello, **Freshservice**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5f50f-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f50f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5f50f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f50f-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Freshservice op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="5f50f-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f50f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Freshservice is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f50f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="5f50f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Freshservice toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="5f50f-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="5f50f-141">Wijs in Freshservice, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="5f50f-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f50f-142">tooconfigure en eenmalige aanmelding Azure AD-test met Freshservice, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f50f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="5f50f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f50f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f50f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f50f-145">**[Maken van een testgebruiker Freshservice](#creating-a-freshservice-test-user)**  -toohave een equivalent van Britta Simon in Freshservice die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5f50f-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f50f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5f50f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f50f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5f50f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f50f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5f50f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f50f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Freshservice configureren.</span><span class="sxs-lookup"><span data-stu-id="5f50f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="5f50f-150">**Azure AD tooconfigure eenmalige aanmelding met Freshservice, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5f50f-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f50f-151">In de Azure-portal op Hallo Hallo **Freshservice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5f50f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5f50f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="5f50f-155">Op Hallo **Freshservice domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="5f50f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5f50f-157">a.</span></span> <span data-ttu-id="5f50f-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="5f50f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="5f50f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5f50f-159">b.</span></span> <span data-ttu-id="5f50f-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="5f50f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f50f-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="5f50f-161">These values are not real.</span></span> <span data-ttu-id="5f50f-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="5f50f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5f50f-163">Neem contact op met [Freshservice Client ondersteuningsteam](https://support.freshservice.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="5f50f-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5f50f-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, Kopieer **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f50f-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="5f50f-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5f50f-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f50f-168">Op Hallo **Freshservice configuratie** sectie, klikt u op **configureren Freshservice** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f50f-169">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5f50f-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="5f50f-171">In een ander browservenster, meld u aan tooyour Freshservice bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="5f50f-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="5f50f-172">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="5f50f-173">![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="5f50f-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="5f50f-174">In Hallo **Customer Portal**, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="5f50f-175">![Beveiliging](./media/active-directory-saas-freshservice-tutorial/ic790815.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="5f50f-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="5f50f-176">In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5f50f-177">![Eenmalige aanmelding](./media/active-directory-saas-freshservice-tutorial/ic790816.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="5f50f-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="5f50f-178">a.</span><span class="sxs-lookup"><span data-stu-id="5f50f-178">a.</span></span> <span data-ttu-id="5f50f-179">Switch **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="5f50f-180">b.</span><span class="sxs-lookup"><span data-stu-id="5f50f-180">b.</span></span> <span data-ttu-id="5f50f-181">Selecteer **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="5f50f-182">c.</span><span class="sxs-lookup"><span data-stu-id="5f50f-182">c.</span></span> <span data-ttu-id="5f50f-183">In Hallo **aanmeldings-URL van SAML** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f50f-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5f50f-184">d.</span><span class="sxs-lookup"><span data-stu-id="5f50f-184">d.</span></span> <span data-ttu-id="5f50f-185">In Hallo **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f50f-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5f50f-186">e.</span><span class="sxs-lookup"><span data-stu-id="5f50f-186">e.</span></span> <span data-ttu-id="5f50f-187">In **beveiliging certificaat vingerafdruk** textbox plakken Hallo **VINGERAFDRUK** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f50f-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5f50f-188">f.</span><span class="sxs-lookup"><span data-stu-id="5f50f-188">f.</span></span> <span data-ttu-id="5f50f-189">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="5f50f-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="5f50f-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="5f50f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f50f-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="5f50f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f50f-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f50f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f50f-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5f50f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f50f-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5f50f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5f50f-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5f50f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f50f-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5f50f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f50f-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f50f-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="5f50f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f50f-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f50f-205">a.</span><span class="sxs-lookup"><span data-stu-id="5f50f-205">a.</span></span> <span data-ttu-id="5f50f-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f50f-207">b.</span><span class="sxs-lookup"><span data-stu-id="5f50f-207">b.</span></span> <span data-ttu-id="5f50f-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f50f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f50f-209">c.</span><span class="sxs-lookup"><span data-stu-id="5f50f-209">c.</span></span> <span data-ttu-id="5f50f-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f50f-211">d.</span><span class="sxs-lookup"><span data-stu-id="5f50f-211">d.</span></span> <span data-ttu-id="5f50f-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="5f50f-213">Een testgebruiker Freshservice maken</span><span class="sxs-lookup"><span data-stu-id="5f50f-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="5f50f-214">Azure AD tooenable gebruikers toolog in tooFreshService, ze in FreshService moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="5f50f-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="5f50f-215">In geval van FreshService Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="5f50f-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="5f50f-216">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5f50f-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f50f-217">Meld u bij tooyour **FreshService** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="5f50f-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="5f50f-218">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="5f50f-219">![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="5f50f-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="5f50f-220">In Hallo **Gebruikersbeheer** sectie, klikt u op **aanvragers**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="5f50f-221">![Aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790818.png "aanvragers")</span><span class="sxs-lookup"><span data-stu-id="5f50f-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="5f50f-222">Klik op **nieuwe aanvrager**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="5f50f-223">![Nieuwe aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790819.png "nieuwe aanvragers")</span><span class="sxs-lookup"><span data-stu-id="5f50f-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="5f50f-224">In Hallo **nieuwe aanvrager** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f50f-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5f50f-225">![Nieuwe aanvrager](./media/active-directory-saas-freshservice-tutorial/ic790820.png "nieuwe aanvrager")</span><span class="sxs-lookup"><span data-stu-id="5f50f-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="5f50f-226">a.</span><span class="sxs-lookup"><span data-stu-id="5f50f-226">a.</span></span> <span data-ttu-id="5f50f-227">Voer Hallo **voornaam** en **e** kenmerken van een geldige Azure Active Directory-account dat u wilt dat tooprovision in Hallo gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="5f50f-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="5f50f-228">b.</span><span class="sxs-lookup"><span data-stu-id="5f50f-228">b.</span></span> <span data-ttu-id="5f50f-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5f50f-230">Hello Azure Active Directory-accounthouder opgehaald een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt</span><span class="sxs-lookup"><span data-stu-id="5f50f-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="5f50f-231">U kunt andere FreshService gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door FreshService tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="5f50f-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Gebruiker toewijzen][200] 

<span data-ttu-id="5f50f-233">**tooassign Britta Simon tooFreshservice, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5f50f-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f50f-234">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5f50f-236">Selecteer in de lijst met de toepassingen van Hallo **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-236">In hello applications list, select **Freshservice**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="5f50f-238">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5f50f-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5f50f-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5f50f-240">Click **Add** button.</span></span> <span data-ttu-id="5f50f-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5f50f-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f50f-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f50f-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f50f-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f50f-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5f50f-246">Testing single sign-on</span></span>

<span data-ttu-id="5f50f-247">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="5f50f-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f50f-248">Als u op Hallo Freshservice tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Freshservice toepassing.</span><span class="sxs-lookup"><span data-stu-id="5f50f-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f50f-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5f50f-249">Additional resources</span></span>

* [<span data-ttu-id="5f50f-250">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f50f-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f50f-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f50f-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

