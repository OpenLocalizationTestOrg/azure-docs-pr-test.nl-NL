---
title: 'Zelfstudie: Azure Active Directory-integratie met Weekdone | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Weekdone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="27d67-103">Zelfstudie: Azure Active Directory-integratie met Weekdone</span><span class="sxs-lookup"><span data-stu-id="27d67-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="27d67-104">In deze zelfstudie leert u hoe toointegrate Weekdone met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27d67-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27d67-105">Weekdone integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="27d67-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27d67-106">U kunt beheren in Azure AD die tooWeekdone toegang heeft</span><span class="sxs-lookup"><span data-stu-id="27d67-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="27d67-107">U kunt uw gebruikers tooautomatically get aangemelde tooWeekdone (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="27d67-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27d67-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="27d67-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27d67-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27d67-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27d67-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="27d67-110">Prerequisites</span></span>

<span data-ttu-id="27d67-111">Azure AD-integratie met Weekdone tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="27d67-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="27d67-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="27d67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27d67-113">Een Weekdone eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="27d67-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27d67-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="27d67-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27d67-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="27d67-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27d67-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="27d67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27d67-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27d67-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27d67-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="27d67-118">Scenario description</span></span>
<span data-ttu-id="27d67-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="27d67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27d67-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="27d67-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27d67-121">Het toevoegen van Weekdone van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="27d67-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="27d67-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="27d67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="27d67-123">Het toevoegen van Weekdone van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="27d67-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="27d67-124">tooconfigure hello integratie van Weekdone in Azure AD, moet u tooadd Weekdone uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="27d67-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27d67-125">**tooadd Weekdone via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="27d67-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d67-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="27d67-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27d67-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="27d67-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27d67-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="27d67-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="27d67-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27d67-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="27d67-133">Typ in het zoekvak Hallo **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="27d67-133">In hello search box, type **Weekdone**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="27d67-135">Selecteer in het deelvenster resultaten hello, **Weekdone**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="27d67-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27d67-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="27d67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27d67-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Weekdone op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="27d67-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27d67-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Weekdone is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27d67-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="27d67-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Weekdone toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="27d67-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="27d67-141">Wijs in Weekdone, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="27d67-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27d67-142">tooconfigure en eenmalige aanmelding Azure AD-test met Weekdone, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d67-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27d67-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="27d67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27d67-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27d67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27d67-145">**[Maken van een testgebruiker Weekdone](#creating-a-weekdone-test-user)**  -toohave een equivalent van Britta Simon in Weekdone die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="27d67-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27d67-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="27d67-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27d67-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="27d67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27d67-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="27d67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27d67-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Weekdone configureren.</span><span class="sxs-lookup"><span data-stu-id="27d67-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="27d67-150">**Azure AD tooconfigure eenmalige aanmelding met Weekdone, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="27d67-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d67-151">In de Azure-portal op Hallo Hallo **Weekdone** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="27d67-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="27d67-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="27d67-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="27d67-155">Op Hallo **Weekdone domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="27d67-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="27d67-157">a.</span><span class="sxs-lookup"><span data-stu-id="27d67-157">a.</span></span> <span data-ttu-id="27d67-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="27d67-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="27d67-159">b.</span><span class="sxs-lookup"><span data-stu-id="27d67-159">b.</span></span> <span data-ttu-id="27d67-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="27d67-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="27d67-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="27d67-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="27d67-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="27d67-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="27d67-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="27d67-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="27d67-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="27d67-165">These values are not real.</span></span> <span data-ttu-id="27d67-166">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="27d67-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="27d67-167">Neem contact op met [Weekdone Client ondersteuningsteam](mailto:hello@weekdone.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="27d67-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="27d67-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="27d67-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="27d67-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="27d67-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="27d67-172">Op Hallo **Weekdone configuratie** sectie, klikt u op **configureren Weekdone** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="27d67-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27d67-173">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="27d67-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="27d67-175">tooconfigure eenmalige aanmelding op **Weekdone** zijde, moet u toosend Hallo gedownload **Metadata XML, Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Weekdone-ondersteuning team](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="27d67-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="27d67-176">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="27d67-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27d67-177">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="27d67-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27d67-178">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27d67-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27d67-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="27d67-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="27d67-180">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="27d67-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="27d67-182">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="27d67-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d67-183">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="27d67-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27d67-185">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="27d67-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27d67-187">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="27d67-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27d67-189">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="27d67-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27d67-191">a.</span><span class="sxs-lookup"><span data-stu-id="27d67-191">a.</span></span> <span data-ttu-id="27d67-192">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27d67-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27d67-193">b.</span><span class="sxs-lookup"><span data-stu-id="27d67-193">b.</span></span> <span data-ttu-id="27d67-194">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27d67-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27d67-195">c.</span><span class="sxs-lookup"><span data-stu-id="27d67-195">c.</span></span> <span data-ttu-id="27d67-196">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="27d67-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27d67-197">d.</span><span class="sxs-lookup"><span data-stu-id="27d67-197">d.</span></span> <span data-ttu-id="27d67-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="27d67-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="27d67-199">Een testgebruiker Weekdone maken</span><span class="sxs-lookup"><span data-stu-id="27d67-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="27d67-200">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Weekdone van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="27d67-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="27d67-201">Weekdone ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="27d67-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="27d67-202">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="27d67-202">There is no action item for you in this section.</span></span> <span data-ttu-id="27d67-203">Een nieuwe gebruiker wordt tijdens een poging tooaccess Weekdone gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="27d67-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="27d67-204">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Weekdone Client ondersteuningsteam](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="27d67-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27d67-205">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d67-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27d67-206">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWeekdone toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="27d67-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="27d67-208">**tooassign Britta Simon tooWeekdone, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="27d67-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d67-209">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="27d67-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="27d67-211">Selecteer in de lijst met de toepassingen van Hallo **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="27d67-211">In hello applications list, select **Weekdone**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="27d67-213">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="27d67-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="27d67-215">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="27d67-215">Click **Add** button.</span></span> <span data-ttu-id="27d67-216">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27d67-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="27d67-218">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="27d67-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27d67-219">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27d67-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27d67-220">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="27d67-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27d67-221">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="27d67-221">Testing single sign-on</span></span>

<span data-ttu-id="27d67-222">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="27d67-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="27d67-223">Als u op Hallo Weekdone tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Weekdone toepassing.</span><span class="sxs-lookup"><span data-stu-id="27d67-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27d67-224">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="27d67-224">Additional resources</span></span>

* [<span data-ttu-id="27d67-225">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27d67-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27d67-226">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27d67-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

