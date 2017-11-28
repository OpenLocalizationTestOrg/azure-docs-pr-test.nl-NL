---
title: "Zelfstudie: Azure Active Directory-integratie met informatie Retail – informatiebeheer | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en informatie Retail – informatiebeheer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="85cbd-103">Zelfstudie: Azure Active Directory-integratie met informatie Retail – informatiebeheer</span><span class="sxs-lookup"><span data-stu-id="85cbd-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="85cbd-104">In deze zelfstudie leert u hoe toointegrate informatie Retail – informatiebeheer met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85cbd-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85cbd-105">Integratie van informatie Retail – informatiebeheer met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85cbd-106">U kunt beheren in Azure AD die toegang tooInfor Retail – Information Management heeft.</span><span class="sxs-lookup"><span data-stu-id="85cbd-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="85cbd-107">U kunt uw gebruikers tooautomatically get aangemelde tooInfor Retail – informatiebeheer (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="85cbd-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="85cbd-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="85cbd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="85cbd-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85cbd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85cbd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85cbd-110">Prerequisites</span></span>

<span data-ttu-id="85cbd-111">tooconfigure Azure AD-integratie met informatie Retail – informatiebeheer, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="85cbd-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="85cbd-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="85cbd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85cbd-113">Een handelsversie informatie – informatiebeheer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="85cbd-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85cbd-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="85cbd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85cbd-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85cbd-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="85cbd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85cbd-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85cbd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85cbd-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="85cbd-118">Scenario description</span></span>
<span data-ttu-id="85cbd-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="85cbd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85cbd-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85cbd-121">Informatie Retail-informatiebeheer uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85cbd-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="85cbd-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="85cbd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="85cbd-123">Informatie Retail-informatiebeheer uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="85cbd-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="85cbd-124">tooconfigure hello integratie van informatie detailhandel – Information Management in Azure AD, moet u tooadd informatie Retail – informatiebeheer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="85cbd-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85cbd-125">**tooadd informatie Retail – informatiebeheer via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="85cbd-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85cbd-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="85cbd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="85cbd-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85cbd-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="85cbd-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85cbd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="85cbd-133">Typ in het zoekvak Hallo **informatie Retail – informatiebeheer**, selecteer **informatie Retail – informatiebeheer** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo de toepassing.</span><span class="sxs-lookup"><span data-stu-id="85cbd-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Informatie Retail – informatiebeheer in de lijst met resultaten Hallo](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="85cbd-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="85cbd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="85cbd-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met informatie Retail – informatiebeheer op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="85cbd-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85cbd-137">Azure AD moet tooknow welke gebruiker Hallo equivalent in de detailhandel van informatie voor eenmalige aanmelding toowork – informatiebeheer is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85cbd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="85cbd-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de detailhandel informatie – informatiebeheer Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="85cbd-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="85cbd-139">In de detailhandel informatie – informatiebeheer Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="85cbd-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="85cbd-140">tooconfigure en eenmalige aanmelding Azure AD-test met informatie Retail – informatiebeheer, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85cbd-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="85cbd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85cbd-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85cbd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85cbd-143">**[Maken van een handelsversie informatie – informatiebeheer testgebruiker](#create-an-infor-retail--information-management-test-user)**  - toohave een equivalent van Britta Simon in de detailhandel informatie – informatiebeheer die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="85cbd-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85cbd-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="85cbd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85cbd-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="85cbd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="85cbd-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="85cbd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="85cbd-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in de detailhandel van uw informatie – informatie Management-toepassing.</span><span class="sxs-lookup"><span data-stu-id="85cbd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="85cbd-148">**tooconfigure eenmalige aanmelding Azure AD met informatie Retail – informatiebeheer uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="85cbd-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="85cbd-149">In Azure-portal op Hallo Hallo **informatie Retail – informatiebeheer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="85cbd-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="85cbd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="85cbd-153">Op Hallo **informatie Retail-URL's en informatie beheerdomein** sectie, voert u Hallo volgende stappen uit als u wenst tooconfigure Hallo toepassing in de IDP geïnitieerd modus:</span><span class="sxs-lookup"><span data-stu-id="85cbd-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Informatie Retail-URL's en informatie beheerdomein eenmalige aanmelding informatie IDP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="85cbd-155">a.</span><span class="sxs-lookup"><span data-stu-id="85cbd-155">a.</span></span> <span data-ttu-id="85cbd-156">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="85cbd-157">b.</span><span class="sxs-lookup"><span data-stu-id="85cbd-157">b.</span></span> <span data-ttu-id="85cbd-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="85cbd-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="85cbd-159">Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="85cbd-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informatie Retail – informatie beheerdomein en URL's eenmalige aanmelding informatie SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="85cbd-161">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="85cbd-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="85cbd-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="85cbd-162">These values are not real.</span></span> <span data-ttu-id="85cbd-163">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="85cbd-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="85cbd-164">Neem contact op met [informatie Retail – informatie Beheerclient ondersteuningsteam](mailto:innovate@infor.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="85cbd-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="85cbd-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="85cbd-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="85cbd-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="85cbd-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="85cbd-169">tooconfigure eenmalige aanmelding op **informatie Retail – informatiebeheer** zijde, moet u toosend Hallo gedownload **Metadata XML** te[informatie Retail-ondersteuningsteam informatiebeheer ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="85cbd-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="85cbd-170">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="85cbd-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="85cbd-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="85cbd-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85cbd-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="85cbd-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85cbd-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85cbd-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="85cbd-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="85cbd-174">Create an Azure AD test user</span></span>

<span data-ttu-id="85cbd-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="85cbd-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="85cbd-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="85cbd-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85cbd-178">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="85cbd-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="85cbd-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="85cbd-182">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85cbd-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="85cbd-184">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="85cbd-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="85cbd-186">a.</span><span class="sxs-lookup"><span data-stu-id="85cbd-186">a.</span></span> <span data-ttu-id="85cbd-187">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85cbd-188">b.</span><span class="sxs-lookup"><span data-stu-id="85cbd-188">b.</span></span> <span data-ttu-id="85cbd-189">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="85cbd-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="85cbd-190">c.</span><span class="sxs-lookup"><span data-stu-id="85cbd-190">c.</span></span> <span data-ttu-id="85cbd-191">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="85cbd-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="85cbd-192">d.</span><span class="sxs-lookup"><span data-stu-id="85cbd-192">d.</span></span> <span data-ttu-id="85cbd-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="85cbd-194">Maken van een handelsversie informatie – informatiebeheer testgebruiker</span><span class="sxs-lookup"><span data-stu-id="85cbd-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="85cbd-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in de detailhandel informatie – informatiebeheer maken.</span><span class="sxs-lookup"><span data-stu-id="85cbd-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="85cbd-196">Neem contact op met [informatie Retail – informatiebeheer ondersteuningsteam](mailto:innovate@infor.com) tooadd Hallo gebruikers in Hallo informatie Retail-platform voor het beheer van informatie.</span><span class="sxs-lookup"><span data-stu-id="85cbd-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="85cbd-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="85cbd-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="85cbd-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooInfor Retail – informatiebeheer.</span><span class="sxs-lookup"><span data-stu-id="85cbd-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="85cbd-200">**tooassign Britta Simon tooInfor Retail – informatiebeheer uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="85cbd-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="85cbd-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="85cbd-203">Selecteer in de lijst met de toepassingen van Hallo **informatie Retail – informatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Hallo informatie Retail – koppelen informatiebeheer in de lijst met Hallo-toepassingen](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="85cbd-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="85cbd-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="85cbd-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="85cbd-207">Click **Add** button.</span></span> <span data-ttu-id="85cbd-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85cbd-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="85cbd-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="85cbd-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85cbd-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85cbd-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85cbd-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="85cbd-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="85cbd-213">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="85cbd-213">Test single sign-on</span></span>

<span data-ttu-id="85cbd-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="85cbd-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85cbd-215">Wanneer u klikt op Hallo informatie Retail – informatiebeheer tegel in Hallo paneel voor Apptoegang, krijgt u automatisch aangemelde tooyour informatie Retail – informatie Management-toepassing.</span><span class="sxs-lookup"><span data-stu-id="85cbd-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="85cbd-216">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85cbd-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85cbd-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="85cbd-217">Additional resources</span></span>

* [<span data-ttu-id="85cbd-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85cbd-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85cbd-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85cbd-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

