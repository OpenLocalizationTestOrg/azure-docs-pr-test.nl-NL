---
title: "Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en IBM Kenexa enquête Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="c7081-103">Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise</span><span class="sxs-lookup"><span data-stu-id="c7081-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="c7081-104">In deze zelfstudie leert u hoe toointegrate IBM Kenexa enquête Enterprise met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7081-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7081-105">IBM Kenexa enquête Enterprise integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c7081-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7081-106">U kunt beheren in Azure AD die toegang tooIBM Kenexa enquête onderneming heeft.</span><span class="sxs-lookup"><span data-stu-id="c7081-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="c7081-107">U kunt uw gebruikers tooautomatically aanmelding tooIBM Kenexa enquête Enterprise inschakelen met behulp van eenmalige aanmelding (SSO) met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="c7081-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c7081-108">U kunt uw accounts op één locatie beheren: hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c7081-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="c7081-109">Als u tooknow meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7081-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7081-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7081-110">Prerequisites</span></span>

<span data-ttu-id="c7081-111">Azure AD-integratie met IBM Kenexa enquête Enterprise tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c7081-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="c7081-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c7081-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7081-113">Een abonnement IBM Kenexa enquête Enterprise SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="c7081-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7081-114">Wanneer u Hallo stappen in deze zelfstudie test, wordt u aangeraden een productie-omgeving niet te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c7081-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="c7081-115">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="c7081-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c7081-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c7081-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7081-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7081-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7081-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c7081-118">Scenario description</span></span>
<span data-ttu-id="c7081-119">In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c7081-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="c7081-120">Hallo scenario beschreven in de zelfstudie Hallo bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c7081-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="c7081-121">IBM Kenexa enquête Enterprise uit Hallo galerie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c7081-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="c7081-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="c7081-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="c7081-123">IBM Kenexa enquête Enterprise van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7081-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="c7081-124">IBM Kenexa enquête Enterprise tooconfigure Hallo integratie van IBM Kenexa enquête onderneming in Azure AD toevoegen via Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c7081-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7081-125">IBM Kenexa enquête Enterprise via Hallo gallery tooadd Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7081-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="c7081-126">In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="c7081-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="c7081-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c7081-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="c7081-130">tooadd een toepassing, klikt u op Hallo **nieuwe toepassing** knop.</span><span class="sxs-lookup"><span data-stu-id="c7081-130">tooadd an application, click hello **New application** button.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="c7081-132">Typ in het zoekvak Hallo **IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="c7081-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="c7081-134">Selecteer in de lijst met resultaten Hallo **IBM Kenexa enquête Enterprise**, en klik vervolgens op Hallo **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c7081-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa enquête Enterprise in de lijst met resultaten Hallo](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c7081-136">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7081-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c7081-137">In deze sectie kunt u configureren en testen van Azure AD-SSO met IBM Kenexa enquête Enterprise op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c7081-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7081-138">Voor eenmalige aanmelding toowork moet Azure AD tooidentify Hallo IBM Kenexa enquête Enterprise gebruiker equivalent in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7081-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="c7081-139">Azure AD moet met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en een bijbehorende gebruiker maken in IBM Kenexa enquête onderneming.</span><span class="sxs-lookup"><span data-stu-id="c7081-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="c7081-140">Hallo-waarde toewijzen Hallo-tooestablish Hallo koppeling relatie **gebruikersnaam** in IBM Kenexa enquête Enterprise als de waarde Hallo Hallo **gebruikersnaam** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7081-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="c7081-141">Hallo bouwstenen in de volgende twee secties Hallo tooconfigure en test Azure AD-SSO met IBM Kenexa enquête Enterprise, voltooid.</span><span class="sxs-lookup"><span data-stu-id="c7081-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c7081-142">Azure AD-eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="c7081-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="c7081-143">In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing IBM Kenexa enquête Enterprise door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="c7081-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="c7081-144">In de Azure-portal op Hallo Hallo **IBM Kenexa enquête Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c7081-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa enquête Enterprise configureren één aanmelding koppeling][4]

2. <span data-ttu-id="c7081-146">In Hallo **eenmalige aanmelding** dialoogvenster in Hallo **modus** de optie **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c7081-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="c7081-148">In Hallo **IBM Kenexa enquête Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7081-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![IBM Kenexa enquête Enterprise domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="c7081-150">a.</span><span class="sxs-lookup"><span data-stu-id="c7081-150">a.</span></span> <span data-ttu-id="c7081-151">In Hallo **id** textbox type een URL met Hallo patroon volgen:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="c7081-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="c7081-152">b.</span><span class="sxs-lookup"><span data-stu-id="c7081-152">b.</span></span> <span data-ttu-id="c7081-153">In Hallo **antwoord-URL** textbox type een URL met Hallo patroon volgen:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="c7081-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7081-154">Hallo voorgaande waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c7081-154">hello preceding values are not real.</span></span> <span data-ttu-id="c7081-155">Deze bijwerken met de werkelijke Hallo-id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="c7081-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="c7081-156">tooobtain Werkelijke waarden, neem contact op met Hallo Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="c7081-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="c7081-157">Onder **SAML-certificaat voor ondertekening van**, klikt u op **certificaat (Base64)**, en sla Hallo certificaat bestand tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="c7081-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![Hallo downloadkoppeling voor het certificaat (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="c7081-159">Hallo IBM Kenexa enquête bedrijfstoepassing verwacht tooreceive Hallo Security Asserties Markup Language (SAML) asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen toohello configuratie van de kenmerken van SAML-token.</span><span class="sxs-lookup"><span data-stu-id="c7081-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="c7081-160">Hallo waarde van Hallo gebruiker-id claim Hallo antwoord moet overeenkomen met Hallo SSO-ID die geconfigureerd in Hallo Kenexa systeem.</span><span class="sxs-lookup"><span data-stu-id="c7081-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="c7081-161">toomap Hallo juiste gebruikers-id in uw organisatie als SSO Internet Datagram Protocol (IDP), werken met Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="c7081-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="c7081-162">Azure AD wordt standaard Hallo gebruikers-id als Hallo gebruiker UPN (User Principal Name)-waarde ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c7081-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="c7081-163">U kunt deze waarde op Hallo wijzigen **kenmerk** tabblad, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7081-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="c7081-164">Hallo-integratie werkt alleen nadat u de toewijzing correct Hallo hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="c7081-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![Hallo gebruikerskenmerken dialoogvenster](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="c7081-166">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c7081-166">Click **Save**.</span></span>

    ![Hallo configureren eenmalige aanmelding knop Opslaan](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7081-168">Hallo tooopen **eenmalige aanmelding configureren** venster onder **IBM Kenexa enquête Enterprise Configuration**, klikt u op **configureren IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="c7081-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Hallo configureren IBM Kenexa enquête Enterprise-koppeling](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="c7081-170">Kopiëren Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML één Service-URL aanmelding** waarden uit Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="c7081-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="c7081-171">In Hallo **eenmalige aanmelding configureren** venster onder **Naslaggids**, kopie Hallo **Sign-Out URL**, **SAML entiteit-ID**, en  **SAML één Service-URL aanmelding** waarden.</span><span class="sxs-lookup"><span data-stu-id="c7081-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="c7081-172">tooconfigure SSO op Hallo **IBM Kenexa enquête Enterprise** zijde, Hallo gedownload verzenden **certificaat (Base64)**, **Sign-Out URL**, **SAML entiteit-ID**, en **SAML één Service-URL aanmelding** waarden toohello [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="c7081-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="c7081-173">U kunt verwijzen tooa beknopte versie van deze instructies in Hallo [Azure-portal](https://portal.azure.com) terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c7081-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="c7081-174">Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, klikt u op Hallo **eenmalige aanmelding** tabblad en vervolgens toegang Hallo ingesloten documentatie via Hallo **configuratie** sectie aan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="c7081-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="c7081-175">toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [documentatie van Azure AD ingesloten](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c7081-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c7081-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c7081-176">Create an Azure AD test user</span></span>
<span data-ttu-id="c7081-177">In deze sectie kunt u testgebruiker Britta Simon in hello Azure-portal maken door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="c7081-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Een Azure AD-testgebruiker maken][100]

1. <span data-ttu-id="c7081-179">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="c7081-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7081-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c7081-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7081-183">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c7081-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7081-185">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7081-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7081-187">a.</span><span class="sxs-lookup"><span data-stu-id="c7081-187">a.</span></span> <span data-ttu-id="c7081-188">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7081-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7081-189">b.</span><span class="sxs-lookup"><span data-stu-id="c7081-189">b.</span></span> <span data-ttu-id="c7081-190">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="c7081-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c7081-191">c.</span><span class="sxs-lookup"><span data-stu-id="c7081-191">c.</span></span> <span data-ttu-id="c7081-192">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="c7081-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c7081-193">d.</span><span class="sxs-lookup"><span data-stu-id="c7081-193">d.</span></span> <span data-ttu-id="c7081-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c7081-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="c7081-195">Een IBM Kenexa enquête Enterprise testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c7081-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="c7081-196">In deze sectie kunt u een gebruiker met de naam van Britta Simon in IBM Kenexa enquête onderneming maken.</span><span class="sxs-lookup"><span data-stu-id="c7081-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="c7081-197">toocreate gebruikers in Hallo IBM Kenexa enquête bedrijfssysteem en kaart Hallo SSO-ID voor deze, kunt u samenwerken met Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="c7081-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="c7081-198">Deze waarde SSO-ID moet ook toegewezen toohello gebruiker id-waarde van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7081-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="c7081-199">U kunt deze standaardinstelling op Hallo wijzigen **kenmerk** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c7081-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c7081-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7081-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c7081-201">In deze sectie kunt u gebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooIBM Kenexa enquête Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c7081-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="c7081-203">tooassign gebruiker Britta Simon tooIBM Kenexa enquête Enterprise, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7081-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="c7081-204">Open in hello Azure-portal, Hallo **toepassingen** weergeven, gaat u toohello **Directory** weergave, selecteer **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c7081-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Hallo 'bedrijfstoepassingen' en 'Alle toepassingen' koppelingen][201] 

2. <span data-ttu-id="c7081-206">In Hallo **toepassingen** selecteert **IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="c7081-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Hallo IBM Kenexa enquête Enterprise koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="c7081-208">Klik in het linkerdeelvenster Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c7081-208">In hello left pane, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="c7081-210">Klik op Hallo **toevoegen** knop en klik vervolgens op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c7081-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="c7081-212">In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c7081-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="c7081-213">In Hallo **gebruikers en groepen** dialoogvenster vak, klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="c7081-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="c7081-214">In Hallo **toevoegen toewijzing** dialoogvenster vak, klikt u op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="c7081-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c7081-215">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c7081-215">Test single sign-on</span></span>

<span data-ttu-id="c7081-216">In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c7081-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="c7081-217">Wanneer u klikt op Hallo **IBM Kenexa enquête Enterprise** tegel in Hallo Toegangsvenster, u moet automatisch aangemeld tooyour IBM Kenexa enquête bedrijfstoepassing.</span><span class="sxs-lookup"><span data-stu-id="c7081-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7081-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c7081-218">Additional resources</span></span>

* [<span data-ttu-id="c7081-219">Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7081-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7081-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7081-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
