---
title: 'Zelfstudie: Azure Active Directory-integratie met Rally Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="92331-103">Zelfstudie: Azure Active Directory-integratie met Rally Software</span><span class="sxs-lookup"><span data-stu-id="92331-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="92331-104">In deze zelfstudie leert u hoe toointegrate Rally Software met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92331-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92331-105">Software Rally integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="92331-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92331-106">U kunt beheren in Azure AD die toegang tooRally Software heeft.</span><span class="sxs-lookup"><span data-stu-id="92331-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="92331-107">U kunt uw gebruikers tooautomatically get aangemelde tooRally Software (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="92331-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="92331-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="92331-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="92331-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92331-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92331-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92331-110">Prerequisites</span></span>

<span data-ttu-id="92331-111">Azure AD-integratie met Software Rally tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="92331-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="92331-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="92331-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92331-113">Een Software Rally eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="92331-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92331-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="92331-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92331-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="92331-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92331-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="92331-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92331-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92331-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92331-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="92331-118">Scenario description</span></span>
<span data-ttu-id="92331-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="92331-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92331-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="92331-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92331-121">Het toevoegen van Software Rally van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="92331-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="92331-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92331-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="92331-123">Het toevoegen van Software Rally van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="92331-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="92331-124">tooconfigure hello integratie van Software Rally in Azure AD, moet u tooadd Rally Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="92331-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92331-125">**tooadd Rally Software uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92331-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92331-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="92331-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="92331-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92331-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92331-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92331-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="92331-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="92331-133">Typ in het zoekvak Hallo **Rally Software**, selecteer **Rally Software** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="92331-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Software in de lijst met resultaten Hallo Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="92331-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="92331-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="92331-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Rally Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="92331-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92331-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Software Rally is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92331-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="92331-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in Software Rally toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="92331-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="92331-139">In Software Rally Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="92331-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="92331-140">tooconfigure en test eenmalige aanmelding Azure AD met Rally Software, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92331-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92331-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="92331-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92331-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92331-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92331-143">**[Maak een testgebruiker Rally Software](#create-a-rally-software-test-user)**  -toohave een equivalent van Britta Simon in Rally Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92331-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="92331-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="92331-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92331-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="92331-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="92331-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="92331-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="92331-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Rally configureren.</span><span class="sxs-lookup"><span data-stu-id="92331-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="92331-148">**Voer tooconfigure Azure AD eenmalige aanmelding met Rally Software Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92331-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="92331-149">In de Azure-portal op Hallo Hallo **Rally Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="92331-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="92331-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="92331-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="92331-153">Op Hallo **Rally Software domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92331-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Software-domein en de URL's eenmalige aanmelding informatie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="92331-155">a.</span><span class="sxs-lookup"><span data-stu-id="92331-155">a.</span></span> <span data-ttu-id="92331-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="92331-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="92331-157">b.</span><span class="sxs-lookup"><span data-stu-id="92331-157">b.</span></span> <span data-ttu-id="92331-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="92331-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92331-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="92331-159">These values are not real.</span></span> <span data-ttu-id="92331-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="92331-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92331-161">Neem contact op met [Rally Software Client ondersteuningsteam](https://help.rallydev.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="92331-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="92331-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="92331-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="92331-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="92331-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92331-166">Op Hallo **softwareconfiguratie Rally** sectie, klikt u op **Rally Software configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="92331-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="92331-167">Kopiëren Hallo **Sign-Out-URL en de entiteit-ID SAML** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="92331-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![De softwareconfiguratie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="92331-169">Meld u bij tooyour **Rally Software** tenant.</span><span class="sxs-lookup"><span data-stu-id="92331-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="92331-170">Klik in de werkbalk bovenaan Hallo Hallo op **Setup**, en selecteer vervolgens **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="92331-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="92331-171">![Abonnement](./media/active-directory-saas-rally-software-tutorial/ic769531.png "abonnement")</span><span class="sxs-lookup"><span data-stu-id="92331-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="92331-172">Klik op Hallo **actie** knop.</span><span class="sxs-lookup"><span data-stu-id="92331-172">Click hello **Action** button.</span></span> <span data-ttu-id="92331-173">Selecteer **abonnement bewerken** op Hallo rechtsboven Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="92331-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="92331-174">Op Hallo **abonnement** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **opslaan en sluiten**:</span><span class="sxs-lookup"><span data-stu-id="92331-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="92331-175">![Verificatie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="92331-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="92331-176">a.</span><span class="sxs-lookup"><span data-stu-id="92331-176">a.</span></span> <span data-ttu-id="92331-177">Selecteer **Rally of eenmalige aanmelding verificatie** uit de vervolgkeuzelijst verificatie.</span><span class="sxs-lookup"><span data-stu-id="92331-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="92331-178">b.</span><span class="sxs-lookup"><span data-stu-id="92331-178">b.</span></span> <span data-ttu-id="92331-179">In Hallo **identiteit provider URL** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92331-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="92331-180">c.</span><span class="sxs-lookup"><span data-stu-id="92331-180">c.</span></span> <span data-ttu-id="92331-181">In Hallo **eenmalige aanmelding, afmelding** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92331-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="92331-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="92331-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="92331-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="92331-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="92331-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92331-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="92331-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="92331-185">Create an Azure AD test user</span></span>

<span data-ttu-id="92331-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="92331-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="92331-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92331-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92331-189">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="92331-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="92331-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="92331-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="92331-193">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="92331-195">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92331-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="92331-197">a.</span><span class="sxs-lookup"><span data-stu-id="92331-197">a.</span></span> <span data-ttu-id="92331-198">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92331-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92331-199">b.</span><span class="sxs-lookup"><span data-stu-id="92331-199">b.</span></span> <span data-ttu-id="92331-200">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="92331-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="92331-201">c.</span><span class="sxs-lookup"><span data-stu-id="92331-201">c.</span></span> <span data-ttu-id="92331-202">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="92331-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="92331-203">d.</span><span class="sxs-lookup"><span data-stu-id="92331-203">d.</span></span> <span data-ttu-id="92331-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="92331-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="92331-205">Een testgebruiker Rally Software maken</span><span class="sxs-lookup"><span data-stu-id="92331-205">Create a Rally Software test user</span></span>

<span data-ttu-id="92331-206">Voor Azure AD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello Rally softwaretoepassing met behulp van de namen van de Azure Active Directory-gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="92331-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="92331-207">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92331-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="92331-208">Meld u bij tooyour Rally Software tenant.</span><span class="sxs-lookup"><span data-stu-id="92331-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="92331-209">Ga te**Setup \> gebruikers**, en klik vervolgens op **+ nieuw toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="92331-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="92331-210">![Gebruikers](./media/active-directory-saas-rally-software-tutorial/ic781039.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="92331-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="92331-211">Hallo typenaam in een tekstvak voor de nieuwe gebruiker Hallo en klik vervolgens op **toevoegen met Details**.</span><span class="sxs-lookup"><span data-stu-id="92331-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="92331-212">In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="92331-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="92331-213">![Gebruiker maken](./media/active-directory-saas-rally-software-tutorial/ic781040.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="92331-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="92331-214">a.</span><span class="sxs-lookup"><span data-stu-id="92331-214">a.</span></span> <span data-ttu-id="92331-215">In Hallo **gebruikersnaam** textbox Hallo-typenaam van de gebruiker zoals **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="92331-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="92331-216">b.</span><span class="sxs-lookup"><span data-stu-id="92331-216">b.</span></span> <span data-ttu-id="92331-217">In **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="92331-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="92331-218">c.</span><span class="sxs-lookup"><span data-stu-id="92331-218">c.</span></span> <span data-ttu-id="92331-219">In **voornaam** tekst hello eerste naam van gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="92331-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="92331-220">d.</span><span class="sxs-lookup"><span data-stu-id="92331-220">d.</span></span> <span data-ttu-id="92331-221">In **achternaam** tekst hello laatste naam van gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="92331-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="92331-222">e.</span><span class="sxs-lookup"><span data-stu-id="92331-222">e.</span></span> <span data-ttu-id="92331-223">Klik op **opslaan en sluiten**.</span><span class="sxs-lookup"><span data-stu-id="92331-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="92331-224">U kunt andere Software Rally gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Software Rally tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="92331-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="92331-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="92331-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="92331-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooRally Software.</span><span class="sxs-lookup"><span data-stu-id="92331-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="92331-228">**tooassign Britta Simon tooRally Software, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="92331-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="92331-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92331-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="92331-231">Selecteer in de lijst met de toepassingen van Hallo **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="92331-231">In hello applications list, select **Rally Software**.</span></span>

    ![Hallo Rally Software koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="92331-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="92331-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="92331-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="92331-235">Click **Add** button.</span></span> <span data-ttu-id="92331-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="92331-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="92331-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92331-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92331-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="92331-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92331-241">Test single sign-on</span></span>

<span data-ttu-id="92331-242">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="92331-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92331-243">Als u op Hallo Rally Software tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Rally softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="92331-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92331-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="92331-244">Additional resources</span></span>

* [<span data-ttu-id="92331-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92331-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92331-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92331-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

