---
title: 'Zelfstudie: Azure Active Directory-integratie met DigiCert | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en DigiCert.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="ca8a6-103">Zelfstudie: Azure Active Directory-integratie met DigiCert</span><span class="sxs-lookup"><span data-stu-id="ca8a6-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="ca8a6-104">In deze zelfstudie leert u hoe toointegrate DigiCert met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca8a6-105">DigiCert integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ca8a6-106">U kunt beheren in Azure AD die tooDigiCert toegang heeft</span><span class="sxs-lookup"><span data-stu-id="ca8a6-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="ca8a6-107">U kunt uw gebruikers tooautomatically get aangemelde tooDigiCert (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ca8a6-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca8a6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ca8a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ca8a6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca8a6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ca8a6-110">Prerequisites</span></span>

<span data-ttu-id="ca8a6-111">Azure AD-integratie met DigiCert tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="ca8a6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ca8a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca8a6-113">Een DigiCert eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ca8a6-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca8a6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca8a6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca8a6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca8a6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca8a6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ca8a6-118">Scenario description</span></span>
<span data-ttu-id="ca8a6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca8a6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca8a6-121">Het toevoegen van DigiCert van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ca8a6-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="ca8a6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca8a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="ca8a6-123">Het toevoegen van DigiCert van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ca8a6-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="ca8a6-124">tooconfigure hello integratie van DigiCert in Azure AD, moet u tooadd DigiCert uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ca8a6-125">**tooadd DigiCert via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ca8a6-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca8a6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca8a6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ca8a6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ca8a6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ca8a6-133">Typ in het zoekvak Hallo **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-133">In hello search box, type **DigiCert**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="ca8a6-135">Selecteer in het deelvenster resultaten hello, **DigiCert**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca8a6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca8a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca8a6-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met DigiCert op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ca8a6-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ca8a6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in DigiCert is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="ca8a6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in DigiCert toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="ca8a6-141">Wijs in DigiCert, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ca8a6-142">tooconfigure en eenmalige aanmelding Azure AD-test met DigiCert, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ca8a6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ca8a6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca8a6-145">**[Maken van een testgebruiker DigiCert](#creating-a-digicert-test-user)**  -toohave een equivalent van Britta Simon in DigiCert die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca8a6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca8a6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca8a6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ca8a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca8a6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing DigiCert configureren.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="ca8a6-150">**Azure AD tooconfigure eenmalige aanmelding met DigiCert, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ca8a6-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca8a6-151">In de Azure-portal op Hallo Hallo **DigiCert** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ca8a6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="ca8a6-155">Op Hallo **DigiCert-domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="ca8a6-157">Hallo SAML asserties verwacht DigiCert toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ca8a6-158">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="ca8a6-159">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ca8a6-160">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="ca8a6-162">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ca8a6-163">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ca8a6-163">Attribute Name</span></span> | <span data-ttu-id="ca8a6-164">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ca8a6-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ca8a6-165">Bedrijf</span><span class="sxs-lookup"><span data-stu-id="ca8a6-165">company</span></span> | <span data-ttu-id="ca8a6-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="ca8a6-166">< companycode ></span></span> |
    | <span data-ttu-id="ca8a6-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="ca8a6-167">digicertrole</span></span> | <span data-ttu-id="ca8a6-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="ca8a6-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="ca8a6-169">waarde van Hallo **bedrijf** kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="ca8a6-170">Deze waarde bijwerken met de werkelijke bedrijfscode.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-170">Update this value with actual company code.</span></span> <span data-ttu-id="ca8a6-171">tooget Hallo-waarde van **bedrijf** Neem contact op met het kenmerk [DigiCert ondersteuningsteam](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="ca8a6-172">a.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-172">a.</span></span> <span data-ttu-id="ca8a6-173">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ca8a6-176">b.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-176">b.</span></span> <span data-ttu-id="ca8a6-177">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="ca8a6-178">c.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-178">c.</span></span> <span data-ttu-id="ca8a6-179">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ca8a6-180">d.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-180">d.</span></span> <span data-ttu-id="ca8a6-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="ca8a6-182">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="ca8a6-184">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-184">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ca8a6-186">tooconfigure eenmalige aanmelding op **DigiCert** zijde, moet u toosend Hallo gedownload **Metadata XML** te[DigiCert ondersteuningsteam](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="ca8a6-187">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ca8a6-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ca8a6-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ca8a6-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca8a6-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca8a6-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ca8a6-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca8a6-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ca8a6-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ca8a6-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca8a6-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca8a6-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca8a6-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca8a6-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca8a6-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca8a6-203">a.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-203">a.</span></span> <span data-ttu-id="ca8a6-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca8a6-205">b.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-205">b.</span></span> <span data-ttu-id="ca8a6-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca8a6-207">c.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-207">c.</span></span> <span data-ttu-id="ca8a6-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ca8a6-209">d.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-209">d.</span></span> <span data-ttu-id="ca8a6-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="ca8a6-211">Een testgebruiker DigiCert maken</span><span class="sxs-lookup"><span data-stu-id="ca8a6-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="ca8a6-212">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in DigiCert maken.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="ca8a6-213">Neem contact op met [DigiCert ondersteuningsteam](mailto:support@digicert.com) tooadd Hallo gebruikers in DigiCert.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ca8a6-214">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca8a6-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ca8a6-215">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDigiCert toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ca8a6-217">**tooassign Britta Simon tooDigiCert, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ca8a6-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca8a6-218">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ca8a6-220">Selecteer in de lijst met de toepassingen van Hallo **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-220">In hello applications list, select **DigiCert**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="ca8a6-222">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ca8a6-224">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-224">Click **Add** button.</span></span> <span data-ttu-id="ca8a6-225">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ca8a6-227">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ca8a6-228">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca8a6-229">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca8a6-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca8a6-230">Testing single sign-on</span></span>

<span data-ttu-id="ca8a6-231">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ca8a6-232">Als u op Hallo DigiCert-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour DeigiCert toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca8a6-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="ca8a6-233">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca8a6-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ca8a6-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ca8a6-234">Additional resources</span></span>

* [<span data-ttu-id="ca8a6-235">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca8a6-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca8a6-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca8a6-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

