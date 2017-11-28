---
title: 'Zelfstudie: Azure Active Directory-integratie met Kintone | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="992ce-103">Zelfstudie: Azure Active Directory-integratie met Kintone</span><span class="sxs-lookup"><span data-stu-id="992ce-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="992ce-104">In deze zelfstudie leert u hoe toointegrate Kintone met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="992ce-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="992ce-105">Kintone integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="992ce-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="992ce-106">U kunt beheren in Azure AD die tooKintone toegang heeft</span><span class="sxs-lookup"><span data-stu-id="992ce-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="992ce-107">U kunt uw gebruikers tooautomatically get aangemelde tooKintone (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="992ce-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="992ce-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="992ce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="992ce-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="992ce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="992ce-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="992ce-110">Prerequisites</span></span>

<span data-ttu-id="992ce-111">Azure AD-integratie met Kintone tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="992ce-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="992ce-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="992ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="992ce-113">Een Kintone eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="992ce-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="992ce-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="992ce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="992ce-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="992ce-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="992ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="992ce-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="992ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="992ce-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="992ce-118">Scenario description</span></span>
<span data-ttu-id="992ce-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="992ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="992ce-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="992ce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="992ce-121">Het toevoegen van Kintone van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="992ce-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="992ce-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="992ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="992ce-123">Het toevoegen van Kintone van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="992ce-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="992ce-124">tooconfigure hello integratie van Kintone in Azure AD, moet u tooadd Kintone uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="992ce-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="992ce-125">**tooadd Kintone via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="992ce-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="992ce-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="992ce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="992ce-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="992ce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="992ce-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="992ce-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="992ce-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="992ce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="992ce-133">Typ in het zoekvak Hallo **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="992ce-133">In hello search box, type **Kintone**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="992ce-135">Selecteer in het deelvenster resultaten hello, **Kintone**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="992ce-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="992ce-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="992ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="992ce-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Kintone op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="992ce-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="992ce-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kintone is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="992ce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="992ce-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kintone toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="992ce-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="992ce-141">Wijs in Kintone, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="992ce-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="992ce-142">tooconfigure en eenmalige aanmelding Azure AD-test met Kintone, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="992ce-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="992ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="992ce-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="992ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="992ce-145">**[Maken van een testgebruiker Kintone](#creating-a-kintone-test-user)**  -toohave een equivalent van Britta Simon in Kintone die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="992ce-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="992ce-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="992ce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="992ce-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="992ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="992ce-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="992ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="992ce-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kintone configureren.</span><span class="sxs-lookup"><span data-stu-id="992ce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="992ce-150">**Azure AD tooconfigure eenmalige aanmelding met Kintone, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="992ce-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="992ce-151">In de Azure-portal op Hallo Hallo **Kintone** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="992ce-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="992ce-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="992ce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="992ce-155">Op Hallo **Kintone domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="992ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="992ce-157">a.</span></span> <span data-ttu-id="992ce-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="992ce-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="992ce-159">b.</span><span class="sxs-lookup"><span data-stu-id="992ce-159">b.</span></span> <span data-ttu-id="992ce-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="992ce-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="992ce-161">These values are not real.</span></span> <span data-ttu-id="992ce-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="992ce-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="992ce-163">Neem contact op met [Kintone Client ondersteuningsteam](https://www.kintone.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="992ce-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="992ce-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="992ce-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="992ce-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="992ce-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="992ce-168">Op Hallo **Kintone configuratie** sectie, klikt u op **configureren Kintone** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="992ce-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="992ce-169">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="992ce-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="992ce-171">In een ander browservenster, meld u aan bij uw **Kintone** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="992ce-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="992ce-172">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="992ce-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="992ce-173">![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="992ce-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="992ce-174">Klik op **gebruikers & Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="992ce-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="992ce-175">![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruikers & Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="992ce-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="992ce-176">Onder **Systeembeheer \> beveiliging** klikt u op **aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="992ce-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="992ce-177">![Aanmelding](./media/active-directory-saas-kintone-tutorial/ic785881.png "aanmelding")</span><span class="sxs-lookup"><span data-stu-id="992ce-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="992ce-178">Klik op **inschakelen SAML-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="992ce-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="992ce-179">![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="992ce-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="992ce-180">Voer in Hallo sectie SAML-verificatie, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="992ce-181">![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="992ce-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="992ce-182">a.</span><span class="sxs-lookup"><span data-stu-id="992ce-182">a.</span></span> <span data-ttu-id="992ce-183">In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="992ce-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="992ce-184">b.</span><span class="sxs-lookup"><span data-stu-id="992ce-184">b.</span></span> <span data-ttu-id="992ce-185">In Hallo **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="992ce-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="992ce-186">c.</span><span class="sxs-lookup"><span data-stu-id="992ce-186">c.</span></span> <span data-ttu-id="992ce-187">Klik op **Bladeren** tooupload uw gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="992ce-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="992ce-188">d.</span><span class="sxs-lookup"><span data-stu-id="992ce-188">d.</span></span> <span data-ttu-id="992ce-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="992ce-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="992ce-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="992ce-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="992ce-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="992ce-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="992ce-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="992ce-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="992ce-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="992ce-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="992ce-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="992ce-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="992ce-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="992ce-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="992ce-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="992ce-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="992ce-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="992ce-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="992ce-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="992ce-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="992ce-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="992ce-205">a.</span><span class="sxs-lookup"><span data-stu-id="992ce-205">a.</span></span> <span data-ttu-id="992ce-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="992ce-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="992ce-207">b.</span><span class="sxs-lookup"><span data-stu-id="992ce-207">b.</span></span> <span data-ttu-id="992ce-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="992ce-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="992ce-209">c.</span><span class="sxs-lookup"><span data-stu-id="992ce-209">c.</span></span> <span data-ttu-id="992ce-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="992ce-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="992ce-211">d.</span><span class="sxs-lookup"><span data-stu-id="992ce-211">d.</span></span> <span data-ttu-id="992ce-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="992ce-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="992ce-213">Een testgebruiker Kintone maken</span><span class="sxs-lookup"><span data-stu-id="992ce-213">Creating a Kintone test user</span></span>

<span data-ttu-id="992ce-214">Azure AD tooenable gebruikers toolog in tooKintone, ze in Kintone moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="992ce-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="992ce-215">In geval van Kintone Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="992ce-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="992ce-216">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="992ce-217">Meld u bij tooyour **Kintone** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="992ce-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="992ce-218">Klik op **instelling**.</span><span class="sxs-lookup"><span data-stu-id="992ce-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="992ce-219">![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="992ce-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="992ce-220">Klik op **gebruikers & Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="992ce-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="992ce-221">![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruiker & Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="992ce-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="992ce-222">Onder **Gebruikersbeheer**, klikt u op **afdelingen gebr & uikers**.</span><span class="sxs-lookup"><span data-stu-id="992ce-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="992ce-223">![Afdeling gebr & uikers](./media/active-directory-saas-kintone-tutorial/ic785888.png "afdeling gebr & uikers")</span><span class="sxs-lookup"><span data-stu-id="992ce-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="992ce-224">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="992ce-224">Click **New User**.</span></span>
   
    <span data-ttu-id="992ce-225">![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785889.png "nieuwe gebruikers")</span><span class="sxs-lookup"><span data-stu-id="992ce-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="992ce-226">In Hallo **nieuwe gebruiker** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="992ce-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="992ce-227">![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785890.png "nieuwe gebruikers")</span><span class="sxs-lookup"><span data-stu-id="992ce-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="992ce-228">a.</span><span class="sxs-lookup"><span data-stu-id="992ce-228">a.</span></span> <span data-ttu-id="992ce-229">Typ een **weergavenaam**, **aanmeldingsnaam**, **nieuw wachtwoord**, **wachtwoord bevestigen**, **e-mailadres**, en andere details van een geldige AAD-account dat u wilt dat tooprovision in Hallo bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="992ce-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="992ce-230">b.</span><span class="sxs-lookup"><span data-stu-id="992ce-230">b.</span></span> <span data-ttu-id="992ce-231">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="992ce-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="992ce-232">U kunt andere Kintone gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Kintone tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="992ce-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="992ce-233">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="992ce-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="992ce-234">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKintone toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="992ce-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="992ce-236">**tooassign Britta Simon tooKintone, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="992ce-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="992ce-237">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="992ce-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="992ce-239">Selecteer in de lijst met de toepassingen van Hallo **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="992ce-239">In hello applications list, select **Kintone**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="992ce-241">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="992ce-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="992ce-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="992ce-243">Click **Add** button.</span></span> <span data-ttu-id="992ce-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="992ce-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="992ce-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="992ce-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="992ce-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="992ce-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="992ce-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="992ce-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="992ce-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="992ce-249">Testing single sign-on</span></span>

<span data-ttu-id="992ce-250">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="992ce-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="992ce-251">Als u op Hallo Kintone tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kintone toepassing.</span><span class="sxs-lookup"><span data-stu-id="992ce-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="992ce-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="992ce-252">Additional resources</span></span>

* [<span data-ttu-id="992ce-253">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="992ce-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="992ce-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="992ce-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

