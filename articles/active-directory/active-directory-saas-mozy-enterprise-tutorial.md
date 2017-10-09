---
title: 'Zelfstudie: Azure Active Directory-integratie met Mozy Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="7938c-103">Zelfstudie: Azure Active Directory-integratie met Mozy voor ondernemingen</span><span class="sxs-lookup"><span data-stu-id="7938c-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="7938c-104">In deze zelfstudie leert u hoe toointegrate Mozy Enterprise met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7938c-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7938c-105">Mozy-onderneming integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7938c-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7938c-106">U kunt beheren in Azure AD wie toegang tot tooMozy Enterprise heeft</span><span class="sxs-lookup"><span data-stu-id="7938c-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="7938c-107">U kunt uw gebruikers tooautomatically get aangemelde tooMozy Enterprise (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7938c-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7938c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7938c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7938c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7938c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7938c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7938c-110">Prerequisites</span></span>

<span data-ttu-id="7938c-111">tooconfigure Azure AD-integratie met Mozy voor ondernemingen, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7938c-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="7938c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7938c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7938c-113">Een Mozy Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7938c-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7938c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7938c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7938c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7938c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7938c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7938c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7938c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7938c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7938c-118">Scenario description</span></span>
<span data-ttu-id="7938c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7938c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7938c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7938c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7938c-121">Het toevoegen van Mozy Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7938c-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="7938c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7938c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="7938c-123">Het toevoegen van Mozy Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7938c-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="7938c-124">tooconfigure hello integratie van Mozy Enterprise in Azure AD, moet u tooadd Mozy Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7938c-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7938c-125">**tooadd Mozy Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7938c-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7938c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7938c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7938c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7938c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7938c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7938c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7938c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7938c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7938c-133">Typ in het zoekvak Hallo **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="7938c-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="7938c-135">Selecteer in het deelvenster resultaten hello, **Mozy Enterprise**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7938c-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7938c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7938c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7938c-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Mozy ondernemingen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7938c-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7938c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de onderneming Mozy is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7938c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="7938c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de onderneming Mozy Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7938c-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="7938c-141">In de onderneming Mozy, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7938c-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7938c-142">tooconfigure en test eenmalige aanmelding Azure AD met Mozy voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7938c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7938c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7938c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7938c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7938c-145">**[Maken van een testgebruiker Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave een equivalent van Britta Simon in Mozy onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7938c-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7938c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7938c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7938c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7938c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7938c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7938c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7938c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7938c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="7938c-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Mozy Enterprise, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7938c-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="7938c-151">In de Azure-portal op Hallo Hallo **Mozy Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7938c-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7938c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7938c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="7938c-155">Op Hallo **Mozy Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="7938c-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="7938c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7938c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="7938c-158">This value is not real.</span></span> <span data-ttu-id="7938c-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="7938c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7938c-160">Neem contact op met [Mozy Enterprise Client ondersteuningsteam](http://support.mozy.com/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="7938c-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="7938c-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7938c-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="7938c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7938c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7938c-165">Op Hallo **Mozy Ondernemingsconfiguratie** sectie, klikt u op **configureren Mozy Enterprise** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7938c-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7938c-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7938c-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="7938c-168">In een ander browservenster, meld u bij uw bedrijf Mozy Enterprise site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7938c-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="7938c-169">In Hallo **configuratie** sectie, klikt u op **verificatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="7938c-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="7938c-170">![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "verificatiebeleid")</span><span class="sxs-lookup"><span data-stu-id="7938c-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="7938c-171">Op Hallo **verificatiebeleid** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="7938c-172">![Verificatiebeleid](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "verificatiebeleid")</span><span class="sxs-lookup"><span data-stu-id="7938c-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="7938c-173">a.</span><span class="sxs-lookup"><span data-stu-id="7938c-173">a.</span></span> <span data-ttu-id="7938c-174">Selecteer **adreslijstservice** als **Provider**.</span><span class="sxs-lookup"><span data-stu-id="7938c-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="7938c-175">b.</span><span class="sxs-lookup"><span data-stu-id="7938c-175">b.</span></span> <span data-ttu-id="7938c-176">Selecteer **Gebruik LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="7938c-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="7938c-177">c.</span><span class="sxs-lookup"><span data-stu-id="7938c-177">c.</span></span> <span data-ttu-id="7938c-178">Klik op Hallo **SAML-verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7938c-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="7938c-179">d.</span><span class="sxs-lookup"><span data-stu-id="7938c-179">d.</span></span> <span data-ttu-id="7938c-180">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **-URL voor webverificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="7938c-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="7938c-181">e.</span><span class="sxs-lookup"><span data-stu-id="7938c-181">e.</span></span> <span data-ttu-id="7938c-182">Plakken **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML-eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="7938c-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="7938c-183">f.</span><span class="sxs-lookup"><span data-stu-id="7938c-183">f.</span></span> <span data-ttu-id="7938c-184">De gedownloade base-64 gecodeerde certificaat Open in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **SAML certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="7938c-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="7938c-185">g.</span><span class="sxs-lookup"><span data-stu-id="7938c-185">g.</span></span> <span data-ttu-id="7938c-186">Selecteer **eenmalige aanmelding inschakelen voor beheerders toolog met hun netwerkreferenties**.</span><span class="sxs-lookup"><span data-stu-id="7938c-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="7938c-187">h.</span><span class="sxs-lookup"><span data-stu-id="7938c-187">h.</span></span> <span data-ttu-id="7938c-188">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7938c-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7938c-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7938c-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7938c-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7938c-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7938c-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7938c-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7938c-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7938c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7938c-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7938c-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7938c-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7938c-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7938c-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7938c-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7938c-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7938c-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7938c-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7938c-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7938c-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7938c-204">a.</span><span class="sxs-lookup"><span data-stu-id="7938c-204">a.</span></span> <span data-ttu-id="7938c-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7938c-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7938c-206">b.</span><span class="sxs-lookup"><span data-stu-id="7938c-206">b.</span></span> <span data-ttu-id="7938c-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7938c-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7938c-208">c.</span><span class="sxs-lookup"><span data-stu-id="7938c-208">c.</span></span> <span data-ttu-id="7938c-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7938c-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7938c-210">d.</span><span class="sxs-lookup"><span data-stu-id="7938c-210">d.</span></span> <span data-ttu-id="7938c-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7938c-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="7938c-212">Maken van een testgebruiker Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="7938c-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="7938c-213">In volgorde tooenable Azure AD gebruikers toolog in Mozy onderneming, moeten ze worden ingericht in Mozy onderneming.</span><span class="sxs-lookup"><span data-stu-id="7938c-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="7938c-214">In geval van Mozy onderneming Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="7938c-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="7938c-215">U kunt andere Mozy Enterprise gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Mozy Enterprise tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7938c-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="7938c-216">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="7938c-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7938c-217">Meld u bij tooyour **Mozy Enterprise** tenant.</span><span class="sxs-lookup"><span data-stu-id="7938c-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="7938c-218">Klik op **gebruikers**, en klik vervolgens op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7938c-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="7938c-219">![Gebruikers](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="7938c-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7938c-220">Hallo **nieuwe gebruiker toevoegen** optie wordt alleen weergegeven als **Mozy** is geselecteerd als de provider Hallo onder **verificatiebeleid**.</span><span class="sxs-lookup"><span data-stu-id="7938c-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="7938c-221">Als SAML-verificatie is geconfigureerd, worden klikt u vervolgens Hallo gebruikers automatisch toegevoegd op de eerste aanmelding via eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="7938c-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="7938c-222">Uitvoeren op de nieuwe gebruikersdialoogvenster Hallo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7938c-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="7938c-223">![Gebruikers toevoegen](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="7938c-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="7938c-224">a.</span><span class="sxs-lookup"><span data-stu-id="7938c-224">a.</span></span> <span data-ttu-id="7938c-225">Van Hallo **kiest u een groep** , selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="7938c-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="7938c-226">b.</span><span class="sxs-lookup"><span data-stu-id="7938c-226">b.</span></span> <span data-ttu-id="7938c-227">Van Hallo **wat voor soort gebruiker** , selecteert u een type.</span><span class="sxs-lookup"><span data-stu-id="7938c-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="7938c-228">c.</span><span class="sxs-lookup"><span data-stu-id="7938c-228">c.</span></span> <span data-ttu-id="7938c-229">In Hallo **gebruikersnaam** textbox Hallo typenaam van hello Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7938c-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="7938c-230">d.</span><span class="sxs-lookup"><span data-stu-id="7938c-230">d.</span></span> <span data-ttu-id="7938c-231">In Hallo **e** textbox type Hallo e-mailadres van hello Azure AD-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7938c-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="7938c-232">e.</span><span class="sxs-lookup"><span data-stu-id="7938c-232">e.</span></span> <span data-ttu-id="7938c-233">Selecteer **gebruiker instructie e-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="7938c-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="7938c-234">f.</span><span class="sxs-lookup"><span data-stu-id="7938c-234">f.</span></span> <span data-ttu-id="7938c-235">Klik op **toevoegen van gebruiker (s)**.</span><span class="sxs-lookup"><span data-stu-id="7938c-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="7938c-236">Na het maken van Hallo gebruiker een e-mailbericht verzonden toohello Azure AD-gebruiker met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="7938c-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7938c-237">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7938c-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7938c-238">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7938c-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7938c-240">**tooassign Britta Simon tooMozy Enterprise, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7938c-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="7938c-241">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7938c-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7938c-243">Selecteer in de lijst met de toepassingen van Hallo **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="7938c-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="7938c-245">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7938c-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7938c-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7938c-247">Click **Add** button.</span></span> <span data-ttu-id="7938c-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7938c-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7938c-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7938c-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7938c-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7938c-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7938c-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7938c-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7938c-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7938c-253">Testing single sign-on</span></span>

<span data-ttu-id="7938c-254">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7938c-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7938c-255">Als u op Hallo Mozy Enterprise-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina Mozy bedrijfstoepassing.</span><span class="sxs-lookup"><span data-stu-id="7938c-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="7938c-256">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7938c-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7938c-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7938c-257">Additional resources</span></span>

* [<span data-ttu-id="7938c-258">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7938c-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7938c-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7938c-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

