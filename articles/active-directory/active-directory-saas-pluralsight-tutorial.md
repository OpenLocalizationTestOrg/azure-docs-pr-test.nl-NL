---
title: 'Zelfstudie: Azure Active Directory-integratie met Pluralsight | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Pluralsight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="aa119-103">Zelfstudie: Azure Active Directory-integratie met Pluralsight</span><span class="sxs-lookup"><span data-stu-id="aa119-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="aa119-104">In deze zelfstudie leert u hoe toointegrate Pluralsight met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa119-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa119-105">Pluralsight integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="aa119-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa119-106">U kunt beheren in Azure AD die tooPluralsight toegang heeft</span><span class="sxs-lookup"><span data-stu-id="aa119-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="aa119-107">U kunt uw gebruikers tooautomatically get aangemelde tooPluralsight (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="aa119-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa119-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="aa119-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa119-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa119-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa119-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa119-110">Prerequisites</span></span>

<span data-ttu-id="aa119-111">Azure AD-integratie met Pluralsight tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="aa119-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="aa119-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="aa119-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa119-113">Een Pluralsight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="aa119-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa119-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="aa119-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa119-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="aa119-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa119-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="aa119-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa119-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa119-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa119-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="aa119-118">Scenario description</span></span>
<span data-ttu-id="aa119-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="aa119-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa119-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="aa119-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa119-121">Het toevoegen van Pluralsight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="aa119-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="aa119-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa119-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="aa119-123">Het toevoegen van Pluralsight van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="aa119-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="aa119-124">tooconfigure hello integratie van Pluralsight in Azure AD, moet u tooadd Pluralsight uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="aa119-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa119-125">**tooadd Pluralsight via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aa119-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa119-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aa119-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa119-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa119-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa119-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa119-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="aa119-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="aa119-133">Typ in het zoekvak Hallo **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="aa119-133">In hello search box, type **Pluralsight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="aa119-135">Selecteer in het deelvenster resultaten hello, **Pluralsight**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa119-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa119-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa119-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa119-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Pluralsight op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="aa119-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa119-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Pluralsight is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa119-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="aa119-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Pluralsight toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="aa119-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="aa119-141">Wijs in Pluralsight, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="aa119-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aa119-142">tooconfigure en eenmalige aanmelding Azure AD-test met Pluralsight, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa119-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa119-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="aa119-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa119-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa119-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa119-145">**[Maken van een testgebruiker Pluralsight](#creating-a-pluralsight-test-user)**  -toohave een equivalent van Britta Simon in Pluralsight die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa119-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa119-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aa119-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa119-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="aa119-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa119-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="aa119-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa119-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Pluralsight configureren.</span><span class="sxs-lookup"><span data-stu-id="aa119-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="aa119-150">**Azure AD tooconfigure eenmalige aanmelding met Pluralsight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aa119-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa119-151">In de Azure-portal op Hallo Hallo **Pluralsight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="aa119-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="aa119-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aa119-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="aa119-155">Op Hallo **Pluralsight domein en de URL's** sectie, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="aa119-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="aa119-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="aa119-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa119-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="aa119-158">This value is not real.</span></span> <span data-ttu-id="aa119-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="aa119-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="aa119-160">Neem contact op met [Pluralsight Client ondersteuningsteam](mailto:support@pluralsight.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="aa119-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="aa119-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="aa119-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="aa119-163">Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in hello Azure-portal en tooconfigure SSO in Hallo Pluralsight toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa119-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="aa119-164">Hallo Pluralsight toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="aa119-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="aa119-165">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="aa119-165">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="aa119-167">U kunt ook toevoegen Hallo **'Unieke ID'** kenmerk met de Hallo geschikte waarde zoals werknemer-id of iets anders dat tegemoetkomt aan voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="aa119-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="aa119-168">Let ook op dit is niet het vereiste kenmerk Hallo; echter, u kunt deze toevoegen Hallo unieke gebruikers te identificeren.</span><span class="sxs-lookup"><span data-stu-id="aa119-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="aa119-169">tooadd hello vereist **SAML-token kenmerken**, Voer voor elke rij die wordt weergegeven in onderstaande tabel voor hello, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa119-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="aa119-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="aa119-170">Attribute Name</span></span> | <span data-ttu-id="aa119-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="aa119-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="aa119-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="aa119-172">First Name</span></span> |<span data-ttu-id="aa119-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="aa119-173">user.givenname</span></span> |
   | <span data-ttu-id="aa119-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="aa119-174">Last Name</span></span> |<span data-ttu-id="aa119-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="aa119-175">user.surname</span></span> |
   | <span data-ttu-id="aa119-176">E-mail</span><span class="sxs-lookup"><span data-stu-id="aa119-176">Email</span></span> |<span data-ttu-id="aa119-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="aa119-177">user.mail</span></span> |
   
   <span data-ttu-id="aa119-178">a.</span><span class="sxs-lookup"><span data-stu-id="aa119-178">a.</span></span> <span data-ttu-id="aa119-179">Klik op **gebruikerskenmerk toevoegen** tooopen hello **toevoegen gebruiker Attribure** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="aa119-181">b.</span><span class="sxs-lookup"><span data-stu-id="aa119-181">b.</span></span> <span data-ttu-id="aa119-182">In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="aa119-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="aa119-183">c.</span><span class="sxs-lookup"><span data-stu-id="aa119-183">c.</span></span> <span data-ttu-id="aa119-184">Van Hallo **kenmerkwaarde** wilt weergeven, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="aa119-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="aa119-185">d.</span><span class="sxs-lookup"><span data-stu-id="aa119-185">d.</span></span> <span data-ttu-id="aa119-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="aa119-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="aa119-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="aa119-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="aa119-189">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team en de gedownloade metagegevensbestand Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="aa119-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="aa119-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="aa119-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa119-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="aa119-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa119-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa119-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa119-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="aa119-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa119-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="aa119-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="aa119-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aa119-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa119-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aa119-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa119-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="aa119-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa119-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="aa119-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa119-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa119-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa119-205">a.</span><span class="sxs-lookup"><span data-stu-id="aa119-205">a.</span></span> <span data-ttu-id="aa119-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa119-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa119-207">b.</span><span class="sxs-lookup"><span data-stu-id="aa119-207">b.</span></span> <span data-ttu-id="aa119-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa119-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa119-209">c.</span><span class="sxs-lookup"><span data-stu-id="aa119-209">c.</span></span> <span data-ttu-id="aa119-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="aa119-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa119-211">d.</span><span class="sxs-lookup"><span data-stu-id="aa119-211">d.</span></span> <span data-ttu-id="aa119-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa119-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="aa119-213">Een testgebruiker Pluralsight maken</span><span class="sxs-lookup"><span data-stu-id="aa119-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="aa119-214">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Pluralsight van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa119-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="aa119-215">Neem contact op met [Pluralsight Client ondersteuningsteam](mailto:support@pluralsight.com) tooadd Hallo gebruikers in Hallo Pluralsight-account.</span><span class="sxs-lookup"><span data-stu-id="aa119-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa119-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa119-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa119-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPluralsight toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="aa119-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="aa119-219">**tooassign Britta Simon tooPluralsight, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="aa119-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa119-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa119-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="aa119-222">Selecteer in de lijst met de toepassingen van Hallo **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="aa119-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="aa119-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="aa119-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="aa119-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="aa119-226">Click **Add** button.</span></span> <span data-ttu-id="aa119-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="aa119-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa119-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa119-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa119-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa119-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa119-232">Testing single sign-on</span></span>

<span data-ttu-id="aa119-233">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="aa119-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa119-234">Als u op Hallo Pluralsight tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Pluralsight toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa119-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="aa119-235">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa119-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa119-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="aa119-236">Additional resources</span></span>

* [<span data-ttu-id="aa119-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa119-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa119-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa119-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

