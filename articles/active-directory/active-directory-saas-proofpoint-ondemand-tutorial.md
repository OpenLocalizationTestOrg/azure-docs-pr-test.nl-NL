---
title: 'Zelfstudie: Azure Active Directory-integratie met Proofpoint op verzoek | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Proofpoint op aanvraag.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="e1aff-103">Zelfstudie: Azure Active Directory-integratie met Proofpoint op aanvraag</span><span class="sxs-lookup"><span data-stu-id="e1aff-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="e1aff-104">In deze zelfstudie leert u hoe toointegrate Proofpoint op aanvraag met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1aff-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1aff-105">Proofpoint op verzoek integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1aff-106">U kunt beheren in Azure AD die toegang tooProofpoint op aanvraag</span><span class="sxs-lookup"><span data-stu-id="e1aff-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="e1aff-107">U kunt uw gebruikers tooautomatically get aangemelde tooProofpoint op verzoek (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e1aff-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1aff-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e1aff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1aff-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1aff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1aff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e1aff-110">Prerequisites</span></span>

<span data-ttu-id="e1aff-111">tooconfigure Azure AD-integratie met Proofpoint op verzoek, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e1aff-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="e1aff-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e1aff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1aff-113">Een Proofpoint op verzoek-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e1aff-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1aff-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e1aff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1aff-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1aff-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e1aff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1aff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1aff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1aff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e1aff-118">Scenario description</span></span>
<span data-ttu-id="e1aff-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e1aff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1aff-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1aff-121">Het toevoegen van Proofpoint op verzoek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e1aff-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="e1aff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e1aff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="e1aff-123">Het toevoegen van Proofpoint op verzoek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e1aff-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="e1aff-124">tooconfigure hello integratie van Proofpoint op verzoek in Azure AD, moet u tooadd Proofpoint op verzoek van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e1aff-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1aff-125">**tooadd Proofpoint op verzoek vanuit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e1aff-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1aff-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e1aff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1aff-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1aff-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e1aff-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e1aff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e1aff-133">Typ in het zoekvak Hallo **Proofpoint op verzoek**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="e1aff-135">Selecteer in het deelvenster resultaten hello, **Proofpoint op verzoek**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1aff-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1aff-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e1aff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1aff-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Proofpoint op verzoek op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e1aff-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1aff-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Proofpoint op verzoek is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1aff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="e1aff-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Proofpoint op aanvraag toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e1aff-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="e1aff-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Proofpoint op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e1aff-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="e1aff-142">tooconfigure en Azure AD test eenmalige aanmelding Proofpoint op verzoek, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1aff-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e1aff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1aff-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1aff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1aff-145">**[Maken van een Proofpoint op aanvraag testgebruiker](#creating-a-proofpoint-on-demand-test-user)**  -toohave een equivalent van Britta Simon in Proofpoint op aanvraag die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e1aff-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1aff-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e1aff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1aff-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e1aff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1aff-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e1aff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1aff-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Proofpoint op verzoek-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1aff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="e1aff-150">**Azure AD tooconfigure eenmalige aanmelding met Proofpoint op aanvraag uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e1aff-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1aff-151">In de Azure-portal op Hallo Hallo **Proofpoint op verzoek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e1aff-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e1aff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="e1aff-155">Op Hallo **Proofpoint op verzoek-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="e1aff-157">Hallo a.In **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="e1aff-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="e1aff-158">b.</span><span class="sxs-lookup"><span data-stu-id="e1aff-158">b.</span></span> <span data-ttu-id="e1aff-159">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="e1aff-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="e1aff-160">c.</span><span class="sxs-lookup"><span data-stu-id="e1aff-160">c.</span></span>  <span data-ttu-id="e1aff-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="e1aff-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e1aff-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="e1aff-162">These values are not hello real.</span></span> <span data-ttu-id="e1aff-163">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="e1aff-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="e1aff-164">Neem contact op met [Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e1aff-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="e1aff-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e1aff-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="e1aff-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e1aff-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e1aff-169">Op Hallo **Proofpoint op verzoek-configuratie** sectie, klikt u op **Proofpoint op verzoek configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e1aff-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1aff-170">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e1aff-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="e1aff-172">tooconfigure eenmalige aanmelding op **Proofpoint op verzoek** zijde, moet u toosend Hallo gedownload **Certificate(Base64)**,**SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** te[Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="e1aff-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="e1aff-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e1aff-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1aff-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e1aff-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1aff-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1aff-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1aff-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e1aff-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1aff-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e1aff-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e1aff-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e1aff-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1aff-180">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e1aff-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1aff-182">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="e1aff-182">These values are not hello real.</span></span> <span data-ttu-id="e1aff-183">Bijwerken van deze waarden met Hallo werkelijke</span><span class="sxs-lookup"><span data-stu-id="e1aff-183">Update these values with hello actual</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1aff-185">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e1aff-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1aff-187">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1aff-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1aff-189">a.</span><span class="sxs-lookup"><span data-stu-id="e1aff-189">a.</span></span> <span data-ttu-id="e1aff-190">In Hallo **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="e1aff-191">b.</span><span class="sxs-lookup"><span data-stu-id="e1aff-191">b.</span></span> <span data-ttu-id="e1aff-192">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1aff-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="e1aff-193">c.</span><span class="sxs-lookup"><span data-stu-id="e1aff-193">c.</span></span> <span data-ttu-id="e1aff-194">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1aff-195">d.</span><span class="sxs-lookup"><span data-stu-id="e1aff-195">d.</span></span> <span data-ttu-id="e1aff-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="e1aff-197">Maken van een Proofpoint op aanvraag testgebruiker</span><span class="sxs-lookup"><span data-stu-id="e1aff-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="e1aff-198">In deze sectie maakt u Britta Simon aangeroepen in Proofpoint op verzoek van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e1aff-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="e1aff-199">Werken met [Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services) tooadd gebruikers in Hallo Proofpoint op verzoek-platform.</span><span class="sxs-lookup"><span data-stu-id="e1aff-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1aff-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1aff-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1aff-201">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooProofpoint op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e1aff-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e1aff-203">**tooassign Britta Simon tooProofpoint op aanvraag uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e1aff-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1aff-204">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e1aff-206">Selecteer in de lijst met de toepassingen van Hallo **Proofpoint op verzoek**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="e1aff-208">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e1aff-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e1aff-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e1aff-210">Click **Add** button.</span></span> <span data-ttu-id="e1aff-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e1aff-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e1aff-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e1aff-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1aff-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e1aff-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1aff-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e1aff-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1aff-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e1aff-216">Testing single sign-on</span></span>

<span data-ttu-id="e1aff-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e1aff-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1aff-218">Wanneer u klikt op Hallo **Proofpoint op verzoek** tegel op Hallo paneel voor Apptoegang, moet u automatisch worden aangemeld op tooyour Proofpoint op verzoek-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e1aff-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="e1aff-219">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1aff-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="e1aff-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e1aff-220">Additional resources</span></span>

* [<span data-ttu-id="e1aff-221">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1aff-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1aff-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1aff-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

