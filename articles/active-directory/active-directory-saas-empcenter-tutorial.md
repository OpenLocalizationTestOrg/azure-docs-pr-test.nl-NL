---
title: 'Zelfstudie: Azure Active Directory-integratie met EmpCenter | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en EmpCenter.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: cce5d86db550327eb73660fb78cea7e6d5428890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="d97e5-103">Zelfstudie: Azure Active Directory-integratie met EmpCenter</span><span class="sxs-lookup"><span data-stu-id="d97e5-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="d97e5-104">In deze zelfstudie leert u hoe toointegrate EmpCenter met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d97e5-104">In this tutorial, you learn how toointegrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d97e5-105">EmpCenter integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-105">Integrating EmpCenter with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d97e5-106">U kunt beheren in Azure AD die tooEmpCenter toegang heeft</span><span class="sxs-lookup"><span data-stu-id="d97e5-106">You can control in Azure AD who has access tooEmpCenter</span></span>
- <span data-ttu-id="d97e5-107">U kunt uw gebruikers tooautomatically get aangemelde tooEmpCenter (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d97e5-107">You can enable your users tooautomatically get signed-on tooEmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d97e5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d97e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d97e5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d97e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d97e5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d97e5-110">Prerequisites</span></span>

<span data-ttu-id="d97e5-111">Azure AD-integratie met EmpCenter tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d97e5-111">tooconfigure Azure AD integration with EmpCenter, you need hello following items:</span></span>

- <span data-ttu-id="d97e5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d97e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d97e5-113">Een EmpCenter eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d97e5-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d97e5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d97e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d97e5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d97e5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d97e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d97e5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d97e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d97e5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d97e5-118">Scenario description</span></span>
<span data-ttu-id="d97e5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d97e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d97e5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d97e5-121">Het toevoegen van EmpCenter van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d97e5-121">Adding EmpCenter from hello gallery</span></span>
2. <span data-ttu-id="d97e5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d97e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-hello-gallery"></a><span data-ttu-id="d97e5-123">Het toevoegen van EmpCenter van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d97e5-123">Adding EmpCenter from hello gallery</span></span>
<span data-ttu-id="d97e5-124">tooconfigure hello integratie van EmpCenter in Azure AD, moet u tooadd EmpCenter uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d97e5-124">tooconfigure hello integration of EmpCenter into Azure AD, you need tooadd EmpCenter from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d97e5-125">**tooadd EmpCenter via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d97e5-125">**tooadd EmpCenter from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97e5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d97e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d97e5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d97e5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d97e5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d97e5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d97e5-133">Typ in het zoekvak Hallo **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-133">In hello search box, type **EmpCenter**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="d97e5-135">Selecteer in het deelvenster resultaten hello, **EmpCenter**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d97e5-135">In hello results panel, select **EmpCenter**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d97e5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d97e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d97e5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met EmpCenter op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d97e5-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d97e5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in EmpCenter is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d97e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EmpCenter is tooa user in Azure AD.</span></span> <span data-ttu-id="d97e5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in EmpCenter toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d97e5-140">In other words, a link relationship between an Azure AD user and hello related user in EmpCenter needs toobe established.</span></span>

<span data-ttu-id="d97e5-141">Wijs in EmpCenter, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d97e5-141">In EmpCenter, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d97e5-142">tooconfigure en eenmalige aanmelding Azure AD-test met EmpCenter, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-142">tooconfigure and test Azure AD single sign-on with EmpCenter, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d97e5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d97e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d97e5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d97e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d97e5-145">**[Maken van een testgebruiker EmpCenter](#creating-an-empcenter-test-user)**  -toohave een equivalent van Britta Simon in EmpCenter die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d97e5-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - toohave a counterpart of Britta Simon in EmpCenter that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d97e5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d97e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d97e5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d97e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d97e5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d97e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d97e5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing EmpCenter configureren.</span><span class="sxs-lookup"><span data-stu-id="d97e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="d97e5-150">**Azure AD tooconfigure eenmalige aanmelding met EmpCenter, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d97e5-150">**tooconfigure Azure AD single sign-on with EmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97e5-151">In de Azure-portal op Hallo Hallo **EmpCenter** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-151">In hello Azure portal, on hello **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d97e5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d97e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="d97e5-155">Op Hallo **EmpCenter domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-155">On hello **EmpCenter Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="d97e5-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="d97e5-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="d97e5-158">hello value is not real.</span></span> <span data-ttu-id="d97e5-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="d97e5-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d97e5-160">Neem contact op met [EmpCenter Client ondersteuningsteam](http://www.workforcesoftware.com/services/customer-support/) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="d97e5-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="d97e5-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d97e5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="d97e5-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d97e5-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d97e5-165">tooconfigure eenmalige aanmelding op **EmpCenter** zijde, moet u toosend Hallo gedownload **Metadata XML** te[EmpCenter ondersteuningsteam](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="d97e5-165">tooconfigure single sign-on on **EmpCenter** side, you need toosend hello downloaded **Metadata XML** too[EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="d97e5-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d97e5-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d97e5-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d97e5-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d97e5-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d97e5-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d97e5-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d97e5-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d97e5-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d97e5-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d97e5-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d97e5-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d97e5-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d97e5-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97e5-174">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d97e5-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d97e5-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d97e5-178">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d97e5-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d97e5-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d97e5-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d97e5-182">a.</span><span class="sxs-lookup"><span data-stu-id="d97e5-182">a.</span></span> <span data-ttu-id="d97e5-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d97e5-184">b.</span><span class="sxs-lookup"><span data-stu-id="d97e5-184">b.</span></span> <span data-ttu-id="d97e5-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d97e5-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d97e5-186">c.</span><span class="sxs-lookup"><span data-stu-id="d97e5-186">c.</span></span> <span data-ttu-id="d97e5-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d97e5-188">d.</span><span class="sxs-lookup"><span data-stu-id="d97e5-188">d.</span></span> <span data-ttu-id="d97e5-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="d97e5-190">Een testgebruiker EmpCenter maken</span><span class="sxs-lookup"><span data-stu-id="d97e5-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="d97e5-191">In de volgorde tooenable Azure AD gebruikers toolog in tooEmpCenter, moeten ze worden ingericht in EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d97e5-191">In order tooenable Azure AD users toolog in tooEmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="d97e5-192">In geval van EmpCenter Hallo Hallo-gebruikersaccounts moeten toobe gemaakt door uw [EmpCenter ondersteuningsteam](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="d97e5-192">In hello case of EmpCenter, hello user accounts need toobe created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="d97e5-193">U kunt andere EmpCenter gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door EmpCenter tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="d97e5-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter tooprovision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d97e5-194">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97e5-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d97e5-195">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEmpCenter toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="d97e5-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEmpCenter.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d97e5-197">**tooassign Britta Simon tooEmpCenter, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d97e5-197">**tooassign Britta Simon tooEmpCenter, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97e5-198">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d97e5-200">Selecteer in de lijst met de toepassingen van Hallo **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-200">In hello applications list, select **EmpCenter**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="d97e5-202">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d97e5-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d97e5-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d97e5-204">Click **Add** button.</span></span> <span data-ttu-id="d97e5-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d97e5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d97e5-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d97e5-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d97e5-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d97e5-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d97e5-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d97e5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d97e5-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d97e5-210">Testing single sign-on</span></span>


<span data-ttu-id="d97e5-211">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="d97e5-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d97e5-212">Als u op Hallo EmpCenter tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour EmpCenter toepassing.</span><span class="sxs-lookup"><span data-stu-id="d97e5-212">When you click hello EmpCenter tile in hello Access Panel, you should get automatically signed-on tooyour EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d97e5-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d97e5-213">Additional resources</span></span>

* [<span data-ttu-id="d97e5-214">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d97e5-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d97e5-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d97e5-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

