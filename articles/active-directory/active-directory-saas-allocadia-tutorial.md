---
title: 'Zelfstudie: Azure Active Directory-integratie met Allocadia | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Allocadia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="3f084-103">Zelfstudie: Azure Active Directory-integratie met Allocadia</span><span class="sxs-lookup"><span data-stu-id="3f084-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="3f084-104">In deze zelfstudie leert u hoe toointegrate Allocadia met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3f084-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f084-105">Allocadia integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3f084-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3f084-106">U kunt beheren in Azure AD die tooAllocadia toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3f084-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="3f084-107">U kunt uw gebruikers tooautomatically get aangemelde tooAllocadia (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3f084-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f084-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3f084-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3f084-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f084-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f084-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f084-110">Prerequisites</span></span>

<span data-ttu-id="3f084-111">Azure AD-integratie met Allocadia tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3f084-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="3f084-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3f084-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f084-113">Een Allocadia eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3f084-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f084-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f084-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f084-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f084-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3f084-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f084-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f084-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f084-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3f084-118">Scenario description</span></span>
<span data-ttu-id="3f084-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f084-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f084-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3f084-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f084-121">Het toevoegen van Allocadia van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3f084-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="3f084-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f084-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="3f084-123">Het toevoegen van Allocadia van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3f084-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="3f084-124">tooconfigure hello integratie van Allocadia in Azure AD, moet u tooadd Allocadia uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3f084-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3f084-125">**tooadd Allocadia via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3f084-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f084-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f084-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f084-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f084-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3f084-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f084-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3f084-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f084-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3f084-133">Typ in het zoekvak Hallo **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="3f084-133">In hello search box, type **Allocadia**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="3f084-135">Selecteer in het deelvenster resultaten hello, **Allocadia**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f084-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f084-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f084-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f084-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Allocadia op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3f084-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3f084-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Allocadia is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f084-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="3f084-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Allocadia toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3f084-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="3f084-141">Wijs in Allocadia, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="3f084-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3f084-142">tooconfigure en eenmalige aanmelding Azure AD-test met Allocadia, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3f084-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3f084-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3f084-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3f084-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f084-145">**[Maken van een testgebruiker Allocadia](#creating-an-allocadia-test-user)**  -toohave een equivalent van Britta Simon in Allocadia die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3f084-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f084-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3f084-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f084-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3f084-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f084-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3f084-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f084-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Allocadia configureren.</span><span class="sxs-lookup"><span data-stu-id="3f084-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="3f084-150">**Azure AD tooconfigure eenmalige aanmelding met Allocadia, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3f084-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f084-151">In de Azure-portal op Hallo Hallo **Allocadia** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3f084-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3f084-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3f084-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="3f084-155">Op Hallo **Allocadia domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="3f084-157">a.</span><span class="sxs-lookup"><span data-stu-id="3f084-157">a.</span></span> <span data-ttu-id="3f084-158">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="3f084-159">Voor de testomgeving-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="3f084-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="3f084-160">Voor de productie-omgeving-`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="3f084-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="3f084-161">b.</span><span class="sxs-lookup"><span data-stu-id="3f084-161">b.</span></span> <span data-ttu-id="3f084-162">In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="3f084-163">Voor de testomgeving-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="3f084-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="3f084-164">Voor de productie-omgeving-`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="3f084-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f084-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3f084-165">These values are not real.</span></span> <span data-ttu-id="3f084-166">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="3f084-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="3f084-167">Neem contact op met [Allocadia ondersteuningsteam](mailTo:support@allocadia.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3f084-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="3f084-168">Hallo SAML asserties verwacht Allocadia toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="3f084-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3f084-169">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="3f084-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="3f084-170">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="3f084-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3f084-171">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="3f084-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="3f084-173">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="3f084-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3f084-174">Attribute Name</span></span> | <span data-ttu-id="3f084-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3f084-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="3f084-176">Voornaam</span><span class="sxs-lookup"><span data-stu-id="3f084-176">firstname</span></span> | <span data-ttu-id="3f084-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3f084-177">user.givenname</span></span> |
    | <span data-ttu-id="3f084-178">Achternaam</span><span class="sxs-lookup"><span data-stu-id="3f084-178">lastname</span></span> | <span data-ttu-id="3f084-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="3f084-179">user.surname</span></span> |
    | <span data-ttu-id="3f084-180">E-mail</span><span class="sxs-lookup"><span data-stu-id="3f084-180">email</span></span> | <span data-ttu-id="3f084-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="3f084-181">user.mail</span></span> |
    
    <span data-ttu-id="3f084-182">a.</span><span class="sxs-lookup"><span data-stu-id="3f084-182">a.</span></span> <span data-ttu-id="3f084-183">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f084-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="3f084-185">b.</span><span class="sxs-lookup"><span data-stu-id="3f084-185">b.</span></span> <span data-ttu-id="3f084-186">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3f084-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3f084-188">c.</span><span class="sxs-lookup"><span data-stu-id="3f084-188">c.</span></span> <span data-ttu-id="3f084-189">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3f084-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="3f084-190">d.</span><span class="sxs-lookup"><span data-stu-id="3f084-190">d.</span></span> <span data-ttu-id="3f084-191">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f084-191">Click **Ok**.</span></span>



6. <span data-ttu-id="3f084-192">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3f084-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="3f084-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3f084-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3f084-196">tooconfigure eenmalige aanmelding op **Allocadia** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Allocadia ondersteuningsteam](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="3f084-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="3f084-197">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3f084-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3f084-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3f084-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3f084-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3f084-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3f084-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f084-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f084-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3f084-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f084-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3f084-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3f084-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3f084-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f084-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3f084-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f084-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3f084-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f084-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3f084-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f084-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f084-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f084-213">a.</span><span class="sxs-lookup"><span data-stu-id="3f084-213">a.</span></span> <span data-ttu-id="3f084-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3f084-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f084-215">b.</span><span class="sxs-lookup"><span data-stu-id="3f084-215">b.</span></span> <span data-ttu-id="3f084-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3f084-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f084-217">c.</span><span class="sxs-lookup"><span data-stu-id="3f084-217">c.</span></span> <span data-ttu-id="3f084-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3f084-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3f084-219">d.</span><span class="sxs-lookup"><span data-stu-id="3f084-219">d.</span></span> <span data-ttu-id="3f084-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f084-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="3f084-221">Een testgebruiker Allocadia maken</span><span class="sxs-lookup"><span data-stu-id="3f084-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="3f084-222">Toepassing ondersteunt Just in time gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="3f084-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="3f084-223">Na verificatie gebruikers in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f084-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3f084-224">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f084-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3f084-225">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAllocadia toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3f084-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3f084-227">**tooassign Britta Simon tooAllocadia, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3f084-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="3f084-228">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3f084-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3f084-230">Selecteer in de lijst met de toepassingen van Hallo **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="3f084-230">In hello applications list, select **Allocadia**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="3f084-232">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3f084-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3f084-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3f084-234">Click **Add** button.</span></span> <span data-ttu-id="3f084-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f084-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3f084-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f084-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3f084-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f084-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f084-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3f084-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f084-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3f084-240">Testing single sign-on</span></span>

<span data-ttu-id="3f084-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3f084-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3f084-242">Als u op Hallo Allocadia tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Allocadia toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f084-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="3f084-243">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangsvenster](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3f084-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f084-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3f084-244">Additional resources</span></span>

* [<span data-ttu-id="3f084-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f084-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f084-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3f084-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

