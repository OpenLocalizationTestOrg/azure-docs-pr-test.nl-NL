---
title: 'Zelfstudie: Azure Active Directory-integratie met ThirdLight | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ThirdLight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="505cb-103">Zelfstudie: Azure Active Directory-integratie met ThirdLight</span><span class="sxs-lookup"><span data-stu-id="505cb-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="505cb-104">In deze zelfstudie leert u hoe toointegrate ThirdLight met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="505cb-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="505cb-105">ThirdLight integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="505cb-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="505cb-106">U kunt beheren in Azure AD die tooThirdLight toegang heeft</span><span class="sxs-lookup"><span data-stu-id="505cb-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="505cb-107">U kunt uw gebruikers tooautomatically get aangemelde tooThirdLight (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="505cb-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="505cb-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="505cb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="505cb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="505cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="505cb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="505cb-110">Prerequisites</span></span>

<span data-ttu-id="505cb-111">Azure AD-integratie met ThirdLight tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="505cb-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="505cb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="505cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="505cb-113">Een ThirdLight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="505cb-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="505cb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="505cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="505cb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="505cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="505cb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="505cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="505cb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="505cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="505cb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="505cb-118">Scenario description</span></span>
<span data-ttu-id="505cb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="505cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="505cb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="505cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="505cb-121">Het toevoegen van ThirdLight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="505cb-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="505cb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="505cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="505cb-123">Het toevoegen van ThirdLight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="505cb-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="505cb-124">tooconfigure hello integratie van ThirdLight in Azure AD, moet u tooadd ThirdLight uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="505cb-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="505cb-125">**tooadd ThirdLight via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="505cb-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="505cb-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="505cb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="505cb-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="505cb-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="505cb-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="505cb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="505cb-133">Typ in het zoekvak Hallo **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="505cb-133">In hello search box, type **ThirdLight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="505cb-135">Selecteer in het deelvenster resultaten hello, **ThirdLight**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="505cb-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="505cb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="505cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="505cb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ThirdLight op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="505cb-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="505cb-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ThirdLight is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="505cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="505cb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ThirdLight toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="505cb-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="505cb-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="505cb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="505cb-142">tooconfigure en eenmalige aanmelding Azure AD-test met ThirdLight, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="505cb-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="505cb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="505cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="505cb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="505cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="505cb-145">**[Maken van een testgebruiker ThirdLight](#creating-a-thirdlight-test-user)**  -toohave een equivalent van Britta Simon in ThirdLight die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="505cb-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="505cb-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="505cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="505cb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="505cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="505cb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="505cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="505cb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ThirdLight configureren.</span><span class="sxs-lookup"><span data-stu-id="505cb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="505cb-150">**Azure AD tooconfigure eenmalige aanmelding met ThirdLight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="505cb-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="505cb-151">In de Azure-portal op Hallo Hallo **ThirdLight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="505cb-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="505cb-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="505cb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="505cb-155">Op Hallo **ThirdLight domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="505cb-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="505cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="505cb-157">a.</span></span> <span data-ttu-id="505cb-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="505cb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="505cb-159">b.</span><span class="sxs-lookup"><span data-stu-id="505cb-159">b.</span></span> <span data-ttu-id="505cb-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="505cb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="505cb-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="505cb-161">These values are not real.</span></span> <span data-ttu-id="505cb-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en Identiifer.</span><span class="sxs-lookup"><span data-stu-id="505cb-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="505cb-163">Neem contact op met [ThirdLight Client ondersteuningsteam](https://www.thirdlight.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="505cb-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="505cb-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="505cb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="505cb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="505cb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="505cb-168">In een ander browservenster, meld u aan tooyour ThirdLight bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="505cb-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="505cb-169">Ga te**configuratie \> Systeembeheer**, en klik vervolgens op **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="505cb-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="505cb-170">![Systeembeheer](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="505cb-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="505cb-171">In de configuratiesectie Hallo SAML2, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="505cb-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="505cb-172">![Eenmalige aanmelding SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="505cb-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="505cb-173">a.</span><span class="sxs-lookup"><span data-stu-id="505cb-173">a.</span></span> <span data-ttu-id="505cb-174">Selecteer **eenmalige aanmelding SAML2 inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="505cb-175">b.</span><span class="sxs-lookup"><span data-stu-id="505cb-175">b.</span></span> <span data-ttu-id="505cb-176">Als **bron voor IdP metagegevens**, selecteer **IdP-metagegevens laden van XML**.</span><span class="sxs-lookup"><span data-stu-id="505cb-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="505cb-177">c.</span><span class="sxs-lookup"><span data-stu-id="505cb-177">c.</span></span> <span data-ttu-id="505cb-178">Open metagegevensbestand Hallo gedownload, Hallo inhoud kopiëren en plak deze in Hallo **IdP metagegevens-XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="505cb-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="505cb-179">d.</span><span class="sxs-lookup"><span data-stu-id="505cb-179">d.</span></span> <span data-ttu-id="505cb-180">Klik op **instellingen opslaan SAML2**.</span><span class="sxs-lookup"><span data-stu-id="505cb-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="505cb-181">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="505cb-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="505cb-182">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="505cb-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="505cb-183">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="505cb-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="505cb-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="505cb-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="505cb-185">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="505cb-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="505cb-187">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="505cb-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="505cb-188">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="505cb-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="505cb-190">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="505cb-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="505cb-192">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="505cb-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="505cb-194">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="505cb-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="505cb-196">a.</span><span class="sxs-lookup"><span data-stu-id="505cb-196">a.</span></span> <span data-ttu-id="505cb-197">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="505cb-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="505cb-198">b.</span><span class="sxs-lookup"><span data-stu-id="505cb-198">b.</span></span> <span data-ttu-id="505cb-199">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="505cb-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="505cb-200">c.</span><span class="sxs-lookup"><span data-stu-id="505cb-200">c.</span></span> <span data-ttu-id="505cb-201">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="505cb-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="505cb-202">d.</span><span class="sxs-lookup"><span data-stu-id="505cb-202">d.</span></span> <span data-ttu-id="505cb-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="505cb-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="505cb-204">Een testgebruiker ThirdLight maken</span><span class="sxs-lookup"><span data-stu-id="505cb-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="505cb-205">Azure AD tooenable gebruikers toolog in tooThirdLight, ze in ThirdLight moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="505cb-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="505cb-206">In geval van ThirdLight Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="505cb-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="505cb-207">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="505cb-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="505cb-208">Meld u bij tooyour **ThirdLight** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="505cb-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="505cb-209">Ga te**gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="505cb-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="505cb-210">Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="505cb-211">Klik op **nieuwe gebruiker toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="505cb-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="505cb-212">Voer **hello Username, naam of beschrijving, E-mail, kiest u een vooraf ingestelde of van nieuwe groepsleden** van een geldige AAD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="505cb-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="505cb-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="505cb-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="505cb-214">U kunt andere Thirdlight gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Thirdlight tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="505cb-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="505cb-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="505cb-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="505cb-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooThirdLight toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="505cb-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="505cb-218">**tooassign Britta Simon tooThirdLight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="505cb-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="505cb-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="505cb-221">Selecteer in de lijst met de toepassingen van Hallo **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="505cb-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="505cb-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="505cb-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="505cb-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="505cb-225">Click **Add** button.</span></span> <span data-ttu-id="505cb-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="505cb-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="505cb-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="505cb-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="505cb-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="505cb-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="505cb-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="505cb-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="505cb-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="505cb-231">Testing single sign-on</span></span>

<span data-ttu-id="505cb-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="505cb-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="505cb-233">Als u op Hallo ThirdLight tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ThirdLight toepassing.</span><span class="sxs-lookup"><span data-stu-id="505cb-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="505cb-234">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="505cb-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="505cb-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="505cb-235">Additional resources</span></span>

* [<span data-ttu-id="505cb-236">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="505cb-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="505cb-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="505cb-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

