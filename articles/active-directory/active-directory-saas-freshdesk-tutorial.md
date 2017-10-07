---
title: 'Zelfstudie: Azure Active Directory-integratie met FreshDesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="4e87c-103">Zelfstudie: Azure Active Directory-integratie met FreshDesk</span><span class="sxs-lookup"><span data-stu-id="4e87c-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="4e87c-104">In deze zelfstudie leert u hoe toointegrate FreshDesk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e87c-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e87c-105">FreshDesk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e87c-106">U kunt beheren in Azure AD die tooFreshDesk toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4e87c-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="4e87c-107">U kunt uw gebruikers tooautomatically get aangemelde tooFreshDesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4e87c-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e87c-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="4e87c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="4e87c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e87c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e87c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4e87c-110">Prerequisites</span></span>

<span data-ttu-id="4e87c-111">Azure AD-integratie met FreshDesk tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4e87c-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="4e87c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4e87c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e87c-113">Een FreshDesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4e87c-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e87c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4e87c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e87c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e87c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4e87c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4e87c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e87c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e87c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4e87c-118">Scenario description</span></span>
<span data-ttu-id="4e87c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4e87c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e87c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e87c-121">Het toevoegen van FreshDesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4e87c-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="4e87c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e87c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="4e87c-123">Het toevoegen van FreshDesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4e87c-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="4e87c-124">tooconfigure hello integratie van FreshDesk in Azure AD, moet u tooadd FreshDesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4e87c-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e87c-125">**tooadd FreshDesk via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e87c-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e87c-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4e87c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e87c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e87c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4e87c-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4e87c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4e87c-133">Typ in het zoekvak Hallo **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-133">In hello search box, type **FreshDesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="4e87c-135">Selecteer in het deelvenster resultaten hello, **FreshDesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e87c-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e87c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e87c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e87c-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FreshDesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4e87c-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4e87c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FreshDesk is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e87c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="4e87c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FreshDesk toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4e87c-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="4e87c-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="4e87c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="4e87c-142">tooconfigure en eenmalige aanmelding Azure AD-test met FreshDesk, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e87c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4e87c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e87c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e87c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e87c-145">**[Maken van een testgebruiker FreshDesk](#creating-a-freshdesk-test-user)**  -toohave een equivalent van Britta Simon in FreshDesk die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="4e87c-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="4e87c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e87c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e87c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4e87c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e87c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4e87c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e87c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing FreshDesk configureren.</span><span class="sxs-lookup"><span data-stu-id="4e87c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="4e87c-150">**Azure AD tooconfigure eenmalige aanmelding met FreshDesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e87c-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e87c-151">In hello Azure Management portal op Hallo **FreshDesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4e87c-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e87c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="4e87c-155">Op Hallo **FreshDesk domein en de URL's** sectie, Voer Hallo **aanmeldings-URL** als: `https://<tenant-name>.freshdesk.com` of een andere waarde Freshdesk is voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="4e87c-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="4e87c-157">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="4e87c-157">Please note that this is not the real value.</span></span> <span data-ttu-id="4e87c-158">U moet de waarde wordt bijgewerkt met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e87c-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="4e87c-159">Neem contact op met [FreshDesk Client ondersteuningsteam](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="4e87c-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="4e87c-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla Hallo certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4e87c-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="4e87c-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4e87c-162">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e87c-164">Op Hallo **FreshDesk configuratie** sectie, klikt u op **FreshDesk configureren** venster tooopen configureren eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e87c-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="4e87c-165">Kopieer Hallo SAML Single Sign-On Service-URL en Sign-Out-URL van Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="4e87c-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="4e87c-167">In een ander browservenster, meld u bij uw bedrijf Freshdesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4e87c-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="4e87c-168">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="4e87c-169">![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="4e87c-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="4e87c-170">In Hallo **algemene instellingen** tabblad **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="4e87c-171">![Beveiliging](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="4e87c-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="4e87c-172">In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4e87c-173">![Eenmalige aanmelding](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="4e87c-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="4e87c-174">a.</span><span class="sxs-lookup"><span data-stu-id="4e87c-174">a.</span></span> <span data-ttu-id="4e87c-175">Voor **eenmalige aanmelding op (SSO)**, selecteer **op**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="4e87c-176">b.</span><span class="sxs-lookup"><span data-stu-id="4e87c-176">b.</span></span> <span data-ttu-id="4e87c-177">Selecteer **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="4e87c-178">c.</span><span class="sxs-lookup"><span data-stu-id="4e87c-178">c.</span></span> <span data-ttu-id="4e87c-179">Type Hallo **SAML Single Sign-On Service-URL** u vanuit Azure-portal hebt gekopieerd in Hallo **aanmeldings-URL van SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="4e87c-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="4e87c-180">d.</span><span class="sxs-lookup"><span data-stu-id="4e87c-180">d.</span></span> <span data-ttu-id="4e87c-181">Type Hallo **Sign-Out URL** u vanuit Azure-portal hebt gekopieerd in Hallo **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4e87c-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="4e87c-182">e.</span><span class="sxs-lookup"><span data-stu-id="4e87c-182">e.</span></span> <span data-ttu-id="4e87c-183">Kopiëren Hallo **vingerafdruk** waarde van het certificaat Hallo gedownload vanuit Azure-portal en plak deze in Hallo **beveiliging certificaat vingerafdruk** textbox.</span><span class="sxs-lookup"><span data-stu-id="4e87c-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="4e87c-184">Zie voor meer informatie [hoe tooretrieve vingerafdrukwaarde van een certificaat](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="4e87c-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="4e87c-185">f.</span><span class="sxs-lookup"><span data-stu-id="4e87c-185">f.</span></span> <span data-ttu-id="4e87c-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e87c-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4e87c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e87c-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4e87c-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4e87c-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e87c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e87c-191">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4e87c-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e87c-193">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4e87c-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e87c-195">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e87c-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e87c-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e87c-199">a.</span><span class="sxs-lookup"><span data-stu-id="4e87c-199">a.</span></span> <span data-ttu-id="4e87c-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e87c-201">b.</span><span class="sxs-lookup"><span data-stu-id="4e87c-201">b.</span></span> <span data-ttu-id="4e87c-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e87c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e87c-203">c.</span><span class="sxs-lookup"><span data-stu-id="4e87c-203">c.</span></span> <span data-ttu-id="4e87c-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e87c-205">d.</span><span class="sxs-lookup"><span data-stu-id="4e87c-205">d.</span></span> <span data-ttu-id="4e87c-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="4e87c-207">Een testgebruiker FreshDesk maken</span><span class="sxs-lookup"><span data-stu-id="4e87c-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="4e87c-208">In de volgorde tooenable Azure AD gebruikers toolog in FreshDesk, moeten ze worden ingericht in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="4e87c-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="4e87c-209">In geval van FreshDesk Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="4e87c-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="4e87c-210">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="4e87c-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e87c-211">Meld u bij tooyour **Freshdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="4e87c-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="4e87c-212">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="4e87c-213">![Beheerder](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="4e87c-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="4e87c-214">In Hallo **algemene instellingen** tabblad **Agents**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="4e87c-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="4e87c-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="4e87c-216">Klik op **nieuwe Agent**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="4e87c-217">![De nieuwe Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "nieuwe-Agent")</span><span class="sxs-lookup"><span data-stu-id="4e87c-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="4e87c-218">Op Hallo agentgegevens dialoogvenster uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e87c-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="4e87c-219">![Agentgegevens](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "agentgegevens")</span><span class="sxs-lookup"><span data-stu-id="4e87c-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="4e87c-220">a.</span><span class="sxs-lookup"><span data-stu-id="4e87c-220">a.</span></span> <span data-ttu-id="4e87c-221">In Hallo **volledige naam** textbox Hallo-typenaam van de gewenste tooprovision hello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="4e87c-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="4e87c-222">b.</span><span class="sxs-lookup"><span data-stu-id="4e87c-222">b.</span></span> <span data-ttu-id="4e87c-223">In Hallo **e** textbox type hello Azure AD e-mailadres van hello Azure AD-account die u wilt tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4e87c-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="4e87c-224">c.</span><span class="sxs-lookup"><span data-stu-id="4e87c-224">c.</span></span> <span data-ttu-id="4e87c-225">In Hallo **titel** textbox type Hallo titel van de gewenste tooprovision hello Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="4e87c-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="4e87c-226">d.</span><span class="sxs-lookup"><span data-stu-id="4e87c-226">d.</span></span> <span data-ttu-id="4e87c-227">Selecteer **Agents rol**, en klik vervolgens op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="4e87c-228">e.</span><span class="sxs-lookup"><span data-stu-id="4e87c-228">e.</span></span> <span data-ttu-id="4e87c-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="4e87c-230">Hello Azure AD-accounthouder krijgt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4e87c-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="4e87c-231">U kunt andere Freshdesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Freshdesk tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="4e87c-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="4e87c-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="4e87c-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4e87c-233">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e87c-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4e87c-234">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooBox toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="4e87c-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4e87c-236">**tooassign Britta Simon tooFreshDesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e87c-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e87c-237">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4e87c-239">Selecteer in de lijst met de toepassingen van Hallo **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="4e87c-241">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4e87c-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4e87c-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4e87c-243">Click **Add** button.</span></span> <span data-ttu-id="4e87c-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e87c-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4e87c-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e87c-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e87c-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e87c-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e87c-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e87c-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e87c-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e87c-249">Testing single sign-on</span></span>

<span data-ttu-id="4e87c-250">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4e87c-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4e87c-251">Als u op Hallo FreshDesk tegel in Hallo Toegangsvenster, krijgt u aanmelding pagina tooget aangemelde tooyour FreshDesk toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e87c-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e87c-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4e87c-252">Additional resources</span></span>

* [<span data-ttu-id="4e87c-253">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e87c-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e87c-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e87c-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

