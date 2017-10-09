---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Cloud voor de klant.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="64fc8-103">Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant</span><span class="sxs-lookup"><span data-stu-id="64fc8-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="64fc8-104">In deze zelfstudie leert u hoe toointegrate SAP Cloud voor klanten met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64fc8-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64fc8-105">Integratie van SAP Cloud voor klanten met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64fc8-106">U kunt beheren in Azure AD die toegang tooSAP Cloud voor de klant heeft</span><span class="sxs-lookup"><span data-stu-id="64fc8-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="64fc8-107">U kunt uw gebruikers tooautomatically get aangemelde tooSAP Cloud inschakelen voor de klant (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="64fc8-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64fc8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="64fc8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="64fc8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64fc8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64fc8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64fc8-110">Prerequisites</span></span>

<span data-ttu-id="64fc8-111">Azure AD-integratie met SAP Cloud voor klant tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="64fc8-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="64fc8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="64fc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64fc8-113">Een Cloud SAP voor eenmalige aanmelding klant abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="64fc8-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64fc8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="64fc8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64fc8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64fc8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="64fc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64fc8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64fc8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64fc8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="64fc8-118">Scenario description</span></span>
<span data-ttu-id="64fc8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="64fc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64fc8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64fc8-121">SAP Cloud toe te voegen voor de klant uit Hallo galerie</span><span class="sxs-lookup"><span data-stu-id="64fc8-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="64fc8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64fc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="64fc8-123">SAP Cloud toe te voegen voor de klant uit Hallo galerie</span><span class="sxs-lookup"><span data-stu-id="64fc8-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="64fc8-124">tooconfigure hello integratie van SAP Cloud voor klanten met Azure AD, moet u tooadd SAP-Cloud van Hallo galerie tooyour lijst met beheerde SaaS-apps voor de klant.</span><span class="sxs-lookup"><span data-stu-id="64fc8-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64fc8-125">**tooadd SAP Cloud voor klant via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64fc8-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64fc8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="64fc8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64fc8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64fc8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="64fc8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64fc8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="64fc8-133">Typ in het zoekvak Hallo **SAP Cloud voor klant**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="64fc8-135">Selecteer in het deelvenster resultaten hello, **SAP Cloud voor klant**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="64fc8-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64fc8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64fc8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64fc8-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAP Cloud voor klant op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="64fc8-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64fc8-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Cloud SAP voor de klant is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64fc8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="64fc8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Cloud voor klant SAP Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="64fc8-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="64fc8-141">In de Cloud SAP voor de klant, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="64fc8-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64fc8-142">tooconfigure en test eenmalige aanmelding Azure AD met SAP Cloud voor de klant, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64fc8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="64fc8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64fc8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64fc8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64fc8-145">**[Maken van een Cloud SAP voor klant testgebruiker](#creating-a-sap-cloud-for-customer-test-user)**  -toohave een equivalent van Britta Simon in SAP Cloud voor de klant die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="64fc8-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64fc8-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="64fc8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64fc8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="64fc8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64fc8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="64fc8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64fc8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Cloud SAP voor toepassing van de klant.</span><span class="sxs-lookup"><span data-stu-id="64fc8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="64fc8-150">**tooconfigure eenmalige aanmelding Azure AD met SAP Cloud voor klant, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64fc8-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="64fc8-151">In Azure-portal op Hallo Hallo **SAP Cloud voor klant** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="64fc8-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="64fc8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="64fc8-155">Op Hallo **SAP Cloud voor domein van de klant en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="64fc8-157">a.</span><span class="sxs-lookup"><span data-stu-id="64fc8-157">a.</span></span> <span data-ttu-id="64fc8-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="64fc8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="64fc8-159">b.</span><span class="sxs-lookup"><span data-stu-id="64fc8-159">b.</span></span> <span data-ttu-id="64fc8-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="64fc8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64fc8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="64fc8-161">These values are not real.</span></span> <span data-ttu-id="64fc8-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="64fc8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="64fc8-163">Neem contact op met [SAP Cloud voor klant Client ondersteuningsteam](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="64fc8-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="64fc8-164">Op Hallo **gebruikerskenmerken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="64fc8-166">a.</span><span class="sxs-lookup"><span data-stu-id="64fc8-166">a.</span></span> <span data-ttu-id="64fc8-167">In **gebruikers-id** lijst, selecteer Hallo **ExtractMailPrefix()** functie.</span><span class="sxs-lookup"><span data-stu-id="64fc8-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="64fc8-168">b.</span><span class="sxs-lookup"><span data-stu-id="64fc8-168">b.</span></span> <span data-ttu-id="64fc8-169">Van Hallo **Mail** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="64fc8-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="64fc8-170">Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="64fc8-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="64fc8-171">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="64fc8-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="64fc8-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="64fc8-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="64fc8-175">Op Hallo **SAP Cloud voor de configuratie van de klant** sectie, klikt u op **SAP Cloud configureren voor de klant** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="64fc8-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="64fc8-176">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="64fc8-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="64fc8-178">tooget SSO is geconfigureerd, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="64fc8-179">a.</span><span class="sxs-lookup"><span data-stu-id="64fc8-179">a.</span></span> <span data-ttu-id="64fc8-180">De aanmelding in de Cloud SAP voor Customer portal met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="64fc8-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="64fc8-181">b.</span><span class="sxs-lookup"><span data-stu-id="64fc8-181">b.</span></span> <span data-ttu-id="64fc8-182">Navigeer toohello **toepassings- en algemene beheertaak gebruiker** en klik op Hallo **identiteitsprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="64fc8-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="64fc8-183">c.</span><span class="sxs-lookup"><span data-stu-id="64fc8-183">c.</span></span> <span data-ttu-id="64fc8-184">Klik op **nieuwe identiteitsprovider** en selecteer Hallo metagegevens XML-bestand die u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="64fc8-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="64fc8-185">Door het importeren van metagegevens Hallo uploadt Hallo systeem automatisch Hallo vereist handtekeningcertificaat en -versleutelingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="64fc8-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="64fc8-187">d.</span><span class="sxs-lookup"><span data-stu-id="64fc8-187">d.</span></span> <span data-ttu-id="64fc8-188">Azure Active Directory vereist Hallo element Assertion Consumer Service-URL in Hallo SAML-aanvraag, dus selecteer Hallo **Assertion Consumer Service-URL opnemen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="64fc8-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="64fc8-189">e.</span><span class="sxs-lookup"><span data-stu-id="64fc8-189">e.</span></span> <span data-ttu-id="64fc8-190">Klik op **activeren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="64fc8-191">f.</span><span class="sxs-lookup"><span data-stu-id="64fc8-191">f.</span></span> <span data-ttu-id="64fc8-192">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="64fc8-192">Save your changes.</span></span>
   
    <span data-ttu-id="64fc8-193">g.</span><span class="sxs-lookup"><span data-stu-id="64fc8-193">g.</span></span> <span data-ttu-id="64fc8-194">Klik op Hallo **mijn systeem** tabblad.</span><span class="sxs-lookup"><span data-stu-id="64fc8-194">Click hello **My System** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="64fc8-196">h.</span><span class="sxs-lookup"><span data-stu-id="64fc8-196">h.</span></span> <span data-ttu-id="64fc8-197">In **Azure AD aanmelding URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="64fc8-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="64fc8-199">ik.</span><span class="sxs-lookup"><span data-stu-id="64fc8-199">i.</span></span> <span data-ttu-id="64fc8-200">Opgeven of Hallo werknemer handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door het selecteren van Hallo **handmatige identiteit Provider selectie**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="64fc8-201">j.</span><span class="sxs-lookup"><span data-stu-id="64fc8-201">j.</span></span> <span data-ttu-id="64fc8-202">In Hallo **URL SSO** sectie Hallo URL opgeven die moet worden gebruikt door uw werknemers toosign op toohello systeem.</span><span class="sxs-lookup"><span data-stu-id="64fc8-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="64fc8-203">In Hallo **tooEmployee URL verzonden** lijst, kunt u kiezen tussen Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="64fc8-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="64fc8-204">**Niet-SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="64fc8-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="64fc8-205">Hallo system verzendt alleen Hallo normale system URL toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="64fc8-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="64fc8-206">Hallo werknemer kan niet aanmelden met eenmalige aanmelding, en moet gebruik wachtwoord of certificaat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="64fc8-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="64fc8-207">**URL VOOR EENMALIGE AANMELDING**</span><span class="sxs-lookup"><span data-stu-id="64fc8-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="64fc8-208">Hallo system verzendt alleen Hallo URL SSO toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="64fc8-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="64fc8-209">Hallo werknemers kan zich aanmelden met behulp van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="64fc8-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="64fc8-210">Authenticatie-aanvraag wordt omgeleid via Hallo IdP.</span><span class="sxs-lookup"><span data-stu-id="64fc8-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="64fc8-211">**Automatische selectie**</span><span class="sxs-lookup"><span data-stu-id="64fc8-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="64fc8-212">Als eenmalige aanmelding niet actief is, verzendt het afdruksysteem van Hallo Hallo normale system URL toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="64fc8-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="64fc8-213">Als eenmalige aanmelding actief is, controleert Hallo system of Hallo werknemer een wachtwoord heeft.</span><span class="sxs-lookup"><span data-stu-id="64fc8-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="64fc8-214">Als een wachtwoord beschikbaar is, worden zowel de URL van de SSO- en Non-SSO-toohello werknemer verzonden.</span><span class="sxs-lookup"><span data-stu-id="64fc8-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="64fc8-215">Als Hallo werknemer geen wachtwoord heeft, is alleen Hallo URL SSO echter toohello werknemer verzonden.</span><span class="sxs-lookup"><span data-stu-id="64fc8-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="64fc8-216">k.</span><span class="sxs-lookup"><span data-stu-id="64fc8-216">k.</span></span> <span data-ttu-id="64fc8-217">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="64fc8-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="64fc8-218">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="64fc8-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64fc8-219">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="64fc8-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64fc8-220">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64fc8-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64fc8-221">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="64fc8-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="64fc8-222">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="64fc8-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="64fc8-224">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64fc8-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64fc8-225">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="64fc8-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64fc8-227">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64fc8-229">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="64fc8-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64fc8-231">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="64fc8-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64fc8-233">a.</span><span class="sxs-lookup"><span data-stu-id="64fc8-233">a.</span></span> <span data-ttu-id="64fc8-234">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64fc8-235">b.</span><span class="sxs-lookup"><span data-stu-id="64fc8-235">b.</span></span> <span data-ttu-id="64fc8-236">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64fc8-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64fc8-237">c.</span><span class="sxs-lookup"><span data-stu-id="64fc8-237">c.</span></span> <span data-ttu-id="64fc8-238">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64fc8-239">d.</span><span class="sxs-lookup"><span data-stu-id="64fc8-239">d.</span></span> <span data-ttu-id="64fc8-240">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="64fc8-241">Maken van een Cloud SAP voor klant testgebruiker</span><span class="sxs-lookup"><span data-stu-id="64fc8-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="64fc8-242">In deze sectie maakt u Britta Simon aangeroepen in SAP Cloud voor klant van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="64fc8-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="64fc8-243">Neem contact op met [SAP Cloud voor afdeling Klantenondersteuning](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd Hallo gebruikers in Hallo SAP Cloud voor klant-platform.</span><span class="sxs-lookup"><span data-stu-id="64fc8-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="64fc8-244">Zorg dat NameID waarde met de Hallo gebruikersnaam veld in Hallo SAP Cloud voor klant-platform overeenkomen moet.</span><span class="sxs-lookup"><span data-stu-id="64fc8-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64fc8-245">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="64fc8-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="64fc8-246">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP Cloud voor de klant.</span><span class="sxs-lookup"><span data-stu-id="64fc8-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="64fc8-248">**tooassign Britta Simon tooSAP Cloud voor de klant, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="64fc8-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="64fc8-249">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="64fc8-251">Selecteer in de lijst met de toepassingen van Hallo **SAP Cloud voor klant**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="64fc8-253">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="64fc8-255">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="64fc8-255">Click **Add** button.</span></span> <span data-ttu-id="64fc8-256">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64fc8-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="64fc8-258">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="64fc8-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64fc8-259">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64fc8-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64fc8-260">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="64fc8-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64fc8-261">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="64fc8-261">Testing single sign-on</span></span>

<span data-ttu-id="64fc8-262">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="64fc8-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="64fc8-263">Als u op Hallo SAP Cloud voor klant-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour SAP Cloud voor de toepassing van de klant.</span><span class="sxs-lookup"><span data-stu-id="64fc8-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="64fc8-264">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64fc8-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64fc8-265">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="64fc8-265">Additional resources</span></span>

* [<span data-ttu-id="64fc8-266">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64fc8-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64fc8-267">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64fc8-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

