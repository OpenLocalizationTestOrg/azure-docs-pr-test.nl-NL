---
title: 'Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="90311-103">Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="90311-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="90311-104">In deze zelfstudie leert u hoe toointegrate ScaleX Enterprise met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90311-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90311-105">ScaleX-onderneming integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="90311-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90311-106">U kunt beheren in Azure AD wie toegang tot tooScaleX Enterprise heeft</span><span class="sxs-lookup"><span data-stu-id="90311-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="90311-107">U kunt uw gebruikers tooautomatically get aangemelde tooScaleX Enterprise (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="90311-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90311-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="90311-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90311-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="90311-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="90311-110">Wat is er toegang tot toepassingen en eenmalige aanmelding met [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90311-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90311-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="90311-111">Prerequisites</span></span>

<span data-ttu-id="90311-112">tooconfigure Azure AD-integratie met ScaleX voor ondernemingen, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="90311-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="90311-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="90311-113">An Azure AD subscription</span></span>
- <span data-ttu-id="90311-114">Een ScaleX Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="90311-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90311-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="90311-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90311-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="90311-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90311-117">Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="90311-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="90311-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90311-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90311-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="90311-119">Scenario description</span></span>
<span data-ttu-id="90311-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90311-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90311-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="90311-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90311-122">Het toevoegen van ScaleX Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="90311-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="90311-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90311-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="90311-124">Het toevoegen van ScaleX Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="90311-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="90311-125">tooconfigure hello integratie van ScaleX onderneming in tooAzure AD, moet u tooadd ScaleX Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="90311-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90311-126">**tooadd ScaleX Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90311-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90311-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90311-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90311-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90311-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90311-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90311-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="90311-132">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="90311-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="90311-134">Typ in het zoekvak Hallo **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="90311-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="90311-136">Selecteer in het deelvenster resultaten hello, **ScaleX Enterprise**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="90311-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90311-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90311-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90311-139">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met ScaleX Enterprise op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="90311-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90311-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de onderneming ScaleX is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90311-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="90311-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de onderneming ScaleX Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="90311-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="90311-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ScaleX onderneming.</span><span class="sxs-lookup"><span data-stu-id="90311-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="90311-143">tooconfigure en test eenmalige aanmelding Azure AD met ScaleX voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="90311-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90311-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="90311-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90311-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90311-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90311-146">**[Maken van een testgebruiker ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave een equivalent van Britta Simon in ScaleX onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="90311-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90311-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="90311-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90311-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="90311-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90311-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="90311-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90311-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="90311-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="90311-151">**Voer tooconfigure Azure AD eenmalige aanmelding met ScaleX Enterprise, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90311-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="90311-152">In de Azure-portal op Hallo Hallo **ScaleX Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="90311-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="90311-154">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="90311-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="90311-156">Op Hallo **ScaleX Enterprise domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="90311-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="90311-158">a.</span><span class="sxs-lookup"><span data-stu-id="90311-158">a.</span></span> <span data-ttu-id="90311-159">In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="90311-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="90311-160">b.</span><span class="sxs-lookup"><span data-stu-id="90311-160">b.</span></span> <span data-ttu-id="90311-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="90311-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="90311-162">Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="90311-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="90311-164">In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="90311-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="90311-165">Deze zijn niet Hallo echte waarden.</span><span class="sxs-lookup"><span data-stu-id="90311-165">These are not hello real values.</span></span> <span data-ttu-id="90311-166">Werk deze waarden met Hallo werkelijke id, de antwoord-URL of de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="90311-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="90311-167">Neem contact op met [ScaleX Enterprise Client ondersteuningsteam](http://info.rescale.com/contact_sales) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="90311-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="90311-168">Uw toepassing ScaleX verwacht Hallo SAML asserties in een specifieke indeling waarvoor u toomodify aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="90311-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="90311-169">Klik op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje tooopen Hallo aangepaste kenmerken instellingen.</span><span class="sxs-lookup"><span data-stu-id="90311-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="90311-171">a.</span><span class="sxs-lookup"><span data-stu-id="90311-171">a.</span></span> <span data-ttu-id="90311-172">Klik met de rechtermuisknop op Hallo kenmerk **naam** en klik op verwijderen.</span><span class="sxs-lookup"><span data-stu-id="90311-172">Right click hello attribute **name** and click delete.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="90311-174">b.</span><span class="sxs-lookup"><span data-stu-id="90311-174">b.</span></span> <span data-ttu-id="90311-175">Klik op **emailaddress** venster kenmerk tooopen Hallo-kenmerk bewerken.</span><span class="sxs-lookup"><span data-stu-id="90311-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="90311-176">Wijzig de waarde van **user.mail** te**user.userprincipalname** en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="90311-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="90311-178">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="90311-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="90311-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="90311-180">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="90311-182">Op Hallo **ScaleX Ondernemingsconfiguratie** sectie, klikt u op **configureren ScaleX Enterprise** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="90311-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="90311-183">Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="90311-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="90311-185">tooconfigure eenmalige aanmelding op **ScaleX Enterprise** side, aanmelding toohello ScaleX Enterprise bedrijfswebsite als beheerder.</span><span class="sxs-lookup"><span data-stu-id="90311-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="90311-186">Klik rechts op Hallo in Hallo bovenste menu en selecteer **Contoso beheer**.</span><span class="sxs-lookup"><span data-stu-id="90311-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90311-187">Contoso is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="90311-187">Contoso is just an example.</span></span> <span data-ttu-id="90311-188">Dit moet de werkelijke naam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="90311-188">This should be your actual Company Name.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="90311-190">Selecteer **integraties** van Hallo bovenste menu en selecteer **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="90311-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="90311-192">Voer Hallo formulier als volgt:</span><span class="sxs-lookup"><span data-stu-id="90311-192">Complete hello form as follows:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="90311-194">a.</span><span class="sxs-lookup"><span data-stu-id="90311-194">a.</span></span> <span data-ttu-id="90311-195">Selecteer **'Alle gebruikers die kan worden geverifieerd met eenmalige aanmelding maken'.**</span><span class="sxs-lookup"><span data-stu-id="90311-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="90311-196">b.</span><span class="sxs-lookup"><span data-stu-id="90311-196">b.</span></span> <span data-ttu-id="90311-197">**Service Provider saml**: de waarde van de Hallo plakken ***urn: oasis: namen: tc: SAML:2.0:nameid-indeling: permanente***</span><span class="sxs-lookup"><span data-stu-id="90311-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="90311-198">c.</span><span class="sxs-lookup"><span data-stu-id="90311-198">c.</span></span> <span data-ttu-id="90311-199">**Naam van identiteitsprovider e veld in de ACS-antwoord**: de waarde van de Hallo plakken`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="90311-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="90311-200">d.</span><span class="sxs-lookup"><span data-stu-id="90311-200">d.</span></span> <span data-ttu-id="90311-201">**Identiteit EntityDescriptor entiteit-ID van Provider:** plakken Hallo **SAML entiteit-ID** waarde gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="90311-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="90311-202">e.</span><span class="sxs-lookup"><span data-stu-id="90311-202">e.</span></span> <span data-ttu-id="90311-203">**ID-Provider SingleSignOnService URL:** plakken Hallo **SAML Single Sign-On Service-URL** van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="90311-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="90311-204">f.</span><span class="sxs-lookup"><span data-stu-id="90311-204">f.</span></span> <span data-ttu-id="90311-205">**Provider openbare X509 identiteitscertificaat:** Open Hallo X509 certificaat gedownload van hello Azure in Kladblok en plak Hallo-inhoud in dit vak.</span><span class="sxs-lookup"><span data-stu-id="90311-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="90311-206">Zorg ervoor dat er dat geen regeleinden in Hallo middelste Hallo certificaat inhoud.</span><span class="sxs-lookup"><span data-stu-id="90311-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="90311-207">g.</span><span class="sxs-lookup"><span data-stu-id="90311-207">g.</span></span> <span data-ttu-id="90311-208">Hallo selectievakjes volgende controleren: **ingeschakeld, NameID versleutelen en aanmelding AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="90311-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="90311-209">h.</span><span class="sxs-lookup"><span data-stu-id="90311-209">h.</span></span> <span data-ttu-id="90311-210">Klik op **SSO-Update-instellingen** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="90311-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="90311-211">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="90311-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90311-212">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="90311-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90311-213">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90311-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90311-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="90311-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="90311-215">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="90311-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="90311-217">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90311-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90311-218">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90311-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90311-220">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="90311-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90311-222">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90311-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90311-224">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="90311-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90311-226">a.</span><span class="sxs-lookup"><span data-stu-id="90311-226">a.</span></span> <span data-ttu-id="90311-227">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90311-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90311-228">b.</span><span class="sxs-lookup"><span data-stu-id="90311-228">b.</span></span> <span data-ttu-id="90311-229">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90311-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90311-230">c.</span><span class="sxs-lookup"><span data-stu-id="90311-230">c.</span></span> <span data-ttu-id="90311-231">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="90311-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90311-232">d.</span><span class="sxs-lookup"><span data-stu-id="90311-232">d.</span></span> <span data-ttu-id="90311-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="90311-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="90311-234">Maken van een testgebruiker ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="90311-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="90311-235">Azure AD tooenable gebruikers toolog in tooScaleX Enterprise, moeten ze worden ingericht in tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="90311-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="90311-236">In geval van ScaleX onderneming Hallo inrichting is een automatische taak en er zijn geen handmatige stappen vereist.</span><span class="sxs-lookup"><span data-stu-id="90311-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="90311-237">Elke gebruiker die kan worden geverifieerd met eenmalige aanmelding referenties worden automatisch ingericht op Hallo ScaleX aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="90311-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90311-238">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="90311-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90311-239">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door de gebruiker toegang tooScaleX Enterprise verlenen.</span><span class="sxs-lookup"><span data-stu-id="90311-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="90311-241">**tooassign Britta Simon tooScaleX Enterprise, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="90311-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="90311-242">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90311-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="90311-244">Selecteer in de lijst met de toepassingen van Hallo **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="90311-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="90311-246">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="90311-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="90311-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="90311-248">Click **Add** button.</span></span> <span data-ttu-id="90311-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90311-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="90311-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="90311-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90311-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90311-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90311-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90311-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="90311-254">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90311-254">Testing single sign-on</span></span>

<span data-ttu-id="90311-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="90311-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="90311-256">Klik op Hallo ScaleX Enterprise-tegel in Hallo paneel voor Apptoegang, wordt u automatisch aangemelde tooyour ScaleX bedrijfstoepassing.</span><span class="sxs-lookup"><span data-stu-id="90311-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="90311-257">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="90311-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="90311-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="90311-258">Additional resources</span></span>

* [<span data-ttu-id="90311-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90311-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90311-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90311-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

