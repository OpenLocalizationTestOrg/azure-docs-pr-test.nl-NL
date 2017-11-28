---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler persoonlijke toegang (ZPA) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zscaler persoonlijke toegang (ZPA).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="2426c-103">Zelfstudie: Azure Active Directory-integratie met Zscaler persoonlijke toegang (ZPA)</span><span class="sxs-lookup"><span data-stu-id="2426c-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="2426c-104">In deze zelfstudie leert u hoe toointegrate Zscaler persoonlijke toegang (ZPA) met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2426c-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2426c-105">Zscaler persoonlijke toegang (ZPA) integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2426c-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2426c-106">U kunt beheren in Azure AD wie toegang tot tooZscaler persoonlijke toegang (ZPA heeft)</span><span class="sxs-lookup"><span data-stu-id="2426c-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="2426c-107">U kunt uw gebruikers tooautomatically get aangemelde tooZscaler persoonlijke toegang (ZPA) (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="2426c-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2426c-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="2426c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2426c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2426c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2426c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2426c-110">Prerequisites</span></span>

<span data-ttu-id="2426c-111">tooconfigure Azure AD-integratie met Zscaler persoonlijke toegang (ZPA), moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2426c-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="2426c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2426c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2426c-113">Een Zscaler persoonlijke toegang (ZPA) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2426c-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2426c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2426c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2426c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2426c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2426c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2426c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2426c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2426c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2426c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2426c-118">Scenario description</span></span>
<span data-ttu-id="2426c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2426c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2426c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2426c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2426c-121">Zscaler persoonlijke toegang (ZPA) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="2426c-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="2426c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2426c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="2426c-123">Zscaler persoonlijke toegang (ZPA) uit de galerie Hallo toe te voegen</span><span class="sxs-lookup"><span data-stu-id="2426c-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="2426c-124">tooconfigure hello integratie van Zscaler persoonlijke toegang (ZPA) in Azure AD, moet u tooadd Zscaler persoonlijke toegang (ZPA) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2426c-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2426c-125">**tooadd Zscaler persoonlijke toegang (ZPA) uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2426c-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2426c-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2426c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2426c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2426c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2426c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2426c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2426c-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2426c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2426c-133">Typ in het zoekvak Hallo **Zscaler persoonlijke toegang (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="2426c-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="2426c-135">Selecteer in het deelvenster resultaten hello, **Zscaler persoonlijke toegang (ZPA)**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2426c-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2426c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2426c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2426c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Zscaler persoonlijke toegang (ZPA) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2426c-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2426c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zscaler persoonlijke toegang (ZPA) is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2426c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="2426c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in Zscaler persoonlijke toegang (ZPA) toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2426c-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="2426c-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="2426c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="2426c-142">tooconfigure en test eenmalige aanmelding Azure AD met Zscaler persoonlijke toegang (ZPA), moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2426c-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2426c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2426c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2426c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2426c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2426c-145">**[Maken van een testgebruiker Zscaler persoonlijke toegang (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave een equivalent van Britta Simon in Zscaler persoonlijke toegang (ZPA) die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="2426c-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2426c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2426c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2426c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2426c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2426c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2426c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2426c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="2426c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="2426c-150">**tooconfigure eenmalige aanmelding Azure AD met Zscaler persoonlijke toegang (ZPA), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2426c-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="2426c-151">In hello Azure Management portal op Hallo **Zscaler persoonlijke toegang (ZPA)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2426c-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2426c-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2426c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="2426c-155">Op Hallo **Zscaler persoonlijke toegang (ZPA)-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2426c-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="2426c-157">a.</span><span class="sxs-lookup"><span data-stu-id="2426c-157">a.</span></span> <span data-ttu-id="2426c-158">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="2426c-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="2426c-159">b.</span><span class="sxs-lookup"><span data-stu-id="2426c-159">b.</span></span> <span data-ttu-id="2426c-160">In Hallo **id** textbox, type:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="2426c-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2426c-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="2426c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="2426c-162">U hebt deze waarden Hello werkelijke Meld u aan bij de URL en de id tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2426c-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="2426c-163">We raden hier u toouse Hallo unieke waarde van de URL in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="2426c-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="2426c-164">Neem contact op met [Zscaler persoonlijke toegang (ZPA) ondersteuningsteam](https://help.zscaler.com/zpa-submit-ticket) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2426c-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="2426c-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="2426c-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="2426c-167">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="2426c-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2426c-168">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2426c-168">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="2426c-170">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2426c-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="2426c-172">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2426c-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="2426c-174">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2426c-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="2426c-176">In een ander browservenster, meld u bij uw bedrijf Zscaler persoonlijke toegang (ZPA) site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2426c-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="2426c-177">Navigeer te**beheerder** en klik vervolgens op **Idp configuratie**.</span><span class="sxs-lookup"><span data-stu-id="2426c-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="2426c-179">In Hallo **Idp configuratie** sectie, klikt u op **nieuwe IDP-configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2426c-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="2426c-181">In Hallo **nieuwe IDP configuratie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2426c-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="2426c-183">a.</span><span class="sxs-lookup"><span data-stu-id="2426c-183">a.</span></span> <span data-ttu-id="2426c-184">Klik op **bestand selecteren** en uw van het gedownloade metagegevensbestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="2426c-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="2426c-185">b.</span><span class="sxs-lookup"><span data-stu-id="2426c-185">b.</span></span> <span data-ttu-id="2426c-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2426c-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2426c-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2426c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="2426c-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2426c-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2426c-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2426c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2426c-191">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2426c-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2426c-193">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2426c-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2426c-195">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2426c-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2426c-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2426c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2426c-199">a.</span><span class="sxs-lookup"><span data-stu-id="2426c-199">a.</span></span> <span data-ttu-id="2426c-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2426c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2426c-201">b.</span><span class="sxs-lookup"><span data-stu-id="2426c-201">b.</span></span> <span data-ttu-id="2426c-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2426c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2426c-203">c.</span><span class="sxs-lookup"><span data-stu-id="2426c-203">c.</span></span> <span data-ttu-id="2426c-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2426c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2426c-205">d.</span><span class="sxs-lookup"><span data-stu-id="2426c-205">d.</span></span> <span data-ttu-id="2426c-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2426c-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="2426c-207">Maken van een testgebruiker Zscaler persoonlijke toegang (ZPA)</span><span class="sxs-lookup"><span data-stu-id="2426c-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="2426c-208">In deze sectie maakt u een gebruiker met de naam Britta Simon in Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="2426c-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="2426c-209">Neem contact op met [Zscaler persoonlijke toegang (ZPA) ondersteuningsteam](https://help.zscaler.com/zpa-submit-ticket) tooadd Hallo gebruikers in Hallo Zscaler persoonlijke toegang (ZPA) platform.</span><span class="sxs-lookup"><span data-stu-id="2426c-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2426c-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2426c-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2426c-211">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van haar tooZscaler toegang tot persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="2426c-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2426c-213">**tooassign Britta Simon tooZscaler persoonlijke toegang (ZPA), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2426c-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="2426c-214">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2426c-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2426c-216">Selecteer in de lijst met de toepassingen van Hallo **Zscaler persoonlijke toegang (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="2426c-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="2426c-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2426c-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2426c-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2426c-220">Click **Add** button.</span></span> <span data-ttu-id="2426c-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2426c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2426c-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2426c-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2426c-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2426c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2426c-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2426c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2426c-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2426c-226">Testing single sign-on</span></span>

<span data-ttu-id="2426c-227">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2426c-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2426c-228">Als u op Hallo Zscaler persoonlijke toegang (ZPA)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zscaler persoonlijke toegang (ZPA)-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2426c-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2426c-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2426c-229">Additional resources</span></span>

* [<span data-ttu-id="2426c-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2426c-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2426c-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2426c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png