---
title: 'Zelfstudie: Azure Active Directory-integratie met IQNavigator VMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="d0423-103">Zelfstudie: Azure Active Directory-integratie met IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="d0423-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="d0423-104">In deze zelfstudie leert u hoe toointegrate IQNavigator VMS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0423-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0423-105">IQNavigator VMS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d0423-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0423-106">U kunt beheren in Azure AD wie toegang tot tooIQNavigator virtuele machines heeft</span><span class="sxs-lookup"><span data-stu-id="d0423-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="d0423-107">U kunt uw gebruikers tooautomatically get aangemelde tooIQNavigator VMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d0423-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0423-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d0423-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0423-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0423-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0423-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d0423-110">Prerequisites</span></span>

<span data-ttu-id="d0423-111">Azure AD-integratie met IQNavigator VMS tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d0423-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="d0423-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d0423-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0423-113">Een IQNavigator VMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d0423-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0423-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d0423-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0423-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d0423-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0423-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d0423-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0423-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0423-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0423-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d0423-118">Scenario description</span></span>
<span data-ttu-id="d0423-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d0423-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0423-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d0423-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0423-121">Het toevoegen van IQNavigator VMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d0423-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="d0423-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0423-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="d0423-123">Het toevoegen van IQNavigator VMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d0423-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="d0423-124">tooconfigure hello integratie van IQNavigator VMS in Azure AD, moet u tooadd IQNavigator VMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d0423-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0423-125">**tooadd IQNavigator VMS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d0423-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0423-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d0423-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0423-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0423-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0423-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0423-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d0423-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0423-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d0423-133">Typ in het zoekvak Hallo **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="d0423-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="d0423-135">Selecteer in het deelvenster resultaten hello, **IQNavigator VMS**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0423-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0423-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0423-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0423-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD IQNavigator VMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d0423-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0423-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in IQNavigator VMS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0423-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="d0423-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in IQNavigator VMS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d0423-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="d0423-141">In IQNavigator VMS, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d0423-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0423-142">tooconfigure en test eenmalige aanmelding Azure AD IQNavigator VMS, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0423-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0423-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d0423-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0423-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0423-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0423-145">**[Maken van een testgebruiker IQNavigator VMS](#creating-a-iqnavigator-vms-test-user)**  -toohave een equivalent van Britta Simon in IQNavigator VMS die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d0423-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0423-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d0423-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0423-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d0423-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0423-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d0423-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0423-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing IQNavigator VMS configureren.</span><span class="sxs-lookup"><span data-stu-id="d0423-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="d0423-150">**Azure AD tooconfigure eenmalige aanmelding met IQNavigator VMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d0423-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0423-151">In de Azure-portal op Hallo Hallo **IQNavigator VMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d0423-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d0423-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d0423-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="d0423-155">Op Hallo **IQNavigator VMS domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0423-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="d0423-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0423-157">a.</span></span> <span data-ttu-id="d0423-158">In Hallo **id** textbox type Hallo URL:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="d0423-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="d0423-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0423-159">b.</span></span> <span data-ttu-id="d0423-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="d0423-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="d0423-161">Controleer **weergeven geavanceerde instellingen voor URL**, Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d0423-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="d0423-163">In Hallo **Relay-status** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="d0423-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0423-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d0423-164">These values are not real.</span></span> <span data-ttu-id="d0423-165">Deze waarden met de huidige antwoord-URL en de Relay status Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d0423-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="d0423-166">Neem contact op met [IQNavigator VMS Client ondersteuningsteam](https://www.beeline.com/iqn-product-support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d0423-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="d0423-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d0423-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0423-169">Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="d0423-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="d0423-170">a.</span><span class="sxs-lookup"><span data-stu-id="d0423-170">a.</span></span> <span data-ttu-id="d0423-171">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="d0423-171">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="d0423-173">b.</span><span class="sxs-lookup"><span data-stu-id="d0423-173">b.</span></span> <span data-ttu-id="d0423-174">Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0423-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="d0423-176">c.</span><span class="sxs-lookup"><span data-stu-id="d0423-176">c.</span></span> <span data-ttu-id="d0423-177">Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="d0423-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="d0423-179">d.</span><span class="sxs-lookup"><span data-stu-id="d0423-179">d.</span></span> <span data-ttu-id="d0423-180">Ga nu toohello eigenschappenpagina van **IQNavigator VMS** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="d0423-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="d0423-182">e.</span><span class="sxs-lookup"><span data-stu-id="d0423-182">e.</span></span> <span data-ttu-id="d0423-183">Hallo genereren **metagegevens-URL** met Hallo patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d0423-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="d0423-184">IQNavigator toepassing hello unieke gebruikers-id-waarde in Hallo-naam-id claim verwacht.</span><span class="sxs-lookup"><span data-stu-id="d0423-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="d0423-185">De klant kunt Hallo correcte waarde voor het Hallo-naam-id claim toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d0423-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="d0423-186">In dit geval hebben we Hallo gebruiker toegewezen. UserPrincipalName voor Hallo demo doel.</span><span class="sxs-lookup"><span data-stu-id="d0423-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="d0423-187">Maar tooyour op basis van organisatie-instellingen moet u de juiste waarde Hallo voor toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d0423-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="d0423-189">Op Hallo **IQNavigator VMS configuratie** sectie, klikt u op **IQNavigator virtuele machines configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d0423-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d0423-190">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d0423-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="d0423-192">tooconfigure eenmalige aanmelding op **IQNavigator VMS** clientzijde, moet u toosend hello **metagegevens-URL**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te [IQNavigator VMS ondersteuningsteam](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="d0423-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="d0423-193">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d0423-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d0423-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d0423-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0423-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d0423-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0423-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0423-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0423-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d0423-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0423-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d0423-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d0423-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d0423-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0423-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d0423-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0423-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d0423-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0423-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d0423-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0423-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d0423-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0423-209">a.</span><span class="sxs-lookup"><span data-stu-id="d0423-209">a.</span></span> <span data-ttu-id="d0423-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0423-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0423-211">b.</span><span class="sxs-lookup"><span data-stu-id="d0423-211">b.</span></span> <span data-ttu-id="d0423-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0423-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0423-213">c.</span><span class="sxs-lookup"><span data-stu-id="d0423-213">c.</span></span> <span data-ttu-id="d0423-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d0423-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0423-215">d.</span><span class="sxs-lookup"><span data-stu-id="d0423-215">d.</span></span> <span data-ttu-id="d0423-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0423-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="d0423-217">Een testgebruiker IQNavigator VMS maken</span><span class="sxs-lookup"><span data-stu-id="d0423-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="d0423-218">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in IQNavigator VMS van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d0423-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="d0423-219">Werken met [IQNavigator VMS ondersteuningsteam](https://www.beeline.com/iqn-product-support/) tooadd Hallo gebruikers in Hallo IQNavigator VMS-account.</span><span class="sxs-lookup"><span data-stu-id="d0423-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0423-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0423-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0423-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooIQNavigator virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="d0423-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d0423-223">**tooassign Britta Simon tooIQNavigator virtuele machines, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d0423-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0423-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0423-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d0423-226">Selecteer in de lijst met de toepassingen van Hallo **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="d0423-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="d0423-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d0423-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d0423-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d0423-230">Click **Add** button.</span></span> <span data-ttu-id="d0423-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0423-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d0423-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d0423-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0423-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0423-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0423-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0423-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0423-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0423-236">Testing single sign-on</span></span>

<span data-ttu-id="d0423-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d0423-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0423-238">Als u op Hallo IQNavigator VMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour IQNavigator VMS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0423-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="d0423-239">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0423-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0423-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d0423-240">Additional resources</span></span>

* [<span data-ttu-id="d0423-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0423-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0423-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0423-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

