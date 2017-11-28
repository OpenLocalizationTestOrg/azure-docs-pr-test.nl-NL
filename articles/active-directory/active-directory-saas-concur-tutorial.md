---
title: 'Zelfstudie: Azure Active Directory-integratie met Concur | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="2d3d4-103">Zelfstudie: Azure Active Directory-integratie met Concur</span><span class="sxs-lookup"><span data-stu-id="2d3d4-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="2d3d4-104">In deze zelfstudie leert u hoe toointegrate instemming met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d3d4-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d3d4-105">Concur integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d3d4-106">U kunt beheren in Azure AD die tooConcur toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2d3d4-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="2d3d4-107">U kunt uw gebruikers tooautomatically get aangemelde tooConcur (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2d3d4-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d3d4-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2d3d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d3d4-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d3d4-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d3d4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2d3d4-110">Prerequisites</span></span>

<span data-ttu-id="2d3d4-111">Azure AD-integratie met Concur tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="2d3d4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2d3d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d3d4-113">Een Concur eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2d3d4-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d3d4-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d3d4-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d3d4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d3d4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d3d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d3d4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2d3d4-118">Scenario description</span></span>
<span data-ttu-id="2d3d4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d3d4-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d3d4-121">Het toevoegen van Concur van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2d3d4-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="2d3d4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d3d4-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="2d3d4-123">Hallo-configuratie van uw abonnement Concur voor federatieve eenmalige aanmelding via SAML is een afzonderlijke taak, die u moet contact opnemen met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="2d3d4-124">Het toevoegen van Concur van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2d3d4-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="2d3d4-125">tooconfigure hello integratie van Concur in Azure AD, moet u tooadd Concur uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d3d4-126">**tooadd Concur via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d3d4-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d3d4-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d3d4-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d3d4-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2d3d4-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2d3d4-134">Typ in het zoekvak Hallo **Concur**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-134">In hello search box, type **Concur**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="2d3d4-136">Selecteer in het deelvenster resultaten hello, **Concur**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d3d4-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d3d4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d3d4-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Concur op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2d3d4-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d3d4-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Concur is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="2d3d4-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Concur toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="2d3d4-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Concur.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="2d3d4-143">tooconfigure en eenmalige aanmelding Azure AD-test met Concur, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d3d4-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d3d4-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d3d4-146">**[Maken van een testgebruiker Concur](#creating-a-concur-test-user)**  -toohave een equivalent van Britta Simon in Concur die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d3d4-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d3d4-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d3d4-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2d3d4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d3d4-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Concur configureren.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="2d3d4-151">**Azure AD tooconfigure eenmalige aanmelding met Concur, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d3d4-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d3d4-152">In de Azure-portal op Hallo Hallo **Concur** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2d3d4-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="2d3d4-156">Op Hallo **instemming domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="2d3d4-158">a.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-158">a.</span></span> <span data-ttu-id="2d3d4-159">In Hallo **aanmelden URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="2d3d4-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="2d3d4-160">b.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-160">b.</span></span> <span data-ttu-id="2d3d4-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="2d3d4-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d3d4-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-162">These values are not hello real.</span></span> <span data-ttu-id="2d3d4-163">Deze waarden Hello werkelijke Meld u aan bij de URL en de id-update.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="2d3d4-164">Neem contact op met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="2d3d4-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="2d3d4-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-167">Click **Save** button.</span></span>

    <span data-ttu-id="2d3d4-168">![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="2d3d4-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="2d3d4-169">tooconfigure eenmalige aanmelding op **Concur** zijde, moet u toosend Hallo gedownload **Metadata XML** tooConcur ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="2d3d4-170">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="2d3d4-171">Hallo-configuratie van uw abonnement Concur voor federatieve eenmalige aanmelding via SAML is een afzonderlijke taak, die u moet contact opnemen met [Client instemming ondersteuningsteam](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="2d3d4-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d3d4-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d3d4-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d3d4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d3d4-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2d3d4-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d3d4-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2d3d4-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d3d4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d3d4-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d3d4-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d3d4-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d3d4-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3d4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d3d4-187">a.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-187">a.</span></span> <span data-ttu-id="2d3d4-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d3d4-189">b.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-189">b.</span></span> <span data-ttu-id="2d3d4-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d3d4-191">c.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-191">c.</span></span> <span data-ttu-id="2d3d4-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d3d4-193">d.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-193">d.</span></span> <span data-ttu-id="2d3d4-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="2d3d4-195">Een testgebruiker Concur maken</span><span class="sxs-lookup"><span data-stu-id="2d3d4-195">Creating a Concur test user</span></span>

<span data-ttu-id="2d3d4-196">Toepassing ondersteunt Hallo Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d3d4-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d3d4-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d3d4-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooConcur toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2d3d4-200">**tooassign Britta Simon tooConcur, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2d3d4-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d3d4-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2d3d4-203">Selecteer in de lijst met de toepassingen van Hallo **Concur**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-203">In hello applications list, select **Concur**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="2d3d4-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2d3d4-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-207">Click **Add** button.</span></span> <span data-ttu-id="2d3d4-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2d3d4-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d3d4-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d3d4-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d3d4-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2d3d4-213">Testing single sign-on</span></span>

<span data-ttu-id="2d3d4-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d3d4-215">Als u op Hallo Concur tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Concur toepassing.</span><span class="sxs-lookup"><span data-stu-id="2d3d4-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="2d3d4-216">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d3d4-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2d3d4-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2d3d4-217">Additional resources</span></span>

* [<span data-ttu-id="2d3d4-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d3d4-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d3d4-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d3d4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2d3d4-220">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="2d3d4-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

