---
title: 'Zelfstudie: Azure Active Directory-integratie met MaxxPoint | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en MaxxPoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="2f7bf-103">Zelfstudie: Azure Active Directory-integratie met MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="2f7bf-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="2f7bf-104">In deze zelfstudie leert u hoe toointegrate MaxxPoint met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f7bf-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f7bf-105">MaxxPoint integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f7bf-106">U kunt beheren in Azure AD die tooMaxxPoint toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2f7bf-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="2f7bf-107">U kunt uw gebruikers tooautomatically get aangemelde tooMaxxPoint (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2f7bf-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f7bf-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2f7bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f7bf-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f7bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f7bf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f7bf-110">Prerequisites</span></span>

<span data-ttu-id="2f7bf-111">Azure AD-integratie met MaxxPoint tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="2f7bf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2f7bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f7bf-113">Een MaxxPoint eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2f7bf-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f7bf-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f7bf-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f7bf-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2f7bf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f7bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f7bf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2f7bf-118">Scenario description</span></span>
<span data-ttu-id="2f7bf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f7bf-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f7bf-121">Het toevoegen van MaxxPoint van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2f7bf-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="2f7bf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2f7bf-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="2f7bf-123">Het toevoegen van MaxxPoint van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2f7bf-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="2f7bf-124">tooconfigure hello integratie van MaxxPoint in Azure AD, moet u tooadd MaxxPoint uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f7bf-125">**tooadd MaxxPoint via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2f7bf-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f7bf-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f7bf-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f7bf-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2f7bf-131">Klik op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster tooadd nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2f7bf-133">Typ in het zoekvak Hallo **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="2f7bf-135">Selecteer in het deelvenster resultaten hello, **MaxxPoint**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f7bf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2f7bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f7bf-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met MaxxPoint op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f7bf-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in MaxxPoint is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="2f7bf-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in MaxxPoint toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="2f7bf-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="2f7bf-142">tooconfigure en eenmalige aanmelding Azure AD-test met MaxxPoint, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f7bf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f7bf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f7bf-145">**[Maken van een testgebruiker MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave een equivalent van Britta Simon in MaxxPoint die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2f7bf-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f7bf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f7bf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2f7bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f7bf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing MaxxPoint configureren.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="2f7bf-150">**Azure AD tooconfigure eenmalige aanmelding met MaxxPoint, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2f7bf-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f7bf-151">In de Azure-portal op Hallo Hallo **MaxxPoint** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2f7bf-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="2f7bf-155">Op Hallo **MaxxPoint domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, geen tooperform eventuele stappen nodig.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="2f7bf-157">Op Hallo **MaxxPoint domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="2f7bf-159">a.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-159">a.</span></span> <span data-ttu-id="2f7bf-160">Klik op **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="2f7bf-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="2f7bf-161">b.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-161">b.</span></span> <span data-ttu-id="2f7bf-162">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="2f7bf-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f7bf-163">Houd er rekening mee dat dit geen Hallo echte waarde is.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="2f7bf-164">U hebt deze waarde Hello werkelijke aanmelden URL tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="2f7bf-165">Aanroepen van MaxxPoint team voor **888-728-0950** tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="2f7bf-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="2f7bf-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2f7bf-170">tooget SSO is geconfigureerd voor uw toepassing, ondersteuningsteam MaxxPoint niet aanroepen voor **888-728-0950** en ze helpt u verder gaat op hoe ze Hallo tooprovide gedownload **Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="2f7bf-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f7bf-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f7bf-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f7bf-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f7bf-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2f7bf-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f7bf-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2f7bf-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2f7bf-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f7bf-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f7bf-180">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f7bf-182">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f7bf-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f7bf-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f7bf-186">a.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-186">a.</span></span> <span data-ttu-id="2f7bf-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f7bf-188">b.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-188">b.</span></span> <span data-ttu-id="2f7bf-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f7bf-190">c.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-190">c.</span></span> <span data-ttu-id="2f7bf-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f7bf-192">d.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-192">d.</span></span> <span data-ttu-id="2f7bf-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="2f7bf-194">Een testgebruiker MaxxPoint maken</span><span class="sxs-lookup"><span data-stu-id="2f7bf-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="2f7bf-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in MaxxPoint maken.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="2f7bf-196">Neem contact op met het ondersteuningsteam MaxxPoint op **888-728-0950** tooadd Hallo gebruikers in Hallo MaxxPoint toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f7bf-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f7bf-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f7bf-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooMaxxPoint toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2f7bf-200">**tooassign Britta Simon tooMaxxPoint, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2f7bf-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f7bf-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2f7bf-203">Selecteer in de lijst met de toepassingen van Hallo **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="2f7bf-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2f7bf-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-207">Click **Add** button.</span></span> <span data-ttu-id="2f7bf-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2f7bf-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f7bf-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f7bf-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f7bf-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2f7bf-213">Testing single sign-on</span></span>

<span data-ttu-id="2f7bf-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f7bf-215">Als u op Hallo MaxxPoint tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour MaxxPoint toepassing.</span><span class="sxs-lookup"><span data-stu-id="2f7bf-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2f7bf-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2f7bf-216">Additional resources</span></span>

* [<span data-ttu-id="2f7bf-217">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f7bf-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f7bf-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f7bf-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png