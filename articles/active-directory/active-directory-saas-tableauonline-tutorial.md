---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Online | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding van Azure Active Directory en Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="30717-103">Zelfstudie: Azure Active Directory-integratie met Tableau Online</span><span class="sxs-lookup"><span data-stu-id="30717-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="30717-104">In deze zelfstudie leert u hoe toointegrate Tableau Online met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30717-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30717-105">Online Tableau integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="30717-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30717-106">U kunt beheren in Azure AD die Online tooTableau toegang heeft</span><span class="sxs-lookup"><span data-stu-id="30717-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="30717-107">U kunt uw gebruikers tooautomatically get aangemelde tooTableau Online (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="30717-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30717-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="30717-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="30717-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30717-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30717-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="30717-110">Prerequisites</span></span>

<span data-ttu-id="30717-111">Azure AD-integratie met Tableau Online tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="30717-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="30717-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="30717-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30717-113">Een Tableau Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="30717-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30717-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="30717-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30717-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="30717-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30717-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="30717-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30717-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30717-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30717-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="30717-118">Scenario description</span></span>
<span data-ttu-id="30717-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="30717-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30717-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="30717-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30717-121">Het toevoegen van Online Tableau van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="30717-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="30717-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="30717-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="30717-123">Het toevoegen van Online Tableau van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="30717-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="30717-124">tooconfigure hello integratie Tableau online met Azure AD, moet u tooadd Tableau Online uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="30717-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30717-125">**tooadd Tableau Online via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="30717-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30717-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="30717-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30717-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="30717-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30717-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="30717-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="30717-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="30717-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="30717-133">Typ in het zoekvak Hallo **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="30717-133">In hello search box, type **Tableau Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="30717-135">Selecteer in het deelvenster resultaten hello, **Tableau Online**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="30717-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30717-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="30717-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30717-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="30717-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="30717-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tableau Online is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30717-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="30717-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Tableau Online toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="30717-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="30717-141">In Online Tableau, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="30717-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30717-142">tooconfigure en test eenmalige aanmelding Azure AD met Tableau Online, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="30717-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30717-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="30717-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30717-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30717-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30717-145">**[Maken van een Online Tableau testgebruiker](#creating-a-tableau-online-test-user)**  -toohave een equivalent van Britta Simon in Tableau Online die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="30717-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30717-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="30717-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30717-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="30717-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30717-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="30717-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30717-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Tableau Online configureren.</span><span class="sxs-lookup"><span data-stu-id="30717-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="30717-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Online Tableau, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="30717-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="30717-151">In de Azure-portal op Hallo Hallo **Tableau Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="30717-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="30717-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="30717-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="30717-155">Op Hallo **Tableau Online domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="30717-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="30717-157">a.</span><span class="sxs-lookup"><span data-stu-id="30717-157">a.</span></span> <span data-ttu-id="30717-158">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="30717-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="30717-159">b.</span><span class="sxs-lookup"><span data-stu-id="30717-159">b.</span></span> <span data-ttu-id="30717-160">In Hallo **id** textbox type Hallo URL:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="30717-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="30717-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="30717-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="30717-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="30717-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30717-165">In een ander browservenster, aanmelding tooyour Tableau on line toepassing.</span><span class="sxs-lookup"><span data-stu-id="30717-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="30717-166">Ga te**instellingen** en vervolgens **verificatie**.</span><span class="sxs-lookup"><span data-stu-id="30717-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="30717-168">tooenable SAML onder **verificatietypen** sectie.</span><span class="sxs-lookup"><span data-stu-id="30717-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="30717-169">Controleer de Hallo **eenmalige aanmelding met SAML** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="30717-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="30717-171">Schuif omlaag totdat **metagegevensbestand importeren in Tableau Online** sectie.</span><span class="sxs-lookup"><span data-stu-id="30717-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="30717-172">Klik op Bladeren en importeer Hallo-metagegevensbestand die u hebt gedownload van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30717-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="30717-173">Klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="30717-173">Then, click **Apply**.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="30717-175">In Hallo **overeen met asserties** sectie, plaatst u Hallo bijbehorende identiteitsprovider assertion naam voor **e-mailadres**, **voornaam**, en **achternaam** .</span><span class="sxs-lookup"><span data-stu-id="30717-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="30717-176">tooget deze gegevens vanuit Azure AD:</span><span class="sxs-lookup"><span data-stu-id="30717-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="30717-177">a.</span><span class="sxs-lookup"><span data-stu-id="30717-177">a.</span></span> <span data-ttu-id="30717-178">In hello Azure-portal, gaat u op Hallo **Tableau Online** pagina van de integratie van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="30717-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="30717-179">b.</span><span class="sxs-lookup"><span data-stu-id="30717-179">b.</span></span> <span data-ttu-id="30717-180">Selecteer in de sectie kenmerken Hallo Hallo **'weergeven en bewerken van alle andere gebruikerskenmerken '** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="30717-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="30717-182">c.</span><span class="sxs-lookup"><span data-stu-id="30717-182">c.</span></span> <span data-ttu-id="30717-183">Hallo namespace-waarde van deze kenmerken kopiëren: givenname, e-mail- en achternaam met behulp van Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="30717-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="30717-185">d.</span><span class="sxs-lookup"><span data-stu-id="30717-185">d.</span></span> <span data-ttu-id="30717-186">Klik op **user.givenname** waarde</span><span class="sxs-lookup"><span data-stu-id="30717-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="30717-187">e.</span><span class="sxs-lookup"><span data-stu-id="30717-187">e.</span></span> <span data-ttu-id="30717-188">Hallo-waarde in Hallo kopiëren **naamruimte** textbox.</span><span class="sxs-lookup"><span data-stu-id="30717-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="30717-190">f.</span><span class="sxs-lookup"><span data-stu-id="30717-190">f.</span></span> <span data-ttu-id="30717-191">toocopy hello namesapce waarden voor Hallo e-mail- en achternaam volgen Hallo vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="30717-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="30717-192">g.</span><span class="sxs-lookup"><span data-stu-id="30717-192">g.</span></span> <span data-ttu-id="30717-193">Schakel over naar toohello Tableau on line toepassing en stel vervolgens Hallo **Tableau Online kenmerken** sectie als volgt:</span><span class="sxs-lookup"><span data-stu-id="30717-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="30717-194">E-mailadres: **mail** of **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="30717-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="30717-195">Voornaam: **givenname**</span><span class="sxs-lookup"><span data-stu-id="30717-195">First name: **givenname**</span></span>
     * <span data-ttu-id="30717-196">Achternaam: **achternaam**</span><span class="sxs-lookup"><span data-stu-id="30717-196">Last name: **surname**</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="30717-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="30717-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30717-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="30717-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30717-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30717-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30717-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="30717-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="30717-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="30717-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="30717-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="30717-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30717-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="30717-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30717-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="30717-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30717-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="30717-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30717-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="30717-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30717-213">a.</span><span class="sxs-lookup"><span data-stu-id="30717-213">a.</span></span> <span data-ttu-id="30717-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30717-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30717-215">b.</span><span class="sxs-lookup"><span data-stu-id="30717-215">b.</span></span> <span data-ttu-id="30717-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30717-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30717-217">c.</span><span class="sxs-lookup"><span data-stu-id="30717-217">c.</span></span> <span data-ttu-id="30717-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="30717-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="30717-219">d.</span><span class="sxs-lookup"><span data-stu-id="30717-219">d.</span></span> <span data-ttu-id="30717-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="30717-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="30717-221">Maken van een Online Tableau testgebruiker</span><span class="sxs-lookup"><span data-stu-id="30717-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="30717-222">In deze sectie maakt maken u een gebruiker die is aangeroepen terwijl Britta Simon Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="30717-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="30717-223">Op **Tableau Online**, klikt u op **instellingen** en vervolgens **verificatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="30717-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="30717-224">Schuif naar beneden te**gebruikers selecteren** sectie.</span><span class="sxs-lookup"><span data-stu-id="30717-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="30717-225">Klik op **gebruikers toevoegen** en vervolgens **Voer e-mailadressen**.</span><span class="sxs-lookup"><span data-stu-id="30717-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="30717-227">Selecteer **toevoegen van gebruikers voor eenmalige aanmelding (SSO) verificatie**.</span><span class="sxs-lookup"><span data-stu-id="30717-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="30717-228">In Hallo **e-mailadressen opgeven** textbox toevoegenbritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="30717-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="30717-230">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="30717-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30717-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="30717-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="30717-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTableau Online.</span><span class="sxs-lookup"><span data-stu-id="30717-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="30717-234">**tooassign Britta Simon tooTableau Online uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="30717-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="30717-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="30717-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="30717-237">Selecteer in de lijst met de toepassingen van Hallo **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="30717-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="30717-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="30717-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="30717-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="30717-241">Click **Add** button.</span></span> <span data-ttu-id="30717-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="30717-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="30717-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="30717-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30717-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="30717-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30717-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="30717-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30717-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="30717-247">Testing single sign-on</span></span>

<span data-ttu-id="30717-248">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="30717-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="30717-249">Wanneer u Online Tableau Hallo-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Tableau on line toepassing.</span><span class="sxs-lookup"><span data-stu-id="30717-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30717-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="30717-250">Additional resources</span></span>

* [<span data-ttu-id="30717-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30717-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30717-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="30717-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

