---
title: 'Zelfstudie: Azure Active Directory-integratie met HR2day door Merces | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en HR2day door Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="126ae-103">Zelfstudie: Azure Active Directory-integratie met HR2day door Merces</span><span class="sxs-lookup"><span data-stu-id="126ae-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="126ae-104">In deze zelfstudie leert u hoe toointegrate HR2day door Merces met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="126ae-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="126ae-105">HR2day door Merces integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="126ae-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="126ae-106">U kunt beheren in Azure AD die tooHR2day door Merces toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="126ae-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="126ae-107">U kunt uw gebruikers tooautomatically ophalen aangemeld tooHR2day door Merces met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="126ae-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="126ae-108">U kunt uw accounts op één centrale locatie--hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="126ae-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="126ae-109">Zie voor meer informatie over de integratie met Azure AD SaaS [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="126ae-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="126ae-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="126ae-110">Prerequisites</span></span>

<span data-ttu-id="126ae-111">Azure AD-integratie met HR2day door Merces tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="126ae-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="126ae-112">Een Azure AD-abonnement.</span><span class="sxs-lookup"><span data-stu-id="126ae-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="126ae-113">Een HR2day door eenmalige aanmelding Merces abonnement ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="126ae-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="126ae-114">Met behulp van een productie-omgeving tootest Hallo stappen in deze zelfstudie aanbevolen niet.</span><span class="sxs-lookup"><span data-stu-id="126ae-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="126ae-115">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="126ae-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="126ae-116">Gebruik uw productieomgeving geen tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="126ae-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="126ae-117">Ophalen van een [één maand gratis proefversie van Azure AD](https://azure.microsoft.com/pricing/free-trial/) als u nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="126ae-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="126ae-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="126ae-118">Scenario description</span></span>
<span data-ttu-id="126ae-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="126ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="126ae-120">Hallo-scenario dat hier wordt beschreven, bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="126ae-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="126ae-121">Het toevoegen van HR2day door Merces van Hallo-galerie.</span><span class="sxs-lookup"><span data-stu-id="126ae-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="126ae-122">Configureren en testen van Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="126ae-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="126ae-123">HR2day door Merces van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="126ae-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="126ae-124">tooconfigure hello integratie van HR2day door Merces in Azure AD HR2day door Merces uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="126ae-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="126ae-125">**tooadd HR2day door Merces via Hallo gallery nemen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="126ae-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="126ae-126">In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="126ae-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="126ae-128">Ga te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="126ae-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="126ae-131">tooadd een nieuwe toepassing selecteert Hallo **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="126ae-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="126ae-133">Typ in het zoekvak Hallo **HR2day door Merces**.</span><span class="sxs-lookup"><span data-stu-id="126ae-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="126ae-135">Selecteer in het deelvenster resultaten hello, **HR2day door Merces**, en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="126ae-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="126ae-137">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="126ae-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="126ae-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met HR2day door Merces op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="126ae-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="126ae-139">Voor één aanmelding toowork moet Azure AD tooknow die Hallo equivalent in HR2day door Merces tooa gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="126ae-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="126ae-140">Met andere woorden, moet u een koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HR2day door Merces tooestablish.</span><span class="sxs-lookup"><span data-stu-id="126ae-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="126ae-141">Wijs in HR2day door Merces hello **gebruikersnaam** in Azure AD te **gebruikersnaam** tooestablish Hallo relatie.</span><span class="sxs-lookup"><span data-stu-id="126ae-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="126ae-142">tooconfigure en eenmalige aanmelding Azure AD-test met HR2day door Merces, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="126ae-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="126ae-143">[Eenmalige aanmelding Azure AD configureren](#configuring-azure-ad-single-sign-on): uw toouse gebruikers deze functie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="126ae-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="126ae-144">[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user): Azure AD Test eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="126ae-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="126ae-145">[Maken van een HR2day door Merces testgebruiker](#creating-an-hr2day-by-merces-test-user): maken van een exemplaar van Britta Simon in HR2day door Merces die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="126ae-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="126ae-146">[Toewijzen van de testgebruiker hello Azure AD](#assigning-the-azure-ad-test-user): inschakelen Britta Simon toouse eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="126ae-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="126ae-147">[Test eenmalige aanmelding](#testing-single-sign-on): controleren of Hallo configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="126ae-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="126ae-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="126ae-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="126ae-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw HR2day door Merces toepassing.</span><span class="sxs-lookup"><span data-stu-id="126ae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="126ae-150">**Azure AD tooconfigure eenmalige aanmelding met HR2day door Merces, nemen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="126ae-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="126ae-151">In de Azure-portal op Hallo Hallo **HR2day door Merces** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="126ae-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="126ae-153">tooenable eenmalige aanmelding, in Hallo **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="126ae-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="126ae-155">In Hallo **HR2day Merces domein en URL's** sectie kan nemen Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="126ae-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="126ae-157">a.</span><span class="sxs-lookup"><span data-stu-id="126ae-157">a.</span></span> <span data-ttu-id="126ae-158">In Hallo **aanmeldings-URL** vak een URL met behulp van Hallo patroon volgen: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="126ae-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="126ae-159">b.</span><span class="sxs-lookup"><span data-stu-id="126ae-159">b.</span></span> <span data-ttu-id="126ae-160">In Hallo **id** vak een URL met behulp van Hallo patroon volgen: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="126ae-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="126ae-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="126ae-161">These values are not real.</span></span> <span data-ttu-id="126ae-162">Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="126ae-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="126ae-163">Neem contact op met Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="126ae-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="126ae-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie **Certificate(Base64)**, en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="126ae-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="126ae-166">Deze sectie wordt beschreven hoe tooenable gebruikers tooauthenticate tooHR2day door Merces aan hun account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="126ae-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="126ae-167">Ze doen dit met behulp van de federatieserver die gebaseerd op Hallo SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="126ae-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="126ae-168">Uw HR2day door Merces toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token.</span><span class="sxs-lookup"><span data-stu-id="126ae-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="126ae-169">Hallo volgende Schermafbeelding toont een voorbeeld hiervan.</span><span class="sxs-lookup"><span data-stu-id="126ae-169">hello following screenshot shows an example of this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="126ae-171">Voordat u de SAML-verklaring Hallo configureren kunt, moet u contact opneemt Hallo [HR2day door Merces Client ondersteuningsteam](mailto:servicedesk@merces.nl) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="126ae-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="126ae-172">U moet deze waarde toocomplete Hallo stappen in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="126ae-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="126ae-173">In Hallo **eenmalige aanmelding** dialoogvenster in Hallo **gebruikerskenmerken** sectie, Hallo SAML-token kenmerk configureren zoals wordt weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="126ae-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="126ae-174">Los Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="126ae-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="126ae-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="126ae-175">Attribute name</span></span>    |   <span data-ttu-id="126ae-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="126ae-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="126ae-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="126ae-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="126ae-178">join ([e] '102938475Z' ' @ '</span><span class="sxs-lookup"><span data-stu-id="126ae-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="126ae-179">a.</span><span class="sxs-lookup"><span data-stu-id="126ae-179">a.</span></span> <span data-ttu-id="126ae-180">Hallo tooopen **kenmerk toevoegen** dialoogvenster Selecteer **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="126ae-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="126ae-183">b.</span><span class="sxs-lookup"><span data-stu-id="126ae-183">b.</span></span> <span data-ttu-id="126ae-184">In Hallo **naam** in het vak **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="126ae-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="126ae-185">c.</span><span class="sxs-lookup"><span data-stu-id="126ae-185">c.</span></span> <span data-ttu-id="126ae-186">Van Hallo **waarde** selecteert **Join()**.</span><span class="sxs-lookup"><span data-stu-id="126ae-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="126ae-187">d.</span><span class="sxs-lookup"><span data-stu-id="126ae-187">d.</span></span> <span data-ttu-id="126ae-188">Van Hallo **tekenreeks1** selecteert **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="126ae-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="126ae-189">e.</span><span class="sxs-lookup"><span data-stu-id="126ae-189">e.</span></span> <span data-ttu-id="126ae-190">Voor **tekenreeks2**, typ Hallo unieke id die wordt geleverd door uw team HR2day.</span><span class="sxs-lookup"><span data-stu-id="126ae-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="126ae-191">f.</span><span class="sxs-lookup"><span data-stu-id="126ae-191">f.</span></span> <span data-ttu-id="126ae-192">In Hallo **scheidingsteken** in het vak  **@** .</span><span class="sxs-lookup"><span data-stu-id="126ae-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="126ae-193">g.</span><span class="sxs-lookup"><span data-stu-id="126ae-193">g.</span></span> <span data-ttu-id="126ae-194">Selecteer **Ok**.</span><span class="sxs-lookup"><span data-stu-id="126ae-194">Select **Ok**.</span></span>

7. <span data-ttu-id="126ae-195">Selecteer Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="126ae-195">Select hello **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="126ae-197">In Hallo **HR2day door Merces configuratie** sectie **HR2day configureren door Merces** tooopen hello **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="126ae-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="126ae-198">Kopiëren Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="126ae-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="126ae-200">tooconfigure eenmalige aanmelding voor uw toepassing, neem contact op met de Hallo [HR2day door Merces client ondersteuningsteam](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="126ae-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="126ae-201">Hallo gedownload koppelen **Certificate(Base64)** tooyour e-bestand.</span><span class="sxs-lookup"><span data-stu-id="126ae-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="126ae-202">Bieden ook Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** zodat ze kunnen worden geconfigureerd voor eenmalige aanmelding-integratie.</span><span class="sxs-lookup"><span data-stu-id="126ae-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="126ae-203">Vermeld toohello Merces team dat deze integratie moet entiteit-ID toobe ingesteld met Hallo patroon Hallo **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="126ae-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="126ae-204">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="126ae-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="126ae-205">Nadat u deze app van Hallo toevoegen **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **Single Sign-On** tabblad. Vervolgens toegang Hallo documentatie via Hallo ingesloten **configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="126ae-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="126ae-206">Meer informatie over Hallo embedded-documentatie-functie in Hallo [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="126ae-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="126ae-207">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="126ae-207">Create an Azure AD test user</span></span>
<span data-ttu-id="126ae-208">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="126ae-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="126ae-210">**een testgebruiker in Azure AD toocreate nemen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="126ae-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="126ae-211">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="126ae-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="126ae-213">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="126ae-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="126ae-215">tooopen hello **gebruiker** dialoogvenster, **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="126ae-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="126ae-217">In Hallo **gebruiker** in het dialoogvenster nemen Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="126ae-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="126ae-219">a.</span><span class="sxs-lookup"><span data-stu-id="126ae-219">a.</span></span> <span data-ttu-id="126ae-220">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="126ae-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="126ae-221">b.</span><span class="sxs-lookup"><span data-stu-id="126ae-221">b.</span></span> <span data-ttu-id="126ae-222">In Hallo **gebruikersnaam** vak, type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="126ae-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="126ae-223">c.</span><span class="sxs-lookup"><span data-stu-id="126ae-223">c.</span></span> <span data-ttu-id="126ae-224">Selecteer **wachtwoord weergeven**, en schrijf Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="126ae-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="126ae-225">d.</span><span class="sxs-lookup"><span data-stu-id="126ae-225">d.</span></span> <span data-ttu-id="126ae-226">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="126ae-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="126ae-227">Een HR2day door Merces testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="126ae-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="126ae-228">Hallo-doel van deze sectie is toocreate Britta Simon in HR2day aangeroepen door Merces van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="126ae-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="126ae-229">tooadd Hallo Hallo HR2day-account, het werken met Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="126ae-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="126ae-230">Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="126ae-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="126ae-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="126ae-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="126ae-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooHR2day toegang door Merces verlenen.</span><span class="sxs-lookup"><span data-stu-id="126ae-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="126ae-234">**tooassign Britta Simon tooHR2day door Merces, nemen Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="126ae-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="126ae-235">In hello Azure portal, open Hallo toepassingen bekijken, gaat toohello directory weergeven, en ga vervolgens te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="126ae-236">Selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-236">Next, select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="126ae-238">Selecteer in de lijst met de toepassingen van Hallo **HR2day door Merces**.</span><span class="sxs-lookup"><span data-stu-id="126ae-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="126ae-240">Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="126ae-242">Selecteer Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="126ae-242">Select hello **Add** button.</span></span> <span data-ttu-id="126ae-243">Klik op Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="126ae-245">In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="126ae-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="126ae-246">Klik op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="126ae-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="126ae-247">In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="126ae-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="126ae-248">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="126ae-248">Test single sign-on</span></span>

<span data-ttu-id="126ae-249">Hallo doel van deze sectie is tootest uw configuratie Azure AD eenmalige aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="126ae-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="126ae-250">Wanneer u Hallo HR2day door Merces-tegel in Hallo Toegangsvenster selecteert, ophalen u automatisch aangemeld tooyour HR2day door Merces toepassing.</span><span class="sxs-lookup"><span data-stu-id="126ae-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="126ae-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="126ae-251">Additional resources</span></span>

* [<span data-ttu-id="126ae-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="126ae-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="126ae-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="126ae-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

