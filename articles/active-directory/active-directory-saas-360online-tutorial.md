---
title: 'Zelfstudie: Azure Active Directory-integratie met 360 Online | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 360 Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 413e4e2c41336f99e1999857c788c5dac15be4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="56e31-103">Zelfstudie: Azure Active Directory-integratie met 360 Online</span><span class="sxs-lookup"><span data-stu-id="56e31-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="56e31-104">In deze zelfstudie leert u hoe toointegrate 360 Online met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56e31-104">In this tutorial, you learn how toointegrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56e31-105">360 Online integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="56e31-105">Integrating 360 Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56e31-106">U kunt beheren in Azure AD die Online too360 toegang heeft</span><span class="sxs-lookup"><span data-stu-id="56e31-106">You can control in Azure AD who has access too360 Online</span></span>
- <span data-ttu-id="56e31-107">U kunt uw gebruikers tooautomatically get aangemelde too360 inschakelen Online (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="56e31-107">You can enable your users tooautomatically get signed-on too360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56e31-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="56e31-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56e31-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56e31-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56e31-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="56e31-110">Prerequisites</span></span>

<span data-ttu-id="56e31-111">Azure AD-integratie met 360 Online tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="56e31-111">tooconfigure Azure AD integration with 360 Online, you need hello following items:</span></span>

- <span data-ttu-id="56e31-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="56e31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56e31-113">Een 360 Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="56e31-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56e31-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="56e31-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56e31-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="56e31-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56e31-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="56e31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56e31-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56e31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56e31-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="56e31-118">Scenario description</span></span>
<span data-ttu-id="56e31-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="56e31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56e31-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="56e31-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56e31-121">360 Online toevoegen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="56e31-121">Adding 360 Online from hello gallery</span></span>
2. <span data-ttu-id="56e31-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56e31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-hello-gallery"></a><span data-ttu-id="56e31-123">360 Online toevoegen van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="56e31-123">Adding 360 Online from hello gallery</span></span>
<span data-ttu-id="56e31-124">tooconfigure hello integratie van 360 Online met Azure AD, moet u tooadd 360 Online uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="56e31-124">tooconfigure hello integration of 360 Online into Azure AD, you need tooadd 360 Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56e31-125">**tooadd 360 Online uitvoeren via Hallo gallery Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56e31-125">**tooadd 360 Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56e31-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="56e31-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56e31-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56e31-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56e31-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56e31-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="56e31-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56e31-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="56e31-133">Typ in het zoekvak Hallo **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="56e31-133">In hello search box, type **360 Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="56e31-135">Selecteer in het deelvenster resultaten hello, **360 Online**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="56e31-135">In hello results panel, select **360 Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56e31-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56e31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56e31-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 360 Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="56e31-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="56e31-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 360 Online is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56e31-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 360 Online is tooa user in Azure AD.</span></span> <span data-ttu-id="56e31-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in 360 moet Online toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="56e31-140">In other words, a link relationship between an Azure AD user and hello related user in 360 Online needs toobe established.</span></span>

<span data-ttu-id="56e31-141">Wijs in 360 Online Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="56e31-141">In 360 Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56e31-142">tooconfigure en eenmalige aanmelding Azure AD-test met 360 Online, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56e31-142">tooconfigure and test Azure AD single sign-on with 360 Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56e31-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="56e31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56e31-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56e31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56e31-145">**[Maken van een 360 Online testgebruiker](#creating-a-360-online-test-user)**  -toohave een equivalent van Britta Simon in 360 Online die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="56e31-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - toohave a counterpart of Britta Simon in 360 Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56e31-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="56e31-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56e31-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="56e31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56e31-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="56e31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56e31-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing met 360 Online configureren.</span><span class="sxs-lookup"><span data-stu-id="56e31-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="56e31-150">**Voer tooconfigure Azure AD eenmalige aanmelding met 360 Online Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56e31-150">**tooconfigure Azure AD single sign-on with 360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="56e31-151">In de Azure-portal op Hallo Hallo **360 Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="56e31-151">In hello Azure portal, on hello **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="56e31-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="56e31-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="56e31-155">Op Hallo **360 Online domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56e31-155">On hello **360 Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="56e31-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="56e31-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56e31-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="56e31-158">hello value is not real.</span></span> <span data-ttu-id="56e31-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="56e31-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="56e31-160">Neem contact op met [360 Online Client ondersteuningsteam](mailto:360online@software-innovation.com) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="56e31-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="56e31-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="56e31-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="56e31-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="56e31-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56e31-165">tooconfigure eenmalige aanmelding op **360 Online** zijde, moet u toosend Hallo gedownload **Metadata XML** te[360 Online ondersteuningsteam](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="56e31-165">tooconfigure single sign-on on **360 Online** side, you need toosend hello downloaded **Metadata XML** too[360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="56e31-166">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="56e31-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56e31-167">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="56e31-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56e31-168">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56e31-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56e31-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="56e31-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="56e31-170">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="56e31-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="56e31-172">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56e31-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56e31-173">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="56e31-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56e31-175">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="56e31-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56e31-177">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="56e31-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56e31-179">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56e31-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56e31-181">a.</span><span class="sxs-lookup"><span data-stu-id="56e31-181">a.</span></span> <span data-ttu-id="56e31-182">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56e31-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56e31-183">b.</span><span class="sxs-lookup"><span data-stu-id="56e31-183">b.</span></span> <span data-ttu-id="56e31-184">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56e31-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56e31-185">c.</span><span class="sxs-lookup"><span data-stu-id="56e31-185">c.</span></span> <span data-ttu-id="56e31-186">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="56e31-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56e31-187">d.</span><span class="sxs-lookup"><span data-stu-id="56e31-187">d.</span></span> <span data-ttu-id="56e31-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="56e31-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="56e31-189">Een 360 Online testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="56e31-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="56e31-190">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in 360 Online.</span><span class="sxs-lookup"><span data-stu-id="56e31-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="56e31-191">u moet toocontact [360 Online ondersteuningsteam](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="56e31-191">you need toocontact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="56e31-192">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="56e31-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="56e31-193">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang too360 Online.</span><span class="sxs-lookup"><span data-stu-id="56e31-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too360 Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="56e31-195">**tooassign Britta Simon too360 Online, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="56e31-195">**tooassign Britta Simon too360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="56e31-196">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="56e31-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="56e31-198">Selecteer in de lijst met de toepassingen van Hallo **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="56e31-198">In hello applications list, select **360 Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="56e31-200">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="56e31-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="56e31-202">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="56e31-202">Click **Add** button.</span></span> <span data-ttu-id="56e31-203">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56e31-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="56e31-205">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="56e31-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56e31-206">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56e31-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56e31-207">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56e31-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56e31-208">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="56e31-208">Testing single sign-on</span></span>

<span data-ttu-id="56e31-209">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="56e31-209">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="56e31-210">Wanneer u Online Hallo 360 tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour 360 on line toepassing.</span><span class="sxs-lookup"><span data-stu-id="56e31-210">When you click hello 360 Online tile in hello Access Panel, you should get automatically signed-on tooyour 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56e31-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="56e31-211">Additional resources</span></span>

* [<span data-ttu-id="56e31-212">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56e31-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56e31-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56e31-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

