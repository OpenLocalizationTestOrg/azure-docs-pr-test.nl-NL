---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="89ac2-103">Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="89ac2-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="89ac2-104">In deze zelfstudie leert u hoe toointegrate Dropbox voor bedrijven gebruiken met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89ac2-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89ac2-105">Dropbox voor bedrijven integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89ac2-106">U kunt beheren in Azure AD wie toegang tot tooDropbox voor bedrijven heeft</span><span class="sxs-lookup"><span data-stu-id="89ac2-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="89ac2-107">U kunt uw gebruikers tooautomatically get aangemelde tooDropbox voor bedrijven (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="89ac2-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89ac2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="89ac2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="89ac2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89ac2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89ac2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="89ac2-110">Prerequisites</span></span>

<span data-ttu-id="89ac2-111">tooconfigure Azure AD-integratie met Dropbox voor bedrijven, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="89ac2-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="89ac2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="89ac2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89ac2-113">Een Dropbox voor eenmalige aanmelding Business abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="89ac2-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89ac2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="89ac2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89ac2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89ac2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="89ac2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89ac2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89ac2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89ac2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="89ac2-118">Scenario description</span></span>
<span data-ttu-id="89ac2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="89ac2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89ac2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89ac2-121">Het toevoegen van Dropbox voor bedrijven van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89ac2-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="89ac2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89ac2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="89ac2-123">Het toevoegen van Dropbox voor bedrijven van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="89ac2-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="89ac2-124">tooconfigure hello integratie van Dropbox voor bedrijven met Azure AD, moet u tooadd Dropbox uit Hallo galerie tooyour lijst met beheerde SaaS-apps voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="89ac2-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89ac2-125">**tooadd Dropbox voor bedrijven via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89ac2-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89ac2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89ac2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89ac2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89ac2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="89ac2-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="89ac2-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="89ac2-133">Typ in het zoekvak Hallo **Dropbox voor bedrijven**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="89ac2-135">Selecteer in het deelvenster resultaten hello, **Dropbox voor bedrijven**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89ac2-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89ac2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89ac2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89ac2-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Dropbox voor bedrijven op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="89ac2-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="89ac2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Dropbox voor bedrijven is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89ac2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="89ac2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Dropbox voor bedrijven toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="89ac2-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="89ac2-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="89ac2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="89ac2-142">tooconfigure en test eenmalige aanmelding Azure AD met Dropbox voor bedrijven, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89ac2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="89ac2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89ac2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89ac2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89ac2-145">**[Maken van een Dropbox voor zakelijke testgebruiker](#creating-a-dropbox-for-business-test-user)**  -toohave een equivalent van Britta Simon in Dropbox voor bedrijven die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="89ac2-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89ac2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89ac2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89ac2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="89ac2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89ac2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="89ac2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89ac2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw dropbox geplaatst voor Business-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89ac2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="89ac2-150">**Azure AD tooconfigure eenmalige aanmelding met Dropbox voor bedrijven, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89ac2-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="89ac2-151">In de Azure-portal op Hallo Hallo **Dropbox voor bedrijven** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="89ac2-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="89ac2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="89ac2-155">Op Hallo **Dropbox voor Business-domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="89ac2-156">a.</span><span class="sxs-lookup"><span data-stu-id="89ac2-156">a.</span></span> <span data-ttu-id="89ac2-157">Meld u aan op tooyour Dropbox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="89ac2-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="89ac2-158">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="89ac2-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="89ac2-159">b.</span><span class="sxs-lookup"><span data-stu-id="89ac2-159">b.</span></span> <span data-ttu-id="89ac2-160">Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="89ac2-161">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="89ac2-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="89ac2-162">c.</span><span class="sxs-lookup"><span data-stu-id="89ac2-162">c.</span></span> <span data-ttu-id="89ac2-163">Op Hallo **beheerconsole**, klikt u op **verificatie** in het linkernavigatievenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="89ac2-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="89ac2-164">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="89ac2-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="89ac2-165">d.</span><span class="sxs-lookup"><span data-stu-id="89ac2-165">d.</span></span> <span data-ttu-id="89ac2-166">In Hallo **eenmalige aanmelding** sectie **eenmalige aanmelding inschakelen**, en klik vervolgens op **meer** tooexpand in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="89ac2-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="89ac2-167">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="89ac2-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="89ac2-168">e.</span><span class="sxs-lookup"><span data-stu-id="89ac2-168">e.</span></span> <span data-ttu-id="89ac2-169">Kopieer de URL Hallo naast te**kunnen gebruikers zich aanmelden door te voeren van het e-mailadres of kunnen ze rechtstreeks naar**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="89ac2-171">f.</span><span class="sxs-lookup"><span data-stu-id="89ac2-171">f.</span></span> <span data-ttu-id="89ac2-172">Op de Azure-portal, op Hallo Hallo **aanmeldings-URL** textbox plakken Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="89ac2-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="89ac2-174">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="89ac2-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89ac2-175">Deze waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="89ac2-175">This value is not real value.</span></span> <span data-ttu-id="89ac2-176">Hallo waarde bijwerken met Hallo werkelijke aanmeldings-URL u via een sectie voor eenmalige aanmelding krijgen.</span><span class="sxs-lookup"><span data-stu-id="89ac2-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="89ac2-177">Neem contact op met [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="89ac2-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="89ac2-178">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="89ac2-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="89ac2-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="89ac2-180">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89ac2-182">Op Hallo **Dropbox voor zakelijke configuratie** sectie, klikt u op **Dropbox configureren voor bedrijven** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="89ac2-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="89ac2-183">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="89ac2-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="89ac2-185">tooconfigure eenmalige aanmelding op **Dropbox voor bedrijven** zijde, gaat u op uw Dropbox voor bedrijven-tenant in Hallo **eenmalige aanmelding** sectie Hallo **verificatie** pagina Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="89ac2-186">![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "eenmalige aanmelding configureren")</span><span class="sxs-lookup"><span data-stu-id="89ac2-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="89ac2-187">a.</span><span class="sxs-lookup"><span data-stu-id="89ac2-187">a.</span></span> <span data-ttu-id="89ac2-188">Klik op **vereist**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-188">Click **Required**.</span></span>
   
    <span data-ttu-id="89ac2-189">b.</span><span class="sxs-lookup"><span data-stu-id="89ac2-189">b.</span></span> <span data-ttu-id="89ac2-190">In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **aanmelden URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="89ac2-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="89ac2-191">c.</span><span class="sxs-lookup"><span data-stu-id="89ac2-191">c.</span></span> <span data-ttu-id="89ac2-192">Klik op **certificaat kiezen**, en blader vervolgens tooyour **Base64-gecodeerde certificaatbestand**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="89ac2-193">d.</span><span class="sxs-lookup"><span data-stu-id="89ac2-193">d.</span></span> <span data-ttu-id="89ac2-194">Klik op **wijzigingen opslaan** toocomplete Hallo-configuratie op uw DropBox voor bedrijven-tenant.</span><span class="sxs-lookup"><span data-stu-id="89ac2-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="89ac2-195">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="89ac2-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89ac2-196">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="89ac2-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89ac2-197">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89ac2-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89ac2-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="89ac2-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="89ac2-199">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="89ac2-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="89ac2-201">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89ac2-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89ac2-202">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="89ac2-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="89ac2-204">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89ac2-206">Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89ac2-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89ac2-208">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="89ac2-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89ac2-210">a.</span><span class="sxs-lookup"><span data-stu-id="89ac2-210">a.</span></span> <span data-ttu-id="89ac2-211">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89ac2-212">b.</span><span class="sxs-lookup"><span data-stu-id="89ac2-212">b.</span></span> <span data-ttu-id="89ac2-213">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89ac2-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89ac2-214">c.</span><span class="sxs-lookup"><span data-stu-id="89ac2-214">c.</span></span> <span data-ttu-id="89ac2-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89ac2-216">d.</span><span class="sxs-lookup"><span data-stu-id="89ac2-216">d.</span></span> <span data-ttu-id="89ac2-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="89ac2-218">Een Dropbox voor zakelijke testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="89ac2-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="89ac2-219">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Dropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="89ac2-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="89ac2-220">Dropbox voor bedrijven ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="89ac2-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="89ac2-221">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="89ac2-221">There is no action item for you in this section.</span></span> <span data-ttu-id="89ac2-222">Als een gebruiker niet al in Dropbox voor bedrijven bestaat, wordt een nieuw gemaakt wanneer u tooaccess Dropbox voor bedrijven probeert.</span><span class="sxs-lookup"><span data-stu-id="89ac2-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="89ac2-223">Als u een gebruiker handmatig, neem contact op met toocreate moet [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="89ac2-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89ac2-224">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89ac2-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89ac2-225">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooDropbox voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="89ac2-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="89ac2-227">**tooassign Britta Simon tooDropbox voor bedrijven, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="89ac2-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="89ac2-228">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="89ac2-230">Selecteer in de lijst met de toepassingen van Hallo **Dropbox voor bedrijven**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="89ac2-232">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="89ac2-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="89ac2-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="89ac2-234">Click **Add** button.</span></span> <span data-ttu-id="89ac2-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89ac2-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="89ac2-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="89ac2-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89ac2-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89ac2-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89ac2-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89ac2-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89ac2-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="89ac2-240">Testing single sign-on</span></span>

<span data-ttu-id="89ac2-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="89ac2-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89ac2-242">Als u op Dropbox hello voor bedrijven-tegel in Hallo toegangsvenster klikt, krijgt u de aanmeldingspagina van uw Dropbox voor Business-toepassing.</span><span class="sxs-lookup"><span data-stu-id="89ac2-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89ac2-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="89ac2-243">Additional resources</span></span>

* [<span data-ttu-id="89ac2-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89ac2-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89ac2-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89ac2-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="89ac2-246">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="89ac2-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

