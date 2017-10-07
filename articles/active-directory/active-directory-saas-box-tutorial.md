---
title: 'Zelfstudie: Azure Active Directory-integratie met vak | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en vak.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="90cd0-103">Zelfstudie: Azure Active Directory-integratie met het selectievakje</span><span class="sxs-lookup"><span data-stu-id="90cd0-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="90cd0-104">In deze zelfstudie leert u hoe toointegrate vak met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90cd0-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90cd0-105">Vak integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90cd0-106">U kunt beheren in Azure AD die tooBox toegang heeft</span><span class="sxs-lookup"><span data-stu-id="90cd0-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="90cd0-107">U kunt uw gebruikers tooautomatically get aangemelde tooBox (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="90cd0-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90cd0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="90cd0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90cd0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90cd0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90cd0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="90cd0-110">Prerequisites</span></span>

<span data-ttu-id="90cd0-111">Azure AD-integratie met Box tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="90cd0-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="90cd0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="90cd0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90cd0-113">Een selectievakje eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="90cd0-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90cd0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="90cd0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90cd0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90cd0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="90cd0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90cd0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90cd0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90cd0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="90cd0-118">Scenario description</span></span>
<span data-ttu-id="90cd0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90cd0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90cd0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90cd0-121">Vak uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="90cd0-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="90cd0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90cd0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="90cd0-123">Vak uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="90cd0-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="90cd0-124">tooconfigure hello integratie van het selectievakje in Azure AD, moet u tooadd vak uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="90cd0-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90cd0-125">**tooadd uit Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90cd0-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90cd0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90cd0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90cd0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90cd0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="90cd0-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="90cd0-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="90cd0-133">Typ in het zoekvak Hallo **vak**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-133">In hello search box, type **Box**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="90cd0-135">Selecteer in het deelvenster resultaten hello, **vak**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="90cd0-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90cd0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90cd0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90cd0-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met vak op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="90cd0-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90cd0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in vak is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90cd0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="90cd0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in vak toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="90cd0-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="90cd0-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in vak.</span><span class="sxs-lookup"><span data-stu-id="90cd0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="90cd0-142">tooconfigure en test eenmalige aanmelding Azure AD met Box, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90cd0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="90cd0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90cd0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90cd0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90cd0-145">**[Maken van een gebruiker vak testen](#creating-a-box-test-user)**  -toohave een equivalent van Britta Simon in dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="90cd0-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90cd0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="90cd0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90cd0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="90cd0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90cd0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="90cd0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90cd0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing vak.</span><span class="sxs-lookup"><span data-stu-id="90cd0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="90cd0-150">**Voer tooconfigure Azure AD eenmalige aanmelding met vak Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90cd0-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="90cd0-151">In de Azure-portal op Hallo Hallo **vak** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="90cd0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="90cd0-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="90cd0-155">Op Hallo **in het domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="90cd0-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="90cd0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90cd0-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="90cd0-158">This value is not real.</span></span> <span data-ttu-id="90cd0-159">Hallo-waarde met de Hallo werkelijke aanmeldings-URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="90cd0-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="90cd0-160">Neem contact op met [Box Client ondersteuningsteam](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="90cd0-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="90cd0-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="90cd0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="90cd0-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="90cd0-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90cd0-165">tooget SSO is geconfigureerd voor uw toepassing, neem contact op met [Box Client ondersteuningsteam](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) en voorzien Hallo gedownload XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="90cd0-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="90cd0-166">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="90cd0-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90cd0-167">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="90cd0-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90cd0-168">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90cd0-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90cd0-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="90cd0-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="90cd0-170">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="90cd0-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="90cd0-172">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90cd0-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90cd0-173">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90cd0-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90cd0-175">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90cd0-177">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="90cd0-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90cd0-179">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="90cd0-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90cd0-181">a.</span><span class="sxs-lookup"><span data-stu-id="90cd0-181">a.</span></span> <span data-ttu-id="90cd0-182">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90cd0-183">b.</span><span class="sxs-lookup"><span data-stu-id="90cd0-183">b.</span></span> <span data-ttu-id="90cd0-184">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90cd0-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90cd0-185">c.</span><span class="sxs-lookup"><span data-stu-id="90cd0-185">c.</span></span> <span data-ttu-id="90cd0-186">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90cd0-187">d.</span><span class="sxs-lookup"><span data-stu-id="90cd0-187">d.</span></span> <span data-ttu-id="90cd0-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="90cd0-189">Maken van een gebruiker vak testen</span><span class="sxs-lookup"><span data-stu-id="90cd0-189">Creating a Box test user</span></span>

<span data-ttu-id="90cd0-190">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in het vak.</span><span class="sxs-lookup"><span data-stu-id="90cd0-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="90cd0-191">Vak ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="90cd0-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="90cd0-192">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="90cd0-192">There is no action item for you in this section.</span></span> <span data-ttu-id="90cd0-193">Als een gebruiker in het vak nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess vak probeert.</span><span class="sxs-lookup"><span data-stu-id="90cd0-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90cd0-194">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="90cd0-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90cd0-195">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBox toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="90cd0-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="90cd0-197">**tooassign Britta Simon tooBox, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90cd0-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="90cd0-198">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="90cd0-200">Selecteer in de lijst met de toepassingen van Hallo **vak**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-200">In hello applications list, select **Box**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="90cd0-202">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="90cd0-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="90cd0-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="90cd0-204">Click **Add** button.</span></span> <span data-ttu-id="90cd0-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90cd0-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="90cd0-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="90cd0-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90cd0-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90cd0-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90cd0-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90cd0-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90cd0-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90cd0-210">Testing single sign-on</span></span>

<span data-ttu-id="90cd0-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="90cd0-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="90cd0-212">Als u op Hallo vak tegel in Hallo Toegangsvenster, krijgt u aanmelding pagina tooget aangemelde tooyour vak toepassing.</span><span class="sxs-lookup"><span data-stu-id="90cd0-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90cd0-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="90cd0-213">Additional resources</span></span>

* [<span data-ttu-id="90cd0-214">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90cd0-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90cd0-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90cd0-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="90cd0-216">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="90cd0-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

