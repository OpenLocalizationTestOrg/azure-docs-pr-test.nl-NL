---
title: 'Zelfstudie: Azure Active Directory-integratie met instructies voor Microsoft | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en instructies over het Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 59a8b856fd2dc75a37e9bb8f46ced066bcd0fd56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="4c5b2-103">Zelfstudie: Azure Active Directory-integratie met instructies voor Microsoft</span><span class="sxs-lookup"><span data-stu-id="4c5b2-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="4c5b2-104">In deze zelfstudie leert u hoe toointegrate instructies over het Microsoft met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-104">In this tutorial, you learn how toointegrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c5b2-105">Instructies over het Microsoft integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-105">Integrating Directions on Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c5b2-106">U kunt beheren in Azure AD die toegang tooDirections op Microsoft</span><span class="sxs-lookup"><span data-stu-id="4c5b2-106">You can control in Azure AD who has access tooDirections on Microsoft</span></span>
- <span data-ttu-id="4c5b2-107">U kunt uw gebruikers tooautomatically get aangemelde tooDirections op Microsoft (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4c5b2-107">You can enable your users tooautomatically get signed-on tooDirections on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c5b2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4c5b2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4c5b2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c5b2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4c5b2-110">Prerequisites</span></span>

<span data-ttu-id="4c5b2-111">Azure AD-integratie met instructies voor Microsoft tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-111">tooconfigure Azure AD integration with Directions on Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="4c5b2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4c5b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c5b2-113">Een instructies voor eenmalige aanmelding Microsoft abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="4c5b2-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c5b2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c5b2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c5b2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c5b2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c5b2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4c5b2-118">Scenario description</span></span>
<span data-ttu-id="4c5b2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c5b2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c5b2-121">Het toevoegen van richtingen op Microsoft van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4c5b2-121">Adding Directions on Microsoft from hello gallery</span></span>
2. <span data-ttu-id="4c5b2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c5b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-hello-gallery"></a><span data-ttu-id="4c5b2-123">Het toevoegen van richtingen op Microsoft van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4c5b2-123">Adding Directions on Microsoft from hello gallery</span></span>
<span data-ttu-id="4c5b2-124">tooconfigure hello integratie van instructies over het Microsoft met Azure AD, moet u tooadd instructies over het Microsoft uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-124">tooconfigure hello integration of Directions on Microsoft into Azure AD, you need tooadd Directions on Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c5b2-125">**tooadd instructies over het Microsoft via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c5b2-125">**tooadd Directions on Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c5b2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c5b2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c5b2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4c5b2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4c5b2-133">Typ in het zoekvak Hallo **instructies over het Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-133">In hello search box, type **Directions on Microsoft**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="4c5b2-135">Selecteer in het deelvenster resultaten hello, **instructies over het Microsoft**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-135">In hello results panel, select **Directions on Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c5b2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c5b2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c5b2-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met instructies voor Microsoft op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4c5b2-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c5b2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in richtingen op Microsoft is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Directions on Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="4c5b2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo kanten op Microsoft toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-140">In other words, a link relationship between an Azure AD user and hello related user in Directions on Microsoft needs toobe established.</span></span>

<span data-ttu-id="4c5b2-141">In richtingen op Microsoft hello waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-141">In Directions on Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c5b2-142">tooconfigure en test eenmalige aanmelding Azure AD met instructies voor Microsoft, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-142">tooconfigure and test Azure AD single sign-on with Directions on Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c5b2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c5b2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c5b2-145">**[Maken van een richtingen op Microsoft testgebruiker](#creating-a-directions-on-microsoft-test-user)**  -toohave een equivalent van Britta Simon kanten op Microsoft die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - toohave a counterpart of Britta Simon in Directions on Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c5b2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c5b2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c5b2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4c5b2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c5b2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw richtingen op Microsoft-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="4c5b2-150">**Voer tooconfigure Azure AD eenmalige aanmelding met instructies voor Microsoft hello stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c5b2-150">**tooconfigure Azure AD single sign-on with Directions on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c5b2-151">In Azure-portal op Hallo Hallo **instructies over het Microsoft** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-151">In hello Azure portal, on hello **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4c5b2-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="4c5b2-155">Op Hallo **instructies over het Microsoft-Domain en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-155">On hello **Directions on Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="4c5b2-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-157">a.</span></span> <span data-ttu-id="4c5b2-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="4c5b2-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-159">b.</span></span> <span data-ttu-id="4c5b2-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="4c5b2-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-161">These values are not real.</span></span> <span data-ttu-id="4c5b2-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c5b2-163">Neem contact op met [instructies over het Microsoft Client ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4c5b2-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="4c5b2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c5b2-168">tooconfigure eenmalige aanmelding op **instructies over het Microsoft** zijde, moet u toosend Hallo gedownload **Metadata XML** te[instructies over het Microsoft-ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-168">tooconfigure single sign-on on **Directions on Microsoft** side, you need toosend hello downloaded **Metadata XML** too[Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="4c5b2-169">tooenable hello richtingen op Microsoft ondersteuning voor team toolocate uw federatieve sitelidmaatschap, gegevens van uw bedrijf opnemen in uw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-169">tooenable hello Directions on Microsoft support team toolocate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="4c5b2-170">Eenmalige aanmelding voor instructies over het Microsoft moet toobe ingeschakeld door Hallo [instructies over het Microsoft Client ondersteuningsteam](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-170">Single sign-on for Directions on Microsoft needs toobe enabled by hello [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="4c5b2-171">U ontvangt een melding wanneer eenmalige aanmelding is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="4c5b2-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c5b2-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c5b2-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c5b2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c5b2-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4c5b2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c5b2-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4c5b2-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c5b2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c5b2-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c5b2-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c5b2-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c5b2-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c5b2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c5b2-187">a.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-187">a.</span></span> <span data-ttu-id="4c5b2-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c5b2-189">b.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-189">b.</span></span> <span data-ttu-id="4c5b2-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c5b2-191">c.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-191">c.</span></span> <span data-ttu-id="4c5b2-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4c5b2-193">d.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-193">d.</span></span> <span data-ttu-id="4c5b2-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="4c5b2-195">Maken van een richtingen op Microsoft testgebruiker</span><span class="sxs-lookup"><span data-stu-id="4c5b2-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="4c5b2-196">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooDirections op Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-196">There is no action item for you tooconfigure user provisioning tooDirections on Microsoft.</span></span>  

<span data-ttu-id="4c5b2-197">Wanneer een toegewezen gebruiker probeert toolog in tooDirections op Microsoft met behulp van het toegangsvenster hello, controleert aanwijzingen voor Microsoft of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-197">When an assigned user tries toolog in tooDirections on Microsoft using hello access panel, Directions on Microsoft checks whether hello user exists.</span></span> <span data-ttu-id="4c5b2-198">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door de richtlijnen van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4c5b2-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c5b2-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4c5b2-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDirections op Microsoft toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirections on Microsoft.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4c5b2-202">**tooassign Britta Simon tooDirections op Microsoft, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c5b2-202">**tooassign Britta Simon tooDirections on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c5b2-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4c5b2-205">Selecteer in de lijst met de toepassingen van Hallo **instructies over het Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-205">In hello applications list, select **Directions on Microsoft**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="4c5b2-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4c5b2-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-209">Click **Add** button.</span></span> <span data-ttu-id="4c5b2-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4c5b2-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c5b2-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c5b2-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c5b2-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c5b2-215">Testing single sign-on</span></span>

<span data-ttu-id="4c5b2-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="4c5b2-217">Als u op Hallo instructies over het Microsoft-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour richtingen op Microsoft-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c5b2-217">When you click hello Directions on Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Directions on Microsoft application.</span></span>

<span data-ttu-id="4c5b2-218">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c5b2-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4c5b2-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4c5b2-219">Additional resources</span></span>

* [<span data-ttu-id="4c5b2-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c5b2-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c5b2-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c5b2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

