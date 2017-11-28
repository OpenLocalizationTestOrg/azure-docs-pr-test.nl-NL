---
title: 'Zelfstudie: Azure Active Directory-integratie met myPolicies | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en myPolicies.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="ffc68-103">Zelfstudie: Azure Active Directory-integratie met myPolicies</span><span class="sxs-lookup"><span data-stu-id="ffc68-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="ffc68-104">In deze zelfstudie leert u hoe toointegrate myPolicies met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ffc68-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ffc68-105">MyPolicies integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ffc68-106">U kunt beheren in Azure AD die toomyPolicies toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ffc68-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="ffc68-107">U kunt uw gebruikers tooautomatically get aangemelde toomyPolicies (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ffc68-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ffc68-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ffc68-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ffc68-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ffc68-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffc68-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ffc68-110">Prerequisites</span></span>

<span data-ttu-id="ffc68-111">Azure AD-integratie met myPolicies tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ffc68-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="ffc68-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ffc68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ffc68-113">Een myPolicies eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ffc68-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ffc68-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ffc68-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ffc68-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ffc68-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ffc68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ffc68-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ffc68-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ffc68-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ffc68-118">Scenario description</span></span>
<span data-ttu-id="ffc68-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ffc68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ffc68-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ffc68-121">Het toevoegen van myPolicies van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ffc68-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="ffc68-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ffc68-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="ffc68-123">Het toevoegen van myPolicies van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ffc68-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="ffc68-124">tooconfigure hello integratie van myPolicies in Azure AD, moet u tooadd myPolicies uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ffc68-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ffc68-125">**tooadd myPolicies via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ffc68-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffc68-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ffc68-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ffc68-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ffc68-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ffc68-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ffc68-133">Typ in het zoekvak Hallo **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-133">In hello search box, type **myPolicies**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="ffc68-135">Selecteer in het deelvenster resultaten hello, **myPolicies**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ffc68-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ffc68-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ffc68-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ffc68-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met myPolicies op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ffc68-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ffc68-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in myPolicies is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffc68-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="ffc68-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in myPolicies toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ffc68-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="ffc68-141">Wijs in myPolicies, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ffc68-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ffc68-142">tooconfigure en eenmalige aanmelding Azure AD-test met myPolicies, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ffc68-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ffc68-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ffc68-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ffc68-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ffc68-145">**[Maken van een testgebruiker myPolicies](#creating-a-mypolicies-test-user)**  -toohave een equivalent van Britta Simon in myPolicies die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ffc68-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ffc68-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ffc68-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ffc68-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ffc68-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ffc68-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ffc68-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ffc68-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing myPolicies configureren.</span><span class="sxs-lookup"><span data-stu-id="ffc68-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="ffc68-150">**Azure AD tooconfigure eenmalige aanmelding met myPolicies, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ffc68-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffc68-151">In de Azure-portal op Hallo Hallo **myPolicies** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ffc68-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ffc68-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="ffc68-155">Op Hallo **myPolicies domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="ffc68-157">a.</span><span class="sxs-lookup"><span data-stu-id="ffc68-157">a.</span></span> <span data-ttu-id="ffc68-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="ffc68-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="ffc68-159">b.</span><span class="sxs-lookup"><span data-stu-id="ffc68-159">b.</span></span> <span data-ttu-id="ffc68-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="ffc68-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ffc68-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ffc68-161">These values are not real.</span></span> <span data-ttu-id="ffc68-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ffc68-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ffc68-163">Neem contact op met [myPolicies ondersteuningsteam](mailto:support@mypolicies.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ffc68-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="ffc68-164">Hallo myPolicies toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="ffc68-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="ffc68-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="ffc68-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ffc68-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ffc68-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ffc68-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ffc68-167">hello following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="ffc68-169">Klik op **weergeven en alle andere gebruikerskenmerken bewerken** checkbox in Hallo **gebruikerskenmerken** sectie tooexpand Hallo kenmerken.</span><span class="sxs-lookup"><span data-stu-id="ffc68-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="ffc68-170">Volgende stappen uit op elke Hallo weergegeven kenmerken - Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ffc68-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="ffc68-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ffc68-171">Attribute Name</span></span> | <span data-ttu-id="ffc68-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ffc68-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="ffc68-173">Voornaam</span><span class="sxs-lookup"><span data-stu-id="ffc68-173">givenname</span></span> | <span data-ttu-id="ffc68-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ffc68-174">user.givenname</span></span> |
    | <span data-ttu-id="ffc68-175">Achternaam</span><span class="sxs-lookup"><span data-stu-id="ffc68-175">surname</span></span> | <span data-ttu-id="ffc68-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="ffc68-176">user.surname</span></span> |
    | <span data-ttu-id="ffc68-177">EmailAddress</span><span class="sxs-lookup"><span data-stu-id="ffc68-177">emailaddress</span></span> | <span data-ttu-id="ffc68-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="ffc68-178">user.mail</span></span> |
    | <span data-ttu-id="ffc68-179">naam</span><span class="sxs-lookup"><span data-stu-id="ffc68-179">name</span></span> | <span data-ttu-id="ffc68-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="ffc68-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="ffc68-181">a.</span><span class="sxs-lookup"><span data-stu-id="ffc68-181">a.</span></span> <span data-ttu-id="ffc68-182">Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ffc68-184">b.</span><span class="sxs-lookup"><span data-stu-id="ffc68-184">b.</span></span> <span data-ttu-id="ffc68-185">Hallo URL waarde verwijderen uit Hallo **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="ffc68-186">c.</span><span class="sxs-lookup"><span data-stu-id="ffc68-186">c.</span></span> <span data-ttu-id="ffc68-187">Klik op **Ok** toosave Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="ffc68-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="ffc68-188">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ffc68-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="ffc68-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ffc68-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ffc68-192">Op Hallo **myPolicies configuratie** sectie, klikt u op **configureren myPolicies** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ffc68-193">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ffc68-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="ffc68-195">tooconfigure eenmalige aanmelding op **myPolicies** zijde, moet u toosend Hallo gedownload **Certificate(Base64)** en **SAML Single Sign-On Service-URL** te[myPolicies ondersteuningsteam](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="ffc68-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ffc68-196">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ffc68-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ffc68-197">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ffc68-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ffc68-198">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ffc68-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ffc68-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ffc68-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="ffc68-200">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ffc68-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ffc68-202">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ffc68-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffc68-203">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ffc68-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ffc68-205">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ffc68-207">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ffc68-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ffc68-209">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ffc68-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ffc68-211">a.</span><span class="sxs-lookup"><span data-stu-id="ffc68-211">a.</span></span> <span data-ttu-id="ffc68-212">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ffc68-213">b.</span><span class="sxs-lookup"><span data-stu-id="ffc68-213">b.</span></span> <span data-ttu-id="ffc68-214">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ffc68-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ffc68-215">c.</span><span class="sxs-lookup"><span data-stu-id="ffc68-215">c.</span></span> <span data-ttu-id="ffc68-216">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ffc68-217">d.</span><span class="sxs-lookup"><span data-stu-id="ffc68-217">d.</span></span> <span data-ttu-id="ffc68-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="ffc68-219">Een testgebruiker myPolicies maken</span><span class="sxs-lookup"><span data-stu-id="ffc68-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="ffc68-220">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in myPolicies maken.</span><span class="sxs-lookup"><span data-stu-id="ffc68-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="ffc68-221">Werken met [myPolicies ondersteuningsteam](mailto:support@mypolicies.com) Hallo gebruikers toevoegen in Hallo myPolicies platform.</span><span class="sxs-lookup"><span data-stu-id="ffc68-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="ffc68-222">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ffc68-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ffc68-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffc68-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ffc68-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen toomyPolicies toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ffc68-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ffc68-226">**tooassign Britta Simon toomyPolicies, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ffc68-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ffc68-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ffc68-229">Selecteer in de lijst met de toepassingen van Hallo **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-229">In hello applications list, select **myPolicies**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="ffc68-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ffc68-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ffc68-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ffc68-233">Click **Add** button.</span></span> <span data-ttu-id="ffc68-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ffc68-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ffc68-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ffc68-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ffc68-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffc68-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ffc68-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ffc68-239">Testing single sign-on</span></span>

<span data-ttu-id="ffc68-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ffc68-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ffc68-241">Als u op Hallo myPolicies-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour myPolicies toepassing.</span><span class="sxs-lookup"><span data-stu-id="ffc68-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="ffc68-242">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ffc68-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ffc68-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ffc68-243">Additional resources</span></span>

* [<span data-ttu-id="ffc68-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffc68-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ffc68-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ffc68-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

