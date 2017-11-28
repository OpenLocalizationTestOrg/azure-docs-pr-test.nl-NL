---
title: 'Zelfstudie: Azure Active Directory-integratie met identiteitsverificatie voor SAP HANA Cloud Platform | Microsoft Docs'
description: Ontdek hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP HANA Cloud Platform identiteitsverificatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="841f1-103">Zelfstudie: Azure Active Directory-integratie met identiteitsverificatie voor SAP HANA Cloud-Platform</span><span class="sxs-lookup"><span data-stu-id="841f1-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="841f1-104">In deze zelfstudie leert u hoe toointegrate SAP HANA Cloud Platform-ID-verificatie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="841f1-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="841f1-105">SAP HANA Cloud Platform-ID-verificatie wordt gebruikt als een proxy IdP tooaccess SAP-toepassingen met behulp van Azure AD als belangrijkste IdP Hallo.</span><span class="sxs-lookup"><span data-stu-id="841f1-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="841f1-106">SAP HANA Cloud Platform-identiteitsverificatie integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="841f1-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="841f1-107">U kunt beheren in Azure AD die tooSAP-toegangstoepassing heeft</span><span class="sxs-lookup"><span data-stu-id="841f1-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="841f1-108">U kunt uw gebruikers tooautomatically get aangemelde tooSAP toepassingen eenmalige aanmelding (SSO) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="841f1-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="841f1-109">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="841f1-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="841f1-110">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="841f1-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="841f1-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="841f1-111">Prerequisites</span></span>

<span data-ttu-id="841f1-112">tooconfigure Azure AD-integratie met identiteitsverificatie voor SAP HANA Cloud-Platform, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="841f1-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="841f1-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="841f1-113">An Azure AD subscription</span></span>
- <span data-ttu-id="841f1-114">Een **identiteitsverificatie voor SAP HANA Cloud Platform** SSO abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="841f1-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="841f1-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="841f1-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="841f1-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="841f1-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="841f1-117">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="841f1-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="841f1-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="841f1-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="841f1-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="841f1-119">Scenario description</span></span>
<span data-ttu-id="841f1-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="841f1-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="841f1-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="841f1-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="841f1-122">Het toevoegen van identiteitsverificatie voor SAP HANA Cloud Platform van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="841f1-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="841f1-123">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="841f1-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="841f1-124">Vooraleer Hallo technische gegevens, is het essentieel toounderstand Hallo concepten die u gaat toolook op.</span><span class="sxs-lookup"><span data-stu-id="841f1-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="841f1-125">Hallo identiteitsverificatie voor SAP HANA Cloud-Platform en Azure Active Directory federation kunt u tooimplement eenmalige aanmelding via toepassingen of services die zijn beveiligd door AAD (als een IdP) met SAP-toepassingen en services die zijn beveiligd door SAP HANA Cloud Platform-identiteit -Verificatie.</span><span class="sxs-lookup"><span data-stu-id="841f1-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="841f1-126">Op dit moment fungeert identiteitsverificatie voor SAP HANA Cloud Platform als een Proxy-identiteitsprovider tooSAP-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="841f1-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="841f1-127">Azure Active Directory wordt op zijn beurt fungeert als Hallo voorloopspaties id-Provider in deze installatie.</span><span class="sxs-lookup"><span data-stu-id="841f1-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="841f1-128">Hallo volgende diagram illustreert dit:</span><span class="sxs-lookup"><span data-stu-id="841f1-128">hello following diagram illustrates this:</span></span>    

![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="841f1-130">Met deze instelling wordt uw tenant identiteitsverificatie voor SAP HANA Cloud-Platform worden geconfigureerd als een vertrouwde toepassing in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="841f1-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="841f1-131">Alle SAP-toepassingen en services die u wilt dat tooprotect via deze manier worden vervolgens geconfigureerd in de beheerconsole van Hallo identiteitsverificatie voor SAP HANA Cloud Platform!</span><span class="sxs-lookup"><span data-stu-id="841f1-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="841f1-132">Dit betekent dat autorisatie voor het verlenen van toegang tooSAP toepassingen en services-behoeften tootake plaats in identiteitsverificatie voor SAP HANA Cloud Platform voor dergelijke installatie (als tegengestelde tooconfiguring autorisatie in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="841f1-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="841f1-133">Identiteitsverificatie voor SAP HANA Cloud Platform configureren als een toepassing via hello Azure Active Directory Marketplace, hoeft u niet tootake antwoord voor het configureren van benodigde afzonderlijke claims / SAML asserties en transformaties nodig tooproduce een geldige verificatietoken voor SAP-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="841f1-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="841f1-134">Web-SSO is momenteel getest door beide partijen alleen.</span><span class="sxs-lookup"><span data-stu-id="841f1-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="841f1-135">Stromen nodig voor App-naar-API of API-API-communicatie moeten werken, maar zijn niet getest, nog.</span><span class="sxs-lookup"><span data-stu-id="841f1-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="841f1-136">Ze worden getest als onderdeel van de volgende activiteiten.</span><span class="sxs-lookup"><span data-stu-id="841f1-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="841f1-137">Identiteitsverificatie voor SAP HANA Cloud Platform van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="841f1-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="841f1-138">tooconfigure hello integratie van identiteitsverificatie voor SAP HANA Cloud-Platform in Azure AD, moet u tooadd identiteitsverificatie voor SAP HANA Cloud Platform uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="841f1-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="841f1-139">**tooadd SAP HANA Cloud Platform identiteitsverificatie via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="841f1-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="841f1-140">In Hallo [ **Azure Management portal**](https://portal.azure.com), Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="841f1-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="841f1-142">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="841f1-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="841f1-143">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="841f1-143">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="841f1-145">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="841f1-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="841f1-147">Typ in het zoekvak Hallo **identiteitsverificatie voor SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="841f1-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="841f1-149">Selecteer in het deelvenster resultaten hello, **identiteitsverificatie voor SAP HANA Cloud Platform**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="841f1-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="841f1-151">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="841f1-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="841f1-152">In deze sectie kunt u configureren en testen van Azure AD-SSO met SAP HANA Cloud Platform identiteitsverificatie op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="841f1-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="841f1-153">Voor eenmalige aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in identiteitsverificatie voor SAP HANA Cloud Platform is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="841f1-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="841f1-154">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in identiteitsverificatie voor SAP HANA Cloud Platform toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="841f1-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="841f1-155">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in identiteitsverificatie voor SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="841f1-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="841f1-156">tooconfigure en test Azure AD-SSO met identiteitsverificatie voor SAP HANA Cloud-Platform, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="841f1-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="841f1-157">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="841f1-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="841f1-158">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="841f1-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="841f1-159">**[Maken van een testgebruiker identiteitsverificatie voor SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave een equivalent van Britta Simon in SAP HANA Cloud Platform verificatie van de identiteit die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="841f1-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="841f1-160">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="841f1-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="841f1-161">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="841f1-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="841f1-162">Configuratie van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="841f1-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="841f1-163">In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in hello Azure Management portal en eenmalige aanmelding configureren in uw toepassing identiteitsverificatie voor SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="841f1-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="841f1-164">Hallo SAML asserties verwacht identiteitsverificatie voor SAP HANA Cloud Platform toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="841f1-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="841f1-165">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="841f1-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="841f1-166">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="841f1-166">hello following screenshot shows an example for this.</span></span>

![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="841f1-168">**Azure AD-SSO met SAP HANA Cloud Platform identiteitsverificatie tooconfigure uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="841f1-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="841f1-169">In hello Azure Management portal op Hallo **identiteitsverificatie voor SAP HANA Cloud Platform** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="841f1-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="841f1-171">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="841f1-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren][5]

3. <span data-ttu-id="841f1-173">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster als uw SAP-toepassing een kenmerk bijvoorbeeld 'firstName' wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="841f1-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="841f1-174">Voeg op Hallo SAML-token kenmerken dialoogvenster Hallo 'firstName'-kenmerk.</span><span class="sxs-lookup"><span data-stu-id="841f1-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="841f1-175">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Eenmalige aanmelding configureren][6]

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="841f1-178">In Hallo **kenmerknaam** textbox type Hallo kenmerknaam 'firstName'.</span><span class="sxs-lookup"><span data-stu-id="841f1-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="841f1-179">Van Hallo **kenmerkwaarde** wilt weergeven, selecteer Hallo kenmerkwaarde 'user.givenname'.</span><span class="sxs-lookup"><span data-stu-id="841f1-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="841f1-180">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="841f1-180">Click **Ok**.</span></span>

4. <span data-ttu-id="841f1-181">Op Hallo **SAP HANA Cloud Platform identiteit verificatiedomein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="841f1-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="841f1-183">In Hallo **aanmelding op URL** textbox, typt u Hallo aanmelding op de URL voor Hallo SAP-toepassing.</span><span class="sxs-lookup"><span data-stu-id="841f1-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="841f1-184">In Hallo **id** textbox Hallo typewaarde patroon volgen:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="841f1-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="841f1-185">Als u deze waarde niet weet, volg Hallo identiteitsverificatie voor SAP HANA Cloud Platform documentatie op [Tenantconfiguratie SAML 2.0](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="841f1-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="841f1-186">Op Hallo **SAP HANA Cloud Identity verificatie platformconfiguratie** sectie, klikt u op **configureren SAP HANA Cloud Platform identiteitsverificatie** tooopen **aanmeldingconfigureren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="841f1-187">Klik vervolgens op **SAML XML-metagegevens** en Hallo-bestand op uw computer op te slaan.</span><span class="sxs-lookup"><span data-stu-id="841f1-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="841f1-190">tooget SSO is geconfigureerd voor uw toepassing gaat tooSAP HANA Cloud Platform identiteit verificatie-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="841f1-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="841f1-191">Hallo-URL heeft Hallo patroon volgen:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="841f1-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="841f1-192">Volg Hallo-documentatie op identiteitsverificatie voor SAP HANA Cloud Platform te[Configure Microsoft Azure AD als zakelijke id-Provider op identiteitsverificatie voor SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="841f1-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="841f1-193">Klik in hello Azure Management portal op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="841f1-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="841f1-194">Volgende stappen uit als u tooadd wilt en eenmalige aanmelding voor een andere SAP-toepassing inschakelen hello blijven.</span><span class="sxs-lookup"><span data-stu-id="841f1-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="841f1-195">Herhaal de stappen onder Hallo sectie 'Toevoegen SAP HANA Cloud Platform identiteitsverificatie uit de galerie Hallo' tooadd een ander exemplaar van identiteitsverificatie voor SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="841f1-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="841f1-196">In hello Azure Management portal op Hallo **identiteitsverificatie voor SAP HANA Cloud Platform** toepassing Integratiepagina, klikt u op **gekoppelde aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="841f1-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Gekoppelde aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="841f1-198">Vervolgens Hallo-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="841f1-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="841f1-199">de nieuwe toepassing Hello wordt Hallo SSO-configuratie voor de vorige SAP-toepassing hello gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="841f1-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="841f1-200">Controleer of u gebruik Hallo dezelfde zakelijke identiteitsproviders in Hallo SAP HANA Cloud Platform identiteit verificatie-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="841f1-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="841f1-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="841f1-201">Create an Azure AD test user</span></span>
<span data-ttu-id="841f1-202">Hallo-doel van deze sectie is toocreate een testgebruiker in de nieuwe portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="841f1-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="841f1-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="841f1-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="841f1-205">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="841f1-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="841f1-207">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="841f1-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="841f1-209">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="841f1-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="841f1-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="841f1-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="841f1-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="841f1-214">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="841f1-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="841f1-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="841f1-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="841f1-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="841f1-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="841f1-217">Maak een testgebruiker identiteitsverificatie voor SAP HANA Cloud-Platform</span><span class="sxs-lookup"><span data-stu-id="841f1-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="841f1-218">U hoeft niet toocreate een gebruiker op identiteitsverificatie voor SAP HANA Cloud-Platform.</span><span class="sxs-lookup"><span data-stu-id="841f1-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="841f1-219">Gebruikers die zich in het archief hello Azure AD-gebruiker kunnen Hallo SSO-functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="841f1-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="841f1-220">SAP HANA Cloud Platform-identiteitsverificatie ondersteunt Hallo identiteitsfederatie optie.</span><span class="sxs-lookup"><span data-stu-id="841f1-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="841f1-221">Deze optie kunt Hallo toepassing toocheck als Hallo gebruikers door de zakelijke identiteitsprovider Hallo geverifieerde in Hallo store van SAP HANA Cloud Platform identiteit gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="841f1-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="841f1-222">In de standaardinstelling Hallo is Hallo identiteitsfederatie optie uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="841f1-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="841f1-223">Als identiteitsfederatie is ingeschakeld, zijn alleen Hallo-gebruikers die worden geïmporteerd in identiteitsverificatie voor SAP HANA Cloud-Platform kunnen tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="841f1-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="841f1-224">Voor meer informatie over hoe tooenable of schakelt u identiteitsfederatie met SAP HANA Cloud Platform identiteitsverificatie, identiteitsfederatie inschakelen met SAP HANA Cloud Platform identiteitsverificatie in zien [identiteitsfederatie configureren Hello Store van SAP HANA Cloud Platform identiteit gebruikersverificatie. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="841f1-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="841f1-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="841f1-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="841f1-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooSAP HANA Cloud Platform identiteitsverificatie verlenen.</span><span class="sxs-lookup"><span data-stu-id="841f1-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="841f1-228">**tooassign Britta Simon tooSAP HANA Cloud Platform identiteitsverificatie Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="841f1-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="841f1-229">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="841f1-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="841f1-231">Selecteer in de lijst met de toepassingen van Hallo **identiteitsverificatie voor SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="841f1-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="841f1-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="841f1-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="841f1-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="841f1-235">Click **Add** button.</span></span> <span data-ttu-id="841f1-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="841f1-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="841f1-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="841f1-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="841f1-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="841f1-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="841f1-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="841f1-241">Test single sign-on</span></span>

<span data-ttu-id="841f1-242">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="841f1-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="841f1-243">Als u op Hallo identiteitsverificatie voor SAP HANA Cloud Platform-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour identiteitsverificatie voor SAP HANA Cloud Platform-toepassing.</span><span class="sxs-lookup"><span data-stu-id="841f1-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="841f1-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="841f1-244">Additional resources</span></span>

* [<span data-ttu-id="841f1-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="841f1-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="841f1-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="841f1-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png