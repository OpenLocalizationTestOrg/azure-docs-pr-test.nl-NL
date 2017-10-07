---
title: 'Zelfstudie: Azure Active Directory-integratie met Zendesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="3d733-103">Zelfstudie: Azure Active Directory-integratie met Zendesk</span><span class="sxs-lookup"><span data-stu-id="3d733-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="3d733-104">In deze zelfstudie leert u hoe toointegrate Zendesk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d733-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d733-105">Zendesk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3d733-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d733-106">U kunt beheren in Azure AD die tooZendesk toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3d733-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="3d733-107">U kunt uw gebruikers tooautomatically get aangemelde tooZendesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3d733-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d733-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3d733-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3d733-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d733-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d733-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3d733-110">Prerequisites</span></span>

<span data-ttu-id="3d733-111">Azure AD-integratie met Zendesk tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3d733-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="3d733-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3d733-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d733-113">Een Zendesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3d733-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3d733-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d733-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3d733-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d733-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3d733-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d733-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d733-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3d733-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3d733-118">Scenario description</span></span>
<span data-ttu-id="3d733-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d733-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d733-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3d733-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d733-121">Het toevoegen van Zendesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3d733-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="3d733-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d733-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="3d733-123">Het toevoegen van Zendesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3d733-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="3d733-124">tooconfigure hello integratie van Zendesk in Azure AD, moet u tooadd Zendesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3d733-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d733-125">**tooadd Zendesk via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3d733-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d733-126">In Hallo  **[Azure Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3d733-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d733-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d733-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d733-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d733-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3d733-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3d733-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3d733-133">Typ in het zoekvak Hallo **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="3d733-133">In hello search box, type **Zendesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="3d733-135">Selecteer in het deelvenster resultaten hello, **Zendesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d733-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d733-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d733-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d733-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zendesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3d733-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d733-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Zendesk is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d733-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="3d733-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in de Zendesk toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3d733-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="3d733-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="3d733-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="3d733-142">tooconfigure en eenmalige aanmelding Azure AD-test met Zendesk, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d733-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3d733-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d733-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d733-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d733-145">**[Maken van een testgebruiker Zendesk](#creating-a-zendesk-test-user)**  -toohave een equivalent van Britta Simon in Zendesk die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3d733-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d733-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3d733-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d733-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3d733-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d733-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3d733-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d733-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Zendesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d733-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="3d733-150">**Azure AD tooconfigure eenmalige aanmelding met Zendesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3d733-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d733-151">In de Azure-portal op Hallo Hallo **Zendesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3d733-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3d733-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3d733-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="3d733-155">Op Hallo **Zendesk-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="3d733-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d733-157">a.</span></span> <span data-ttu-id="3d733-158">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="3d733-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="3d733-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d733-159">b.</span></span> <span data-ttu-id="3d733-160">In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="3d733-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d733-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3d733-161">These values are not real.</span></span> <span data-ttu-id="3d733-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en identificatie-URL.</span><span class="sxs-lookup"><span data-stu-id="3d733-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="3d733-163">Neem contact op met [Zendesk-ondersteuningsteam](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3d733-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="3d733-164">Hallo SAML asserties verwacht Zendesk in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="3d733-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3d733-165">Er zijn geen verplichte SAML-kenmerken, maar u kunt desgewenst een kenmerk uit toevoegen **gebruikerskenmerken** sectie door de volgende Hallo onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="3d733-167">a.</span><span class="sxs-lookup"><span data-stu-id="3d733-167">a.</span></span> <span data-ttu-id="3d733-168">Klik op Hallo **weergeven en bewerken Hallo andere kenmerken** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3d733-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="3d733-170">b.</span><span class="sxs-lookup"><span data-stu-id="3d733-170">b.</span></span> <span data-ttu-id="3d733-171">Klik op Hallo **kenmerk toevoegen** tooopen **toevoegen kenmerk** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d733-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3d733-173">c.</span><span class="sxs-lookup"><span data-stu-id="3d733-173">c.</span></span> <span data-ttu-id="3d733-174">In Hallo **naam** textbox typenaam van het Hallo-kenmerk (bijvoorbeeld **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="3d733-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="3d733-175">d.</span><span class="sxs-lookup"><span data-stu-id="3d733-175">d.</span></span> <span data-ttu-id="3d733-176">Van Hallo **waarde** wilt weergeven, selecteer Hallo kenmerkwaarde (als **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="3d733-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="3d733-177">e.</span><span class="sxs-lookup"><span data-stu-id="3d733-177">e.</span></span> <span data-ttu-id="3d733-178">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="3d733-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="3d733-179">U kenmerken tooadd uitbreidingskenmerken die zich niet in Azure AD standaard gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d733-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="3d733-180">Klik op [gebruikerskenmerken die kunnen worden ingesteld in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) kenmerken van een volledige lijst met tooget Hallo van SAML **Zendesk** accepteert.</span><span class="sxs-lookup"><span data-stu-id="3d733-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="3d733-181">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="3d733-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="3d733-183">Op Hallo **Zendesk configuratie** sectie, klikt u op **configureren Zendesk** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3d733-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3d733-184">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3d733-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="3d733-186">In een ander browservenster, meld u bij uw bedrijf Zendesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d733-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="3d733-187">Klik op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3d733-187">Click **Admin**.</span></span>

9. <span data-ttu-id="3d733-188">Klik in het Hallo navigatiedeelvenster links op **instellingen**, en klik vervolgens op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="3d733-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="3d733-189">Op Hallo **beveiliging** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="3d733-190">![Beveiliging](./media/active-directory-saas-zendesk-tutorial/ic773089.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="3d733-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="3d733-191">![Eenmalige aanmelding](./media/active-directory-saas-zendesk-tutorial/ic773090.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="3d733-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="3d733-192">a.</span><span class="sxs-lookup"><span data-stu-id="3d733-192">a.</span></span> <span data-ttu-id="3d733-193">Klik op Hallo **Admin & Agents** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3d733-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="3d733-194">b.</span><span class="sxs-lookup"><span data-stu-id="3d733-194">b.</span></span> <span data-ttu-id="3d733-195">Selecteer **eenmalige aanmelding (SSO) en SAML**, en selecteer vervolgens **SAML**.</span><span class="sxs-lookup"><span data-stu-id="3d733-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="3d733-196">c.</span><span class="sxs-lookup"><span data-stu-id="3d733-196">c.</span></span> <span data-ttu-id="3d733-197">In **SAML SSO URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3d733-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="3d733-198">d.</span><span class="sxs-lookup"><span data-stu-id="3d733-198">d.</span></span> <span data-ttu-id="3d733-199">In **externe URL voor afmelden** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3d733-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="3d733-200">e.</span><span class="sxs-lookup"><span data-stu-id="3d733-200">e.</span></span> <span data-ttu-id="3d733-201">In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3d733-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="3d733-202">f.</span><span class="sxs-lookup"><span data-stu-id="3d733-202">f.</span></span> <span data-ttu-id="3d733-203">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3d733-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d733-204">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3d733-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d733-205">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d733-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3d733-207">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3d733-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d733-208">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3d733-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d733-210">toodisplay hello lijst met gebruikers te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3d733-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d733-212">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d733-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d733-214">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3d733-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d733-216">a.</span><span class="sxs-lookup"><span data-stu-id="3d733-216">a.</span></span> <span data-ttu-id="3d733-217">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d733-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d733-218">b.</span><span class="sxs-lookup"><span data-stu-id="3d733-218">b.</span></span> <span data-ttu-id="3d733-219">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d733-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d733-220">c.</span><span class="sxs-lookup"><span data-stu-id="3d733-220">c.</span></span> <span data-ttu-id="3d733-221">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3d733-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3d733-222">d.</span><span class="sxs-lookup"><span data-stu-id="3d733-222">d.</span></span> <span data-ttu-id="3d733-223">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d733-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="3d733-224">Een testgebruiker Zendesk maken</span><span class="sxs-lookup"><span data-stu-id="3d733-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="3d733-225">Azure AD tooenable gebruikers toolog in **Zendesk**, deze moeten worden ingericht in **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="3d733-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="3d733-226">Afhankelijk van het Hallo-rol is toegewezen in Hallo apps, verwacht dat de Hallo gedrag:</span><span class="sxs-lookup"><span data-stu-id="3d733-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="3d733-227">**Eindgebruikers** accounts automatisch worden ingericht als u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="3d733-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="3d733-228">**Agent** en **Admin** accounts moeten handmatig worden ingericht in toobe **Zendesk** voordat u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="3d733-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="3d733-229">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3d733-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d733-230">Meld u bij tooyour **Zendesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="3d733-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="3d733-231">Selecteer Hallo **klantenlijst** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3d733-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="3d733-232">Selecteer Hallo **gebruiker** tabblad en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3d733-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="3d733-233">![Gebruiker toevoegen](./media/active-directory-saas-zendesk-tutorial/ic773632.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="3d733-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="3d733-234">Typ de e-mailadres Hallo van een bestaande Azure AD-account dat u wilt tooprovision en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3d733-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="3d733-235">![Nieuwe gebruiker](./media/active-directory-saas-zendesk-tutorial/ic773633.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="3d733-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="3d733-236">U kunt andere Zendesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Zendesk tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="3d733-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3d733-237">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d733-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3d733-238">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooZendesk toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3d733-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3d733-240">**tooassign Britta Simon tooZendesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3d733-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d733-241">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d733-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3d733-243">Selecteer in de lijst met de toepassingen van Hallo **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="3d733-243">In hello applications list, select **Zendesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="3d733-245">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3d733-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3d733-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3d733-247">Click **Add** button.</span></span> <span data-ttu-id="3d733-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d733-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3d733-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3d733-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d733-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d733-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d733-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d733-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d733-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d733-253">Testing single sign-on</span></span>

<span data-ttu-id="3d733-254">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3d733-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3d733-255">Als u op Hallo Zendesk-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zendesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d733-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="3d733-256">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d733-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d733-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3d733-257">Additional resources</span></span>

* [<span data-ttu-id="3d733-258">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d733-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d733-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d733-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
