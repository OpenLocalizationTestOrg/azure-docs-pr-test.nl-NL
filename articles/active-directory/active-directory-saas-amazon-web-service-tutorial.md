---
title: 'Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="a1cb7-103">Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="a1cb7-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="a1cb7-104">In deze zelfstudie leert u hoe toointegrate Amazon Web Services (AWS) met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1cb7-105">Amazon Web Services (AWS) integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1cb7-106">U kunt beheren in Azure AD wie toegang tot tooAmazon Web Services (AWS heeft)</span><span class="sxs-lookup"><span data-stu-id="a1cb7-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="a1cb7-107">U kunt uw gebruikers tooautomatically get aangemelde tooAmazon Web Services (AWS) (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="a1cb7-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1cb7-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a1cb7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a1cb7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="a1cb7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a1cb7-110">Prerequisites</span></span>

<span data-ttu-id="a1cb7-111">tooconfigure Azure AD-integratie met Amazon Web Services (AWS), moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="a1cb7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a1cb7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1cb7-113">Amazon Web Services (AWS) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a1cb7-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1cb7-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1cb7-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1cb7-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a1cb7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1cb7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a1cb7-118">Scenario description</span></span>
<span data-ttu-id="a1cb7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1cb7-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1cb7-121">Amazon Web Services (AWS) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a1cb7-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="a1cb7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1cb7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="a1cb7-123">Amazon Web Services (AWS) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="a1cb7-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="a1cb7-124">tooconfigure hello integratie van Amazon Web Services (AWS) in Azure AD, moet u tooadd Amazon Web Services (AWS) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1cb7-125">**tooadd Amazon Web Services (AWS) uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1cb7-126">In Hallo  **[Azure Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1cb7-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1cb7-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a1cb7-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a1cb7-133">Typ in het zoekvak Hallo **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="a1cb7-135">Selecteer in het deelvenster resultaten hello, **Amazon Web Services (AWS)**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1cb7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1cb7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1cb7-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Amazon Web Services (AWS) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1cb7-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Amazon Web Services (AWS) is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="a1cb7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Amazon Web Services (AWS) toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="a1cb7-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="a1cb7-142">tooconfigure en test eenmalige aanmelding Azure AD met Amazon Web Services (AWS), moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1cb7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1cb7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1cb7-145">**[Maken van een gebruiker met Amazon Web Services test](#creating-an-amazon-web-services-test-user)**  -toohave een equivalent van Britta Simon in Amazon Web Services (AWS) die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a1cb7-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1cb7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1cb7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a1cb7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1cb7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="a1cb7-150">**tooconfigure eenmalige aanmelding Azure AD met Amazon Web Services (AWS) uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="a1cb7-151">In hello Azure-Portal op Hallo **Amazon Web Services (AWS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a1cb7-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="a1cb7-155">Op Hallo **Amazon Web Services (AWS) domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="a1cb7-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="a1cb7-159">Hallo softwaretoepassing Amazon Web Services (AWS) verwacht Hallo SAML asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a1cb7-160">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="a1cb7-161">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a1cb7-162">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-162">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="a1cb7-164">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a1cb7-165">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="a1cb7-165">Attribute Name</span></span>  | <span data-ttu-id="a1cb7-166">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="a1cb7-166">Attribute Value</span></span> | <span data-ttu-id="a1cb7-167">naamruimte</span><span class="sxs-lookup"><span data-stu-id="a1cb7-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="a1cb7-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="a1cb7-168">RoleSessionName</span></span> | <span data-ttu-id="a1cb7-169">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a1cb7-169">user.userprincipalname</span></span> | <span data-ttu-id="a1cb7-170">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="a1cb7-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="a1cb7-171">Rol</span><span class="sxs-lookup"><span data-stu-id="a1cb7-171">Role</span></span>            | <span data-ttu-id="a1cb7-172">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="a1cb7-172">user.assignedroles</span></span> |  <span data-ttu-id="a1cb7-173">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="a1cb7-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="a1cb7-174">U moet tooconfigure Hallo gebruikers inrichten in Azure AD toofetch alle Hallo-rollen van AWS-Console.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="a1cb7-175">Raadpleeg Hallo inrichting van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="a1cb7-176">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-176">a.</span></span> <span data-ttu-id="a1cb7-177">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="a1cb7-179">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-179">b.</span></span> <span data-ttu-id="a1cb7-180">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a1cb7-182">c.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-182">c.</span></span> <span data-ttu-id="a1cb7-183">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="a1cb7-184">Hallo Namespace-waarde die is opgegeven hierboven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="a1cb7-185">d.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-185">d.</span></span> <span data-ttu-id="a1cb7-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-186">Click **Ok**.</span></span>

7. <span data-ttu-id="a1cb7-187">Klik op **opslaan** knop toosave Hallo instellingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a1cb7-189">In een ander browservenster, aanmelding tooyour Amazon Web Services (AWS) bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="a1cb7-190">Klik op **Console-startpagina**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-190">Click **Console Home**.</span></span>
   
    ![Eenmalige aanmelding configureren][11]

10. <span data-ttu-id="a1cb7-192">Klik op **IAM** van **beveiliging, identiteit en compatibiliteit** service.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Eenmalige aanmelding configureren][12]

11. <span data-ttu-id="a1cb7-194">Klik op **identiteitsproviders**, en klik vervolgens op **Provider maken**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Eenmalige aanmelding configureren][13]

12. <span data-ttu-id="a1cb7-196">Op Hallo **Provider configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][14]
 
    <span data-ttu-id="a1cb7-198">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-198">a.</span></span> <span data-ttu-id="a1cb7-199">Als **providertype**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="a1cb7-200">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-200">b.</span></span> <span data-ttu-id="a1cb7-201">In Hallo **providernaam** textbox, typ een providernaam (bijvoorbeeld: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="a1cb7-202">c.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-202">c.</span></span> <span data-ttu-id="a1cb7-203">tooupload uw gedownloade metagegevensbestand, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="a1cb7-204">d.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-204">d.</span></span> <span data-ttu-id="a1cb7-205">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="a1cb7-206">Op Hallo **providerinformatie controleren** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Eenmalige aanmelding configureren][15]

14. <span data-ttu-id="a1cb7-208">Klik op **rollen**, en klik vervolgens op **nieuwe rol maken**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Eenmalige aanmelding configureren][16]

15. <span data-ttu-id="a1cb7-210">Op Hallo **rolnaam ingesteld** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Eenmalige aanmelding configureren][17] 

    <span data-ttu-id="a1cb7-212">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-212">a.</span></span> <span data-ttu-id="a1cb7-213">In Hallo **rolnaam** textbox, typ een rolnaam (bijvoorbeeld: *testgebruiker*).</span><span class="sxs-lookup"><span data-stu-id="a1cb7-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="a1cb7-214">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-214">b.</span></span> <span data-ttu-id="a1cb7-215">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="a1cb7-216">Op Hallo **Roltype Selecteer** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Eenmalige aanmelding configureren][18] 

    <span data-ttu-id="a1cb7-218">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-218">a.</span></span> <span data-ttu-id="a1cb7-219">Selecteer **rol voor toegang van de Provider identiteit**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="a1cb7-220">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-220">b.</span></span> <span data-ttu-id="a1cb7-221">In Hallo **Grant Web eenmalige aanmelding (WebSSO) toegang tooSAML providers** sectie, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="a1cb7-222">Op Hallo **vertrouwensrelatie tot stand brengen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Eenmalige aanmelding configureren][19] 

    <span data-ttu-id="a1cb7-224">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-224">a.</span></span> <span data-ttu-id="a1cb7-225">Selecteer als SAML-provider Hallo SAML provider die u eerder hebt gemaakt (bijvoorbeeld: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="a1cb7-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="a1cb7-226">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-226">b.</span></span> <span data-ttu-id="a1cb7-227">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="a1cb7-228">Op Hallo **controleren rol vertrouwen** dialoogvenster, klikt u op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Eenmalige aanmelding configureren][32]

19. <span data-ttu-id="a1cb7-230">Op Hallo **beleid koppelen** dialoogvenster, klikt u op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Eenmalige aanmelding configureren][33]

20. <span data-ttu-id="a1cb7-232">Op Hallo **revisie** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren][34]
 
    <span data-ttu-id="a1cb7-234">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-234">a.</span></span> <span data-ttu-id="a1cb7-235">Klik op **rol maken**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-235">Click **Create Role**.</span></span>

    <span data-ttu-id="a1cb7-236">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-236">b.</span></span> <span data-ttu-id="a1cb7-237">Zo veel functies naar behoefte maken en deze toohello identiteitsprovider toewijzen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="a1cb7-238">Hallo gebruikersinrichting, toofetch nu alle Hallo-rollen van AWS configureren</span><span class="sxs-lookup"><span data-stu-id="a1cb7-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="a1cb7-239">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-239">a.</span></span> <span data-ttu-id="a1cb7-240">In Hallo AWS-Console-aanmelding met het root-account</span><span class="sxs-lookup"><span data-stu-id="a1cb7-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="a1cb7-241">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-241">b.</span></span> <span data-ttu-id="a1cb7-242">Klik op de naam van uw in Hallo rechterbovenhoek en klik vervolgens op Hallo **mijn beveiligingsreferenties** optie.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="a1cb7-243">Hiermee opent u een scherm als een waarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="a1cb7-244">Klik op de knop Hallo **beveiligingsreferenties** knop toopass Hallo scherm.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Eenmalige aanmelding configureren][36]

       ![Eenmalige aanmelding configureren][37]

    <span data-ttu-id="a1cb7-247">c.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-247">c.</span></span> <span data-ttu-id="a1cb7-248">Klik in het Hallo toegangstoetsen Hallo op de sectie **toegangssleutel maken** knop.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="a1cb7-249">Hiermee wordt Hallo toegangssleutel-ID en een token waarde gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Eenmalige aanmelding configureren][38]

    <span data-ttu-id="a1cb7-251">d.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-251">d.</span></span> <span data-ttu-id="a1cb7-252">Kopieer deze beide waarden en ook downloaden, zodat u deze niet kwijtraakt.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="a1cb7-253">e.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-253">e.</span></span> <span data-ttu-id="a1cb7-254">Klik in hello Azure-Portal op Hallo Amazon Web Services (AWS) toepassing Integratiepagina **inrichten**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Eenmalige aanmelding configureren][35]

    <span data-ttu-id="a1cb7-256">f.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-256">f.</span></span> <span data-ttu-id="a1cb7-257">Hallo inrichten modus te instellen**automatische**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Eenmalige aanmelding configureren][39]

    <span data-ttu-id="a1cb7-259">g.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-259">g.</span></span> <span data-ttu-id="a1cb7-260">Nu in Hallo **clientsecret** en **geheim Token** plakt u de bijbehorende waarden hello, die u hebt gekopieerd vanaf AWS-Console.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="a1cb7-261">h.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-261">h.</span></span> <span data-ttu-id="a1cb7-262">U kunt klikken op Hallo **testverbinding** knop tootest Hallo connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="a1cb7-263">Wanneer die is geslaagd kunt u inrichting connector Hallo beginnen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Eenmalige aanmelding configureren][40]

    <span data-ttu-id="a1cb7-265">ik.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-265">i.</span></span> <span data-ttu-id="a1cb7-266">Nu te inschakelen Hallo inrichten Status**op**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="a1cb7-267">Hallo rollen ophalen uit de toepassing hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-267">This starts fetching hello roles from hello application.</span></span>

       ![Eenmalige aanmelding configureren][41]

    > [!NOTE]
    > <span data-ttu-id="a1cb7-269">Azure AD inrichten de service wordt uitgevoerd elke na bepaalde tijd toosync Hallo rollen van AWS.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="a1cb7-270">U ziet alle Hallo identiteitsprovider gekoppeld AWS rollen in Azure AD en u ze kunt gebruiken bij het toewijzen van Hallo toepassing toousers of groepen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1cb7-271">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a1cb7-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1cb7-272">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a1cb7-274">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1cb7-275">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1cb7-277">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1cb7-279">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1cb7-281">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1cb7-283">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-283">a.</span></span> <span data-ttu-id="a1cb7-284">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1cb7-285">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-285">b.</span></span> <span data-ttu-id="a1cb7-286">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1cb7-287">c.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-287">c.</span></span> <span data-ttu-id="a1cb7-288">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a1cb7-289">d.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-289">d.</span></span> <span data-ttu-id="a1cb7-290">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="a1cb7-291">Maken van een testgebruiker Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="a1cb7-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="a1cb7-292">In de volgorde tooenable Azure AD gebruikers toolog in tooAmazon Web Services (AWS) als ze in Amazon Web Services (AWS) worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="a1cb7-293">In geval van Hallo van Amazon Web Services (AWS) is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="a1cb7-294">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1cb7-295">Meld u bij tooyour **Amazon Web Services (AWS)** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="a1cb7-296">Klik op Hallo **Console-startpagina** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-296">Click hello **Console Home** icon.</span></span> 
   
    ![Eenmalige aanmelding configureren][11]

3. <span data-ttu-id="a1cb7-298">Klik op Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-298">Click Identity and Access Management.</span></span> 
   
    ![Eenmalige aanmelding configureren][28]

4. <span data-ttu-id="a1cb7-300">In Hallo Dashboard, klikt u op **gebruikers**, en klik vervolgens op **Create New Users**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Eenmalige aanmelding configureren][29]

5. <span data-ttu-id="a1cb7-302">Uitvoeren in het dialoogvenster van de gebruiker maken hello, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a1cb7-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][30]   
    
    <span data-ttu-id="a1cb7-304">a.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-304">a.</span></span> <span data-ttu-id="a1cb7-305">In Hallo **Voer gebruikersnamen** tekstvakken, typ de naam van Brita Simon gebruiker (userprincipalname) in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="a1cb7-306">b.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-306">b.</span></span> <span data-ttu-id="a1cb7-307">Klik op **maken.**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a1cb7-308">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1cb7-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a1cb7-309">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen haar toegang tooAmazon Web Services (AWS) verleent.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a1cb7-311">**tooassign Britta Simon tooAmazon Web Services (AWS), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a1cb7-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="a1cb7-312">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a1cb7-314">Selecteer in de lijst met de toepassingen van Hallo **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="a1cb7-316">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a1cb7-318">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-318">Click **Add** button.</span></span> <span data-ttu-id="a1cb7-319">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a1cb7-321">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1cb7-322">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1cb7-323">Op **rol selecteren** tabblad, selecteer Hallo juiste rol voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="a1cb7-324">Alle deze rollen worden weergegeven met de rolnaam Hallo en de naam van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="a1cb7-325">Op deze manier kunt u eenvoudig hello rollen van AWS identificeren.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="a1cb7-326">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1cb7-327">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a1cb7-327">Testing single sign-on</span></span>

<span data-ttu-id="a1cb7-328">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a1cb7-329">Als u op Hallo Amazon Web Services (AWS)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Amazon Web Services (AWS)-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1cb7-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a1cb7-330">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a1cb7-330">Additional resources</span></span>

* [<span data-ttu-id="a1cb7-331">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1cb7-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1cb7-332">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1cb7-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
