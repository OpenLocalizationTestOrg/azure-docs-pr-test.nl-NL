---
title: 'Zelfstudie: Azure Active Directory-integratie met Hallo middelen Portal | Microsoft Docs'
description: Ontdek hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Hallo Portal middelen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="2424e-103">Zelfstudie: Azure Active Directory-integratie met Hallo middelen Portal</span><span class="sxs-lookup"><span data-stu-id="2424e-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="2424e-104">In deze zelfstudie leert u hoe toointegrate Hallo middelen Portal met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2424e-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2424e-105">Hallo integreren biedt met Azure AD-Portal middelen Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2424e-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2424e-106">U kunt beheren in Azure AD wie toegang tot toohello Funding Portal heeft</span><span class="sxs-lookup"><span data-stu-id="2424e-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="2424e-107">U kunt uw gebruikers tooautomatically get aangemelde toohello Funding-Portal met hun Azure AD-accounts (Single Sign-On) inschakelen</span><span class="sxs-lookup"><span data-stu-id="2424e-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2424e-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2424e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2424e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2424e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2424e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2424e-110">Prerequisites</span></span>

<span data-ttu-id="2424e-111">tooconfigure Azure AD-integratie met Hallo Funding Portal, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2424e-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="2424e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2424e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2424e-113">Een Hallo eenmalige aanmelding middelen Portal abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="2424e-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2424e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2424e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2424e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2424e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2424e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2424e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2424e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2424e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2424e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2424e-118">Scenario description</span></span>
<span data-ttu-id="2424e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2424e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2424e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2424e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2424e-121">Toe te voegen Hallo Hallo galerie Funding-Portal</span><span class="sxs-lookup"><span data-stu-id="2424e-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="2424e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2424e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="2424e-123">Toe te voegen Hallo Hallo galerie Funding-Portal</span><span class="sxs-lookup"><span data-stu-id="2424e-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="2424e-124">tooconfigure hello integratie van Hallo Funding Portal in Azure AD, moet u tooadd Hallo Funding Hallo galerie tooyour lijst met beheerde apps met SaaS-Portal.</span><span class="sxs-lookup"><span data-stu-id="2424e-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2424e-125">**tooadd middelen Portal uit de galerie Hallo Hallo, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="2424e-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2424e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2424e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2424e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2424e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2424e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2424e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2424e-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2424e-133">Typ in het zoekvak Hallo **Hallo middelen Portal**.</span><span class="sxs-lookup"><span data-stu-id="2424e-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="2424e-135">Selecteer in het deelvenster resultaten hello, **Portal middelen Hallo**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2424e-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2424e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2424e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2424e-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Hallo die middelen Portal op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2424e-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2424e-139">Voor één aanmelding toowork Azure AD moet tooknow welke gebruiker van de bijbehorende equivalent Hallo Hallo middelen Portal is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2424e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="2424e-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in Hallo Hallo middelen Portal moet toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2424e-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="2424e-141">In Hallo middelen Portal, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2424e-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2424e-142">tooconfigure en test eenmalige aanmelding Azure AD Hello Funding Portal, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2424e-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2424e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2424e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2424e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2424e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2424e-145">**[Maken van Hallo middelen Portal een testgebruiker](#creating-the-funding-portal-test-user)**  -toohave een equivalent van Britta Simon in Hallo Funding Portal die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2424e-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2424e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2424e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2424e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2424e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2424e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2424e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2424e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Hallo middelen Portal-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2424e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="2424e-150">**tooconfigure Azure AD eenmalige aanmelding met Portal middelen hello, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2424e-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="2424e-151">In Azure-portal op Hallo Hallo **Portal middelen Hallo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2424e-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2424e-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2424e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="2424e-155">Op Hallo **Hallo Portal domein middelen en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2424e-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="2424e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2424e-157">a.</span></span> <span data-ttu-id="2424e-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="2424e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="2424e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2424e-159">b.</span></span> <span data-ttu-id="2424e-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="2424e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2424e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2424e-161">These values are not real.</span></span> <span data-ttu-id="2424e-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="2424e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2424e-163">Neem contact op met [Hallo middelen Portal Client ondersteuningsteam](mailto:info@regenteducation.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2424e-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="2424e-164">Hallo middelen Portal-toepassing verwacht hello SAML asserties toocontain een kenmerk genaamd 'externalId1'.</span><span class="sxs-lookup"><span data-stu-id="2424e-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="2424e-165">Hallo-waarde van 'externalId1' moet een erkende studentID.</span><span class="sxs-lookup"><span data-stu-id="2424e-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="2424e-166">Configureer de claim 'externalId1' Hallo voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="2424e-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="2424e-167">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2424e-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="2424e-168">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="2424e-168">hello following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="2424e-170">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2424e-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="2424e-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="2424e-171">Attribute Name</span></span> | <span data-ttu-id="2424e-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="2424e-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="2424e-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="2424e-173">externalId1</span></span> | <span data-ttu-id="2424e-174">User.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="2424e-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="2424e-175">a.</span><span class="sxs-lookup"><span data-stu-id="2424e-175">a.</span></span> <span data-ttu-id="2424e-176">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2424e-179">b.</span><span class="sxs-lookup"><span data-stu-id="2424e-179">b.</span></span> <span data-ttu-id="2424e-180">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="2424e-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="2424e-181">c.</span><span class="sxs-lookup"><span data-stu-id="2424e-181">c.</span></span> <span data-ttu-id="2424e-182">Van Hallo **kenmerkwaarde** lijst, selecteer Hallo-kenmerk moet toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="2424e-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="2424e-183">Bijvoorbeeld, als u Hallo StudentID waarde in Hallo ExtensionAttribute1 hebt opgeslagen, selecteert u user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="2424e-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="2424e-184">d.</span><span class="sxs-lookup"><span data-stu-id="2424e-184">d.</span></span> <span data-ttu-id="2424e-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2424e-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="2424e-186">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2424e-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="2424e-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2424e-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2424e-190">tooconfigure eenmalige aanmelding op **Portal middelen Hallo** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Hallo middelen Portal ondersteuningsteam](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="2424e-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="2424e-191">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2424e-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2424e-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2424e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2424e-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2424e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2424e-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2424e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2424e-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2424e-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="2424e-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2424e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2424e-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2424e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2424e-199">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2424e-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2424e-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2424e-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2424e-203">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2424e-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2424e-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2424e-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2424e-207">a.</span><span class="sxs-lookup"><span data-stu-id="2424e-207">a.</span></span> <span data-ttu-id="2424e-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2424e-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2424e-209">b.</span><span class="sxs-lookup"><span data-stu-id="2424e-209">b.</span></span> <span data-ttu-id="2424e-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2424e-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2424e-211">c.</span><span class="sxs-lookup"><span data-stu-id="2424e-211">c.</span></span> <span data-ttu-id="2424e-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2424e-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2424e-213">d.</span><span class="sxs-lookup"><span data-stu-id="2424e-213">d.</span></span> <span data-ttu-id="2424e-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2424e-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="2424e-215">Hallo middelen Portal testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2424e-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="2424e-216">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Hallo Funding Portal maken.</span><span class="sxs-lookup"><span data-stu-id="2424e-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="2424e-217">Werken met [Hallo middelen Portal ondersteuningsteam](mailto:info@regenteducation.com) tooadd testgebruiker Hallo en SSO in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="2424e-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2424e-218">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2424e-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2424e-219">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang toohello Funding-Portal.</span><span class="sxs-lookup"><span data-stu-id="2424e-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2424e-221">**tooassign Britta Simon toohello Funding Portal, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2424e-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="2424e-222">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2424e-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2424e-224">Selecteer in de lijst met de toepassingen van Hallo **Hallo middelen Portal**.</span><span class="sxs-lookup"><span data-stu-id="2424e-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="2424e-226">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2424e-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2424e-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2424e-228">Click **Add** button.</span></span> <span data-ttu-id="2424e-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2424e-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2424e-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2424e-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2424e-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2424e-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2424e-234">Testing single sign-on</span></span>

<span data-ttu-id="2424e-235">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="2424e-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2424e-236">Als u op Hallo Hallo middelen Portal tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Hallo middelen Portal-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2424e-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2424e-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2424e-237">Additional resources</span></span>

* [<span data-ttu-id="2424e-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2424e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2424e-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2424e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

