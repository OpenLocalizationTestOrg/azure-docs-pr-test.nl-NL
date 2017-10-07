---
title: 'Zelfstudie: Azure Active Directory-integratie met Panopto | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Panopto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="dbbe8-103">Zelfstudie: Azure Active Directory-integratie met Panopto</span><span class="sxs-lookup"><span data-stu-id="dbbe8-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="dbbe8-104">In deze zelfstudie leert u hoe toointegrate Panopto met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbbe8-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbbe8-105">Panopto integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dbbe8-106">U kunt beheren in Azure AD die tooPanopto toegang heeft</span><span class="sxs-lookup"><span data-stu-id="dbbe8-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="dbbe8-107">U kunt uw gebruikers tooautomatically get aangemelde tooPanopto (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="dbbe8-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbbe8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="dbbe8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dbbe8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbbe8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbbe8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dbbe8-110">Prerequisites</span></span>

<span data-ttu-id="dbbe8-111">Azure AD-integratie met Panopto tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="dbbe8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dbbe8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbbe8-113">Een Panopto eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="dbbe8-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbbe8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbbe8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbbe8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbbe8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbbe8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbbe8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dbbe8-118">Scenario description</span></span>
<span data-ttu-id="dbbe8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbbe8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbbe8-121">Het toevoegen van Panopto van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dbbe8-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="dbbe8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dbbe8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="dbbe8-123">Het toevoegen van Panopto van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dbbe8-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="dbbe8-124">tooconfigure hello integratie van Panopto in Azure AD, moet u tooadd Panopto uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dbbe8-125">**tooadd Panopto via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dbbe8-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbbe8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbbe8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dbbe8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="dbbe8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="dbbe8-133">Typ in het zoekvak Hallo **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-133">In hello search box, type **Panopto**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="dbbe8-135">Selecteer in het deelvenster resultaten hello, **Panopto**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbbe8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dbbe8-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="dbbe8-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Panopto op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dbbe8-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dbbe8-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Panopto is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="dbbe8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Panopto toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="dbbe8-141">Wijs in Panopto, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dbbe8-142">tooconfigure en eenmalige aanmelding Azure AD-test met Panopto, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dbbe8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dbbe8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbbe8-145">**[Maken van een testgebruiker Panopto](#creating-a-panopto-test-user)**  -toohave een equivalent van Britta Simon in Panopto die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbbe8-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbbe8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbbe8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="dbbe8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbbe8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Panopto configureren.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="dbbe8-150">**Azure AD tooconfigure eenmalige aanmelding met Panopto, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dbbe8-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbbe8-151">In de Azure-portal op Hallo Hallo **Panopto** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="dbbe8-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="dbbe8-155">Op Hallo **Panopto domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="dbbe8-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="dbbe8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dbbe8-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-158">This value is not real.</span></span> <span data-ttu-id="dbbe8-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dbbe8-160">Neem contact op met [Panopto Client ondersteuningsteam](mailto:support@panopto.com‎) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="dbbe8-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="dbbe8-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dbbe8-165">Op Hallo **Panopto configuratie** sectie, klikt u op **configureren Panopto** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dbbe8-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="dbbe8-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="dbbe8-168">In een ander browservenster, meld u aan tooyour Panopto bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="dbbe8-169">Klik in de werkbalk aan de linkerkant Hallo Hallo op **System**, en klik vervolgens op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="dbbe8-170">![Systeem](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span><span class="sxs-lookup"><span data-stu-id="dbbe8-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="dbbe8-171">Klik op **Provider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="dbbe8-172">![ID-Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "id-Providers")</span><span class="sxs-lookup"><span data-stu-id="dbbe8-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="dbbe8-173">Voer in Hallo sectie SAML-provider, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dbbe8-174">![SaaS-configuratie](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS-configuratie")</span><span class="sxs-lookup"><span data-stu-id="dbbe8-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="dbbe8-175">a.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-175">a.</span></span> <span data-ttu-id="dbbe8-176">Van Hallo **providertype** selecteert **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="dbbe8-177">b.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-177">b.</span></span> <span data-ttu-id="dbbe8-178">In Hallo **exemplaarnaam** textbox, typ een naam voor het Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="dbbe8-179">c.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-179">c.</span></span> <span data-ttu-id="dbbe8-180">In Hallo **beschrijving** textbox, typt u een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="dbbe8-181">d.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-181">d.</span></span> <span data-ttu-id="dbbe8-182">In **pagina-Url Stuiteren** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dbbe8-183">e.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-183">e.</span></span> <span data-ttu-id="dbbe8-184">In Hallo **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dbbe8-185">f.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-185">f.</span></span> <span data-ttu-id="dbbe8-186">Open uw base-64 gecodeerde certificaat dat u hebt gedownload van Azure portal, kopie Hallo inhoud ervan in tooyour Klembord, en plak deze toohello **openbare sleutel** textbox.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="dbbe8-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dbbe8-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dbbe8-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dbbe8-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dbbe8-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbbe8-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dbbe8-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="dbbe8-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="dbbe8-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dbbe8-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbbe8-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbbe8-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbbe8-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbbe8-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dbbe8-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbbe8-203">a.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-203">a.</span></span> <span data-ttu-id="dbbe8-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbbe8-205">b.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-205">b.</span></span> <span data-ttu-id="dbbe8-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbbe8-207">c.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-207">c.</span></span> <span data-ttu-id="dbbe8-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dbbe8-209">d.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-209">d.</span></span> <span data-ttu-id="dbbe8-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="dbbe8-211">Een testgebruiker Panopto maken</span><span class="sxs-lookup"><span data-stu-id="dbbe8-211">Creating a Panopto test user</span></span>

<span data-ttu-id="dbbe8-212">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="dbbe8-213">Wanneer een toegewezen gebruiker toolog in tooPanopto met behulp van het toegangsvenster hello probeert, controleert Panopto of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="dbbe8-214">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Panopto.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="dbbe8-215">U kunt andere Panopto gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Panopto tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dbbe8-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbbe8-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dbbe8-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPanopto toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="dbbe8-219">**tooassign Britta Simon tooPanopto, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dbbe8-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="dbbe8-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="dbbe8-222">Selecteer in de lijst met de toepassingen van Hallo **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-222">In hello applications list, select **Panopto**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="dbbe8-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="dbbe8-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-226">Click **Add** button.</span></span> <span data-ttu-id="dbbe8-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="dbbe8-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dbbe8-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbbe8-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbbe8-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dbbe8-232">Testing single sign-on</span></span>

<span data-ttu-id="dbbe8-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dbbe8-234">Wanneer u Hallo Panopto tegel in Hallo toegangsvenster klikt, moet u de aanmeldingspagina van Panopto toepassing automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="dbbe8-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="dbbe8-235">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dbbe8-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbbe8-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dbbe8-236">Additional resources</span></span>

* [<span data-ttu-id="dbbe8-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbbe8-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbbe8-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbbe8-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

