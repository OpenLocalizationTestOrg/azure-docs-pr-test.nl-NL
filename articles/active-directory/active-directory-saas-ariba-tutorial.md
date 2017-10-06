---
title: 'Zelfstudie: Azure Active Directory-integratie met Ariba | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Ariba.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="a0d85-103">Zelfstudie: Azure Active Directory-integratie met Ariba</span><span class="sxs-lookup"><span data-stu-id="a0d85-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="a0d85-104">In deze zelfstudie leert u hoe toointegrate Ariba met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0d85-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0d85-105">Ariba integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0d85-106">U kunt beheren in Azure AD die tooAriba toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a0d85-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="a0d85-107">U kunt uw gebruikers tooautomatically get aangemelde tooAriba (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a0d85-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0d85-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a0d85-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0d85-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0d85-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0d85-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a0d85-110">Prerequisites</span></span>

<span data-ttu-id="a0d85-111">Azure AD-integratie met Ariba tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a0d85-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="a0d85-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a0d85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0d85-113">Een Ariba eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a0d85-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0d85-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0d85-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0d85-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0d85-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a0d85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0d85-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0d85-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0d85-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a0d85-118">Scenario description</span></span>
<span data-ttu-id="a0d85-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a0d85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0d85-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0d85-121">Het toevoegen van Ariba van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a0d85-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="a0d85-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0d85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="a0d85-123">Het toevoegen van Ariba van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a0d85-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="a0d85-124">tooconfigure hello integratie van Ariba in Azure AD, moet u tooadd Ariba uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a0d85-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0d85-125">**tooadd Ariba via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a0d85-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0d85-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0d85-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0d85-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0d85-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a0d85-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0d85-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a0d85-133">Typ in het zoekvak Hallo **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-133">In hello search box, type **Ariba**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="a0d85-135">Selecteer in het deelvenster resultaten hello, **Ariba**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0d85-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0d85-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0d85-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0d85-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Ariba op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a0d85-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0d85-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Ariba is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0d85-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="a0d85-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Ariba toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a0d85-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="a0d85-141">Wijs in Ariba, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a0d85-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a0d85-142">tooconfigure en eenmalige aanmelding Azure AD-test met Ariba, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0d85-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a0d85-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0d85-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0d85-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0d85-145">**[Maken van een testgebruiker Ariba](#creating-an-ariba-test-user)**  -toohave een equivalent van Britta Simon in Ariba die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a0d85-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0d85-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a0d85-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0d85-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a0d85-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0d85-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a0d85-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0d85-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Ariba configureren.</span><span class="sxs-lookup"><span data-stu-id="a0d85-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="a0d85-150">**Azure AD tooconfigure eenmalige aanmelding met Ariba, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a0d85-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0d85-151">In de Azure-portal op Hallo Hallo **Ariba** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a0d85-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a0d85-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="a0d85-155">Op Hallo **Ariba domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="a0d85-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0d85-157">a.</span></span> <span data-ttu-id="a0d85-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen: `https://<subdomain>.sourcing.ariba.com` of`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="a0d85-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="a0d85-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0d85-159">b.</span></span> <span data-ttu-id="a0d85-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="a0d85-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0d85-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a0d85-161">These values are not real.</span></span> <span data-ttu-id="a0d85-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a0d85-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0d85-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="a0d85-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="a0d85-164">Neem contact op met het ondersteuningsteam Ariba Client op **1-866-218-2155** tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a0d85-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="a0d85-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a0d85-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="a0d85-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a0d85-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0d85-169">tooget SSO is geconfigureerd voor uw toepassing, Ariba ondersteuningsteam niet aanroepen voor **1-866-218-2155** en ze helpt u verder gaat op hoe ze Hallo tooprovide gedownload **certificaat (Base64)** bestand.</span><span class="sxs-lookup"><span data-stu-id="a0d85-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="a0d85-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a0d85-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a0d85-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a0d85-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a0d85-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0d85-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0d85-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a0d85-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0d85-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a0d85-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a0d85-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a0d85-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0d85-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a0d85-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0d85-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0d85-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a0d85-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0d85-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a0d85-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0d85-185">a.</span><span class="sxs-lookup"><span data-stu-id="a0d85-185">a.</span></span> <span data-ttu-id="a0d85-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0d85-187">b.</span><span class="sxs-lookup"><span data-stu-id="a0d85-187">b.</span></span> <span data-ttu-id="a0d85-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0d85-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0d85-189">c.</span><span class="sxs-lookup"><span data-stu-id="a0d85-189">c.</span></span> <span data-ttu-id="a0d85-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0d85-191">d.</span><span class="sxs-lookup"><span data-stu-id="a0d85-191">d.</span></span> <span data-ttu-id="a0d85-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="a0d85-193">Een testgebruiker Ariba maken</span><span class="sxs-lookup"><span data-stu-id="a0d85-193">Creating an Ariba test user</span></span>

<span data-ttu-id="a0d85-194">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Ariba van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a0d85-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="a0d85-195">Werken met het ondersteuningsteam Ariba op **1-866-218-2155** tooadd Hallo gebruikers in Hallo Ariba systeem.</span><span class="sxs-lookup"><span data-stu-id="a0d85-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="a0d85-196">Als u handmatig een gebruiker toocreate nodig, moet u toocontact Hallo Ariba ondersteuningsteam op **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a0d85-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0d85-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a0d85-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAriba toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a0d85-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a0d85-200">**tooassign Britta Simon tooAriba, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a0d85-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0d85-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a0d85-203">Selecteer in de lijst met de toepassingen van Hallo **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-203">In hello applications list, select **Ariba**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="a0d85-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a0d85-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a0d85-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a0d85-207">Click **Add** button.</span></span> <span data-ttu-id="a0d85-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0d85-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a0d85-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0d85-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0d85-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0d85-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0d85-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a0d85-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0d85-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a0d85-213">Testing single sign-on</span></span>
<span data-ttu-id="a0d85-214">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a0d85-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a0d85-215">Als u op Hallo Ariba tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Ariba toepassing.</span><span class="sxs-lookup"><span data-stu-id="a0d85-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a0d85-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a0d85-216">Additional resources</span></span>

* [<span data-ttu-id="a0d85-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0d85-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0d85-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0d85-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

