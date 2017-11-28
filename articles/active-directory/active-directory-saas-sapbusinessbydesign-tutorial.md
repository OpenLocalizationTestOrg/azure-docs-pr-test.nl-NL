---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="55d16-103">Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="55d16-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="55d16-104">In deze zelfstudie leert u hoe toointegrate SAP Business ByDesign met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55d16-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55d16-105">SAP Business ByDesign integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="55d16-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55d16-106">U kunt beheren in Azure AD die toegang tooSAP Business ByDesign heeft.</span><span class="sxs-lookup"><span data-stu-id="55d16-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="55d16-107">U kunt uw gebruikers tooautomatically get aangemelde tooSAP Business ByDesign (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="55d16-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="55d16-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="55d16-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="55d16-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55d16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55d16-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="55d16-110">Prerequisites</span></span>

<span data-ttu-id="55d16-111">Azure AD-integratie met SAP Business ByDesign tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="55d16-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="55d16-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="55d16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55d16-113">Een SAP Business ByDesign eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="55d16-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55d16-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="55d16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55d16-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="55d16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55d16-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="55d16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55d16-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55d16-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55d16-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="55d16-118">Scenario description</span></span>
<span data-ttu-id="55d16-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="55d16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55d16-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="55d16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55d16-121">Het toevoegen van SAP Business ByDesign van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="55d16-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="55d16-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="55d16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="55d16-123">Het toevoegen van SAP Business ByDesign van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="55d16-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="55d16-124">tooconfigure hello integratie van SAP Business ByDesign in Azure AD, moet u tooadd SAP Business ByDesign uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="55d16-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55d16-125">**tooadd SAP Business ByDesign via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="55d16-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d16-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="55d16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="55d16-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55d16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55d16-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55d16-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="55d16-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55d16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="55d16-133">Typ in het zoekvak Hallo **SAP Business ByDesign**, selecteer **SAP Business ByDesign** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="55d16-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign in de lijst met resultaten Hallo](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="55d16-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d16-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="55d16-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met SAP Business ByDesign op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="55d16-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55d16-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SAP Business ByDesign is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55d16-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="55d16-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in een SAP Business ByDesign Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="55d16-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="55d16-139">In een SAP Business ByDesign, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="55d16-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55d16-140">tooconfigure en eenmalige aanmelding Azure AD-test met SAP Business ByDesign, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55d16-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55d16-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="55d16-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55d16-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55d16-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55d16-143">**[Maken van een SAP Business ByDesign testgebruiker](#create-an-sap-business-bydesign-test-user)**  -toohave een equivalent van Britta Simon in SAP Business ByDesign die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="55d16-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55d16-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="55d16-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55d16-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="55d16-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="55d16-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="55d16-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="55d16-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SAP Business ByDesign configureren.</span><span class="sxs-lookup"><span data-stu-id="55d16-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="55d16-148">**tooconfigure eenmalige aanmelding Azure AD met SAP Business ByDesign, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="55d16-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d16-149">In de Azure-portal op Hallo Hallo **SAP Business ByDesign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="55d16-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="55d16-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="55d16-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="55d16-153">Op Hallo **SAP Business ByDesign domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55d16-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en SAP Business ByDesign domein eenmalige aanmelding informatie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="55d16-155">a.</span><span class="sxs-lookup"><span data-stu-id="55d16-155">a.</span></span> <span data-ttu-id="55d16-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="55d16-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="55d16-157">b.</span><span class="sxs-lookup"><span data-stu-id="55d16-157">b.</span></span> <span data-ttu-id="55d16-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="55d16-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55d16-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="55d16-159">These values are not real.</span></span> <span data-ttu-id="55d16-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="55d16-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="55d16-161">Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="55d16-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="55d16-162">Op Hallo **gebruikerskenmerken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55d16-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign kenmerk sectie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="55d16-164">a.</span><span class="sxs-lookup"><span data-stu-id="55d16-164">a.</span></span> <span data-ttu-id="55d16-165">In **gebruikers-id** lijst, selecteer Hallo **ExtractMailPrefix()** functie.</span><span class="sxs-lookup"><span data-stu-id="55d16-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="55d16-166">b.</span><span class="sxs-lookup"><span data-stu-id="55d16-166">b.</span></span> <span data-ttu-id="55d16-167">Van Hallo **Mail** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="55d16-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="55d16-168">Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="55d16-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="55d16-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="55d16-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="55d16-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="55d16-171">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="55d16-173">Op Hallo **SAP Business ByDesign configuratie** sectie, klikt u op **configureren SAP Business ByDesign** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="55d16-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="55d16-174">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="55d16-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![SAP Business ByDesign-configuratie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="55d16-176">tooget SSO is geconfigureerd voor uw toepassing hello stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="55d16-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="55d16-177">a.</span><span class="sxs-lookup"><span data-stu-id="55d16-177">a.</span></span> <span data-ttu-id="55d16-178">Meld u aan op tooyour SAP Business ByDesign portal met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="55d16-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="55d16-179">b.</span><span class="sxs-lookup"><span data-stu-id="55d16-179">b.</span></span> <span data-ttu-id="55d16-180">Navigeer te**toepassings- en algemene beheertaak gebruiker** en klik op Hallo **identiteitsprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="55d16-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="55d16-181">c.</span><span class="sxs-lookup"><span data-stu-id="55d16-181">c.</span></span> <span data-ttu-id="55d16-182">Klik op **nieuwe identiteitsprovider** en selecteer Hallo metagegevens XML-bestand dat u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="55d16-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="55d16-183">Door het importeren van metagegevens Hallo uploadt Hallo systeem automatisch Hallo vereist handtekeningcertificaat en -versleutelingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="55d16-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="55d16-185">d.</span><span class="sxs-lookup"><span data-stu-id="55d16-185">d.</span></span> <span data-ttu-id="55d16-186">Hallo tooinclude **Assertion Consumer Service-URL** in Hallo SAML-aanvraag, selecteer **Assertion Consumer Service-URL opnemen**.</span><span class="sxs-lookup"><span data-stu-id="55d16-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="55d16-187">e.</span><span class="sxs-lookup"><span data-stu-id="55d16-187">e.</span></span> <span data-ttu-id="55d16-188">Klik op **activeren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="55d16-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="55d16-189">f.</span><span class="sxs-lookup"><span data-stu-id="55d16-189">f.</span></span> <span data-ttu-id="55d16-190">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="55d16-190">Save your changes.</span></span>
   
    <span data-ttu-id="55d16-191">g.</span><span class="sxs-lookup"><span data-stu-id="55d16-191">g.</span></span> <span data-ttu-id="55d16-192">Klik op Hallo **mijn systeem** tabblad.</span><span class="sxs-lookup"><span data-stu-id="55d16-192">Click hello **My System** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="55d16-194">h.</span><span class="sxs-lookup"><span data-stu-id="55d16-194">h.</span></span> <span data-ttu-id="55d16-195">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal het in Hallo **Azure AD aanmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="55d16-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="55d16-197">ik.</span><span class="sxs-lookup"><span data-stu-id="55d16-197">i.</span></span> <span data-ttu-id="55d16-198">Opgeven of de werknemer Hallo handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door te selecteren **handmatige identiteit Provider selectie**.</span><span class="sxs-lookup"><span data-stu-id="55d16-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="55d16-199">j.</span><span class="sxs-lookup"><span data-stu-id="55d16-199">j.</span></span> <span data-ttu-id="55d16-200">In Hallo **URL SSO** sectie Hallo URL opgeven die moet worden gebruikt door Hallo werknemer toologon toohello systeem.</span><span class="sxs-lookup"><span data-stu-id="55d16-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="55d16-201">In Hallo URL verzonden tooEmployee vervolgkeuzelijst wordt weergegeven, kunt u kiezen tussen Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="55d16-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="55d16-202">**Niet-SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="55d16-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="55d16-203">Hallo system verzendt alleen Hallo normale system URL toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="55d16-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="55d16-204">Hallo werknemer kan niet aanmelden met eenmalige aanmelding, en moet gebruik wachtwoord of certificaat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="55d16-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="55d16-205">**URL VOOR EENMALIGE AANMELDING**</span><span class="sxs-lookup"><span data-stu-id="55d16-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="55d16-206">Hallo system verzendt alleen Hallo URL SSO toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="55d16-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="55d16-207">Hallo werknemers kan zich aanmelden met behulp van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="55d16-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="55d16-208">Authenticatie-aanvraag wordt omgeleid via Hallo IdP.</span><span class="sxs-lookup"><span data-stu-id="55d16-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="55d16-209">**Automatische selectie**</span><span class="sxs-lookup"><span data-stu-id="55d16-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="55d16-210">Als eenmalige aanmelding niet actief is, verzendt het afdruksysteem van Hallo Hallo normale system URL toohello werknemer.</span><span class="sxs-lookup"><span data-stu-id="55d16-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="55d16-211">Als eenmalige aanmelding actief is, controleert Hallo system of Hallo werknemer een wachtwoord heeft.</span><span class="sxs-lookup"><span data-stu-id="55d16-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="55d16-212">Als een wachtwoord beschikbaar is, worden zowel de URL van de SSO- en Non-SSO-toohello werknemer verzonden.</span><span class="sxs-lookup"><span data-stu-id="55d16-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="55d16-213">Als Hallo werknemer geen wachtwoord heeft, is alleen Hallo URL SSO echter toohello werknemer verzonden.</span><span class="sxs-lookup"><span data-stu-id="55d16-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="55d16-214">k.</span><span class="sxs-lookup"><span data-stu-id="55d16-214">k.</span></span> <span data-ttu-id="55d16-215">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="55d16-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="55d16-216">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="55d16-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55d16-217">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="55d16-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55d16-218">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55d16-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="55d16-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="55d16-219">Create an Azure AD test user</span></span>

<span data-ttu-id="55d16-220">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="55d16-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="55d16-222">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="55d16-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d16-223">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="55d16-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="55d16-225">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="55d16-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="55d16-227">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55d16-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="55d16-229">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55d16-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="55d16-231">a.</span><span class="sxs-lookup"><span data-stu-id="55d16-231">a.</span></span> <span data-ttu-id="55d16-232">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55d16-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55d16-233">b.</span><span class="sxs-lookup"><span data-stu-id="55d16-233">b.</span></span> <span data-ttu-id="55d16-234">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="55d16-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="55d16-235">c.</span><span class="sxs-lookup"><span data-stu-id="55d16-235">c.</span></span> <span data-ttu-id="55d16-236">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="55d16-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="55d16-237">d.</span><span class="sxs-lookup"><span data-stu-id="55d16-237">d.</span></span> <span data-ttu-id="55d16-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55d16-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="55d16-239">Een SAP Business ByDesign testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="55d16-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="55d16-240">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in een SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="55d16-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="55d16-241">Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) tooadd Hallo gebruikers in Hallo SAP Business ByDesign platform.</span><span class="sxs-lookup"><span data-stu-id="55d16-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="55d16-242">Zorg dat NameID waarde met de Hallo gebruikersnaam veld in Hallo SAP Business ByDesign platform overeenkomen moet.</span><span class="sxs-lookup"><span data-stu-id="55d16-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="55d16-243">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="55d16-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="55d16-244">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="55d16-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="55d16-246">**tooassign Britta Simon tooSAP Business ByDesign, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="55d16-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="55d16-247">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55d16-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="55d16-249">Selecteer in de lijst met de toepassingen van Hallo **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="55d16-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![Hallo SAP Business ByDesign koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="55d16-251">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="55d16-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="55d16-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="55d16-253">Click **Add** button.</span></span> <span data-ttu-id="55d16-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55d16-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="55d16-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="55d16-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55d16-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55d16-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55d16-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55d16-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="55d16-259">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="55d16-259">Test single sign-on</span></span>

<span data-ttu-id="55d16-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="55d16-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="55d16-261">Als u op Hallo SAP Business ByDesign tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAP Business ByDesign toepassing.</span><span class="sxs-lookup"><span data-stu-id="55d16-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55d16-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="55d16-262">Additional resources</span></span>

* [<span data-ttu-id="55d16-263">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55d16-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55d16-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55d16-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

