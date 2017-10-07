---
title: 'Zelfstudie: Azure Active Directory-integratie met 8 x 8 virtuele Office | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 8 x 8 virtuele Office.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="c1bf9-103">Zelfstudie: Azure Active Directory-integratie met 8 x 8 virtuele Office</span><span class="sxs-lookup"><span data-stu-id="c1bf9-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="c1bf9-104">In deze zelfstudie leert u hoe toointegrate 8 x 8 virtuele Office met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1bf9-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1bf9-105">Integratie van 8 x 8 virtuele Office met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1bf9-106">U kunt beheren in Azure AD wie toegang tot too8x8 heeft virtuele Office</span><span class="sxs-lookup"><span data-stu-id="c1bf9-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="c1bf9-107">U kunt uw gebruikers in staat om tooautomatically aangemelde too8x8 virtuele Office (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c1bf9-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1bf9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c1bf9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c1bf9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1bf9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1bf9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c1bf9-110">Prerequisites</span></span>

<span data-ttu-id="c1bf9-111">Azure AD-integratie met 8 x 8 virtuele Office tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="c1bf9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c1bf9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1bf9-113">Een 8 x 8 virtuele Office eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c1bf9-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1bf9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1bf9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1bf9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1bf9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1bf9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1bf9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c1bf9-118">Scenario description</span></span>
<span data-ttu-id="c1bf9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1bf9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1bf9-121">Het toevoegen van 8 x 8 virtuele Office van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c1bf9-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="c1bf9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1bf9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="c1bf9-123">Het toevoegen van 8 x 8 virtuele Office van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c1bf9-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="c1bf9-124">tooconfigure hello integratie van 8 x 8 virtuele Office in Azure AD, moet u tooadd 8 x 8 virtuele Office uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1bf9-125">**tooadd 8 x 8 virtuele Office via Hallo gallery uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="c1bf9-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1bf9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1bf9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1bf9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c1bf9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c1bf9-133">Typ in het zoekvak Hallo **8 x 8 virtuele Office**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="c1bf9-135">Selecteer in het deelvenster resultaten hello, **8 x 8 virtuele Office**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1bf9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1bf9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1bf9-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met 8 x 8 die virtuele Office op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c1bf9-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c1bf9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 8 x 8 virtuele Office is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="c1bf9-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in 8 x 8 moet virtuele Office toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="c1bf9-141">In Office 8 x 8 virtuele Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c1bf9-142">tooconfigure en test eenmalige aanmelding Azure AD met 8 x 8 virtuele Office, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1bf9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1bf9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1bf9-145">**[Maken van een testgebruiker van 8 x 8 virtuele Office](#creating-a-8x8-virtual-office-test-user)**  -toohave een equivalent van Britta Simon in 8 x 8 virtuele Office dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1bf9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1bf9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1bf9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c1bf9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1bf9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw 8 x 8 virtuele Office-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="c1bf9-150">**tooconfigure eenmalige aanmelding Azure AD met 8 x 8 virtuele kantoor, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1bf9-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1bf9-151">In de Azure-portal op Hallo Hallo **8 x 8 virtuele Office** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c1bf9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="c1bf9-155">Op Hallo **8 x 8 virtuele Office domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="c1bf9-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-157">a.</span></span> <span data-ttu-id="c1bf9-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="c1bf9-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="c1bf9-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="c1bf9-160">b.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-160">b.</span></span> <span data-ttu-id="c1bf9-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="c1bf9-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="c1bf9-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1bf9-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-163">These values are not real.</span></span> <span data-ttu-id="c1bf9-164">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c1bf9-165">Neem contact op met [8 x 8 virtuele Office ondersteuningsteam](https://www.8x8.com/about-us/contact-us) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="c1bf9-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="c1bf9-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1bf9-170">Op Hallo **8 x 8 virtuele Office-configuratie** sectie, klikt u op **configureren 8 x 8 virtuele Office** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c1bf9-171">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c1bf9-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="c1bf9-173">Eenmalige aanmelding tooyour 8 x 8 virtuele Office tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="c1bf9-174">Selecteer **virtuele Office Account Mgr** in deelvenster van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="c1bf9-176">Selecteer **Business** toomanage account en klik op **aanmelden** knop.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="c1bf9-178">Klik op **Accounts** tabblad in de lijst van Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="c1bf9-180">Klik op **eenmalige aanmelding** in Hallo-lijst van Accounts.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="c1bf9-182">Selecteer **eenmalige aanmelding** onder verificatiemethode en op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="c1bf9-184">Kopiëren **SAML SSO URL**, **Sing uit Service-URL met eenmalige** en **URL-verlener** van Azure AD te**aanmelding In URL**, **afmeldings-URL**  en **URL-verlener** in 8 x 8 virtuele Office.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="c1bf9-186">Klik op **Browser** tooupload Hallo certificaat dat u hebt gedownload van Azure AD en klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c1bf9-187">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c1bf9-188">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c1bf9-189">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1bf9-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1bf9-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c1bf9-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1bf9-191">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c1bf9-193">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1bf9-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1bf9-194">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1bf9-196">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1bf9-198">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1bf9-200">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1bf9-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1bf9-202">a.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-202">a.</span></span> <span data-ttu-id="c1bf9-203">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1bf9-204">b.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-204">b.</span></span> <span data-ttu-id="c1bf9-205">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1bf9-206">c.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-206">c.</span></span> <span data-ttu-id="c1bf9-207">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1bf9-208">d.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-208">d.</span></span> <span data-ttu-id="c1bf9-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="c1bf9-210">Maken van een 8 x 8 virtuele Office-testgebruiker</span><span class="sxs-lookup"><span data-stu-id="c1bf9-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="c1bf9-211">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in 8 x 8 virtuele Office van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="c1bf9-212">8 x 8 virtuele Office ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c1bf9-213">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-213">There is no action item for you in this section.</span></span> <span data-ttu-id="c1bf9-214">Een nieuwe gebruiker wordt gemaakt tijdens een poging tooaccess 8 x 8 virtuele Office als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="c1bf9-215">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [8 x 8 virtuele Office ondersteuningsteam](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="c1bf9-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1bf9-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1bf9-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1bf9-217">In deze sectie, schakelt u Britta Simon toouse Azure eenmalige aanmelding verleent toegang tot virtuele Office too8x8.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c1bf9-219">**tooassign Britta Simon too8x8 virtuele kantoor, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c1bf9-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1bf9-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c1bf9-222">Selecteer in de lijst met de toepassingen van Hallo **8 x 8 virtuele Office**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="c1bf9-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c1bf9-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-226">Click **Add** button.</span></span> <span data-ttu-id="c1bf9-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c1bf9-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1bf9-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1bf9-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1bf9-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c1bf9-232">Testing single sign-on</span></span>

<span data-ttu-id="c1bf9-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1bf9-234">Als u op Hallo 8 x 8 virtuele Office-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour 8 x 8 virtuele Office-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1bf9-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="c1bf9-235">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangsvenster](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c1bf9-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1bf9-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c1bf9-236">Additional resources</span></span>

* [<span data-ttu-id="c1bf9-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1bf9-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1bf9-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1bf9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

