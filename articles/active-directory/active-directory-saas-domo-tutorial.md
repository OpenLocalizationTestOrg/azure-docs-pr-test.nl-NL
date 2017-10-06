---
title: 'Zelfstudie: Azure Active Directory-integratie met Domo | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Domo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="f0b05-103">Zelfstudie: Azure Active Directory-integratie met Domo</span><span class="sxs-lookup"><span data-stu-id="f0b05-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="f0b05-104">In deze zelfstudie leert u hoe toointegrate Domo met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0b05-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0b05-105">Domo integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f0b05-106">U kunt beheren in Azure AD die tooDomo toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f0b05-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="f0b05-107">U kunt uw gebruikers tooautomatically get aangemelde tooDomo (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f0b05-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0b05-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f0b05-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f0b05-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0b05-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0b05-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0b05-110">Prerequisites</span></span>

<span data-ttu-id="f0b05-111">Azure AD-integratie met Domo tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f0b05-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="f0b05-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f0b05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0b05-113">Een Domo eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f0b05-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0b05-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0b05-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0b05-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0b05-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f0b05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0b05-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0b05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0b05-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f0b05-118">Scenario description</span></span>
<span data-ttu-id="f0b05-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0b05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0b05-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0b05-121">Het toevoegen van Domo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f0b05-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="f0b05-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0b05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="f0b05-123">Het toevoegen van Domo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f0b05-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="f0b05-124">tooconfigure hello integratie van Domo in Azure AD, moet u tooadd Domo uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f0b05-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f0b05-125">**tooadd Domo via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0b05-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0b05-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0b05-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0b05-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f0b05-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f0b05-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f0b05-133">Typ in het zoekvak Hallo **Domo**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-133">In hello search box, type **Domo**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="f0b05-135">Selecteer in het deelvenster resultaten hello, **Domo**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0b05-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0b05-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0b05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0b05-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Domo op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f0b05-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f0b05-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Domo is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0b05-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="f0b05-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Domo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f0b05-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="f0b05-141">Wijs in Domo, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f0b05-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f0b05-142">tooconfigure en eenmalige aanmelding Azure AD-test met Domo, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f0b05-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f0b05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f0b05-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0b05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0b05-145">**[Maken van een testgebruiker Domo](#creating-a-domo-test-user)**  -toohave een equivalent van Britta Simon in Domo die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f0b05-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0b05-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f0b05-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0b05-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f0b05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0b05-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f0b05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0b05-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Domo configureren.</span><span class="sxs-lookup"><span data-stu-id="f0b05-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="f0b05-150">**Azure AD tooconfigure eenmalige aanmelding met Domo, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0b05-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0b05-151">In de Azure-portal op Hallo Hallo **Domo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f0b05-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f0b05-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="f0b05-155">Op Hallo **Domo domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="f0b05-157">a.</span><span class="sxs-lookup"><span data-stu-id="f0b05-157">a.</span></span> <span data-ttu-id="f0b05-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="f0b05-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="f0b05-159">b.</span><span class="sxs-lookup"><span data-stu-id="f0b05-159">b.</span></span> <span data-ttu-id="f0b05-160">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="f0b05-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f0b05-161">These values are not real.</span></span> <span data-ttu-id="f0b05-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="f0b05-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f0b05-163">Neem contact op met [Domo Client ondersteuningsteam](mailto:support@domo.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f0b05-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="f0b05-164">Hallo SAML asserties verwacht Domo toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="f0b05-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f0b05-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="f0b05-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="f0b05-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="f0b05-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f0b05-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="f0b05-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="f0b05-169">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="f0b05-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0b05-170">Attribute Name</span></span> | <span data-ttu-id="f0b05-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0b05-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f0b05-172">naam</span><span class="sxs-lookup"><span data-stu-id="f0b05-172">name</span></span> | <span data-ttu-id="f0b05-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="f0b05-173">user.displayname</span></span> |
    | <span data-ttu-id="f0b05-174">E-mail</span><span class="sxs-lookup"><span data-stu-id="f0b05-174">email</span></span> | <span data-ttu-id="f0b05-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="f0b05-175">user.mail</span></span> |
    
    <span data-ttu-id="f0b05-176">a.</span><span class="sxs-lookup"><span data-stu-id="f0b05-176">a.</span></span> <span data-ttu-id="f0b05-177">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f0b05-180">b.</span><span class="sxs-lookup"><span data-stu-id="f0b05-180">b.</span></span> <span data-ttu-id="f0b05-181">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0b05-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f0b05-182">c.</span><span class="sxs-lookup"><span data-stu-id="f0b05-182">c.</span></span> <span data-ttu-id="f0b05-183">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0b05-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f0b05-184">d.</span><span class="sxs-lookup"><span data-stu-id="f0b05-184">d.</span></span> <span data-ttu-id="f0b05-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="f0b05-186">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f0b05-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="f0b05-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f0b05-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="f0b05-190">Op Hallo **Domo configuratie** sectie, klikt u op **configureren Domo** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f0b05-191">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f0b05-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="f0b05-193">tooconfigure eenmalige aanmelding op **Domo** zijde, moet u toosend Hallo gedownload **certificaat**, **SAML entiteit-ID**, Hallo **SAML Single Sign-On-Service URL** en Hallo **Sign-Out URL** te[Domo ondersteuningsteam](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="f0b05-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="f0b05-194">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f0b05-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f0b05-195">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f0b05-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f0b05-196">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f0b05-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f0b05-197">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0b05-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0b05-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f0b05-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0b05-199">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f0b05-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f0b05-201">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0b05-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0b05-202">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0b05-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0b05-204">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0b05-206">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f0b05-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0b05-208">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b05-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0b05-210">a.</span><span class="sxs-lookup"><span data-stu-id="f0b05-210">a.</span></span> <span data-ttu-id="f0b05-211">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0b05-212">b.</span><span class="sxs-lookup"><span data-stu-id="f0b05-212">b.</span></span> <span data-ttu-id="f0b05-213">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0b05-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0b05-214">c.</span><span class="sxs-lookup"><span data-stu-id="f0b05-214">c.</span></span> <span data-ttu-id="f0b05-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f0b05-216">d.</span><span class="sxs-lookup"><span data-stu-id="f0b05-216">d.</span></span> <span data-ttu-id="f0b05-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="f0b05-218">Een testgebruiker Domo maken</span><span class="sxs-lookup"><span data-stu-id="f0b05-218">Creating a Domo test user</span></span>

<span data-ttu-id="f0b05-219">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Domo van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f0b05-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="f0b05-220">Domo ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f0b05-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f0b05-221">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f0b05-221">There is no action item for you in this section.</span></span> <span data-ttu-id="f0b05-222">Een nieuwe gebruiker wordt tijdens een poging tooaccess Domo gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f0b05-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f0b05-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0b05-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f0b05-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDomo toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f0b05-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f0b05-226">**tooassign Britta Simon tooDomo, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f0b05-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0b05-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f0b05-229">Selecteer in de lijst met de toepassingen van Hallo **Domo**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-229">In hello applications list, select **Domo**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="f0b05-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f0b05-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f0b05-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f0b05-233">Click **Add** button.</span></span> <span data-ttu-id="f0b05-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f0b05-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0b05-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f0b05-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0b05-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0b05-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0b05-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0b05-239">Testing single sign-on</span></span>

<span data-ttu-id="f0b05-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f0b05-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="f0b05-241">Als u op Hallo Domo tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Domo toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0b05-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="f0b05-242">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0b05-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0b05-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f0b05-243">Additional resources</span></span>

* [<span data-ttu-id="f0b05-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0b05-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0b05-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0b05-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

