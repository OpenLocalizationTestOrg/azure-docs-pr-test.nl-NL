---
title: 'Zelfstudie: Azure Active Directory-integratie met Zoho | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="7e175-103">Zelfstudie: Azure Active Directory-integratie met Zoho</span><span class="sxs-lookup"><span data-stu-id="7e175-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="7e175-104">In deze zelfstudie leert u hoe toointegrate Zoho met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e175-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e175-105">Zoho integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7e175-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e175-106">U kunt beheren in Azure AD die tooZoho toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="7e175-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="7e175-107">U kunt uw gebruikers tooautomatically get aangemelde tooZoho (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7e175-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7e175-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="7e175-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7e175-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e175-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e175-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e175-110">Prerequisites</span></span>

<span data-ttu-id="7e175-111">Azure AD-integratie met Zoho tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7e175-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="7e175-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7e175-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e175-113">Een Zoho eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7e175-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e175-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e175-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e175-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e175-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7e175-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e175-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e175-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e175-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7e175-118">Scenario description</span></span>
<span data-ttu-id="7e175-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e175-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e175-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7e175-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e175-121">Het toevoegen van Zoho van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7e175-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="7e175-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e175-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="7e175-123">Het toevoegen van Zoho van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7e175-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="7e175-124">tooconfigure hello integratie van Zoho in Azure AD, moet u tooadd Zoho uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7e175-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e175-125">**tooadd Zoho via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e175-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e175-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7e175-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="7e175-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e175-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e175-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e175-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="7e175-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e175-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="7e175-133">Typ in het zoekvak Hallo **Zoho**, selecteer **Zoho** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e175-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho in de lijst met resultaten Hallo](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7e175-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e175-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7e175-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zoho op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7e175-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e175-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zoho is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e175-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="7e175-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Zoho toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7e175-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="7e175-139">Wijs in Zoho, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7e175-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e175-140">tooconfigure en eenmalige aanmelding Azure AD-test met Zoho, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e175-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7e175-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e175-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e175-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e175-143">**[Maak een testgebruiker Zoho](#create-a-zoho-test-user)**  -toohave een equivalent van Britta Simon in Zoho die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e175-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e175-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7e175-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e175-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7e175-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7e175-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7e175-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7e175-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Zoho configureren.</span><span class="sxs-lookup"><span data-stu-id="7e175-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="7e175-148">**Azure AD tooconfigure eenmalige aanmelding met Zoho, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e175-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e175-149">In de Azure-portal op Hallo Hallo **Zoho** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7e175-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7e175-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7e175-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="7e175-153">Op Hallo **Zoho domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Zoho domein eenmalige aanmelding informatie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="7e175-155">a.</span><span class="sxs-lookup"><span data-stu-id="7e175-155">a.</span></span> <span data-ttu-id="7e175-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="7e175-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7e175-157">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="7e175-157">This value is not real.</span></span> <span data-ttu-id="7e175-158">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="7e175-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7e175-159">Neem contact op met [Zoho Client ondersteuningsteam](https://www.zoho.com/mail/contact.html) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="7e175-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="7e175-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7e175-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="7e175-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7e175-162">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e175-164">Op Hallo **Zoho configuratie** sectie, klikt u op **configureren Zoho** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7e175-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7e175-165">Kopiëren Hallo **Sign-Out-URL, de URL wachtwoord wijzigen en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7e175-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Zoho configuratie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="7e175-167">In een ander browservenster, meld u bij uw bedrijf Zoho Mail site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7e175-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="7e175-168">Ga toohello **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="7e175-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="7e175-169">![Het Configuratiescherm](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Configuratiescherm")</span><span class="sxs-lookup"><span data-stu-id="7e175-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="7e175-170">Klik op Hallo **SAML-verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7e175-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="7e175-171">![SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="7e175-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="7e175-172">In Hallo **SAML verificatiegegevens** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e175-173">![Details van SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Details van SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="7e175-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="7e175-174">a.</span><span class="sxs-lookup"><span data-stu-id="7e175-174">a.</span></span> <span data-ttu-id="7e175-175">In Hallo **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7e175-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7e175-176">b.</span><span class="sxs-lookup"><span data-stu-id="7e175-176">b.</span></span> <span data-ttu-id="7e175-177">In Hallo **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7e175-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7e175-178">c.</span><span class="sxs-lookup"><span data-stu-id="7e175-178">c.</span></span> <span data-ttu-id="7e175-179">In Hallo **URL van wijzigen wachtwoord** textbox plakken **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7e175-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="7e175-180">d.</span><span class="sxs-lookup"><span data-stu-id="7e175-180">d.</span></span> <span data-ttu-id="7e175-181">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PublicKey** textbox.</span><span class="sxs-lookup"><span data-stu-id="7e175-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="7e175-182">e.</span><span class="sxs-lookup"><span data-stu-id="7e175-182">e.</span></span> <span data-ttu-id="7e175-183">Als **algoritme**, selecteer **RSA**.</span><span class="sxs-lookup"><span data-stu-id="7e175-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="7e175-184">f.</span><span class="sxs-lookup"><span data-stu-id="7e175-184">f.</span></span> <span data-ttu-id="7e175-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e175-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="7e175-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7e175-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e175-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7e175-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e175-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e175-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7e175-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7e175-189">Create an Azure AD test user</span></span>

<span data-ttu-id="7e175-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7e175-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="7e175-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e175-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e175-193">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="7e175-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7e175-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7e175-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7e175-197">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e175-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7e175-199">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7e175-201">a.</span><span class="sxs-lookup"><span data-stu-id="7e175-201">a.</span></span> <span data-ttu-id="7e175-202">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e175-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e175-203">b.</span><span class="sxs-lookup"><span data-stu-id="7e175-203">b.</span></span> <span data-ttu-id="7e175-204">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="7e175-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7e175-205">c.</span><span class="sxs-lookup"><span data-stu-id="7e175-205">c.</span></span> <span data-ttu-id="7e175-206">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="7e175-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7e175-207">d.</span><span class="sxs-lookup"><span data-stu-id="7e175-207">d.</span></span> <span data-ttu-id="7e175-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7e175-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="7e175-209">Een testgebruiker Zoho maken</span><span class="sxs-lookup"><span data-stu-id="7e175-209">Create a Zoho test user</span></span>

<span data-ttu-id="7e175-210">In volgorde tooenable Azure AD gebruikers toolog in Zoho Mail, moeten ze worden ingericht in Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="7e175-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="7e175-211">In geval van Zoho E-mail Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="7e175-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="7e175-212">U kunt andere Zoho afdruk gebruiker account hulpmiddelen voor het maken of API's geleverd door Zoho Mail tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7e175-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="7e175-213">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e175-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="7e175-214">Meld u bij tooyour **Zoho Mail** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7e175-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="7e175-215">Ga te**Configuratiescherm \> e & Docs**.</span><span class="sxs-lookup"><span data-stu-id="7e175-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="7e175-216">Ga te**Gebruikersdetails \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7e175-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="7e175-217">![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="7e175-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="7e175-218">Op Hallo **gebruikers toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7e175-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e175-219">![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="7e175-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="7e175-220">a.</span><span class="sxs-lookup"><span data-stu-id="7e175-220">a.</span></span> <span data-ttu-id="7e175-221">In Hallo **voornaam** textbox type Hallo voornaam van gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7e175-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="7e175-222">b.</span><span class="sxs-lookup"><span data-stu-id="7e175-222">b.</span></span> <span data-ttu-id="7e175-223">In Hallo **achternaam** textbox type Hallo achternaam van gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e175-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="7e175-224">c.</span><span class="sxs-lookup"><span data-stu-id="7e175-224">c.</span></span> <span data-ttu-id="7e175-225">In Hallo **E-mail-ID** textbox type Hallo e-mail-id van gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7e175-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7e175-226">d.</span><span class="sxs-lookup"><span data-stu-id="7e175-226">d.</span></span> <span data-ttu-id="7e175-227">In Hallo **wachtwoord** textbox, voer het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e175-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="7e175-228">e.</span><span class="sxs-lookup"><span data-stu-id="7e175-228">e.</span></span> <span data-ttu-id="7e175-229">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e175-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="7e175-230">Hello Azure Active Directory-accounthouder ontvangt een e-mail met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="7e175-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7e175-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e175-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7e175-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooZoho toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7e175-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="7e175-234">**tooassign Britta Simon tooZoho, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7e175-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e175-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7e175-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7e175-237">Selecteer in de lijst met de toepassingen van Hallo **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="7e175-237">In hello applications list, select **Zoho**.</span></span>

    ![Hallo Zoho koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="7e175-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7e175-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="7e175-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7e175-241">Click **Add** button.</span></span> <span data-ttu-id="7e175-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e175-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="7e175-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e175-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e175-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e175-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e175-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7e175-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7e175-247">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7e175-247">Test single sign-on</span></span>

<span data-ttu-id="7e175-248">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7e175-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e175-249">Als u op Hallo Zoho tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zoho toepassing.</span><span class="sxs-lookup"><span data-stu-id="7e175-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="7e175-250">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e175-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e175-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7e175-251">Additional resources</span></span>

* [<span data-ttu-id="7e175-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e175-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e175-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e175-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

