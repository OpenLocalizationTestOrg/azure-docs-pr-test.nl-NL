---
title: 'Zelfstudie: Azure Active Directory-integratie met ScreenSteps | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="88437-103">Zelfstudie: Azure Active Directory-integratie met ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="88437-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="88437-104">In deze zelfstudie leert u hoe toointegrate ScreenSteps met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88437-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88437-105">ScreenSteps integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="88437-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88437-106">U kunt beheren in Azure AD die tooScreenSteps toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="88437-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="88437-107">U kunt uw gebruikers tooautomatically get aangemelde tooScreenSteps (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="88437-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="88437-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="88437-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="88437-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88437-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88437-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88437-110">Prerequisites</span></span>

<span data-ttu-id="88437-111">Azure AD-integratie met ScreenSteps tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="88437-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="88437-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="88437-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88437-113">Een ScreenSteps eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="88437-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88437-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="88437-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88437-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88437-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="88437-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88437-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88437-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88437-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="88437-118">Scenario description</span></span>
<span data-ttu-id="88437-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="88437-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88437-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="88437-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88437-121">Het toevoegen van ScreenSteps van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="88437-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="88437-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88437-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="88437-123">Het toevoegen van ScreenSteps van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="88437-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="88437-124">tooconfigure hello integratie van ScreenSteps in Azure AD, moet u tooadd ScreenSteps uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="88437-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88437-125">**tooadd ScreenSteps via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88437-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88437-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="88437-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="88437-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88437-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88437-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88437-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="88437-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88437-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="88437-133">Typ in het zoekvak Hallo **ScreenSteps**, selecteer **ScreenSteps** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="88437-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps in de lijst met resultaten Hallo](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="88437-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="88437-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="88437-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ScreenSteps op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="88437-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88437-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ScreenSteps is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88437-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="88437-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ScreenSteps toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="88437-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="88437-139">Wijs in ScreenSteps, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="88437-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="88437-140">tooconfigure en eenmalige aanmelding Azure AD-test met ScreenSteps, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88437-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="88437-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88437-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88437-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88437-143">**[Maak een testgebruiker ScreenSteps](#create-a-screensteps-test-user)**  -toohave een equivalent van Britta Simon in ScreenSteps die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="88437-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88437-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="88437-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88437-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="88437-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="88437-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="88437-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="88437-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ScreenSteps configureren.</span><span class="sxs-lookup"><span data-stu-id="88437-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="88437-148">**Azure AD tooconfigure eenmalige aanmelding met ScreenSteps, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88437-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="88437-149">In de Azure-portal op Hallo Hallo **ScreenSteps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="88437-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="88437-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="88437-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="88437-153">Op Hallo **ScreenSteps domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en ScreenSteps domein eenmalige aanmelding informatie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="88437-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="88437-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88437-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="88437-156">This value is not real.</span></span> <span data-ttu-id="88437-157">Deze waarde bijwerken Hello werkelijke aanmeldings-URL, die verderop in deze zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="88437-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="88437-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="88437-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="88437-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="88437-160">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88437-162">Op Hallo **ScreenSteps configuratie** sectie, klikt u op **configureren ScreenSteps** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="88437-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88437-163">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="88437-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ScreenSteps configuratie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="88437-165">In een ander browservenster, meld u bij uw bedrijf ScreenSteps site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88437-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="88437-166">Klik op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="88437-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="88437-167">![Accountbeheer](./media/active-directory-saas-screensteps-tutorial/ic778523.png "accountbeheer")</span><span class="sxs-lookup"><span data-stu-id="88437-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="88437-168">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="88437-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="88437-169">![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "externe verificatie")</span><span class="sxs-lookup"><span data-stu-id="88437-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="88437-170">Klik op **Single Sign-on-eindpunt maken**.</span><span class="sxs-lookup"><span data-stu-id="88437-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="88437-171">![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "externe verificatie")</span><span class="sxs-lookup"><span data-stu-id="88437-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="88437-172">In Hallo **maken één aanmelding eindpunt** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="88437-173">![Maak een verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778526.png "een verificatie-eindpunt maken")</span><span class="sxs-lookup"><span data-stu-id="88437-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="88437-174">a.</span><span class="sxs-lookup"><span data-stu-id="88437-174">a.</span></span> <span data-ttu-id="88437-175">In Hallo **titel** textbox, typ een titel.</span><span class="sxs-lookup"><span data-stu-id="88437-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="88437-176">b.</span><span class="sxs-lookup"><span data-stu-id="88437-176">b.</span></span> <span data-ttu-id="88437-177">Van Hallo **modus** selecteert **SAML**.</span><span class="sxs-lookup"><span data-stu-id="88437-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="88437-178">c.</span><span class="sxs-lookup"><span data-stu-id="88437-178">c.</span></span> <span data-ttu-id="88437-179">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="88437-179">Click **Create**.</span></span>

12. <span data-ttu-id="88437-180">**Bewerken** Hallo nieuw eindpunt.</span><span class="sxs-lookup"><span data-stu-id="88437-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="88437-181">![Eindpunt bewerken](./media/active-directory-saas-screensteps-tutorial/ic778528.png "eindpunt bewerken")</span><span class="sxs-lookup"><span data-stu-id="88437-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="88437-182">In Hallo **bewerken één aanmelding eindpunt** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="88437-183">![Externe verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778527.png "externe verificatie-eindpunt")</span><span class="sxs-lookup"><span data-stu-id="88437-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="88437-184">a.</span><span class="sxs-lookup"><span data-stu-id="88437-184">a.</span></span> <span data-ttu-id="88437-185">Klik op **nieuwe SAML certificaat uploadbestand**, en vervolgens uploaden Hallo certificaat dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="88437-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="88437-186">b.</span><span class="sxs-lookup"><span data-stu-id="88437-186">b.</span></span> <span data-ttu-id="88437-187">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **externe aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88437-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="88437-188">c.</span><span class="sxs-lookup"><span data-stu-id="88437-188">c.</span></span> <span data-ttu-id="88437-189">Plakken **Sign-Out URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **afmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88437-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="88437-190">d.</span><span class="sxs-lookup"><span data-stu-id="88437-190">d.</span></span> <span data-ttu-id="88437-191">Selecteer een **groep** tooassign gebruikers toowhen deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="88437-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="88437-192">e.</span><span class="sxs-lookup"><span data-stu-id="88437-192">e.</span></span> <span data-ttu-id="88437-193">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="88437-193">Click **Update**.</span></span>

    <span data-ttu-id="88437-194">f.</span><span class="sxs-lookup"><span data-stu-id="88437-194">f.</span></span> <span data-ttu-id="88437-195">Kopiëren Hallo **SAML Consumer URL** toohello Klembord en plak in toohello **aanmeldings-URL** textbox in **ScreenSteps domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="88437-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="88437-196">g.</span><span class="sxs-lookup"><span data-stu-id="88437-196">g.</span></span> <span data-ttu-id="88437-197">Retourneren van toohello **bewerken één aanmelding eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="88437-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="88437-198">h.</span><span class="sxs-lookup"><span data-stu-id="88437-198">h.</span></span> <span data-ttu-id="88437-199">Klik op Hallo **voor account instellen als standaardbrowser** knop toouse dit eindpunt voor alle gebruikers die zich bij ScreenSteps aanmelden.</span><span class="sxs-lookup"><span data-stu-id="88437-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="88437-200">U kunt ook klikken op Hallo **toevoegen tooSite** knop toouse dit eindpunt voor specifieke sites in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="88437-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="88437-201">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="88437-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88437-202">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="88437-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88437-203">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88437-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="88437-204">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="88437-204">Create an Azure AD test user</span></span>

<span data-ttu-id="88437-205">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="88437-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="88437-207">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88437-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88437-208">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="88437-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="88437-210">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="88437-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="88437-212">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88437-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="88437-214">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88437-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="88437-216">a.</span><span class="sxs-lookup"><span data-stu-id="88437-216">a.</span></span> <span data-ttu-id="88437-217">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88437-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88437-218">b.</span><span class="sxs-lookup"><span data-stu-id="88437-218">b.</span></span> <span data-ttu-id="88437-219">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="88437-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="88437-220">c.</span><span class="sxs-lookup"><span data-stu-id="88437-220">c.</span></span> <span data-ttu-id="88437-221">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="88437-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="88437-222">d.</span><span class="sxs-lookup"><span data-stu-id="88437-222">d.</span></span> <span data-ttu-id="88437-223">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="88437-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="88437-224">Een testgebruiker ScreenSteps maken</span><span class="sxs-lookup"><span data-stu-id="88437-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="88437-225">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in ScreenSteps maken.</span><span class="sxs-lookup"><span data-stu-id="88437-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="88437-226">Werken met [ScreenSteps Client ondersteuningsteam](https://www.screensteps.com/contact) Hallo gebruikers toevoegen in Hallo ScreenSteps platform.</span><span class="sxs-lookup"><span data-stu-id="88437-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="88437-227">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88437-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="88437-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="88437-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="88437-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooScreenSteps toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="88437-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="88437-231">**tooassign Britta Simon tooScreenSteps, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="88437-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="88437-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88437-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="88437-234">Selecteer in de lijst met de toepassingen van Hallo **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="88437-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![Hallo ScreenSteps koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="88437-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="88437-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="88437-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="88437-238">Click **Add** button.</span></span> <span data-ttu-id="88437-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88437-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="88437-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="88437-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88437-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88437-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88437-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88437-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="88437-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88437-244">Test single sign-on</span></span>

<span data-ttu-id="88437-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="88437-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88437-246">Als u op Hallo ScreenSteps-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ScreenSteps toepassing.</span><span class="sxs-lookup"><span data-stu-id="88437-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="88437-247">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88437-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88437-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="88437-248">Additional resources</span></span>

* [<span data-ttu-id="88437-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88437-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88437-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88437-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

