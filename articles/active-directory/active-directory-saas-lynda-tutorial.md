---
title: 'Zelfstudie: Azure Active Directory-integratie met Lynda.com | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="8d588-103">Zelfstudie: Azure Active Directory-integratie met Lynda.com</span><span class="sxs-lookup"><span data-stu-id="8d588-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="8d588-104">In deze zelfstudie leert u hoe toointegrate Lynda.com met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d588-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d588-105">Lynda.com integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8d588-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d588-106">U kunt beheren in Azure AD die tooLynda.com toegang heeft</span><span class="sxs-lookup"><span data-stu-id="8d588-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="8d588-107">U kunt uw gebruikers tooautomatically get aangemelde tooLynda.com (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8d588-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d588-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8d588-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d588-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d588-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d588-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d588-110">Prerequisites</span></span>

<span data-ttu-id="8d588-111">Azure AD-integratie met Lynda.com tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8d588-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="8d588-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8d588-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d588-113">Een Lynda.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8d588-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d588-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8d588-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d588-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8d588-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d588-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8d588-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d588-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d588-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d588-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8d588-118">Scenario description</span></span>
<span data-ttu-id="8d588-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8d588-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d588-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8d588-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d588-121">Het toevoegen van Lynda.com van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8d588-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="8d588-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8d588-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="8d588-123">Het toevoegen van Lynda.com van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8d588-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="8d588-124">tooconfigure hello integratie van Lynda.com in Azure AD, moet u tooadd Lynda.com uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8d588-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d588-125">**tooadd Lynda.com via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8d588-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d588-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d588-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d588-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8d588-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d588-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8d588-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8d588-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d588-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8d588-133">Typ in het zoekvak Hallo **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="8d588-133">In hello search box, type **Lynda.com**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="8d588-135">Selecteer in het deelvenster resultaten hello, **Lynda.com**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8d588-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d588-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8d588-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d588-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Lynda.com op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8d588-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d588-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Lynda.com is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d588-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="8d588-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Lynda.com toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8d588-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="8d588-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="8d588-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="8d588-142">tooconfigure en eenmalige aanmelding Azure AD-test met Lynda.com, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d588-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d588-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8d588-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d588-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d588-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d588-145">**[Maken van een testgebruiker Lynda.com](#creating-a-lyndacom-test-user)**  -toohave een equivalent van Britta Simon in Lynda.com die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8d588-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d588-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8d588-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d588-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8d588-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d588-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8d588-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d588-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Lynda.com configureren.</span><span class="sxs-lookup"><span data-stu-id="8d588-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="8d588-150">**Azure AD tooconfigure eenmalige aanmelding met Lynda.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8d588-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d588-151">In de Azure-portal op Hallo Hallo **Lynda.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8d588-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8d588-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8d588-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="8d588-155">Op Hallo **Lynda.com domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d588-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="8d588-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="8d588-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d588-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="8d588-158">This value is not real.</span></span> <span data-ttu-id="8d588-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="8d588-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8d588-160">Neem contact op met [Lynda.com Client ondersteuningsteam](https://www.linkedin.com/help/lynda/ask) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8d588-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="8d588-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8d588-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="8d588-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8d588-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d588-165">tooconfigure eenmalige aanmelding op **Lynda.com** zijde, moet u toosend Hallo gedownload **Metadata XML** [Lynda.com ondersteuning](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="8d588-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d588-166">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8d588-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d588-167">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8d588-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8d588-169">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8d588-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d588-170">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8d588-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d588-172">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8d588-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d588-174">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8d588-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d588-176">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d588-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d588-178">a.</span><span class="sxs-lookup"><span data-stu-id="8d588-178">a.</span></span> <span data-ttu-id="8d588-179">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d588-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d588-180">b.</span><span class="sxs-lookup"><span data-stu-id="8d588-180">b.</span></span> <span data-ttu-id="8d588-181">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d588-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d588-182">c.</span><span class="sxs-lookup"><span data-stu-id="8d588-182">c.</span></span> <span data-ttu-id="8d588-183">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8d588-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d588-184">d.</span><span class="sxs-lookup"><span data-stu-id="8d588-184">d.</span></span> <span data-ttu-id="8d588-185">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8d588-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="8d588-186">Een testgebruiker Lynda.com maken</span><span class="sxs-lookup"><span data-stu-id="8d588-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="8d588-187">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="8d588-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="8d588-188">Wanneer een toegewezen gebruiker toolog in tooLynda.com met behulp van het toegangsvenster hello probeert, controleert Lynda.com of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="8d588-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="8d588-189">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="8d588-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="8d588-190">U kunt andere Lynda.com gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Lynda.com tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="8d588-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d588-191">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d588-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d588-192">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLynda.com toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8d588-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8d588-194">**tooassign Britta Simon tooLynda.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8d588-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d588-195">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8d588-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8d588-197">Selecteer in de lijst met de toepassingen van Hallo **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="8d588-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="8d588-199">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8d588-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8d588-201">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8d588-201">Click **Add** button.</span></span> <span data-ttu-id="8d588-202">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d588-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8d588-204">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8d588-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d588-205">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d588-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d588-206">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8d588-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d588-207">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8d588-207">Testing single sign-on</span></span>

<span data-ttu-id="8d588-208">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="8d588-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="8d588-209">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d588-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8d588-210">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d588-210">Additional resources</span></span>

* [<span data-ttu-id="8d588-211">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d588-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d588-212">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d588-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

