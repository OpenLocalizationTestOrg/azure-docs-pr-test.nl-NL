---
title: 'Zelfstudie: Azure Active Directory-integratie met OfficeSpace Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en OfficeSpace Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="b7a47-103">Zelfstudie: Azure Active Directory-integratie met OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="b7a47-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="b7a47-104">In deze zelfstudie leert u hoe toointegrate OfficeSpace Software met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7a47-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7a47-105">OfficeSpace Software integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7a47-106">U kunt beheren in Azure AD die toegang tooOfficeSpace Software heeft.</span><span class="sxs-lookup"><span data-stu-id="b7a47-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="b7a47-107">U kunt uw gebruikers tooautomatically get aangemelde tooOfficeSpace Software (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b7a47-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b7a47-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b7a47-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b7a47-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7a47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a47-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7a47-110">Prerequisites</span></span>

<span data-ttu-id="b7a47-111">Azure AD-integratie met OfficeSpace Software tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b7a47-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="b7a47-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b7a47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7a47-113">Een OfficeSpace Software eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b7a47-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7a47-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7a47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7a47-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7a47-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b7a47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7a47-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7a47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7a47-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b7a47-118">Scenario description</span></span>
<span data-ttu-id="b7a47-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7a47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7a47-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7a47-121">Het toevoegen van OfficeSpace Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b7a47-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="b7a47-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b7a47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="b7a47-123">Het toevoegen van OfficeSpace Software van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b7a47-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="b7a47-124">tooconfigure hello integratie van OfficeSpace Software in Azure AD, moet u tooadd OfficeSpace Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b7a47-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7a47-125">**tooadd OfficeSpace Software uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7a47-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7a47-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b7a47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="b7a47-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7a47-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="b7a47-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="b7a47-133">Typ in het zoekvak Hallo **OfficeSpace Software**, selecteer **OfficeSpace Software** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b7a47-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met zoekresultaten OfficeSpace Software in Hallo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b7a47-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a47-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b7a47-136">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met OfficeSpace Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b7a47-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7a47-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in OfficeSpace Software is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7a47-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="b7a47-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in OfficeSpace Software toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b7a47-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="b7a47-139">In OfficeSpace Software, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b7a47-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b7a47-140">tooconfigure en test eenmalige aanmelding Azure AD met OfficeSpace Software, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7a47-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b7a47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7a47-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7a47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7a47-143">**[Maak een testgebruiker OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave een equivalent van Britta Simon in OfficeSpace-Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b7a47-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7a47-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b7a47-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7a47-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b7a47-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b7a47-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b7a47-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b7a47-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b7a47-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="b7a47-148">**Voer tooconfigure Azure AD eenmalige aanmelding met OfficeSpace Software Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7a47-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7a47-149">In de Azure-portal op Hallo Hallo **OfficeSpace Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b7a47-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b7a47-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="b7a47-153">Op Hallo **OfficeSpace Software domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en OfficeSpace Software domein eenmalige aanmelding informatie](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="b7a47-155">a.</span><span class="sxs-lookup"><span data-stu-id="b7a47-155">a.</span></span> <span data-ttu-id="b7a47-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="b7a47-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="b7a47-157">b.</span><span class="sxs-lookup"><span data-stu-id="b7a47-157">b.</span></span> <span data-ttu-id="b7a47-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="b7a47-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b7a47-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b7a47-159">These values are not real.</span></span> <span data-ttu-id="b7a47-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="b7a47-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b7a47-161">Neem contact op met [OfficeSpace Software Client ondersteuningsteam](mailto:support@officespacesoftware.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b7a47-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="b7a47-162">Hallo SAML asserties verwacht OfficeSpace softwaretoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="b7a47-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b7a47-163">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="b7a47-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="b7a47-164">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="b7a47-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b7a47-165">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b7a47-165">hello following screenshot shows an example for this.</span></span>
    
    ![Kenmerk configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="b7a47-167">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **user.mail** als **gebruikers-id** en voor elke rij die wordt weergegeven Voer in Hallo onderstaande tabel Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="b7a47-168">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b7a47-168">Attribute Name</span></span> | <span data-ttu-id="b7a47-169">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b7a47-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b7a47-170">E-mail</span><span class="sxs-lookup"><span data-stu-id="b7a47-170">email</span></span> | <span data-ttu-id="b7a47-171">User.mail</span><span class="sxs-lookup"><span data-stu-id="b7a47-171">user.mail</span></span> |
    | <span data-ttu-id="b7a47-172">naam</span><span class="sxs-lookup"><span data-stu-id="b7a47-172">name</span></span> | <span data-ttu-id="b7a47-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="b7a47-173">user.displayname</span></span> |
    | <span data-ttu-id="b7a47-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="b7a47-174">first_name</span></span> | <span data-ttu-id="b7a47-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b7a47-175">user.givenname</span></span> |
    | <span data-ttu-id="b7a47-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="b7a47-176">last_name</span></span> | <span data-ttu-id="b7a47-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="b7a47-177">user.surname</span></span> |

    <span data-ttu-id="b7a47-178">a.</span><span class="sxs-lookup"><span data-stu-id="b7a47-178">a.</span></span> <span data-ttu-id="b7a47-179">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="b7a47-180">Configureer toevoegen</span><span class="sxs-lookup"><span data-stu-id="b7a47-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Kenmerk configureren](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b7a47-182">b.</span><span class="sxs-lookup"><span data-stu-id="b7a47-182">b.</span></span> <span data-ttu-id="b7a47-183">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b7a47-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b7a47-184">c.</span><span class="sxs-lookup"><span data-stu-id="b7a47-184">c.</span></span> <span data-ttu-id="b7a47-185">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b7a47-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b7a47-186">d.</span><span class="sxs-lookup"><span data-stu-id="b7a47-186">d.</span></span> <span data-ttu-id="b7a47-187">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="b7a47-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="b7a47-188">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="b7a47-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="b7a47-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b7a47-190">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b7a47-192">Op Hallo **OfficeSpace softwareconfiguratie** sectie, klikt u op **OfficeSpace Software configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b7a47-193">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b7a47-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![De softwareconfiguratie voor OfficeSpace](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="b7a47-195">Meld u aan bij uw tenant OfficeSpace Software als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="b7a47-196">Ga te**instellingen** en klik op **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-196">Go too**Settings** and click **Connectors**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="b7a47-198">Klik op **SAML-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-198">Click **SAML Authentication**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="b7a47-200">In Hallo **SAML-verificatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="b7a47-202">a.</span><span class="sxs-lookup"><span data-stu-id="b7a47-202">a.</span></span> <span data-ttu-id="b7a47-203">In Hallo **afmelding provider url** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b7a47-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b7a47-204">b.</span><span class="sxs-lookup"><span data-stu-id="b7a47-204">b.</span></span> <span data-ttu-id="b7a47-205">In Hallo **Client idp doel-url** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b7a47-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b7a47-206">c.</span><span class="sxs-lookup"><span data-stu-id="b7a47-206">c.</span></span> <span data-ttu-id="b7a47-207">Plakken Hallo **vingerafdruk** waarde die u hebt gekopieerd vanuit Azure-portal in Hallo **Client IDP certificaat vingerafdruk** textbox.</span><span class="sxs-lookup"><span data-stu-id="b7a47-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="b7a47-208">d.</span><span class="sxs-lookup"><span data-stu-id="b7a47-208">d.</span></span> <span data-ttu-id="b7a47-209">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="b7a47-210">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b7a47-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7a47-211">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b7a47-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7a47-212">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7a47-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7a47-213">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b7a47-213">Create an Azure AD test user</span></span>

<span data-ttu-id="b7a47-214">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b7a47-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b7a47-216">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7a47-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7a47-217">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b7a47-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b7a47-219">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b7a47-221">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b7a47-223">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7a47-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b7a47-225">a.</span><span class="sxs-lookup"><span data-stu-id="b7a47-225">a.</span></span> <span data-ttu-id="b7a47-226">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7a47-227">b.</span><span class="sxs-lookup"><span data-stu-id="b7a47-227">b.</span></span> <span data-ttu-id="b7a47-228">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="b7a47-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b7a47-229">c.</span><span class="sxs-lookup"><span data-stu-id="b7a47-229">c.</span></span> <span data-ttu-id="b7a47-230">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b7a47-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b7a47-231">d.</span><span class="sxs-lookup"><span data-stu-id="b7a47-231">d.</span></span> <span data-ttu-id="b7a47-232">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="b7a47-233">Een testgebruiker OfficeSpace Software maken</span><span class="sxs-lookup"><span data-stu-id="b7a47-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="b7a47-234">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in OfficeSpace Software van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b7a47-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="b7a47-235">OfficeSpace Software ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b7a47-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b7a47-236">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="b7a47-236">There is no action item for you in this section.</span></span> <span data-ttu-id="b7a47-237">Een nieuwe gebruiker wordt tijdens een poging tooaccess OfficeSpace Software gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b7a47-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="b7a47-238">Als u een gebruiker toocreate handmatig nodig hebt, moet u tooContact [OfficeSpace Software ondersteuningsteam](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="b7a47-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b7a47-239">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7a47-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b7a47-240">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b7a47-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="b7a47-242">**tooassign Britta Simon tooOfficeSpace Software, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b7a47-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7a47-243">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b7a47-245">Selecteer in de lijst met de toepassingen van Hallo **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Hallo OfficeSpace Software koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="b7a47-247">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b7a47-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="b7a47-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b7a47-249">Click **Add** button.</span></span> <span data-ttu-id="b7a47-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="b7a47-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7a47-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7a47-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7a47-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7a47-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b7a47-255">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b7a47-255">Test single sign-on</span></span>

<span data-ttu-id="b7a47-256">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b7a47-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7a47-257">Als u op Hallo OfficeSpace Software-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour OfficeSpace softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="b7a47-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7a47-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b7a47-258">Additional resources</span></span>

* [<span data-ttu-id="b7a47-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7a47-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7a47-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7a47-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

