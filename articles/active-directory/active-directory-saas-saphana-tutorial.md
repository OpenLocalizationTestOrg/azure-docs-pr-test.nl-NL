---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP HANA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="fb5e7-103">Zelfstudie: Azure Active Directory-integratie met SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fb5e7-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="fb5e7-104">In deze zelfstudie leert u hoe toointegrate SAP HANA met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb5e7-105">SAP HANA integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb5e7-106">U kunt beheren in Azure AD wie toegang tot tooSAP HANA heeft</span><span class="sxs-lookup"><span data-stu-id="fb5e7-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="fb5e7-107">U kunt uw gebruikers tooautomatically get aangemelde tooSAP HANA (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fb5e7-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb5e7-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fb5e7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb5e7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb5e7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fb5e7-110">Prerequisites</span></span>

<span data-ttu-id="fb5e7-111">Azure AD-integratie met SAP HANA tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="fb5e7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fb5e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb5e7-113">Een SAP HANA eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fb5e7-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="fb5e7-114">Een actieve HANA exemplaar op een openbare IaaS, on-premises virtuele Azure-machines of grote SAP-exemplaren in Azure</span><span class="sxs-lookup"><span data-stu-id="fb5e7-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="fb5e7-115">Hallo XSA beheer Web Interface evenals HANA Studio is geïnstalleerd op Hallo HANA exemplaar.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5e7-116">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving van SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="fb5e7-117">Hallo-integratie eerst testen in ontwikkeling of staging-omgeving van toepassing hello en vervolgens gebruik Hallo productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="fb5e7-118">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb5e7-119">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb5e7-120">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb5e7-121">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fb5e7-121">Scenario description</span></span>
<span data-ttu-id="fb5e7-122">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb5e7-123">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb5e7-124">Het toevoegen van SAP HANA van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fb5e7-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="fb5e7-125">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fb5e7-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="fb5e7-126">Het toevoegen van SAP HANA van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fb5e7-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="fb5e7-127">tooconfigure hello integratie van SAP HANA in Azure AD, moet u tooadd SAP HANA uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb5e7-128">**tooadd SAP HANA via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fb5e7-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb5e7-129">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="fb5e7-131">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb5e7-132">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-132">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="fb5e7-134">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="fb5e7-136">Typ in het zoekvak Hallo **SAP HANA**, selecteer **SAP HANA** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Hallo nieuwe toepassing](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb5e7-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fb5e7-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb5e7-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SAP HANA op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="fb5e7-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fb5e7-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SAP HANA is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="fb5e7-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SAP HANA toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="fb5e7-142">Wijs in SAP HANA Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb5e7-143">tooconfigure en eenmalige aanmelding Azure AD-test met SAP HANA, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb5e7-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb5e7-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb5e7-146">**[Maken van een SAP HANA-testgebruiker](#creating-a-sap-hana-test-user)**  -toohave een equivalent van Britta Simon in SAP HANA die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb5e7-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb5e7-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb5e7-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fb5e7-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb5e7-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="fb5e7-151">**Voer tooconfigure Azure AD eenmalige aanmelding met SAP HANA Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fb5e7-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb5e7-152">In de Azure-portal op Hallo Hallo **SAP HANA** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fb5e7-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="fb5e7-156">Op Hallo **SAP HANA-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Domein- en URL's van eenmalige aanmelding informatie](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="fb5e7-158">a.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-158">a.</span></span> <span data-ttu-id="fb5e7-159">In Hallo **id** textbox type als:`HA100`</span><span class="sxs-lookup"><span data-stu-id="fb5e7-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="fb5e7-160">b.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-160">b.</span></span> <span data-ttu-id="fb5e7-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="fb5e7-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb5e7-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-162">These values are not real.</span></span> <span data-ttu-id="fb5e7-163">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="fb5e7-164">Neem contact op met [SAP HANA Client ondersteuningsteam](https://cloudplatform.sap.com/contact.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="fb5e7-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="fb5e7-167">Als het certificaat is niet actief vervolgens deze actief maken door te klikken op Hallo selectievakje 'Maken nieuw certificaat active' in hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="fb5e7-168">SAP HANA-toepassing verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="fb5e7-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="fb5e7-170">Hier wordt de Hallo hebt toegewezen **gebruikers-id** met **ExtractMailPrefix()** functie van **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="fb5e7-171">Dit geeft voorvoegsel op Hallo van e-mailadres van Hallo-gebruiker die is Hallo unieke gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="fb5e7-172">Dit wordt toohello SAP HANA-toepassing in elke geslaagde reactie verzonden.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="fb5e7-174">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="fb5e7-175">a.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-175">a.</span></span> <span data-ttu-id="fb5e7-176">In Hallo **gebruikers-id** vervolgkeuzelijst, selecteer **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="fb5e7-177">b.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-177">b.</span></span> <span data-ttu-id="fb5e7-178">In Hallo **Mail** vervolgkeuzelijst, selecteer **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="fb5e7-179">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-179">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="fb5e7-181">tooconfigure eenmalige aanmelding op **SAP HANA** side, aanmelding tooyour **HANA XSA webconsole** door te bladeren toohello respectieve HTTPS-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="fb5e7-182">In de standaardconfiguratie Hallo leidt Hallo URL Hallo aanvraag tooa aanmeldingsscherm, waarvoor Hallo referenties van een geverifieerde SAP HANA-database toocomplete Hallo aanmeldingsproces.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="fb5e7-183">Hallo-gebruiker die zich aanmeldt hebben Hallo bevoegdheden vereist tooperform SAML-beheertaken.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="fb5e7-184">Hallo XSA Web Interface, navigeert u in te**SAML-identiteitsprovider** en klik op Hallo van daaruit **'+'** -knop op Hallo Hallo scherm toodisplay Hallo toevoegen identiteit Provider Informatiedeelvenster onderaan en uit te voeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![ID-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="fb5e7-186">a.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-186">a.</span></span> <span data-ttu-id="fb5e7-187">In Hallo **toevoegen identiteit Provider Info** deelvenster plakken Hallo inhoud Hallo Metadata XML, die u hebt gedownload vanuit Azure-portal naar Hallo **metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Instellingen voor de id-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="fb5e7-189">b.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-189">b.</span></span> <span data-ttu-id="fb5e7-190">Als de inhoud van XML-document Hallo Hallo geldig zijn, Hallo bij het parseren van proces Hallo vereiste informatie op tooinsert haalt in Hallo **onderwerp, de entiteit-ID en de verlener** velden in algemene gegevens Hallo scherm en URL velden in Hallo Hallo Scherm doelgebied, bijvoorbeeld  **basis-URL en SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Instellingen voor de id-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="fb5e7-192">c.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-192">c.</span></span> <span data-ttu-id="fb5e7-193">In het naamvak Hallo Hallo algemene gegevens scherm, voer een naam voor de nieuwe SSO SAML-identiteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="fb5e7-194">de naam Hallo Hallo SAML IDP is verplicht en moet uniek zijn. deze weergegeven in Hallo lijst met beschikbare SAML IDPs die wordt weergegeven als u SAML als Hallo verificatiemethode voor SAP HANA XS toepassingen toouse, bijvoorbeeld bij Hallo verificatie scherm van Hallo XS artefact beheerprogramma voor websites selecteert.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="fb5e7-195">Hallo-details van nieuwe SAML-identiteitsprovider Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="fb5e7-196">Kies **opslaan** toosave details van SAML-identiteitsprovider Hallo Hallo en Hallo nieuwe SAML IDP toohello lijst met bekende SAML IDPs toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![knop Opslaan](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="fb5e7-198">In de Studio HANA binnen Systeemeigenschappen Hallo Hallo **configuratie** tabblad, alleen instellingen door te filteren **saml** en pas Hallo **assertion_timeout** van **10 sec** te**120 sec**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![assertion_timeout instelling](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="fb5e7-200">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb5e7-201">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb5e7-202">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb5e7-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb5e7-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fb5e7-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb5e7-204">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fb5e7-206">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fb5e7-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb5e7-207">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb5e7-209">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb5e7-211">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb5e7-213">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb5e7-215">a.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-215">a.</span></span> <span data-ttu-id="fb5e7-216">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb5e7-217">b.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-217">b.</span></span> <span data-ttu-id="fb5e7-218">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb5e7-219">c.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-219">c.</span></span> <span data-ttu-id="fb5e7-220">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb5e7-221">d.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-221">d.</span></span> <span data-ttu-id="fb5e7-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="fb5e7-223">De gebruiker van een SAP HANA-test maken</span><span class="sxs-lookup"><span data-stu-id="fb5e7-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="fb5e7-224">Azure AD tooenable gebruikers toolog in tooSAP HANA, moeten ze worden ingericht in SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="fb5e7-225">SAP HANA ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fb5e7-226">Als u handmatig een gebruiker toocreate moet, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5e7-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="fb5e7-227">Hallo externe verificatie door de gebruiker Hallo gebruikt, kunt u wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="fb5e7-228">Externe gebruikers worden geverifieerd met behulp van een extern systeem, bijvoorbeeld een Kerberos-systeem.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="fb5e7-229">Voor gedetailleerde informatie over externe identiteiten contact op met uw [domeinbeheerder](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="fb5e7-230">Open Hallo [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) als administrator en inschakelen Hallo DB-gebruiker voor SAML-SSO.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![Gebruiker maken](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="fb5e7-232">Maatstreepjes Hallo onzichtbaar selectievakje toohello links van de **SAML** en volg de koppeling van Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="fb5e7-233">Klik op **toevoegen** tooadd Hallo SAML IDP, en klik op **OK** juiste SAML IDP selecteren Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="fb5e7-234">Hallo toevoegen **externe identiteit** (ex.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="fb5e7-235">Hier BrittaSimon) of kies **''** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="fb5e7-236">Als 'Elke' selectievakje niet is ingeschakeld, wordt de Hallo-gebruikersnaam in HANA tooexactly overeen Hallo-naam van de gebruiker Hallo in Hallo UPN voordat het domeinachtervoegsel hello moet (dat wil zeggen BrittaSimon@contoso.com zou worden BrittaSimon in HANA).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="fb5e7-237">Voor testdoeleinden alle toewijzen **'XS'** rollen toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![rollen toewijzen](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="fb5e7-239">U moet deze geschikt is voor uw gebruiksvoorbeelden alleen machtigingen op te geven.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="fb5e7-240">Hallo gebruiker opslaan.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb5e7-241">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb5e7-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb5e7-242">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="fb5e7-244">**tooassign Britta Simon tooSAP HANA, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fb5e7-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb5e7-245">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fb5e7-247">Selecteer in de lijst met de toepassingen van Hallo **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Gebruiker toewijzen](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="fb5e7-249">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="fb5e7-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-251">Click **Add** button.</span></span> <span data-ttu-id="fb5e7-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="fb5e7-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb5e7-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb5e7-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb5e7-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fb5e7-257">Testing single sign-on</span></span>

<span data-ttu-id="fb5e7-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb5e7-259">Als u op Hallo SAP HANA-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAP HANA-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fb5e7-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="fb5e7-260">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb5e7-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb5e7-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fb5e7-261">Additional resources</span></span>

* [<span data-ttu-id="fb5e7-262">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5e7-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb5e7-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb5e7-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

