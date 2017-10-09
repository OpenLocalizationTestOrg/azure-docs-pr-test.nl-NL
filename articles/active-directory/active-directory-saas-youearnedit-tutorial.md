---
title: 'Zelfstudie: Azure Active Directory-integratie met YouEarnedIt | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en YouEarnedIt.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="557a8-103">Zelfstudie: Azure Active Directory-integratie met YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="557a8-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="557a8-104">In deze zelfstudie leert u hoe toointegrate YouEarnedIt met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="557a8-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="557a8-105">YouEarnedIt integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="557a8-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="557a8-106">U kunt beheren in Azure AD die tooYouEarnedIt toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="557a8-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="557a8-107">U kunt uw gebruikers tooautomatically get aangemelde tooYouEarnedIt (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="557a8-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="557a8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="557a8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="557a8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="557a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="557a8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="557a8-110">Prerequisites</span></span>

<span data-ttu-id="557a8-111">Azure AD-integratie met YouEarnedIt tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="557a8-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="557a8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="557a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="557a8-113">Een YouEarnedIt eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="557a8-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="557a8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="557a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="557a8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="557a8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="557a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="557a8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="557a8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="557a8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="557a8-118">Scenario description</span></span>
<span data-ttu-id="557a8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="557a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="557a8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="557a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="557a8-121">Het toevoegen van YouEarnedIt van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="557a8-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="557a8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="557a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="557a8-123">Het toevoegen van YouEarnedIt van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="557a8-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="557a8-124">tooconfigure hello integratie van YouEarnedIt in Azure AD, moet u tooadd YouEarnedIt uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="557a8-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="557a8-125">**tooadd YouEarnedIt via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="557a8-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="557a8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="557a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="557a8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="557a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="557a8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="557a8-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="557a8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="557a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="557a8-133">Typ in het zoekvak Hallo **YouEarnedt**, selecteer **YouEarnedt** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="557a8-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt in de lijst met resultaten Hallo](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="557a8-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="557a8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="557a8-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met YouEarnedIt op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="557a8-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="557a8-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in YouEarnedIt is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="557a8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="557a8-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in YouEarnedIt toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="557a8-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="557a8-139">Wijs in YouEarnedIt, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="557a8-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="557a8-140">tooconfigure en eenmalige aanmelding Azure AD-test met YouEarnedIt, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="557a8-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="557a8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="557a8-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="557a8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="557a8-143">**[Maak een testgebruiker YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave een equivalent van Britta Simon in YouEarnedIt die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="557a8-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="557a8-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="557a8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="557a8-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="557a8-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="557a8-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="557a8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="557a8-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing YouEarnedIt configureren.</span><span class="sxs-lookup"><span data-stu-id="557a8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="557a8-148">**Azure AD tooconfigure eenmalige aanmelding met YouEarnedIt, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="557a8-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="557a8-149">In de Azure-portal op Hallo Hallo **YouEarnedIt** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="557a8-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="557a8-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="557a8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="557a8-153">Op Hallo **YouEarnedIt domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en YouEarnedIt domein eenmalige aanmelding informatie](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="557a8-155">a.</span><span class="sxs-lookup"><span data-stu-id="557a8-155">a.</span></span> <span data-ttu-id="557a8-156">In Hallo **aanmeldings-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="557a8-157">Omgeving</span><span class="sxs-lookup"><span data-stu-id="557a8-157">Environment</span></span>  | <span data-ttu-id="557a8-158">patroon</span><span class="sxs-lookup"><span data-stu-id="557a8-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="557a8-159">Productie</span><span class="sxs-lookup"><span data-stu-id="557a8-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="557a8-160">Sandbox</span><span class="sxs-lookup"><span data-stu-id="557a8-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="557a8-161">b.</span><span class="sxs-lookup"><span data-stu-id="557a8-161">b.</span></span> <span data-ttu-id="557a8-162">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="557a8-163">Omgeving</span><span class="sxs-lookup"><span data-stu-id="557a8-163">Environment</span></span>  | <span data-ttu-id="557a8-164">patroon</span><span class="sxs-lookup"><span data-stu-id="557a8-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="557a8-165">Productie</span><span class="sxs-lookup"><span data-stu-id="557a8-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="557a8-166">Sandbox</span><span class="sxs-lookup"><span data-stu-id="557a8-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="557a8-167">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="557a8-167">These values are not real.</span></span> <span data-ttu-id="557a8-168">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="557a8-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="557a8-169">Neem contact op met [YouEarnedIt Client ondersteuningsteam](https://youearnedit.freshdesk.com/support/tickets/new) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="557a8-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="557a8-170">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="557a8-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="557a8-172">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="557a8-172">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="557a8-174">Op Hallo **YouEarnedIt configuratie** sectie, klikt u op **configureren YouEarnedIt** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="557a8-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="557a8-175">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="557a8-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![YouEarnedIt configuratie](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="557a8-177">tooconfigure eenmalige aanmelding op **YouEarnedIt** zijde, moet u toosend Hallo gedownload **Certificate(Base64)** en **SAML Single Sign-On Service-URL** te[YouEarnedIt ondersteuningsteam](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="557a8-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="557a8-178">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="557a8-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="557a8-179">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="557a8-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="557a8-180">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="557a8-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="557a8-181">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="557a8-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="557a8-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="557a8-182">Create an Azure AD test user</span></span>

<span data-ttu-id="557a8-183">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="557a8-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="557a8-185">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="557a8-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="557a8-186">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="557a8-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="557a8-188">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="557a8-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="557a8-190">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="557a8-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="557a8-192">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="557a8-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="557a8-194">a.</span><span class="sxs-lookup"><span data-stu-id="557a8-194">a.</span></span> <span data-ttu-id="557a8-195">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="557a8-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="557a8-196">b.</span><span class="sxs-lookup"><span data-stu-id="557a8-196">b.</span></span> <span data-ttu-id="557a8-197">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="557a8-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="557a8-198">c.</span><span class="sxs-lookup"><span data-stu-id="557a8-198">c.</span></span> <span data-ttu-id="557a8-199">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="557a8-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="557a8-200">d.</span><span class="sxs-lookup"><span data-stu-id="557a8-200">d.</span></span> <span data-ttu-id="557a8-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="557a8-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="557a8-202">Een testgebruiker YouEarnedIt maken</span><span class="sxs-lookup"><span data-stu-id="557a8-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="557a8-203">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in YouEarnedIt maken.</span><span class="sxs-lookup"><span data-stu-id="557a8-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="557a8-204">Neem contact op met YouEarnedIt support team tooadd Hallo gebruikers in Hallo YouEarnedIt platform.</span><span class="sxs-lookup"><span data-stu-id="557a8-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="557a8-205">YouEarnedIt verwachten Hallo identiteitsprovider toosupply een EmailAddress of een gebruikersnaam in Hallo NameID kenmerk.</span><span class="sxs-lookup"><span data-stu-id="557a8-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="557a8-206">Verificatie mislukt als een bijbehorende gebruikersnaam of EmailAddress niet in de database Hallo gevonden is of komt niet exact overeen.</span><span class="sxs-lookup"><span data-stu-id="557a8-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="557a8-207">Dit vereist dat de accounts worden geïmporteerd in Hallo YouEarnedIt systeem voordat Hallo SSO-integratie (doorgaans op via de API- of CSV-import).</span><span class="sxs-lookup"><span data-stu-id="557a8-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="557a8-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="557a8-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="557a8-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooYouEarnedIt toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="557a8-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="557a8-211">**tooassign Britta Simon tooYouEarnedIt, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="557a8-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="557a8-212">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="557a8-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="557a8-214">Selecteer in de lijst met de toepassingen van Hallo **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="557a8-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![Hallo YouEarnedIt koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="557a8-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="557a8-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="557a8-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="557a8-218">Click **Add** button.</span></span> <span data-ttu-id="557a8-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="557a8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="557a8-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="557a8-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="557a8-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="557a8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="557a8-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="557a8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="557a8-224">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="557a8-224">Test single sign-on</span></span>

<span data-ttu-id="557a8-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="557a8-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="557a8-226">Als u op Hallo YouEarnedIt tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour YouEarnedIt toepassing.</span><span class="sxs-lookup"><span data-stu-id="557a8-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="557a8-227">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="557a8-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="557a8-228">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="557a8-228">Additional resources</span></span>

* [<span data-ttu-id="557a8-229">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="557a8-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="557a8-230">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="557a8-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

