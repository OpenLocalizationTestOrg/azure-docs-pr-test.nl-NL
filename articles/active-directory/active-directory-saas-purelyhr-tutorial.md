---
title: 'Zelfstudie: Azure Active Directory-integratie met PurelyHR | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PurelyHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="a4e0d-103">Zelfstudie: Azure Active Directory-integratie met PurelyHR</span><span class="sxs-lookup"><span data-stu-id="a4e0d-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="a4e0d-104">In deze zelfstudie leert u hoe toointegrate PurelyHR met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4e0d-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4e0d-105">PurelyHR integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a4e0d-106">U kunt beheren in Azure AD die tooPurelyHR toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a4e0d-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="a4e0d-107">U kunt uw gebruikers tooautomatically get aangemelde tooPurelyHR (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a4e0d-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4e0d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a4e0d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a4e0d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4e0d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4e0d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a4e0d-110">Prerequisites</span></span>

<span data-ttu-id="a4e0d-111">Azure AD-integratie met PurelyHR tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="a4e0d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a4e0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4e0d-113">Een PurelyHR eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a4e0d-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4e0d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4e0d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4e0d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4e0d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4e0d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4e0d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a4e0d-118">Scenario description</span></span>
<span data-ttu-id="a4e0d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4e0d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4e0d-121">Het toevoegen van PurelyHR van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a4e0d-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="a4e0d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e0d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="a4e0d-123">Het toevoegen van PurelyHR van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a4e0d-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="a4e0d-124">tooconfigure hello integratie van PurelyHR in Azure AD, moet u tooadd PurelyHR uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4e0d-125">**tooadd PurelyHR via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e0d-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e0d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4e0d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a4e0d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a4e0d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a4e0d-133">Typ in het zoekvak Hallo **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-133">In hello search box, type **PurelyHR**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="a4e0d-135">Selecteer in het deelvenster resultaten hello, **PurelyHR**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4e0d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e0d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4e0d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met PurelyHR op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a4e0d-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a4e0d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PurelyHR is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="a4e0d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PurelyHR toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="a4e0d-141">Wijs in PurelyHR, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a4e0d-142">tooconfigure en eenmalige aanmelding Azure AD-test met PurelyHR, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4e0d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4e0d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4e0d-145">**[Maken van een testgebruiker PurelyHR](#creating-a-purelyhr-test-user)**  -toohave een equivalent van Britta Simon in PurelyHR die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4e0d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4e0d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4e0d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a4e0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4e0d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PurelyHR configureren.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="a4e0d-150">**Azure AD tooconfigure eenmalige aanmelding met PurelyHR, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e0d-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e0d-151">In de Azure-portal op Hallo Hallo **PurelyHR** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a4e0d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="a4e0d-155">Op Hallo **PurelyHR domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="a4e0d-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="a4e0d-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="a4e0d-158">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="a4e0d-160">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="a4e0d-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="a4e0d-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-161">These values are not hello real.</span></span> <span data-ttu-id="a4e0d-162">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a4e0d-163">Neem contact op met [PurelyHR Client ondersteuningsteam](http://support.purelyhr.com/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="a4e0d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="a4e0d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a4e0d-168">Op Hallo **PurelyHR configuratie** sectie, klikt u op **configureren PurelyHR** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a4e0d-169">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a4e0d-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="a4e0d-171">tooconfigure eenmalige aanmelding op **PurelyHR** side, aanmelding tootheir website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="a4e0d-172">Open Hallo **Dashboard** uit Hallo-opties in het Hallo-werkbalk en klikt u op **SSO instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="a4e0d-173">Hallo-waarden in de vakken Hallo als plakken beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="a4e0d-173">Paste hello values in hello boxes as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="a4e0d-175">a.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-175">a.</span></span> <span data-ttu-id="a4e0d-176">Open Hallo **Certificate(Bas64)** gedownload van hello Azure-portal in Kladblok en kopieer Hallo certificaat waarde.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="a4e0d-177">Plakken Hallo waarde gekopieerd naar Hallo **X.509-certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="a4e0d-178">b.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-178">b.</span></span> <span data-ttu-id="a4e0d-179">In Hallo **URL-verlener Idp** vak, plak Hallo **SAML entiteit-ID** gekopieerd van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="a4e0d-180">c.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-180">c.</span></span> <span data-ttu-id="a4e0d-181">In Hallo **Idp eindpunt-URL** vak, plak Hallo **SAML Single Sign-On Service-URL** gekopieerd van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="a4e0d-182">d.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-182">d.</span></span> <span data-ttu-id="a4e0d-183">Controleer de Hallo **gebruikers automatisch maken** selectievakje tooenable automatisch gebruikers inrichten in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="a4e0d-184">e.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-184">e.</span></span> <span data-ttu-id="a4e0d-185">Klik op **wijzigingen opslaan** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="a4e0d-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a4e0d-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a4e0d-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a4e0d-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4e0d-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a4e0d-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4e0d-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a4e0d-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e0d-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e0d-193">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4e0d-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4e0d-197">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4e0d-199">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4e0d-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4e0d-201">a.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-201">a.</span></span> <span data-ttu-id="a4e0d-202">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4e0d-203">b.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-203">b.</span></span> <span data-ttu-id="a4e0d-204">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4e0d-205">c.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-205">c.</span></span> <span data-ttu-id="a4e0d-206">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a4e0d-207">d.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-207">d.</span></span> <span data-ttu-id="a4e0d-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="a4e0d-209">Een testgebruiker PurelyHR maken</span><span class="sxs-lookup"><span data-stu-id="a4e0d-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="a4e0d-210">Azure AD tooenable gebruikers toolog in tooPurelyHR, ze in PurelyHR moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="a4e0d-211">Inrichting is een automatische taak in PurelyHR, en zijn geen handmatige stappen vereist wanneer de Automatische gebruikersaanvragen is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4e0d-212">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4e0d-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a4e0d-213">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPurelyHR toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a4e0d-215">**tooassign Britta Simon tooPurelyHR, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a4e0d-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4e0d-216">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a4e0d-218">Selecteer in de lijst met de toepassingen van Hallo **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="a4e0d-220">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a4e0d-222">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-222">Click **Add** button.</span></span> <span data-ttu-id="a4e0d-223">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a4e0d-225">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a4e0d-226">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4e0d-227">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4e0d-228">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a4e0d-228">Testing single sign-on</span></span>

<span data-ttu-id="a4e0d-229">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a4e0d-230">Hallo kunnen LMS-tegel in Hallo paneel voor Apptoegang, klikt u op dat u automatisch aangemelde tooyour kunnen LMS toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="a4e0d-231">Zie voor meer informatie over Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a4e0d-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="a4e0d-232">[Inleiding toohello Toegangspaneel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a4e0d-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4e0d-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a4e0d-233">Additional resources</span></span>

* [<span data-ttu-id="a4e0d-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4e0d-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4e0d-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4e0d-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

