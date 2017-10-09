---
title: 'Zelfstudie: Azure Active Directory-integratie met iLMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="89033-103">Zelfstudie: Azure Active Directory-integratie met iLMS</span><span class="sxs-lookup"><span data-stu-id="89033-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="89033-104">In deze zelfstudie leert u hoe toointegrate iLMS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89033-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89033-105">ILMS integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="89033-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89033-106">U kunt beheren in Azure AD die tooiLMS toegang heeft</span><span class="sxs-lookup"><span data-stu-id="89033-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="89033-107">U kunt uw gebruikers tooautomatically get aangemelde tooiLMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="89033-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89033-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="89033-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="89033-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89033-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89033-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89033-110">Prerequisites</span></span>

<span data-ttu-id="89033-111">Azure AD-integratie met iLMS tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="89033-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="89033-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="89033-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89033-113">Een iLMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="89033-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89033-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="89033-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89033-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89033-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="89033-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="89033-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89033-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89033-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="89033-118">Scenario description</span></span>
<span data-ttu-id="89033-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="89033-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89033-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="89033-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89033-121">Het toevoegen van iLMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89033-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="89033-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89033-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="89033-123">Het toevoegen van iLMS van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89033-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="89033-124">tooconfigure hello integratie van iLMS in Azure AD, moet u tooadd iLMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="89033-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89033-125">**tooadd iLMS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89033-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89033-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89033-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89033-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89033-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89033-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89033-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="89033-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="89033-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="89033-133">Typ in het zoekvak Hallo **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="89033-133">In hello search box, type **iLMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="89033-135">Selecteer in het deelvenster resultaten hello, **iLMS**, klikt u vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89033-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89033-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89033-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89033-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met iLMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="89033-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89033-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in iLMS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89033-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="89033-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in iLMS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="89033-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="89033-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in iLMS.</span><span class="sxs-lookup"><span data-stu-id="89033-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="89033-142">tooconfigure en eenmalige aanmelding Azure AD-test met iLMS, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89033-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="89033-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89033-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89033-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89033-145">**[Maken van een testgebruiker iLMS](#creating-an-ilms-test-user)**  -toohave een equivalent van Britta Simon in iLMS die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="89033-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="89033-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89033-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89033-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="89033-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89033-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="89033-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89033-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing iLMS configureren.</span><span class="sxs-lookup"><span data-stu-id="89033-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="89033-150">**Azure AD tooconfigure eenmalige aanmelding met iLMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89033-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="89033-151">In de Azure-portal op Hallo Hallo **iLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="89033-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="89033-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89033-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="89033-155">Op Hallo **iLMS domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="89033-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="89033-157">a.</span><span class="sxs-lookup"><span data-stu-id="89033-157">a.</span></span> <span data-ttu-id="89033-158">In Hallo **id** textbox plakken Hallo **id** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS.</span><span class="sxs-lookup"><span data-stu-id="89033-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="89033-159">b.</span><span class="sxs-lookup"><span data-stu-id="89033-159">b.</span></span> <span data-ttu-id="89033-160">In Hallo **antwoord-URL** textbox plakken Hallo **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS met de volgende Hallo patroon`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="89033-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="89033-161">Deze '123456' is een van de Voorbeeldwaarde van id.</span><span class="sxs-lookup"><span data-stu-id="89033-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="89033-162">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="89033-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="89033-164">In Hallo **aanmeldings-URL** textbox plakken Hallo **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS als`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="89033-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="89033-165">tooenable JIT-inrichting, verwacht iLMS toepassing hello SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="89033-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="89033-166">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="89033-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="89033-167">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="89033-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="89033-168">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="89033-168">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="89033-170">Maak **afdeling, regio** en **deling** kenmerken en Hallo-naam van deze kenmerken in iLMS toevoegen.</span><span class="sxs-lookup"><span data-stu-id="89033-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="89033-171">Alle deze kenmerken die hierboven zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="89033-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="89033-172">U hebt tooenable **Un-recognized-gebruikersaccount maken** in iLMS toomap deze kenmerken.</span><span class="sxs-lookup"><span data-stu-id="89033-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="89033-173">Volg de instructies Hallo [hier](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget een idee op Hallo kenmerken configuratie.</span><span class="sxs-lookup"><span data-stu-id="89033-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="89033-174">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="89033-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="89033-175">Attribute Name</span></span> | <span data-ttu-id="89033-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="89033-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="89033-177">deling</span><span class="sxs-lookup"><span data-stu-id="89033-177">division</span></span> | <span data-ttu-id="89033-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="89033-178">user.department</span></span> |
    | <span data-ttu-id="89033-179">Regio</span><span class="sxs-lookup"><span data-stu-id="89033-179">region</span></span> | <span data-ttu-id="89033-180">User.state</span><span class="sxs-lookup"><span data-stu-id="89033-180">user.state</span></span> |
    | <span data-ttu-id="89033-181">Afdeling</span><span class="sxs-lookup"><span data-stu-id="89033-181">department</span></span> | <span data-ttu-id="89033-182">User.jobtitle</span><span class="sxs-lookup"><span data-stu-id="89033-182">user.jobtitle</span></span> |

    <span data-ttu-id="89033-183">a.</span><span class="sxs-lookup"><span data-stu-id="89033-183">a.</span></span> <span data-ttu-id="89033-184">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89033-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="89033-187">b.</span><span class="sxs-lookup"><span data-stu-id="89033-187">b.</span></span> <span data-ttu-id="89033-188">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="89033-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="89033-189">c.</span><span class="sxs-lookup"><span data-stu-id="89033-189">c.</span></span> <span data-ttu-id="89033-190">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="89033-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="89033-191">d.</span><span class="sxs-lookup"><span data-stu-id="89033-191">d.</span></span> <span data-ttu-id="89033-192">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="89033-192">Click **Ok**</span></span>

7. <span data-ttu-id="89033-193">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="89033-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="89033-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="89033-195">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="89033-197">Aanmelden in een ander browservenster tooyour **iLMS-beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="89033-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="89033-198">Klik op **SSO:SAML** onder **instellingen** tooopen SAML-instellingen op het tabblad en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="89033-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="89033-200">a.</span><span class="sxs-lookup"><span data-stu-id="89033-200">a.</span></span> <span data-ttu-id="89033-201">Vouw Hallo **serviceprovider** sectie en kopieer Hallo **id** en **eindpunt (URL)** waarde.</span><span class="sxs-lookup"><span data-stu-id="89033-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="89033-203">b.</span><span class="sxs-lookup"><span data-stu-id="89033-203">b.</span></span> <span data-ttu-id="89033-204">Onder **identiteitsprovider** sectie, klikt u op **metagegevens importeren**.</span><span class="sxs-lookup"><span data-stu-id="89033-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="89033-205">c.</span><span class="sxs-lookup"><span data-stu-id="89033-205">c.</span></span> <span data-ttu-id="89033-206">Selecteer Hallo **metagegevens** bestand gedownload van Azure-Portal **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="89033-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="89033-208">d.</span><span class="sxs-lookup"><span data-stu-id="89033-208">d.</span></span> <span data-ttu-id="89033-209">Als u wilt dat tooenable JIT inrichting toocreate iLMS accounts voor ongedaan maken-gebruikers herkennen, volgt u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="89033-210">Controleer **Account maken voor niet-herkende gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="89033-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="89033-212">Hallo kenmerken toewijzen in Azure AD met Hallo kenmerken in iLMS.</span><span class="sxs-lookup"><span data-stu-id="89033-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="89033-213">Geef in Hallo kenmerkkolom Hallo-kenmerken naam of het Hallo standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="89033-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="89033-214">e.</span><span class="sxs-lookup"><span data-stu-id="89033-214">e.</span></span> <span data-ttu-id="89033-215">Ga te**bedrijfsregels** tabblad en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="89033-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="89033-217">Controleer **Un-recognized regio's maken, afdelingen en afdelingen** toocreate regio's, afdelingen en afdelingen die gelijktijdig Hallo met eenmalige aanmelding niet al bestaan.</span><span class="sxs-lookup"><span data-stu-id="89033-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="89033-218">Controleer **Update gebruiker profiel tijdens aanmelden** toospecify of Hallo gebruikersprofiel wordt bijgewerkt met elke eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89033-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="89033-219">Als hello **'Update lege waarden voor niet verplichte velden in gebruikersprofiel'** optie is ingeschakeld, optionele profiel velden leeg bij het aanmelden wordt zijn ook voor zorgen dat Hallo iLMS gebruikersprofiel toocontain lege waarden voor deze velden.</span><span class="sxs-lookup"><span data-stu-id="89033-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="89033-220">Controleer **fout meldingse-mail verzenden** en Voer Hallo e-mailadres van de gebruiker Hallo waar u tooreceive Hallo fout meldingse-mail.</span><span class="sxs-lookup"><span data-stu-id="89033-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="89033-221">Klik op **opslaan** knop toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="89033-221">Click **Save** button toosave hello settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="89033-223">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="89033-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89033-224">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="89033-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89033-225">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89033-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89033-226">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="89033-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="89033-227">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="89033-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="89033-229">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89033-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89033-230">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89033-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89033-232">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="89033-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89033-234">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89033-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89033-236">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89033-238">a.</span><span class="sxs-lookup"><span data-stu-id="89033-238">a.</span></span> <span data-ttu-id="89033-239">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89033-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89033-240">b.</span><span class="sxs-lookup"><span data-stu-id="89033-240">b.</span></span> <span data-ttu-id="89033-241">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89033-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89033-242">c.</span><span class="sxs-lookup"><span data-stu-id="89033-242">c.</span></span> <span data-ttu-id="89033-243">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="89033-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89033-244">d.</span><span class="sxs-lookup"><span data-stu-id="89033-244">d.</span></span> <span data-ttu-id="89033-245">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="89033-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="89033-246">Een testgebruiker iLMS maken</span><span class="sxs-lookup"><span data-stu-id="89033-246">Creating an iLMS test user</span></span>

<span data-ttu-id="89033-247">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="89033-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="89033-248">JIT werkt als u hebt geklikt op Hallo **Un-recognized-gebruikersaccount maken** selectievakje tijdens SAML-configuratie-instelling op iLMS-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="89033-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="89033-249">Als u handmatig een gebruiker toocreate moet, volgt u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89033-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="89033-250">Tooyour iLMS bedrijf site aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="89033-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="89033-251">Klik op **'Gebruiker registreren'** onder **gebruikers** tabblad tooopen **gebruiker registreren** pagina.</span><span class="sxs-lookup"><span data-stu-id="89033-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="89033-253">Op Hallo **'Gebruiker registreren'** pagina, voert u Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="89033-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="89033-255">a.</span><span class="sxs-lookup"><span data-stu-id="89033-255">a.</span></span> <span data-ttu-id="89033-256">In Hallo **voornaam** textbox type Hallo voornaam Britta.</span><span class="sxs-lookup"><span data-stu-id="89033-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="89033-257">b.</span><span class="sxs-lookup"><span data-stu-id="89033-257">b.</span></span> <span data-ttu-id="89033-258">In Hallo **achternaam** textbox type Hallo achternaam Simon.</span><span class="sxs-lookup"><span data-stu-id="89033-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="89033-259">c.</span><span class="sxs-lookup"><span data-stu-id="89033-259">c.</span></span> <span data-ttu-id="89033-260">In Hallo **E-mail-ID** textbox type Hallo e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="89033-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="89033-261">d.</span><span class="sxs-lookup"><span data-stu-id="89033-261">d.</span></span> <span data-ttu-id="89033-262">In Hallo **regio** vervolgkeuzelijst, selecteer Hallo-waarde voor de regio.</span><span class="sxs-lookup"><span data-stu-id="89033-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="89033-263">e.</span><span class="sxs-lookup"><span data-stu-id="89033-263">e.</span></span> <span data-ttu-id="89033-264">In Hallo **deling** vervolgkeuzelijst, selecteer Hallo-waarde voor deling.</span><span class="sxs-lookup"><span data-stu-id="89033-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="89033-265">f.</span><span class="sxs-lookup"><span data-stu-id="89033-265">f.</span></span> <span data-ttu-id="89033-266">In Hallo **afdeling** vervolgkeuzelijst, selecteer Hallo-waarde voor de afdeling.</span><span class="sxs-lookup"><span data-stu-id="89033-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="89033-267">g.</span><span class="sxs-lookup"><span data-stu-id="89033-267">g.</span></span> <span data-ttu-id="89033-268">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="89033-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89033-269">U kunt registratie mail toouser verzenden door te selecteren **registratie E-mail verzenden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="89033-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89033-270">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89033-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89033-271">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooiLMS toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="89033-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="89033-273">**tooassign Britta Simon tooiLMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89033-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="89033-274">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89033-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="89033-276">Selecteer in de lijst met de toepassingen van Hallo **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="89033-276">In hello applications list, select **iLMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="89033-278">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="89033-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="89033-280">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="89033-280">Click **Add** button.</span></span> <span data-ttu-id="89033-281">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89033-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="89033-283">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="89033-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89033-284">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89033-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89033-285">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89033-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89033-286">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89033-286">Testing single sign-on</span></span>

<span data-ttu-id="89033-287">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="89033-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89033-288">Als u op Hallo iLMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour iLMS toepassing.</span><span class="sxs-lookup"><span data-stu-id="89033-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89033-289">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="89033-289">Additional resources</span></span>

* [<span data-ttu-id="89033-290">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89033-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89033-291">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89033-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

