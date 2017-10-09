---
title: 'Zelfstudie: Azure Active Directory-integratie met Workpath | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Workpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="65660-103">Zelfstudie: Azure Active Directory-integratie met Workpath</span><span class="sxs-lookup"><span data-stu-id="65660-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="65660-104">In deze zelfstudie leert u hoe toointegrate Workpath met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65660-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65660-105">Workpath integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="65660-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65660-106">U kunt beheren in Azure AD die tooWorkpath toegang heeft</span><span class="sxs-lookup"><span data-stu-id="65660-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="65660-107">U kunt uw gebruikers tooautomatically get aangemelde tooWorkpath (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="65660-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65660-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="65660-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65660-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65660-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65660-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="65660-110">Prerequisites</span></span>

<span data-ttu-id="65660-111">Azure AD-integratie met Workpath tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="65660-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="65660-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="65660-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65660-113">Een Workpath eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="65660-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65660-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="65660-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65660-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="65660-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65660-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="65660-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65660-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65660-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65660-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="65660-118">Scenario description</span></span>
<span data-ttu-id="65660-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="65660-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65660-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="65660-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65660-121">Het toevoegen van Workpath van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="65660-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="65660-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65660-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="65660-123">Het toevoegen van Workpath van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="65660-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="65660-124">tooconfigure hello integratie van Workpath in Azure AD, moet u tooadd Workpath uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="65660-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65660-125">**tooadd Workpath via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65660-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65660-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65660-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65660-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65660-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65660-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65660-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="65660-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65660-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="65660-133">Typ in het zoekvak Hallo **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="65660-133">In hello search box, type **Workpath**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="65660-135">Selecteer in het deelvenster resultaten hello, **Workpath**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="65660-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65660-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65660-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65660-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Workpath op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="65660-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65660-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Workpath is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65660-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="65660-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Workpath toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="65660-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="65660-141">Wijs in Workpath, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="65660-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65660-142">tooconfigure en eenmalige aanmelding Azure AD-test met Workpath, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65660-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65660-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="65660-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65660-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65660-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65660-145">**[Maken van een testgebruiker Workpath](#creating-a-workpath-test-user)**  -toohave een equivalent van Britta Simon in Workpath die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="65660-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65660-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="65660-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65660-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="65660-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65660-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="65660-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65660-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Workpath configureren.</span><span class="sxs-lookup"><span data-stu-id="65660-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="65660-150">**Azure AD tooconfigure eenmalige aanmelding met Workpath, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65660-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="65660-151">In de Azure-portal op Hallo Hallo **Workpath** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="65660-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="65660-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="65660-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="65660-155">Op Hallo **Workpath domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** geïnitieerd modus uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65660-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="65660-157">a.</span><span class="sxs-lookup"><span data-stu-id="65660-157">a.</span></span> <span data-ttu-id="65660-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="65660-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="65660-159">b.</span><span class="sxs-lookup"><span data-stu-id="65660-159">b.</span></span> <span data-ttu-id="65660-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="65660-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="65660-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="65660-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="65660-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus geïnitieerd Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="65660-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="65660-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="65660-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65660-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="65660-165">These values are not real.</span></span> <span data-ttu-id="65660-166">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL, de id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="65660-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="65660-167">Neem contact op met [Workpath ondersteuningsteam](https://help.workpath.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="65660-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="65660-168">Hallo SAML asserties verwacht Workpath toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="65660-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="65660-169">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="65660-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="65660-170">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="65660-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="65660-171">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="65660-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="65660-173">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65660-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="65660-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="65660-174">Attribute Name</span></span> | <span data-ttu-id="65660-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="65660-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="65660-176">Voornaam</span><span class="sxs-lookup"><span data-stu-id="65660-176">first_name</span></span> | <span data-ttu-id="65660-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="65660-177">user.givenname</span></span> |
    | <span data-ttu-id="65660-178">Achternaam</span><span class="sxs-lookup"><span data-stu-id="65660-178">last_name</span></span> | <span data-ttu-id="65660-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="65660-179">user.surname</span></span> |
    
    <span data-ttu-id="65660-180">a.</span><span class="sxs-lookup"><span data-stu-id="65660-180">a.</span></span> <span data-ttu-id="65660-181">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65660-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="65660-183">b.</span><span class="sxs-lookup"><span data-stu-id="65660-183">b.</span></span> <span data-ttu-id="65660-184">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="65660-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="65660-186">c.</span><span class="sxs-lookup"><span data-stu-id="65660-186">c.</span></span> <span data-ttu-id="65660-187">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="65660-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="65660-188">d.</span><span class="sxs-lookup"><span data-stu-id="65660-188">d.</span></span> <span data-ttu-id="65660-189">Hallo laat **Namespace** textbox leeg.</span><span class="sxs-lookup"><span data-stu-id="65660-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="65660-190">e.</span><span class="sxs-lookup"><span data-stu-id="65660-190">e.</span></span> <span data-ttu-id="65660-191">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="65660-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="65660-192">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="65660-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="65660-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="65660-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="65660-196">Op Hallo **Workpath configuratie** sectie, klikt u op **configureren Workpath** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="65660-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65660-197">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="65660-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="65660-199">tooconfigure eenmalige aanmelding op **Workpath** zijde, moet u toosend Hallo gedownload **Metadata XML**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Workpath ondersteuningsteam](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="65660-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="65660-200">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="65660-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65660-201">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="65660-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65660-202">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65660-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65660-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="65660-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="65660-204">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="65660-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="65660-206">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65660-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65660-207">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="65660-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65660-209">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="65660-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65660-211">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="65660-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65660-213">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65660-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65660-215">a.</span><span class="sxs-lookup"><span data-stu-id="65660-215">a.</span></span> <span data-ttu-id="65660-216">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65660-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65660-217">b.</span><span class="sxs-lookup"><span data-stu-id="65660-217">b.</span></span> <span data-ttu-id="65660-218">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65660-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65660-219">c.</span><span class="sxs-lookup"><span data-stu-id="65660-219">c.</span></span> <span data-ttu-id="65660-220">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="65660-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65660-221">d.</span><span class="sxs-lookup"><span data-stu-id="65660-221">d.</span></span> <span data-ttu-id="65660-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="65660-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="65660-223">Een testgebruiker Workpath maken</span><span class="sxs-lookup"><span data-stu-id="65660-223">Creating a Workpath test user</span></span>

<span data-ttu-id="65660-224">Workpath ondersteunt Just in time gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="65660-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="65660-225">Na verificatie gebruikers in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65660-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65660-226">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65660-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65660-227">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWorkpath toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="65660-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="65660-229">**tooassign Britta Simon tooWorkpath, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="65660-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="65660-230">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="65660-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="65660-232">Selecteer in de lijst met de toepassingen van Hallo **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="65660-232">In hello applications list, select **Workpath**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="65660-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="65660-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="65660-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="65660-236">Click **Add** button.</span></span> <span data-ttu-id="65660-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65660-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="65660-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="65660-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65660-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65660-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65660-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="65660-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65660-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="65660-242">Testing single sign-on</span></span>

<span data-ttu-id="65660-243">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="65660-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65660-244">Als u op Hallo Workpath tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Workpath toepassing.</span><span class="sxs-lookup"><span data-stu-id="65660-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="65660-245">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65660-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65660-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="65660-246">Additional resources</span></span>

* [<span data-ttu-id="65660-247">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65660-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65660-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65660-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

