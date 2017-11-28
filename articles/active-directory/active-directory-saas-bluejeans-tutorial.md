---
title: 'Zelfstudie: Azure Active Directory-integratie met BlueJeans | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="e9fdb-103">Zelfstudie: Azure Active Directory-integratie met BlueJeans</span><span class="sxs-lookup"><span data-stu-id="e9fdb-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="e9fdb-104">In deze zelfstudie leert u hoe toointegrate BlueJeans met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9fdb-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9fdb-105">BlueJeans integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9fdb-106">U kunt beheren in Azure AD die tooBlueJeans toegang heeft</span><span class="sxs-lookup"><span data-stu-id="e9fdb-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="e9fdb-107">U kunt uw gebruikers tooautomatically get aangemelde tooBlueJeans (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e9fdb-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9fdb-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e9fdb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e9fdb-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9fdb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9fdb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e9fdb-110">Prerequisites</span></span>

<span data-ttu-id="e9fdb-111">Azure AD-integratie met BlueJeans tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="e9fdb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e9fdb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9fdb-113">Een BlueJeans eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e9fdb-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9fdb-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9fdb-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9fdb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9fdb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9fdb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9fdb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e9fdb-118">Scenario description</span></span>
<span data-ttu-id="e9fdb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9fdb-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9fdb-121">Het toevoegen van BlueJeans van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e9fdb-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="e9fdb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e9fdb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="e9fdb-123">Het toevoegen van BlueJeans van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e9fdb-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="e9fdb-124">tooconfigure hello integratie van BlueJeans in Azure AD, moet u tooadd BlueJeans uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9fdb-125">**tooadd BlueJeans via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9fdb-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9fdb-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9fdb-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e9fdb-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e9fdb-133">Typ in het zoekvak Hallo **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-133">In hello search box, type **BlueJeans**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="e9fdb-135">Selecteer in het deelvenster resultaten hello, **BlueJeans**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9fdb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e9fdb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9fdb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BlueJeans op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e9fdb-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e9fdb-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BlueJeans is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="e9fdb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BlueJeans toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="e9fdb-141">Wijs in BlueJeans, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9fdb-142">tooconfigure en eenmalige aanmelding Azure AD-test met BlueJeans, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9fdb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9fdb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9fdb-145">**[Maken van een testgebruiker BlueJeans](#creating-a-bluejeans-test-user)**  -toohave een equivalent van Britta Simon in BlueJeans die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9fdb-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9fdb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9fdb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e9fdb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9fdb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BlueJeans configureren.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="e9fdb-150">**Azure AD tooconfigure eenmalige aanmelding met BlueJeans, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9fdb-151">In de Azure-portal op Hallo Hallo **BlueJeans** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e9fdb-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="e9fdb-155">Op Hallo **BlueJeans domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="e9fdb-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-157">a.</span></span> <span data-ttu-id="e9fdb-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="e9fdb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="e9fdb-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-159">b.</span></span> <span data-ttu-id="e9fdb-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="e9fdb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9fdb-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-161">These values are not real.</span></span> <span data-ttu-id="e9fdb-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9fdb-163">Neem contact op met [BlueJeans Client ondersteuningsteam](https://support.bluejeans.com/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="e9fdb-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="e9fdb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9fdb-168">Op Hallo **BlueJeans configuratie** sectie, klikt u op **configureren BlueJeans** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e9fdb-169">Kopiëren Hallo **Sign-Out-URL, de URL van wijzigen wachtwoord en de SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="e9fdb-171">Aanmelden in een ander browservenster tooyour **BlueJeans** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="e9fdb-172">Ga te**ADMIN \> groepsinstellingen \> beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="e9fdb-173">![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="e9fdb-174">In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e9fdb-175">![SAML voor eenmalige aanmelding](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML voor eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="e9fdb-176">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-176">a.</span></span> <span data-ttu-id="e9fdb-177">Selecteer **SAML voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="e9fdb-178">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-178">b.</span></span> <span data-ttu-id="e9fdb-179">Selecteer **automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="e9fdb-180">Verplaatsen op Hello stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="e9fdb-181">![Pad van het certificaat](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "pad van het certificaat")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="e9fdb-182">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-182">a.</span></span> <span data-ttu-id="e9fdb-183">Klik op **bestand kiezen**, en vervolgens Hallo gedownload certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="e9fdb-184">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-184">b.</span></span> <span data-ttu-id="e9fdb-185">Plakken **SAML Single Sign-On Service-URL** in Hallo **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="e9fdb-186">c.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-186">c.</span></span> <span data-ttu-id="e9fdb-187">Plakken **URL van wijzigen wachtwoord** in Hallo **URL voor wachtwoord wijzigen** textbox.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="e9fdb-188">d.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-188">d.</span></span> <span data-ttu-id="e9fdb-189">Plakken **Sign-Out URL** in Hallo **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="e9fdb-190">Verplaatsen op Hello stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="e9fdb-191">![Wijzigingen opslaan](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "wijzigingen opslaan")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="e9fdb-192">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-192">a.</span></span> <span data-ttu-id="e9fdb-193">In Hallo **gebruikers-id** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="e9fdb-194">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-194">b.</span></span> <span data-ttu-id="e9fdb-195">In Hallo **e** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="e9fdb-196">c.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-196">c.</span></span> <span data-ttu-id="e9fdb-197">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e9fdb-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9fdb-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9fdb-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9fdb-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9fdb-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e9fdb-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9fdb-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e9fdb-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9fdb-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9fdb-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9fdb-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9fdb-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9fdb-213">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-213">a.</span></span> <span data-ttu-id="e9fdb-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9fdb-215">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-215">b.</span></span> <span data-ttu-id="e9fdb-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9fdb-217">c.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-217">c.</span></span> <span data-ttu-id="e9fdb-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e9fdb-219">d.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-219">d.</span></span> <span data-ttu-id="e9fdb-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="e9fdb-221">Een testgebruiker BlueJeans maken</span><span class="sxs-lookup"><span data-stu-id="e9fdb-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="e9fdb-222">Azure AD tooenable gebruikers toolog in tooBlueJeans, ze in BlueJeans moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="e9fdb-223">In geval van een BlueJeans is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="e9fdb-224">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9fdb-225">Meld u bij tooyour **BlueJeans** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="e9fdb-226">Ga te**ADMIN \> gebruikers beheren \> gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="e9fdb-227">![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="e9fdb-228">Hallo **gebruiker toevoegen** tabblad is alleen beschikbaar als in Hallo **tabblad Beveiliging**, **automatische inrichting inschakelen** is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="e9fdb-229">In Hallo **gebruiker toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9fdb-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="e9fdb-230">![Gebruiker toevoegen](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="e9fdb-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="e9fdb-231">a.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-231">a.</span></span> <span data-ttu-id="e9fdb-232">Typ een **BlueJeans gebruikersnaam**, een **e-mailadres**, een **BlueJeans vergadering ID**, een **beheerder wachtwoordcode**, een **volledige naam** , Hallo **bedrijf** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="e9fdb-233">b.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-233">b.</span></span> <span data-ttu-id="e9fdb-234">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="e9fdb-235">U kunt andere BlueJeans gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door BlueJeans tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e9fdb-236">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9fdb-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e9fdb-237">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBlueJeans toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e9fdb-239">**tooassign Britta Simon tooBlueJeans, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e9fdb-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9fdb-240">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e9fdb-242">Selecteer in de lijst met de toepassingen van Hallo **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="e9fdb-244">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e9fdb-246">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-246">Click **Add** button.</span></span> <span data-ttu-id="e9fdb-247">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e9fdb-249">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9fdb-250">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9fdb-251">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9fdb-252">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e9fdb-252">Testing single sign-on</span></span>

<span data-ttu-id="e9fdb-253">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e9fdb-254">Als u op Hallo BlueJeans-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van BlueJeans toepassing.</span><span class="sxs-lookup"><span data-stu-id="e9fdb-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="e9fdb-255">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9fdb-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9fdb-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e9fdb-256">Additional resources</span></span>

* [<span data-ttu-id="e9fdb-257">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9fdb-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9fdb-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9fdb-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

