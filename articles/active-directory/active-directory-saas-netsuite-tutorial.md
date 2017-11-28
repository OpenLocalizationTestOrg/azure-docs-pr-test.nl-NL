---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="3e8e6-103">Zelfstudie: Azure Active Directory-integratie met Netsuite</span><span class="sxs-lookup"><span data-stu-id="3e8e6-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="3e8e6-104">In deze zelfstudie leert u hoe toointegrate Netsuite met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e8e6-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e8e6-105">Netsuite integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e8e6-106">U kunt beheren in Azure AD die tooNetsuite toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3e8e6-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="3e8e6-107">U kunt uw gebruikers tooautomatically get aangemelde tooNetsuite (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3e8e6-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e8e6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3e8e6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e8e6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e8e6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e8e6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3e8e6-110">Prerequisites</span></span>

<span data-ttu-id="3e8e6-111">Azure AD-integratie met Netsuite tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="3e8e6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3e8e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e8e6-113">Een Netsuite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3e8e6-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e8e6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e8e6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e8e6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e8e6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e8e6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e8e6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3e8e6-118">Scenario description</span></span>
<span data-ttu-id="3e8e6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e8e6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e8e6-121">Het toevoegen van Netsuite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3e8e6-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="3e8e6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e8e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="3e8e6-123">Het toevoegen van Netsuite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3e8e6-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="3e8e6-124">tooconfigure hello integratie van Netsuite in Azure AD, moet u tooadd Netsuite uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e8e6-125">**tooadd Netsuite via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3e8e6-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e8e6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e8e6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e8e6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3e8e6-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3e8e6-133">Typ in het zoekvak Hallo **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-133">In hello search box, type **Netsuite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="3e8e6-135">Selecteer in het deelvenster resultaten hello, **Netsuite**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e8e6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e8e6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e8e6-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Netsuite op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3e8e6-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e8e6-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Netsuite is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="3e8e6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Netsuite toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="3e8e6-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="3e8e6-142">tooconfigure en eenmalige aanmelding Azure AD-test met Netsuite, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e8e6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e8e6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e8e6-145">**[Maken van een testgebruiker Netsuite](#creating-a-netsuite-test-user)**  -toohave een equivalent van Britta Simon in Netsuite die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e8e6-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e8e6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e8e6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3e8e6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e8e6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Netsuite configureren.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="3e8e6-150">**Azure AD tooconfigure eenmalige aanmelding met Netsuite, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3e8e6-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e8e6-151">In de Azure-portal op Hallo Hallo **Netsuite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3e8e6-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="3e8e6-155">Op Hallo **Netsuite domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="3e8e6-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="3e8e6-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e8e6-158">Deze waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-158">This value is not real value.</span></span> <span data-ttu-id="3e8e6-159">Waarde van de update Hallo met Hallo werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="3e8e6-160">Neem contact op met [Netsuite ondersteuningsteam](http://www.netsuite.com/portal/services/support.shtml) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="3e8e6-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="3e8e6-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e8e6-165">Op Hallo **Netsuite configuratie** sectie, klikt u op **configureren Netsuite** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e8e6-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3e8e6-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="3e8e6-168">Een nieuw tabblad openen in uw browser en meld u aan bij uw site van het bedrijf Netsuite als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="3e8e6-169">Klik in de werkbalk bovenaan Hallo Hallo pagina Hallo op **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="3e8e6-171">Van Hallo **instellingstaken** selecteert **integratie**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="3e8e6-173">In Hallo **verificatie beheren** sectie, klikt u op **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="3e8e6-175">Op Hallo **SAML Setup** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="3e8e6-176">a.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-176">a.</span></span> <span data-ttu-id="3e8e6-177">Kopiëren Hallo **SAML Single Sign-On Service-URL** waarde uit de **Naslaggids** sectie van **eenmalige aanmelding configureren** en plak deze in Hallo **id-Provider Aanmeldingspagina** veld Netsuite.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="3e8e6-179">b.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-179">b.</span></span> <span data-ttu-id="3e8e6-180">Selecteer in de Netsuite, **primaire methode voor netwerkverificatie**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="3e8e6-181">c.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-181">c.</span></span> <span data-ttu-id="3e8e6-182">Voor het Hallo-veld met het label **SAMLV2 identiteit Provider metagegevens**, selecteer **IDP metagegevens-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="3e8e6-183">Klik vervolgens op **Bladeren** tooupload Hallo bestand met metagegevens dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="3e8e6-185">d.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-185">d.</span></span> <span data-ttu-id="3e8e6-186">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-186">Click **Submit**.</span></span>

12. <span data-ttu-id="3e8e6-187">In Azure AD, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje en het kenmerk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="3e8e6-189">Voor Hallo **kenmerknaam** veld, typt u in `account`.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="3e8e6-190">Voor Hallo **kenmerkwaarde** veld, typt u in uw Netsuite account-ID. Deze waarde is constante en wijzigen met account.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="3e8e6-191">Instructies voor het toofind je account-ID zijn hieronder vermeld:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="3e8e6-193">a.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-193">a.</span></span> <span data-ttu-id="3e8e6-194">In Netsuite, klikt u op **Setup** in Hallo bovenste navigatiebalk menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="3e8e6-195">b.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-195">b.</span></span> <span data-ttu-id="3e8e6-196">Klik onder Hallo **instellingstaken** sectie van Hallo linkernavigatievenster menu, selecteer Hallo **integratie** sectie en op **Web Services-voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="3e8e6-197">c.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-197">c.</span></span> <span data-ttu-id="3e8e6-198">Kopieer uw Netsuite Account-ID en plak deze in Hallo **kenmerkwaarde** veld in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="3e8e6-200">Voordat gebruikers eenmalige aanmelding in Netsuite uitvoeren kunnen, moeten worden ze eerst de juiste machtigingen Hallo in Netsuite toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="3e8e6-201">Volg onderstaande tooassign Hallo instructies deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="3e8e6-202">a.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-202">a.</span></span> <span data-ttu-id="3e8e6-203">Klik op het menu van de bovenste navigatiebalk hello, **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="3e8e6-205">b.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-205">b.</span></span> <span data-ttu-id="3e8e6-206">Selecteer Hallo linkernavigatievenster menu **gebruikers/rollen**, klikt u vervolgens op **rollen beheren**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="3e8e6-208">c.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-208">c.</span></span> <span data-ttu-id="3e8e6-209">Klik op **nieuwe rol**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-209">Click **New Role**.</span></span>

    <span data-ttu-id="3e8e6-210">d.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-210">d.</span></span> <span data-ttu-id="3e8e6-211">Typ in een **naam** voor uw nieuwe rol en selecteer Hallo **eenmalige aanmelding alleen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="3e8e6-213">e.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-213">e.</span></span> <span data-ttu-id="3e8e6-214">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-214">Click **Save**.</span></span>

    <span data-ttu-id="3e8e6-215">f.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-215">f.</span></span> <span data-ttu-id="3e8e6-216">Klik in het menu bovenaan Hallo Hallo **machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="3e8e6-217">Klik vervolgens op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-217">Then click **Setup**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="3e8e6-219">g.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-219">g.</span></span> <span data-ttu-id="3e8e6-220">Selecteer **ingesteld Up SAM Single Sign-on**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="3e8e6-221">h.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-221">h.</span></span> <span data-ttu-id="3e8e6-222">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-222">Click **Save**.</span></span>

    <span data-ttu-id="3e8e6-223">ik.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-223">i.</span></span> <span data-ttu-id="3e8e6-224">Klik op het menu van de bovenste navigatiebalk hello, **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="3e8e6-226">j.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-226">j.</span></span> <span data-ttu-id="3e8e6-227">Selecteer Hallo linkernavigatievenster menu **gebruikers/rollen**, klikt u vervolgens op **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="3e8e6-229">k.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-229">k.</span></span> <span data-ttu-id="3e8e6-230">Selecteer een testgebruiker.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-230">Select a test user.</span></span> <span data-ttu-id="3e8e6-231">Klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-231">Then click **Edit**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="3e8e6-233">l.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-233">l.</span></span> <span data-ttu-id="3e8e6-234">Selecteer in het dialoogvenster Hallo rollen, Hallo-rol die u hebt gemaakt en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="3e8e6-236">m.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-236">m.</span></span> <span data-ttu-id="3e8e6-237">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="3e8e6-238">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e8e6-239">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e8e6-240">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e8e6-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e8e6-241">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3e8e6-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e8e6-242">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3e8e6-244">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3e8e6-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e8e6-245">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="3e8e6-247">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e8e6-249">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e8e6-251">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3e8e6-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e8e6-253">a.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-253">a.</span></span> <span data-ttu-id="3e8e6-254">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e8e6-255">b.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-255">b.</span></span> <span data-ttu-id="3e8e6-256">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e8e6-257">c.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-257">c.</span></span> <span data-ttu-id="3e8e6-258">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e8e6-259">d.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-259">d.</span></span> <span data-ttu-id="3e8e6-260">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="3e8e6-261">Een testgebruiker Netsuite maken</span><span class="sxs-lookup"><span data-stu-id="3e8e6-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="3e8e6-262">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="3e8e6-263">Netsuite ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="3e8e6-264">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-264">There is no action item for you in this section.</span></span> <span data-ttu-id="3e8e6-265">Als een gebruiker in Netsuite nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Netsuite probeert.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e8e6-266">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e8e6-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e8e6-267">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNetsuite toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3e8e6-269">**tooassign Britta Simon tooNetsuite, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3e8e6-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e8e6-270">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3e8e6-272">Selecteer in de lijst met de toepassingen van Hallo **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-272">In hello applications list, select **Netsuite**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="3e8e6-274">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3e8e6-276">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-276">Click **Add** button.</span></span> <span data-ttu-id="3e8e6-277">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3e8e6-279">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e8e6-280">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e8e6-281">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e8e6-282">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3e8e6-282">Testing single sign-on</span></span>

<span data-ttu-id="3e8e6-283">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e8e6-284">tootest uw eenmalige aanmelding-instellingen, open Hallo Toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meld u aan bij de testaccount Hallo en klikt u op **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="3e8e6-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e8e6-285">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3e8e6-285">Additional resources</span></span>

* [<span data-ttu-id="3e8e6-286">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e8e6-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e8e6-287">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e8e6-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3e8e6-288">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="3e8e6-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

