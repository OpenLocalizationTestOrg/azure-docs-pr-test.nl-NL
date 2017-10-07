---
title: 'Zelfstudie: Azure Active Directory-integratie met SD-elementen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SD-elementen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="c895d-103">Zelfstudie: Azure Active Directory-integratie met SD-elementen</span><span class="sxs-lookup"><span data-stu-id="c895d-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="c895d-104">In deze zelfstudie leert u hoe toointegrate SD-elementen met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c895d-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c895d-105">SD-elementen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c895d-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c895d-106">U kunt beheren in Azure AD wie toegang tot tooSD elementen heeft</span><span class="sxs-lookup"><span data-stu-id="c895d-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="c895d-107">U kunt uw gebruikers tooautomatically get aangemelde tooSD elementen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c895d-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c895d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c895d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c895d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c895d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c895d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c895d-110">Prerequisites</span></span>

<span data-ttu-id="c895d-111">tooconfigure Azure AD-integratie met SD-elementen, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c895d-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="c895d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c895d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c895d-113">Een SD-elementen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c895d-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c895d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c895d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c895d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c895d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c895d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c895d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c895d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c895d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c895d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c895d-118">Scenario description</span></span>
<span data-ttu-id="c895d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c895d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c895d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c895d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c895d-121">Het toevoegen van SD-elementen uit de galerie Hallo</span><span class="sxs-lookup"><span data-stu-id="c895d-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="c895d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c895d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="c895d-123">Het toevoegen van SD-elementen uit de galerie Hallo</span><span class="sxs-lookup"><span data-stu-id="c895d-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="c895d-124">tooconfigure hello integratie van SD-elementen in Azure AD, moet u tooadd SD-elementen in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c895d-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c895d-125">**tooadd SD-elementen uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c895d-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c895d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c895d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c895d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c895d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c895d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c895d-133">Typ in het zoekvak Hallo **SD-elementen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-133">In hello search box, type **SD Elements**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="c895d-135">Selecteer in het deelvenster resultaten hello, **SD-elementen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c895d-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c895d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c895d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c895d-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met SD-elementen die op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c895d-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c895d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SD-elementen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c895d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="c895d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SD-elementen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c895d-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="c895d-141">In de SD-elementen, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c895d-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c895d-142">tooconfigure en test eenmalige aanmelding Azure AD met SD-elementen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c895d-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c895d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c895d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c895d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c895d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c895d-145">**[Maken van een SD-elementen testgebruiker](#creating-a-sd-elements-test-user)**  -toohave een equivalent van Britta Simon in SD-elementen die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c895d-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c895d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c895d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c895d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c895d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c895d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c895d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c895d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SD-elementen.</span><span class="sxs-lookup"><span data-stu-id="c895d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="c895d-150">**Voer tooconfigure Azure AD eenmalige aanmelding met SD-elementen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c895d-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="c895d-151">In de Azure-portal op Hallo Hallo **SD-elementen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c895d-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c895d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c895d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="c895d-155">Op Hallo **SD-elementen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c895d-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="c895d-157">a.</span><span class="sxs-lookup"><span data-stu-id="c895d-157">a.</span></span> <span data-ttu-id="c895d-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="c895d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="c895d-159">b.</span><span class="sxs-lookup"><span data-stu-id="c895d-159">b.</span></span> <span data-ttu-id="c895d-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="c895d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c895d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c895d-161">These values are not real.</span></span> <span data-ttu-id="c895d-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="c895d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c895d-163">Neem contact op met [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c895d-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="c895d-164">Hallo SAML asserties verwacht toepassing SD-elementen in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="c895d-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c895d-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="c895d-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="c895d-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerk'** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="c895d-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="c895d-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="c895d-167">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="c895d-169">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c895d-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="c895d-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c895d-170">Attribute Name</span></span> | <span data-ttu-id="c895d-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="c895d-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c895d-172">E-mail</span><span class="sxs-lookup"><span data-stu-id="c895d-172">email</span></span> |<span data-ttu-id="c895d-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="c895d-173">user.mail</span></span> |
    | <span data-ttu-id="c895d-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="c895d-174">firstname</span></span> |<span data-ttu-id="c895d-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="c895d-175">user.givenname</span></span> |
    | <span data-ttu-id="c895d-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="c895d-176">lastname</span></span> |<span data-ttu-id="c895d-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="c895d-177">user.surname</span></span> |

    <span data-ttu-id="c895d-178">a.</span><span class="sxs-lookup"><span data-stu-id="c895d-178">a.</span></span> <span data-ttu-id="c895d-179">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="c895d-182">b.</span><span class="sxs-lookup"><span data-stu-id="c895d-182">b.</span></span> <span data-ttu-id="c895d-183">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="c895d-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c895d-184">c.</span><span class="sxs-lookup"><span data-stu-id="c895d-184">c.</span></span> <span data-ttu-id="c895d-185">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="c895d-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="c895d-186">d.</span><span class="sxs-lookup"><span data-stu-id="c895d-186">d.</span></span> <span data-ttu-id="c895d-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c895d-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="c895d-188">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c895d-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="c895d-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c895d-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c895d-192">Op Hallo **SD-elementen configuratie** sectie, klikt u op **SD-elementen configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c895d-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c895d-193">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c895d-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="c895d-195">tooget eenmalige aanmelding is ingeschakeld, neem contact op met uw [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) en geeft u het gedownloade bestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="c895d-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="c895d-196">In een ander browservenster, aanmelding tooyour SD-elementen tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c895d-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="c895d-197">Klik in het menu bovenaan Hallo Hallo **System**, en vervolgens **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c895d-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="c895d-199">Op Hallo **instellingen voor eenmalige aanmelding** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c895d-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="c895d-201">a.</span><span class="sxs-lookup"><span data-stu-id="c895d-201">a.</span></span> <span data-ttu-id="c895d-202">Als **SSO Type**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c895d-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="c895d-203">b.</span><span class="sxs-lookup"><span data-stu-id="c895d-203">b.</span></span> <span data-ttu-id="c895d-204">In Hallo **identiteit Provider entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c895d-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="c895d-205">c.</span><span class="sxs-lookup"><span data-stu-id="c895d-205">c.</span></span> <span data-ttu-id="c895d-206">In Hallo **Provider Single Sign-On Identiteitsservice** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c895d-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="c895d-207">d.</span><span class="sxs-lookup"><span data-stu-id="c895d-207">d.</span></span> <span data-ttu-id="c895d-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c895d-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c895d-209">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c895d-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c895d-210">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c895d-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c895d-211">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c895d-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c895d-212">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c895d-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="c895d-213">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c895d-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c895d-215">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c895d-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c895d-216">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c895d-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c895d-218">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c895d-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c895d-220">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c895d-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c895d-222">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c895d-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c895d-224">a.</span><span class="sxs-lookup"><span data-stu-id="c895d-224">a.</span></span> <span data-ttu-id="c895d-225">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c895d-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c895d-226">b.</span><span class="sxs-lookup"><span data-stu-id="c895d-226">b.</span></span> <span data-ttu-id="c895d-227">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c895d-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c895d-228">c.</span><span class="sxs-lookup"><span data-stu-id="c895d-228">c.</span></span> <span data-ttu-id="c895d-229">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c895d-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c895d-230">d.</span><span class="sxs-lookup"><span data-stu-id="c895d-230">d.</span></span> <span data-ttu-id="c895d-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c895d-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="c895d-232">Maken van een testgebruiker SD-elementen</span><span class="sxs-lookup"><span data-stu-id="c895d-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="c895d-233">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SD-elementen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c895d-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="c895d-234">In geval van SD-elementen Hallo is elementen van de SD-gebruikers te maken een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c895d-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="c895d-235">**toocreate Britta Simon in SD-elementen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c895d-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="c895d-236">In een browservenster, aanmelding tooyour SD-elementen bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c895d-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="c895d-237">Klik in het menu bovenaan Hallo Hallo **Gebruikersbeheer**, en vervolgens **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c895d-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="c895d-239">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-239">Click **Add New User**.</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="c895d-241">Op Hallo **nieuwe gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c895d-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="c895d-243">a.</span><span class="sxs-lookup"><span data-stu-id="c895d-243">a.</span></span> <span data-ttu-id="c895d-244">In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c895d-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="c895d-245">b.</span><span class="sxs-lookup"><span data-stu-id="c895d-245">b.</span></span> <span data-ttu-id="c895d-246">In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c895d-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="c895d-247">c.</span><span class="sxs-lookup"><span data-stu-id="c895d-247">c.</span></span> <span data-ttu-id="c895d-248">In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c895d-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="c895d-249">d.</span><span class="sxs-lookup"><span data-stu-id="c895d-249">d.</span></span> <span data-ttu-id="c895d-250">Als **rol**, selecteer **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c895d-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="c895d-251">e.</span><span class="sxs-lookup"><span data-stu-id="c895d-251">e.</span></span> <span data-ttu-id="c895d-252">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="c895d-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c895d-253">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c895d-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c895d-254">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSD elementen.</span><span class="sxs-lookup"><span data-stu-id="c895d-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c895d-256">**tooassign Britta Simon tooSD elementen, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c895d-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="c895d-257">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c895d-259">Selecteer in de lijst met de toepassingen van Hallo **SD-elementen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-259">In hello applications list, select **SD Elements**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="c895d-261">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c895d-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c895d-263">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c895d-263">Click **Add** button.</span></span> <span data-ttu-id="c895d-264">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c895d-266">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c895d-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c895d-267">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c895d-268">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c895d-269">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c895d-269">Testing single sign-on</span></span>

<span data-ttu-id="c895d-270">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c895d-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="c895d-271">Wanneer u Hallo SD-elementen in het deelvenster toegang Hallo tegel klikt, krijgt u automatisch aangemelde tooyour elementen van de SD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c895d-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c895d-272">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c895d-272">Additional resources</span></span>

* [<span data-ttu-id="c895d-273">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c895d-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c895d-274">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c895d-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

