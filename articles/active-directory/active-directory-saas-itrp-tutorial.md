---
title: 'Zelfstudie: Azure Active Directory-integratie met ITRP | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ITRP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="779c5-103">Zelfstudie: Azure Active Directory-integratie met ITRP</span><span class="sxs-lookup"><span data-stu-id="779c5-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="779c5-104">In deze zelfstudie leert u hoe toointegrate ITRP met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="779c5-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="779c5-105">ITRP integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="779c5-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="779c5-106">U kunt beheren in Azure AD die tooITRP toegang heeft</span><span class="sxs-lookup"><span data-stu-id="779c5-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="779c5-107">U kunt uw gebruikers tooautomatically get aangemelde tooITRP (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="779c5-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="779c5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="779c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="779c5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="779c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="779c5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="779c5-110">Prerequisites</span></span>

<span data-ttu-id="779c5-111">Azure AD-integratie met ITRP tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="779c5-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="779c5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="779c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="779c5-113">Een ITRP eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="779c5-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="779c5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="779c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="779c5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="779c5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="779c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="779c5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="779c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="779c5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="779c5-118">Scenario description</span></span>
<span data-ttu-id="779c5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="779c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="779c5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="779c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="779c5-121">Het toevoegen van ITRP van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="779c5-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="779c5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="779c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="779c5-123">Het toevoegen van ITRP van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="779c5-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="779c5-124">tooconfigure hello integratie van ITRP in tooAzure AD, moet u tooadd ITRP uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="779c5-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="779c5-125">**tooadd ITRP via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="779c5-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="779c5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="779c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="779c5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="779c5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="779c5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="779c5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="779c5-133">Typ in het zoekvak Hallo **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="779c5-133">In hello search box, type **ITRP**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="779c5-135">Selecteer in het deelvenster resultaten hello, **ITRP**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="779c5-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="779c5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="779c5-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="779c5-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ITRP op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="779c5-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="779c5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ITRP is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="779c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="779c5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ITRP toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="779c5-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="779c5-141">Wijs in ITRP, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="779c5-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="779c5-142">tooconfigure en eenmalige aanmelding Azure AD-test met ITRP, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="779c5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="779c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="779c5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="779c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="779c5-145">**[Maken van een ITRP testgebruiker](#creating-an-itrp-test-user)**  -toohave een equivalent van Britta Simon in ITRP die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="779c5-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="779c5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="779c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="779c5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="779c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="779c5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="779c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="779c5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ITRP configureren.</span><span class="sxs-lookup"><span data-stu-id="779c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="779c5-150">**Azure AD tooconfigure eenmalige aanmelding met ITRP, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="779c5-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="779c5-151">In de Azure-portal op Hallo Hallo **ITRP** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="779c5-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="779c5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="779c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="779c5-155">Op Hallo **ITRP domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="779c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="779c5-157">a.</span></span> <span data-ttu-id="779c5-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="779c5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="779c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="779c5-159">b.</span></span> <span data-ttu-id="779c5-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="779c5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="779c5-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="779c5-161">These values are not real.</span></span> <span data-ttu-id="779c5-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="779c5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="779c5-163">Neem contact op met [ITRP Client ondersteuningsteam](https://www.itrp.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="779c5-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="779c5-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="779c5-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="779c5-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="779c5-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="779c5-168">Op Hallo **ITRP configuratie** sectie, klikt u op **configureren ITRP** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="779c5-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="779c5-169">Kopiëren Hallo **SAML Single Sign-On Service URL's en Sign-Out** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="779c5-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="779c5-171">In een ander browservenster, meld u aan tooyour ITRP bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="779c5-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="779c5-172">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="779c5-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="779c5-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="779c5-174">Selecteer in de Hallo navigatiedeelvenster links **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="779c5-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="779c5-175">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775571.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="779c5-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="779c5-176">Voer in Hallo Single Sign-On configuratiesectie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="779c5-177">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775572.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="779c5-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="779c5-178">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775573.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="779c5-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="779c5-179">a.</span><span class="sxs-lookup"><span data-stu-id="779c5-179">a.</span></span> <span data-ttu-id="779c5-180">Klik op **Inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-180">Click **Enable**.</span></span>

    <span data-ttu-id="779c5-181">b.</span><span class="sxs-lookup"><span data-stu-id="779c5-181">b.</span></span> <span data-ttu-id="779c5-182">In **externe afmeldings-URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="779c5-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="779c5-183">c.</span><span class="sxs-lookup"><span data-stu-id="779c5-183">c.</span></span> <span data-ttu-id="779c5-184">In **SAML SSO URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="779c5-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="779c5-185">d.In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="779c5-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="779c5-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="779c5-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="779c5-187">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="779c5-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="779c5-188">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="779c5-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="779c5-189">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="779c5-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="779c5-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="779c5-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="779c5-191">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="779c5-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="779c5-193">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="779c5-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="779c5-194">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="779c5-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="779c5-196">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="779c5-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="779c5-198">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="779c5-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="779c5-200">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="779c5-202">a.</span><span class="sxs-lookup"><span data-stu-id="779c5-202">a.</span></span> <span data-ttu-id="779c5-203">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="779c5-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="779c5-204">b.</span><span class="sxs-lookup"><span data-stu-id="779c5-204">b.</span></span> <span data-ttu-id="779c5-205">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="779c5-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="779c5-206">c.</span><span class="sxs-lookup"><span data-stu-id="779c5-206">c.</span></span> <span data-ttu-id="779c5-207">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="779c5-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="779c5-208">d.</span><span class="sxs-lookup"><span data-stu-id="779c5-208">d.</span></span> <span data-ttu-id="779c5-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="779c5-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="779c5-210">Een testgebruiker ITRP maken</span><span class="sxs-lookup"><span data-stu-id="779c5-210">Creating an ITRP test user</span></span>

<span data-ttu-id="779c5-211">Azure AD tooenable gebruikers toolog in tooITRP, ze in tooITRP moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="779c5-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="779c5-212">In geval van ITRP Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="779c5-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="779c5-213">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="779c5-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="779c5-214">Meld u bij tooyour **ITRP** tenant.</span><span class="sxs-lookup"><span data-stu-id="779c5-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="779c5-215">Klik in de werkbalk bovenaan Hallo Hallo op **Records**.</span><span class="sxs-lookup"><span data-stu-id="779c5-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="779c5-216">![Beheerder](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="779c5-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="779c5-217">Selecteer in het pop-upmenu hello, **mensen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="779c5-218">![Mensen](./media/active-directory-saas-itrp-tutorial/ic775587.png "personen")</span><span class="sxs-lookup"><span data-stu-id="779c5-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="779c5-219">Klik op **toevoegen van nieuwe persoon** ('+').</span><span class="sxs-lookup"><span data-stu-id="779c5-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="779c5-220">![Beheerder](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="779c5-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="779c5-221">In het dialoogvenster Hallo nieuwe persoon toevoegen, voert Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="779c5-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="779c5-222">![Gebruiker](./media/active-directory-saas-itrp-tutorial/ic775577.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="779c5-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="779c5-223">a.</span><span class="sxs-lookup"><span data-stu-id="779c5-223">a.</span></span> <span data-ttu-id="779c5-224">Type Hallo **naam**, **e** van een geldige AAD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="779c5-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="779c5-225">b.</span><span class="sxs-lookup"><span data-stu-id="779c5-225">b.</span></span> <span data-ttu-id="779c5-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="779c5-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="779c5-227">U kunt andere ITRP gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ITRP tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="779c5-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="779c5-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="779c5-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="779c5-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooITRP toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="779c5-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="779c5-231">**tooassign Britta Simon tooITRP, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="779c5-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="779c5-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="779c5-234">Selecteer in de lijst met de toepassingen van Hallo **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="779c5-234">In hello applications list, select **ITRP**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="779c5-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="779c5-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="779c5-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="779c5-238">Click **Add** button.</span></span> <span data-ttu-id="779c5-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="779c5-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="779c5-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="779c5-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="779c5-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="779c5-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="779c5-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="779c5-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="779c5-244">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="779c5-244">Testing single sign-on</span></span>

<span data-ttu-id="779c5-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="779c5-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="779c5-246">Als u op Hallo ITRP-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ITRP toepassing.</span><span class="sxs-lookup"><span data-stu-id="779c5-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="779c5-247">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="779c5-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="779c5-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="779c5-248">Additional resources</span></span>

* [<span data-ttu-id="779c5-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="779c5-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="779c5-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="779c5-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

