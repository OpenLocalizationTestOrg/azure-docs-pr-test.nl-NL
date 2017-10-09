---
title: 'Zelfstudie: Azure Active Directory-integratie met BetterWorks | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="caad3-103">Zelfstudie: Azure Active Directory-integratie met BetterWorks</span><span class="sxs-lookup"><span data-stu-id="caad3-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="caad3-104">In deze zelfstudie leert u hoe toointegrate BetterWorks met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="caad3-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="caad3-105">BetterWorks integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="caad3-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="caad3-106">U kunt beheren in Azure AD die tooBetterWorks toegang heeft</span><span class="sxs-lookup"><span data-stu-id="caad3-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="caad3-107">U kunt uw gebruikers tooautomatically get aangemelde tooBetterWorks (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="caad3-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="caad3-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="caad3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="caad3-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="caad3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caad3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="caad3-110">Prerequisites</span></span>

<span data-ttu-id="caad3-111">Azure AD-integratie met BetterWorks tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="caad3-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="caad3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="caad3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="caad3-113">Een BetterWorks eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="caad3-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="caad3-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="caad3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="caad3-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="caad3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="caad3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="caad3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="caad3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="caad3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="caad3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="caad3-118">Scenario description</span></span>
<span data-ttu-id="caad3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="caad3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="caad3-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="caad3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="caad3-121">Het toevoegen van BetterWorks van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="caad3-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="caad3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="caad3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="caad3-123">Het toevoegen van BetterWorks van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="caad3-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="caad3-124">tooconfigure hello integratie van BetterWorks in Azure AD, moet u tooadd BetterWorks uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="caad3-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="caad3-125">**tooadd BetterWorks via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="caad3-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="caad3-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="caad3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="caad3-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="caad3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="caad3-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="caad3-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="caad3-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="caad3-133">Typ in het zoekvak Hallo **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="caad3-133">In hello search box, type **BetterWorks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="caad3-135">Selecteer in het deelvenster resultaten hello, **BetterWorks**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="caad3-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="caad3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="caad3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="caad3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BetterWorks op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="caad3-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="caad3-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BetterWorks is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caad3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="caad3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BetterWorks toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="caad3-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="caad3-141">Wijs in BetterWorks, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="caad3-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="caad3-142">tooconfigure en eenmalige aanmelding Azure AD-test met BetterWorks, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="caad3-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="caad3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="caad3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="caad3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="caad3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="caad3-145">**[Maken van een testgebruiker BetterWorks](#creating-a-betterworks-test-user)**  -toohave een equivalent van Britta Simon in BetterWorks die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="caad3-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="caad3-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="caad3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="caad3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="caad3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="caad3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="caad3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="caad3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BetterWorks configureren.</span><span class="sxs-lookup"><span data-stu-id="caad3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="caad3-150">**Azure AD tooconfigure eenmalige aanmelding met BetterWorks, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="caad3-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="caad3-151">In de Azure-portal op Hallo Hallo **BetterWorks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="caad3-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="caad3-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="caad3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="caad3-155">Op Hallo **BetterWorks domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="caad3-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="caad3-157">a.</span><span class="sxs-lookup"><span data-stu-id="caad3-157">a.</span></span> <span data-ttu-id="caad3-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="caad3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="caad3-159">b.</span><span class="sxs-lookup"><span data-stu-id="caad3-159">b.</span></span> <span data-ttu-id="caad3-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="caad3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="caad3-161">Op Hallo **BetterWorks domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="caad3-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="caad3-163">a.</span><span class="sxs-lookup"><span data-stu-id="caad3-163">a.</span></span> <span data-ttu-id="caad3-164">Klik op Hallo **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="caad3-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="caad3-165">b.</span><span class="sxs-lookup"><span data-stu-id="caad3-165">b.</span></span> <span data-ttu-id="caad3-166">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="caad3-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="caad3-167">Deze zijn niet echte waarden.</span><span class="sxs-lookup"><span data-stu-id="caad3-167">These are not real values.</span></span> <span data-ttu-id="caad3-168">Deze waarden Hello antwoord-URL-id en de werkelijke aanmelding op URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="caad3-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="caad3-169">Neem contact op met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="caad3-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="caad3-170">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="caad3-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="caad3-172">Hallo SAML asserties verwacht BetterWorks toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="caad3-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="caad3-173">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="caad3-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="caad3-174">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**kenmerk**' tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="caad3-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="caad3-175">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="caad3-175">hello following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="caad3-177">Op Hallo **SAML-token kenmerken** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="caad3-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="caad3-178">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="caad3-178">Attribute Name</span></span> | <span data-ttu-id="caad3-179">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="caad3-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="caad3-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="caad3-180">saml_token</span></span>     | <span data-ttu-id="caad3-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="caad3-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="caad3-182">a.</span><span class="sxs-lookup"><span data-stu-id="caad3-182">a.</span></span> <span data-ttu-id="caad3-183">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="caad3-186">b.</span><span class="sxs-lookup"><span data-stu-id="caad3-186">b.</span></span> <span data-ttu-id="caad3-187">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="caad3-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="caad3-188">c.</span><span class="sxs-lookup"><span data-stu-id="caad3-188">c.</span></span> <span data-ttu-id="caad3-189">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="caad3-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="caad3-190">d.</span><span class="sxs-lookup"><span data-stu-id="caad3-190">d.</span></span> <span data-ttu-id="caad3-191">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="caad3-191">Click **Ok**.</span></span>

7. <span data-ttu-id="caad3-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="caad3-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="caad3-194">tooconfigure eenmalige aanmelding op **BetterWorks** zijde, moet u toosend Hallo gedownload **Metadata XML** te[BetterWorks ondersteuningsteam](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="caad3-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="caad3-195">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="caad3-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="caad3-196">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="caad3-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="caad3-197">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="caad3-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="caad3-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="caad3-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="caad3-199">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="caad3-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="caad3-201">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="caad3-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="caad3-202">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="caad3-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="caad3-204">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="caad3-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="caad3-206">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="caad3-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="caad3-208">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="caad3-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="caad3-210">a.</span><span class="sxs-lookup"><span data-stu-id="caad3-210">a.</span></span> <span data-ttu-id="caad3-211">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="caad3-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="caad3-212">b.</span><span class="sxs-lookup"><span data-stu-id="caad3-212">b.</span></span> <span data-ttu-id="caad3-213">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="caad3-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="caad3-214">c.</span><span class="sxs-lookup"><span data-stu-id="caad3-214">c.</span></span> <span data-ttu-id="caad3-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="caad3-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="caad3-216">d.</span><span class="sxs-lookup"><span data-stu-id="caad3-216">d.</span></span> <span data-ttu-id="caad3-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="caad3-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="caad3-218">Een testgebruiker BetterWorks maken</span><span class="sxs-lookup"><span data-stu-id="caad3-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="caad3-219">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BetterWorks maken.</span><span class="sxs-lookup"><span data-stu-id="caad3-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="caad3-220">Werken met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) tooadd Hallo gebruikers in Hallo BetterWorks platform.</span><span class="sxs-lookup"><span data-stu-id="caad3-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="caad3-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="caad3-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="caad3-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBetterWorks toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="caad3-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="caad3-224">**tooassign Britta Simon tooBetterWorks, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="caad3-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="caad3-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="caad3-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="caad3-227">Selecteer in de lijst met de toepassingen van Hallo **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="caad3-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="caad3-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="caad3-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="caad3-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="caad3-231">Click **Add** button.</span></span> <span data-ttu-id="caad3-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="caad3-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="caad3-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="caad3-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="caad3-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="caad3-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="caad3-237">Testing single sign-on</span></span>

<span data-ttu-id="caad3-238">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="caad3-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="caad3-239">Als u op Hallo BetterWorks-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour BetterWorks toepassing.</span><span class="sxs-lookup"><span data-stu-id="caad3-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="caad3-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="caad3-240">Additional resources</span></span>

* [<span data-ttu-id="caad3-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="caad3-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="caad3-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="caad3-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

