---
title: 'Zelfstudie: Azure Active Directory-integratie met Anaplan | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Anaplan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 38eb210d090e7aa720060680259124e941e30541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="06bc5-103">Zelfstudie: Azure Active Directory-integratie met Anaplan</span><span class="sxs-lookup"><span data-stu-id="06bc5-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="06bc5-104">In deze zelfstudie leert u hoe toointegrate Anaplan met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06bc5-104">In this tutorial, you learn how toointegrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06bc5-105">Anaplan integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-105">Integrating Anaplan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06bc5-106">U kunt beheren in Azure AD die tooAnaplan toegang heeft</span><span class="sxs-lookup"><span data-stu-id="06bc5-106">You can control in Azure AD who has access tooAnaplan</span></span>
- <span data-ttu-id="06bc5-107">U kunt uw gebruikers tooautomatically get aangemelde tooAnaplan (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="06bc5-107">You can enable your users tooautomatically get signed-on tooAnaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06bc5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="06bc5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="06bc5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06bc5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06bc5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="06bc5-110">Prerequisites</span></span>

<span data-ttu-id="06bc5-111">Azure AD-integratie met Anaplan tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="06bc5-111">tooconfigure Azure AD integration with Anaplan, you need hello following items:</span></span>

- <span data-ttu-id="06bc5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="06bc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06bc5-113">Een Anaplan eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="06bc5-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06bc5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="06bc5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06bc5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06bc5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="06bc5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06bc5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06bc5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06bc5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="06bc5-118">Scenario description</span></span>
<span data-ttu-id="06bc5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="06bc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06bc5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06bc5-121">Het toevoegen van Anaplan van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="06bc5-121">Adding Anaplan from hello gallery</span></span>
2. <span data-ttu-id="06bc5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06bc5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-hello-gallery"></a><span data-ttu-id="06bc5-123">Het toevoegen van Anaplan van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="06bc5-123">Adding Anaplan from hello gallery</span></span>
<span data-ttu-id="06bc5-124">tooconfigure hello integratie van Anaplan in Azure AD, moet u tooadd Anaplan uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="06bc5-124">tooconfigure hello integration of Anaplan into Azure AD, you need tooadd Anaplan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06bc5-125">**tooadd Anaplan via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="06bc5-125">**tooadd Anaplan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="06bc5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06bc5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06bc5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="06bc5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06bc5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="06bc5-133">Typ in het zoekvak Hallo **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-133">In hello search box, type **Anaplan**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="06bc5-135">Selecteer in het deelvenster resultaten hello, **Anaplan**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="06bc5-135">In hello results panel, select **Anaplan**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06bc5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06bc5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06bc5-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Anaplan op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="06bc5-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06bc5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Anaplan is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06bc5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Anaplan is tooa user in Azure AD.</span></span> <span data-ttu-id="06bc5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Anaplan toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="06bc5-140">In other words, a link relationship between an Azure AD user and hello related user in Anaplan needs toobe established.</span></span>

<span data-ttu-id="06bc5-141">Wijs in Anaplan, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="06bc5-141">In Anaplan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06bc5-142">tooconfigure en eenmalige aanmelding Azure AD-test met Anaplan, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-142">tooconfigure and test Azure AD single sign-on with Anaplan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06bc5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="06bc5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06bc5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06bc5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06bc5-145">**[Maken van een testgebruiker Anaplan](#creating-an-anaplan-test-user)**  -toohave een equivalent van Britta Simon in Anaplan die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="06bc5-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - toohave a counterpart of Britta Simon in Anaplan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06bc5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="06bc5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06bc5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="06bc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06bc5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="06bc5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06bc5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Anaplan configureren.</span><span class="sxs-lookup"><span data-stu-id="06bc5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="06bc5-150">**Azure AD tooconfigure eenmalige aanmelding met Anaplan, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="06bc5-150">**tooconfigure Azure AD single sign-on with Anaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc5-151">In de Azure-portal op Hallo Hallo **Anaplan** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-151">In hello Azure portal, on hello **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="06bc5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="06bc5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="06bc5-155">Op Hallo **Anaplan domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-155">On hello **Anaplan Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="06bc5-157">a.</span><span class="sxs-lookup"><span data-stu-id="06bc5-157">a.</span></span> <span data-ttu-id="06bc5-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="06bc5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="06bc5-159">b.</span><span class="sxs-lookup"><span data-stu-id="06bc5-159">b.</span></span> <span data-ttu-id="06bc5-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="06bc5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06bc5-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="06bc5-161">These values are not real.</span></span> <span data-ttu-id="06bc5-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="06bc5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="06bc5-163">Neem contact op met [Anaplan Client ondersteuningsteam](mailto:support@anaplan.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="06bc5-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="06bc5-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="06bc5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="06bc5-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="06bc5-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06bc5-168">Op Hallo **Anaplan configuratie** sectie, klikt u op **configureren Anaplan** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="06bc5-168">On hello **Anaplan Configuration** section, click **Configure Anaplan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="06bc5-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="06bc5-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="06bc5-171">tooconfigure eenmalige aanmelding op **Anaplan** zijde, moet u toosend Hallo gedownload **Metadata XML**, **SAML entiteit-ID**, **SAML Single Sign-On Service-URL**  en **Sign-Out URL** te[Anaplan ondersteuningsteam](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="06bc5-171">tooconfigure single sign-on on **Anaplan** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   too[Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="06bc5-172">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06bc5-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="06bc5-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="06bc5-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06bc5-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="06bc5-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06bc5-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06bc5-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06bc5-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="06bc5-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="06bc5-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="06bc5-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="06bc5-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="06bc5-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc5-180">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="06bc5-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06bc5-182">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06bc5-184">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="06bc5-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06bc5-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="06bc5-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06bc5-188">a.</span><span class="sxs-lookup"><span data-stu-id="06bc5-188">a.</span></span> <span data-ttu-id="06bc5-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06bc5-190">b.</span><span class="sxs-lookup"><span data-stu-id="06bc5-190">b.</span></span> <span data-ttu-id="06bc5-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="06bc5-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06bc5-192">c.</span><span class="sxs-lookup"><span data-stu-id="06bc5-192">c.</span></span> <span data-ttu-id="06bc5-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06bc5-194">d.</span><span class="sxs-lookup"><span data-stu-id="06bc5-194">d.</span></span> <span data-ttu-id="06bc5-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="06bc5-196">Een testgebruiker Anaplan maken</span><span class="sxs-lookup"><span data-stu-id="06bc5-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="06bc5-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Anaplan maken.</span><span class="sxs-lookup"><span data-stu-id="06bc5-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="06bc5-198">Neem contact op met [Anaplan ondersteuningsteam](mailto:support@anaplan.com) tooadd Hallo gebruikers in Hallo Anaplan platform.</span><span class="sxs-lookup"><span data-stu-id="06bc5-198">Please work with [Anaplan support team](mailto:support@anaplan.com) tooadd hello users in hello Anaplan platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06bc5-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="06bc5-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06bc5-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAnaplan toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="06bc5-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnaplan.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="06bc5-202">**tooassign Britta Simon tooAnaplan, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="06bc5-202">**tooassign Britta Simon tooAnaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="06bc5-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="06bc5-205">Selecteer in de lijst met de toepassingen van Hallo **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-205">In hello applications list, select **Anaplan**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="06bc5-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="06bc5-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="06bc5-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="06bc5-209">Click **Add** button.</span></span> <span data-ttu-id="06bc5-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06bc5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="06bc5-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="06bc5-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06bc5-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06bc5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06bc5-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="06bc5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06bc5-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="06bc5-215">Testing single sign-on</span></span>

<span data-ttu-id="06bc5-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="06bc5-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="06bc5-217">Als u op Hallo Anaplan tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Anaplan toepassing.</span><span class="sxs-lookup"><span data-stu-id="06bc5-217">When you click hello Anaplan tile in hello Access Panel, you should get automatically signed-on tooyour Anaplan application.</span></span>

<span data-ttu-id="06bc5-218">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06bc5-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06bc5-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="06bc5-219">Additional resources</span></span>

* [<span data-ttu-id="06bc5-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06bc5-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06bc5-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06bc5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

