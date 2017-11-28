---
title: 'Zelfstudie: Azure Active Directory-integratie met Velpic SAML | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="b736c-103">Zelfstudie: Azure Active Directory-integratie met Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="b736c-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="b736c-104">In deze zelfstudie leert u hoe toointegrate Velpic SAML met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b736c-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b736c-105">Velpic SAML integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b736c-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b736c-106">U kunt beheren in Azure AD wie toegang tot tooVelpic SAML heeft</span><span class="sxs-lookup"><span data-stu-id="b736c-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="b736c-107">U kunt uw gebruikers tooautomatically get aangemelde tooVelpic SAML (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b736c-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b736c-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="b736c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b736c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b736c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b736c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b736c-110">Prerequisites</span></span>

<span data-ttu-id="b736c-111">Azure AD-integratie met Velpic SAML tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b736c-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="b736c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b736c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b736c-113">Een Velpic SAML-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b736c-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b736c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b736c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b736c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b736c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b736c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b736c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b736c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b736c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b736c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b736c-118">Scenario description</span></span>
<span data-ttu-id="b736c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b736c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b736c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b736c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b736c-121">Het toevoegen van Velpic SAML van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b736c-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="b736c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b736c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="b736c-123">Het toevoegen van Velpic SAML van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b736c-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="b736c-124">tooconfigure hello integratie van Velpic SAML in Azure AD, moet u tooadd Velpic SAML uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b736c-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b736c-125">**tooadd Velpic SAML via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b736c-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b736c-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b736c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b736c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b736c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b736c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b736c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b736c-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b736c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b736c-133">Typ in het zoekvak Hallo **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="b736c-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="b736c-135">Selecteer in het deelvenster resultaten hello, **Velpic SAML**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b736c-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b736c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b736c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b736c-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Velpic SAML op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b736c-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b736c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Velpic SAML is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b736c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="b736c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Velpic SAML toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b736c-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="b736c-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="b736c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="b736c-142">tooconfigure en eenmalige aanmelding Azure AD-test met Velpic SAML, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b736c-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b736c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b736c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b736c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b736c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b736c-145">**[Maken van een testgebruiker Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave een equivalent van Britta Simon in Velpic SAML die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="b736c-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b736c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b736c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b736c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b736c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b736c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b736c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b736c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="b736c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="b736c-150">**Azure AD tooconfigure eenmalige aanmelding met Velpic SAML, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b736c-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="b736c-151">In hello Azure Management portal op Hallo **Velpic SAML** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b736c-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b736c-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b736c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="b736c-155">Voer Hallo-gegevens in Hallo **Velpic SAML-domein en de URL's** sectie -</span><span class="sxs-lookup"><span data-stu-id="b736c-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="b736c-157">a.</span><span class="sxs-lookup"><span data-stu-id="b736c-157">a.</span></span> <span data-ttu-id="b736c-158">In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="b736c-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="b736c-159">b.</span><span class="sxs-lookup"><span data-stu-id="b736c-159">b.</span></span> <span data-ttu-id="b736c-160">In Hallo **id** textbox plakken Hallo **'Eenmalige op URL'** waarde`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="b736c-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b736c-161">Houd er rekening mee dat Hallo aanmelding URL worden geleverd door Hallo Velpic SAML-team en id-waarde beschikbaar zijn bij het configureren van SSO-invoegtoepassing Hallo Velpic SAML-zijde.</span><span class="sxs-lookup"><span data-stu-id="b736c-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="b736c-162">U moet toocopy die de waarde uit de pagina Velpic SAML-toepassing en plakt u deze hier.</span><span class="sxs-lookup"><span data-stu-id="b736c-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="b736c-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b736c-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="b736c-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b736c-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b736c-167">Klik op Hallo Velpic SAML-configuratiesectie, configureer Velpic SAML tooopen configureren aanmelding venster.</span><span class="sxs-lookup"><span data-stu-id="b736c-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="b736c-168">Hallo SAML entiteit-ID van Hallo Naslaggids punt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b736c-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="b736c-169">In een ander browservenster, meld u bij uw bedrijf Velpic SAML site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b736c-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="b736c-170">Klik op **beheren** tabblad en ga te**integratie** sectie waarin u tooclick moet op **Plugins** knop toocreate nieuwe-invoegtoepassing voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b736c-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="b736c-172">Klik op Hallo **'Add invoegtoepassing'** knop.</span><span class="sxs-lookup"><span data-stu-id="b736c-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="b736c-174">Klik op Hallo **SAML** -tegel in Hallo invoegtoepassing toevoegen pagina.</span><span class="sxs-lookup"><span data-stu-id="b736c-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="b736c-176">Hallo-naam van de nieuwe SAML-invoegtoepassing Hallo en klik op Hallo **'Add-** knop.</span><span class="sxs-lookup"><span data-stu-id="b736c-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="b736c-178">Voer Hallo gegevens als volgt in:</span><span class="sxs-lookup"><span data-stu-id="b736c-178">Enter hello details as follows:</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="b736c-180">a.</span><span class="sxs-lookup"><span data-stu-id="b736c-180">a.</span></span> <span data-ttu-id="b736c-181">In Hallo **naam** textbox Hallo-typenaam van SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="b736c-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="b736c-182">b.</span><span class="sxs-lookup"><span data-stu-id="b736c-182">b.</span></span> <span data-ttu-id="b736c-183">In Hallo **URL-verlener** textbox plakken Hallo **SAML entiteit-ID** u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b736c-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="b736c-184">c.</span><span class="sxs-lookup"><span data-stu-id="b736c-184">c.</span></span> <span data-ttu-id="b736c-185">In Hallo **Provider metagegevens Config** Hallo Metadata XML-bestand dat u hebt gedownload van Azure-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="b736c-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="b736c-186">d.</span><span class="sxs-lookup"><span data-stu-id="b736c-186">d.</span></span> <span data-ttu-id="b736c-187">U kunt ook tooenable SAML in tijd inrichten door in te schakelen Hallo **'Automatische Maak nieuwe gebruikers'** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="b736c-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="b736c-188">Als een gebruiker niet in Velpic bestaat en deze markering niet is ingeschakeld, mislukt de Hallo aanmelding van Azure.</span><span class="sxs-lookup"><span data-stu-id="b736c-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="b736c-189">Als het Hallo-vlag is ingeschakeld Hallo gebruiker wordt automatisch worden ingericht in Velpic op Hallo-tijd van de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b736c-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="b736c-190">e.</span><span class="sxs-lookup"><span data-stu-id="b736c-190">e.</span></span> <span data-ttu-id="b736c-191">Kopiëren Hallo **eenmalige op URL** vanuit Hallo tekstvak en plakt Hallo in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b736c-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="b736c-192">f.</span><span class="sxs-lookup"><span data-stu-id="b736c-192">f.</span></span> <span data-ttu-id="b736c-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b736c-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b736c-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b736c-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="b736c-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b736c-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b736c-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b736c-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b736c-198">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b736c-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b736c-200">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b736c-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b736c-202">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b736c-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b736c-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b736c-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b736c-206">a.</span><span class="sxs-lookup"><span data-stu-id="b736c-206">a.</span></span> <span data-ttu-id="b736c-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b736c-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b736c-208">b.</span><span class="sxs-lookup"><span data-stu-id="b736c-208">b.</span></span> <span data-ttu-id="b736c-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b736c-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b736c-210">c.</span><span class="sxs-lookup"><span data-stu-id="b736c-210">c.</span></span> <span data-ttu-id="b736c-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b736c-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b736c-212">d.</span><span class="sxs-lookup"><span data-stu-id="b736c-212">d.</span></span> <span data-ttu-id="b736c-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b736c-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="b736c-214">Een testgebruiker Velpic SAML maken</span><span class="sxs-lookup"><span data-stu-id="b736c-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="b736c-215">Deze stap is meestal niet vereist als toepassing hello alleen in de tijd gebruikersaanvragen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="b736c-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="b736c-216">Als Hallo automatisch gebruikers inrichten niet is ingeschakeld kan vervolgens maken van een handmatige gebruikersaccount worden uitgevoerd zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b736c-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="b736c-217">Meld u aan bij uw site van het bedrijf Velpic SAML als beheerder en voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b736c-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="b736c-218">Klik op het tabblad beheren en ga tooUsers sectie en klik vervolgens op de nieuwe knop tooadd gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b736c-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![gebruiker toevoegen](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="b736c-220">Op Hallo **'Nieuwe gebruiker maken'** dialoogvenster pagina, voert u Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="b736c-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![Gebruiker](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="b736c-222">a.</span><span class="sxs-lookup"><span data-stu-id="b736c-222">a.</span></span> <span data-ttu-id="b736c-223">In Hallo **voornaam** textbox type Hallo voornaam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b736c-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="b736c-224">b.</span><span class="sxs-lookup"><span data-stu-id="b736c-224">b.</span></span> <span data-ttu-id="b736c-225">In Hallo **achternaam** textbox type Hallo achternaam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b736c-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="b736c-226">c.</span><span class="sxs-lookup"><span data-stu-id="b736c-226">c.</span></span> <span data-ttu-id="b736c-227">In Hallo **gebruikersnaam** textbox, typ de gebruikersnaam van Britta Simon Hallo.</span><span class="sxs-lookup"><span data-stu-id="b736c-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="b736c-228">d.</span><span class="sxs-lookup"><span data-stu-id="b736c-228">d.</span></span> <span data-ttu-id="b736c-229">In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="b736c-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="b736c-230">e.</span><span class="sxs-lookup"><span data-stu-id="b736c-230">e.</span></span> <span data-ttu-id="b736c-231">Overige Hallo informatie is optioneel, vult u deze indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b736c-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="b736c-232">f.</span><span class="sxs-lookup"><span data-stu-id="b736c-232">f.</span></span> <span data-ttu-id="b736c-233">Klik op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="b736c-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b736c-234">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b736c-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b736c-235">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooVelpic SAML verlenen.</span><span class="sxs-lookup"><span data-stu-id="b736c-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b736c-237">**tooassign Britta Simon tooVelpic SAML, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b736c-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="b736c-238">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b736c-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b736c-240">Selecteer in de lijst met de toepassingen van Hallo **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="b736c-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="b736c-242">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b736c-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b736c-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b736c-244">Click **Add** button.</span></span> <span data-ttu-id="b736c-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b736c-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b736c-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b736c-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b736c-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b736c-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b736c-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b736c-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b736c-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b736c-250">Testing single sign-on</span></span>

<span data-ttu-id="b736c-251">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b736c-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="b736c-252">Als u op Hallo Velpic SAML-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Velpic SAML-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b736c-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="b736c-253">U ziet Hallo **'Aanmelden met Azure AD'** knop op de aanmeldingspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="b736c-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="b736c-255">Klik op Hallo **'Aanmelden met Azure AD'** knop toolog in tooVelpic met behulp van uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="b736c-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b736c-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b736c-256">Additional resources</span></span>

* [<span data-ttu-id="b736c-257">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b736c-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b736c-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b736c-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

