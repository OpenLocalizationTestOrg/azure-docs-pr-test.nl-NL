---
title: 'Zelfstudie: Azure Active Directory-integratie met Printix | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Printix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="de286-103">Zelfstudie: Azure Active Directory-integratie met Printix</span><span class="sxs-lookup"><span data-stu-id="de286-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="de286-104">In deze zelfstudie leert u hoe toointegrate Printix met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de286-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de286-105">Printix integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="de286-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de286-106">U kunt beheren in Azure AD die tooPrintix toegang heeft</span><span class="sxs-lookup"><span data-stu-id="de286-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="de286-107">U kunt uw gebruikers tooautomatically get aangemelde tooPrintix (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="de286-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de286-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="de286-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de286-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de286-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de286-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de286-110">Prerequisites</span></span>

<span data-ttu-id="de286-111">Azure AD-integratie met Printix tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="de286-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="de286-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="de286-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de286-113">Een Printix eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="de286-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de286-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="de286-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de286-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="de286-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de286-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="de286-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de286-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de286-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de286-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="de286-118">Scenario description</span></span>
<span data-ttu-id="de286-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="de286-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de286-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="de286-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de286-121">Het toevoegen van Printix van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="de286-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="de286-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de286-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="de286-123">Het toevoegen van Printix van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="de286-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="de286-124">tooconfigure hello integratie van Printix in Azure AD, moet u tooadd Printix uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="de286-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de286-125">**tooadd Printix via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de286-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de286-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="de286-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de286-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de286-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de286-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de286-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="de286-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de286-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="de286-133">Typ in het zoekvak Hallo **Printix**.</span><span class="sxs-lookup"><span data-stu-id="de286-133">In hello search box, type **Printix**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="de286-135">Selecteer in het deelvenster resultaten hello, **Printix**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="de286-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de286-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de286-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de286-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Printix op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="de286-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de286-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Printix is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de286-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="de286-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Printix toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="de286-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="de286-141">Wijs in Printix, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="de286-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de286-142">tooconfigure en eenmalige aanmelding Azure AD-test met Printix, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de286-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de286-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="de286-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de286-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de286-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de286-145">**[Maken van een testgebruiker Printix](#creating-a-printix-test-user)**  -toohave een equivalent van Britta Simon in Printix die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="de286-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de286-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="de286-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de286-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="de286-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de286-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="de286-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de286-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Printix configureren.</span><span class="sxs-lookup"><span data-stu-id="de286-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="de286-150">**Azure AD tooconfigure eenmalige aanmelding met Printix, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de286-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="de286-151">In de Azure-portal op Hallo Hallo **Printix** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="de286-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="de286-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="de286-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="de286-155">Op Hallo **Printix domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de286-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="de286-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="de286-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de286-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="de286-158">hello value is not real.</span></span> <span data-ttu-id="de286-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="de286-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="de286-160">Neem contact op met [Printix Client ondersteuningsteam](mailto:support@printix.net) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="de286-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="de286-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="de286-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="de286-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="de286-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de286-165">Eenmalige aanmelding tooyour Printix tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="de286-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="de286-166">In het menu bovenaan Hallo Hallo Klik op de rechterbovenhoek Hallo Hallo-pictogram en selecteer '**verificatie**'.</span><span class="sxs-lookup"><span data-stu-id="de286-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="de286-168">Op Hallo **Setup** tabblad **inschakelen Azure/Office 365-verificatie**</span><span class="sxs-lookup"><span data-stu-id="de286-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="de286-170">Op Hallo **Azure** invoer federatieve metagegevens URL toohello textbox van tabblad '**document met federatieve metagegevens**'.</span><span class="sxs-lookup"><span data-stu-id="de286-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="de286-171">Hallo metagegevens XML-bestand dat u hebt gedownload van Azure AD te koppelen[Printix ondersteuningsteam](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="de286-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="de286-172">Vervolgens Hallo XML-bestand uploaden en een federation-metagegevens-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="de286-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="de286-174">Klik op Hallo '**testen**'knop en klik op'**OK**' knop als Hallo test geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="de286-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="de286-175">Azure active directory-pagina wordt weergegeven wanneer u op Hallo **testen** knop.</span><span class="sxs-lookup"><span data-stu-id="de286-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="de286-176">"Hallo test is geslaagd" betekent hier na het invoeren van Hallo referenties van uw Azure testaccount die er verschijnt een bericht met 'instellingen getest OK'. Klik vervolgens op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="de286-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="de286-178">Klik op Hallo **opslaan** op knop '**verificatie**' pagina.</span><span class="sxs-lookup"><span data-stu-id="de286-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="de286-179">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="de286-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de286-180">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="de286-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de286-181">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de286-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de286-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="de286-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="de286-183">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="de286-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="de286-185">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de286-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de286-186">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="de286-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de286-188">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="de286-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de286-190">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="de286-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de286-192">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de286-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de286-194">a.</span><span class="sxs-lookup"><span data-stu-id="de286-194">a.</span></span> <span data-ttu-id="de286-195">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de286-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de286-196">b.</span><span class="sxs-lookup"><span data-stu-id="de286-196">b.</span></span> <span data-ttu-id="de286-197">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de286-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de286-198">c.</span><span class="sxs-lookup"><span data-stu-id="de286-198">c.</span></span> <span data-ttu-id="de286-199">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="de286-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de286-200">d.</span><span class="sxs-lookup"><span data-stu-id="de286-200">d.</span></span> <span data-ttu-id="de286-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="de286-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="de286-202">Een testgebruiker Printix maken</span><span class="sxs-lookup"><span data-stu-id="de286-202">Creating a Printix test user</span></span>

<span data-ttu-id="de286-203">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Printix van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="de286-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="de286-204">Printix ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="de286-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="de286-205">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="de286-205">There is no action item for you in this section.</span></span> <span data-ttu-id="de286-206">Een nieuwe gebruiker wordt tijdens een poging tooaccess Printix gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="de286-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="de286-207">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Printix ondersteuningsteam](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="de286-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de286-208">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de286-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de286-209">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPrintix toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="de286-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="de286-211">**tooassign Britta Simon tooPrintix, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de286-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="de286-212">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de286-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="de286-214">Selecteer in de lijst met de toepassingen van Hallo **Printix**.</span><span class="sxs-lookup"><span data-stu-id="de286-214">In hello applications list, select **Printix**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="de286-216">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="de286-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="de286-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="de286-218">Click **Add** button.</span></span> <span data-ttu-id="de286-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de286-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="de286-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="de286-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de286-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de286-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de286-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de286-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de286-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de286-224">Testing single sign-on</span></span>

<span data-ttu-id="de286-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="de286-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de286-226">Als u op Hallo Printix tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Printix toepassing.</span><span class="sxs-lookup"><span data-stu-id="de286-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de286-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="de286-227">Additional resources</span></span>

* [<span data-ttu-id="de286-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de286-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de286-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de286-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

