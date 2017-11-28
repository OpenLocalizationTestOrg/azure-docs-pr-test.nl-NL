---
title: 'Zelfstudie: Azure Active Directory-integratie met Kindling | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kindling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="e75c8-103">Zelfstudie: Azure Active Directory-integratie met Kindling</span><span class="sxs-lookup"><span data-stu-id="e75c8-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="e75c8-104">In deze zelfstudie leert u hoe toointegrate Kindling met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e75c8-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e75c8-105">Kindling integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e75c8-106">U kunt beheren in Azure AD die tooKindling toegang heeft</span><span class="sxs-lookup"><span data-stu-id="e75c8-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="e75c8-107">U kunt uw gebruikers tooautomatically get aangemelde tooKindling (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e75c8-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e75c8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e75c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e75c8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="e75c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e75c8-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e75c8-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e75c8-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e75c8-111">Prerequisites</span></span>

<span data-ttu-id="e75c8-112">tooconfigure Azure AD-integratie met Kindling, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e75c8-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="e75c8-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e75c8-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e75c8-114">Een Kindling eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e75c8-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e75c8-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e75c8-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e75c8-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e75c8-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e75c8-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e75c8-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e75c8-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e75c8-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e75c8-119">Scenario description</span></span>
<span data-ttu-id="e75c8-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e75c8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e75c8-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e75c8-122">Het toevoegen van Kindling van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e75c8-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="e75c8-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e75c8-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="e75c8-124">Het toevoegen van Kindling van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e75c8-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="e75c8-125">tooconfigure hello integratie van Kindling met Azure AD, moet u tooadd Kindling uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e75c8-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e75c8-126">**tooadd Kindling uit de galerie hello, Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e75c8-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e75c8-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e75c8-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e75c8-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e75c8-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e75c8-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e75c8-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e75c8-134">Typ in het zoekvak Hallo **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-134">In hello search box, type **Kindling**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="e75c8-136">Selecteer in het deelvenster resultaten hello, **Kindling**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e75c8-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e75c8-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e75c8-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e75c8-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Kindling op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e75c8-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e75c8-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kindling is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e75c8-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="e75c8-141">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kindling behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e75c8-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="e75c8-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Kindling.</span><span class="sxs-lookup"><span data-stu-id="e75c8-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="e75c8-143">tooconfigure en eenmalige aanmelding Azure AD-test met Kindling, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e75c8-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e75c8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e75c8-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e75c8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e75c8-146">**[Maken van een testgebruiker Kindling](#creating-a-kindling-test-user)**  -toohave een equivalent van Britta Simon in die Kindling toohello Azure AD-weergave van de gebruiker gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e75c8-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e75c8-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e75c8-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e75c8-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e75c8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e75c8-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e75c8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e75c8-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kindling configureren.</span><span class="sxs-lookup"><span data-stu-id="e75c8-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="e75c8-151">**tooconfigure eenmalige aanmelding Azure AD met Kindling, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e75c8-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="e75c8-152">In de Azure-portal op Hallo Hallo **Kindling** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e75c8-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e75c8-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="e75c8-156">Op Hallo **Kindling domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="e75c8-158">a.</span><span class="sxs-lookup"><span data-stu-id="e75c8-158">a.</span></span> <span data-ttu-id="e75c8-159">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="e75c8-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="e75c8-160">b.</span><span class="sxs-lookup"><span data-stu-id="e75c8-160">b.</span></span>  <span data-ttu-id="e75c8-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="e75c8-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e75c8-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="e75c8-162">These values are not hello real.</span></span> <span data-ttu-id="e75c8-163">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="e75c8-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="e75c8-164">Neem contact op met [Kindling ondersteuningsteam](mailto:support@kindlingapp.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e75c8-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="e75c8-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e75c8-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="e75c8-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e75c8-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e75c8-169">Op Hallo **Kindling configuratie** sectie, klikt u op **configureren Kindling** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e75c8-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e75c8-170">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e75c8-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="e75c8-172">tooconfigure eenmalige aanmelding op **Kindling** zijde, moet u toosend Hallo gedownload **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**te[Kindling ondersteuningsteam](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="e75c8-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="e75c8-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e75c8-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e75c8-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e75c8-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e75c8-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e75c8-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e75c8-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e75c8-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="e75c8-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e75c8-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e75c8-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e75c8-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e75c8-180">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e75c8-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e75c8-182">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e75c8-184">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e75c8-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e75c8-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e75c8-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e75c8-188">a.</span><span class="sxs-lookup"><span data-stu-id="e75c8-188">a.</span></span> <span data-ttu-id="e75c8-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e75c8-190">b.</span><span class="sxs-lookup"><span data-stu-id="e75c8-190">b.</span></span> <span data-ttu-id="e75c8-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e75c8-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e75c8-192">c.</span><span class="sxs-lookup"><span data-stu-id="e75c8-192">c.</span></span> <span data-ttu-id="e75c8-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e75c8-194">d.</span><span class="sxs-lookup"><span data-stu-id="e75c8-194">d.</span></span> <span data-ttu-id="e75c8-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="e75c8-196">Een testgebruiker Kindling maken</span><span class="sxs-lookup"><span data-stu-id="e75c8-196">Creating a Kindling test user</span></span>

<span data-ttu-id="e75c8-197">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Kindling van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e75c8-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="e75c8-198">Kindling ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="e75c8-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="e75c8-199">U hebt al ingeschakeld in [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e75c8-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="e75c8-200">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="e75c8-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e75c8-201">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e75c8-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e75c8-202">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKindling toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e75c8-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e75c8-204">**tooassign Britta Simon tooKindling, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e75c8-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="e75c8-205">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e75c8-207">Selecteer in de lijst met de toepassingen van Hallo **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-207">In hello applications list, select **Kindling**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="e75c8-209">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e75c8-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e75c8-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e75c8-211">Click **Add** button.</span></span> <span data-ttu-id="e75c8-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e75c8-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e75c8-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e75c8-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e75c8-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e75c8-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e75c8-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e75c8-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e75c8-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e75c8-217">Testing single sign-on</span></span>

<span data-ttu-id="e75c8-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e75c8-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e75c8-219">Als u op Hallo Kindling tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kindling toepassing.</span><span class="sxs-lookup"><span data-stu-id="e75c8-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e75c8-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e75c8-220">Additional resources</span></span>

* [<span data-ttu-id="e75c8-221">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e75c8-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e75c8-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e75c8-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

