---
title: 'Zelfstudie: Azure Active Directory-integratie met BenefitHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BenefitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="eac6b-103">Zelfstudie: Azure Active Directory-integratie met BenefitHub</span><span class="sxs-lookup"><span data-stu-id="eac6b-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="eac6b-104">In deze zelfstudie leert u hoe toointegrate BenefitHub met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eac6b-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eac6b-105">BenefitHub integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eac6b-106">U kunt beheren in Azure AD die tooBenefitHub toegang heeft</span><span class="sxs-lookup"><span data-stu-id="eac6b-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="eac6b-107">U kunt uw gebruikers tooautomatically get aangemelde tooBenefitHub (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="eac6b-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eac6b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="eac6b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eac6b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eac6b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eac6b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eac6b-110">Prerequisites</span></span>

<span data-ttu-id="eac6b-111">Azure AD-integratie met BenefitHub tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="eac6b-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="eac6b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="eac6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eac6b-113">Een BenefitHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="eac6b-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eac6b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="eac6b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eac6b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eac6b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="eac6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eac6b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eac6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eac6b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="eac6b-118">Scenario description</span></span>
<span data-ttu-id="eac6b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="eac6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eac6b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eac6b-121">Het toevoegen van BenefitHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="eac6b-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="eac6b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eac6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="eac6b-123">Het toevoegen van BenefitHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="eac6b-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="eac6b-124">tooconfigure hello integratie van BenefitHub in Azure AD, moet u tooadd BenefitHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="eac6b-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eac6b-125">**tooadd BenefitHub via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eac6b-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eac6b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eac6b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eac6b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eac6b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="eac6b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eac6b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="eac6b-133">Typ in het zoekvak Hallo **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-133">In hello search box, type **BenefitHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="eac6b-135">Selecteer in het deelvenster resultaten hello, **BenefitHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="eac6b-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eac6b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eac6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eac6b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BenefitHub op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eac6b-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eac6b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BenefitHub is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eac6b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="eac6b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BenefitHub toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="eac6b-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="eac6b-141">Wijs in BenefitHub, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="eac6b-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eac6b-142">tooconfigure en eenmalige aanmelding Azure AD-test met BenefitHub, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eac6b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="eac6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eac6b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eac6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eac6b-145">**[Maken van een testgebruiker BenefitHub](#creating-a-benefithub-test-user)**  -toohave een equivalent van Britta Simon in BenefitHub die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="eac6b-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eac6b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eac6b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eac6b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="eac6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eac6b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="eac6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eac6b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BenefitHub configureren.</span><span class="sxs-lookup"><span data-stu-id="eac6b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="eac6b-150">**Azure AD tooconfigure eenmalige aanmelding met BenefitHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eac6b-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="eac6b-151">In de Azure-portal op Hallo Hallo **BenefitHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="eac6b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="eac6b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="eac6b-155">Op Hallo **BenefitHub domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="eac6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="eac6b-157">a.</span></span> <span data-ttu-id="eac6b-158">In Hallo **id** textbox, type:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="eac6b-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="eac6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="eac6b-159">b.</span></span> <span data-ttu-id="eac6b-160">In Hallo **antwoord-URL** textbox, type:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="eac6b-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="eac6b-161">Hallo BenefitHub toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="eac6b-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="eac6b-162">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="eac6b-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="eac6b-163">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="eac6b-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="eac6b-165">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="eac6b-166">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="eac6b-166">Attribute Name</span></span> | <span data-ttu-id="eac6b-167">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="eac6b-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="eac6b-168">OrganizationId</span><span class="sxs-lookup"><span data-stu-id="eac6b-168">organizationid</span></span> | <span data-ttu-id="eac6b-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="eac6b-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="eac6b-170">De waarde van dit kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="eac6b-170">This attribute value is not real.</span></span> <span data-ttu-id="eac6b-171">Deze waarde met de werkelijke organizationid bijwerken.</span><span class="sxs-lookup"><span data-stu-id="eac6b-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="eac6b-172">Neem contact op met [BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs) tooget Hallo werkelijke organizationid.</span><span class="sxs-lookup"><span data-stu-id="eac6b-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="eac6b-173">a.</span><span class="sxs-lookup"><span data-stu-id="eac6b-173">a.</span></span> <span data-ttu-id="eac6b-174">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eac6b-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="eac6b-177">b.</span><span class="sxs-lookup"><span data-stu-id="eac6b-177">b.</span></span> <span data-ttu-id="eac6b-178">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="eac6b-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="eac6b-179">c.</span><span class="sxs-lookup"><span data-stu-id="eac6b-179">c.</span></span> <span data-ttu-id="eac6b-180">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="eac6b-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="eac6b-181">d.</span><span class="sxs-lookup"><span data-stu-id="eac6b-181">d.</span></span> <span data-ttu-id="eac6b-182">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eac6b-183">Voordat u de SAML-verklaring Hallo configureren kunt, moet u toocontact uw [BenefitHub ondersteuning](https://www.benefithub.com/Home/ContactUs) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="eac6b-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="eac6b-184">U moet deze waarde tooconfigure Hallo aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="eac6b-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="eac6b-185">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="eac6b-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="eac6b-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="eac6b-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="eac6b-189">tooconfigure eenmalige aanmelding op **BenefitHub** zijde, moet u toosend Hallo gedownload **Metadata XML** te[BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="eac6b-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="eac6b-190">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="eac6b-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eac6b-191">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="eac6b-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eac6b-192">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="eac6b-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eac6b-193">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eac6b-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eac6b-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="eac6b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="eac6b-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac6b-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="eac6b-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eac6b-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eac6b-198">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eac6b-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eac6b-200">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eac6b-202">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="eac6b-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eac6b-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eac6b-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eac6b-206">a.</span><span class="sxs-lookup"><span data-stu-id="eac6b-206">a.</span></span> <span data-ttu-id="eac6b-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eac6b-208">b.</span><span class="sxs-lookup"><span data-stu-id="eac6b-208">b.</span></span> <span data-ttu-id="eac6b-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eac6b-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eac6b-210">c.</span><span class="sxs-lookup"><span data-stu-id="eac6b-210">c.</span></span> <span data-ttu-id="eac6b-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eac6b-212">d.</span><span class="sxs-lookup"><span data-stu-id="eac6b-212">d.</span></span> <span data-ttu-id="eac6b-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="eac6b-214">Een testgebruiker BenefitHub maken</span><span class="sxs-lookup"><span data-stu-id="eac6b-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="eac6b-215">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BenefitHub maken.</span><span class="sxs-lookup"><span data-stu-id="eac6b-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="eac6b-216">Werken met [BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs) Hallo gebruikers toevoegen in Hallo BenefitHub platform.</span><span class="sxs-lookup"><span data-stu-id="eac6b-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="eac6b-217">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eac6b-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eac6b-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eac6b-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eac6b-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBenefitHub toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="eac6b-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="eac6b-221">**tooassign Britta Simon tooBenefitHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="eac6b-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="eac6b-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="eac6b-224">Selecteer in de lijst met de toepassingen van Hallo **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="eac6b-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="eac6b-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="eac6b-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="eac6b-228">Click **Add** button.</span></span> <span data-ttu-id="eac6b-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eac6b-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="eac6b-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac6b-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eac6b-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eac6b-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eac6b-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eac6b-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eac6b-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eac6b-234">Testing single sign-on</span></span>

<span data-ttu-id="eac6b-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="eac6b-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eac6b-236">Als u op Hallo BenefitHub tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour BenefitHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="eac6b-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="eac6b-237">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="eac6b-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eac6b-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="eac6b-238">Additional resources</span></span>

* [<span data-ttu-id="eac6b-239">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eac6b-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eac6b-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eac6b-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

