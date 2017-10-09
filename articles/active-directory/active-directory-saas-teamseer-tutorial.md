---
title: 'Zelfstudie: Azure Active Directory-integratie met TeamSeer | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="7746f-103">Zelfstudie: Azure Active Directory-integratie met TeamSeer</span><span class="sxs-lookup"><span data-stu-id="7746f-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="7746f-104">In deze zelfstudie leert u hoe toointegrate TeamSeer met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7746f-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7746f-105">TeamSeer integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7746f-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7746f-106">U kunt beheren in Azure AD die tooTeamSeer toegang heeft</span><span class="sxs-lookup"><span data-stu-id="7746f-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="7746f-107">U kunt uw gebruikers tooautomatically get aangemelde tooTeamSeer (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7746f-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7746f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7746f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7746f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7746f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7746f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7746f-110">Prerequisites</span></span>

<span data-ttu-id="7746f-111">Azure AD-integratie met TeamSeer tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7746f-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="7746f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7746f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7746f-113">Een TeamSeer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7746f-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7746f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7746f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7746f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7746f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7746f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7746f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7746f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7746f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7746f-118">Scenario description</span></span>
<span data-ttu-id="7746f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7746f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7746f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7746f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7746f-121">Het toevoegen van TeamSeer van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7746f-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="7746f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7746f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="7746f-123">Het toevoegen van TeamSeer van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7746f-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="7746f-124">tooconfigure hello integratie van TeamSeer in tooAzure AD, moet u tooadd TeamSeer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7746f-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7746f-125">**tooadd TeamSeer via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7746f-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7746f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7746f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7746f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7746f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7746f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7746f-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7746f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7746f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7746f-133">Typ in het zoekvak Hallo **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="7746f-133">In hello search box, type **TeamSeer**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="7746f-135">Selecteer in het deelvenster resultaten hello, **TeamSeer**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7746f-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7746f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7746f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7746f-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TeamSeer op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7746f-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7746f-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TeamSeer is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7746f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="7746f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TeamSeer toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7746f-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="7746f-141">Wijs in TeamSeer, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7746f-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7746f-142">tooconfigure en eenmalige aanmelding Azure AD-test met TeamSeer, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7746f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7746f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7746f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7746f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7746f-145">**[Maken van een testgebruiker TeamSeer](#creating-a-teamseer-test-user)**  -toohave een equivalent van Britta Simon in TeamSeer die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7746f-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7746f-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7746f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7746f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7746f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7746f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7746f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7746f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TeamSeer configureren.</span><span class="sxs-lookup"><span data-stu-id="7746f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="7746f-150">**Azure AD tooconfigure eenmalige aanmelding met TeamSeer, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7746f-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="7746f-151">In de Azure-portal op Hallo Hallo **TeamSeer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7746f-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7746f-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7746f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="7746f-155">Op Hallo **TeamSeer domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="7746f-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="7746f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7746f-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="7746f-158">hello value is not real.</span></span> <span data-ttu-id="7746f-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="7746f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7746f-160">Neem contact op met [TeamSeer Client ondersteuningsteam](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="7746f-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7746f-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7746f-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="7746f-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7746f-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7746f-165">Op Hallo **TeamSeer configuratie** sectie, klikt u op **configureren TeamSeer** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7746f-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7746f-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7746f-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="7746f-168">In een ander browservenster, meld u aan tooyour TeamSeer bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="7746f-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="7746f-169">Ga te**HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="7746f-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="7746f-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR-beheerder")</span><span class="sxs-lookup"><span data-stu-id="7746f-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="7746f-171">Klik op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="7746f-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="7746f-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="7746f-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="7746f-173">Klik op **SAML provider details instellen**.</span><span class="sxs-lookup"><span data-stu-id="7746f-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="7746f-174">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="7746f-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="7746f-175">Voer in Hallo gedeelte details van SAML-provider, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7746f-176">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="7746f-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="7746f-177">a.</span><span class="sxs-lookup"><span data-stu-id="7746f-177">a.</span></span> <span data-ttu-id="7746f-178">Plakken Hallo **Single Sign-On Service-URL** waarde in toohello **URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="7746f-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="7746f-179">b.</span><span class="sxs-lookup"><span data-stu-id="7746f-179">b.</span></span> <span data-ttu-id="7746f-180">Open uw base-64 gecodeerde certificaat in Kladblok, kopie Hallo inhoud ervan in tooyour Klembord en plak deze toohello **IdP openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="7746f-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="7746f-181">toocomplete hello SAML-configuratie van provider, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="7746f-182">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="7746f-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="7746f-183">a.</span><span class="sxs-lookup"><span data-stu-id="7746f-183">a.</span></span> <span data-ttu-id="7746f-184">In Hallo **e-mailadressen testen**, typ de e-mailadres Hallo test van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7746f-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="7746f-185">b.</span><span class="sxs-lookup"><span data-stu-id="7746f-185">b.</span></span> <span data-ttu-id="7746f-186">In Hallo **verlener** textbox type Hallo URL-verlener van Hallo-provider.</span><span class="sxs-lookup"><span data-stu-id="7746f-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="7746f-187">c.</span><span class="sxs-lookup"><span data-stu-id="7746f-187">c.</span></span> <span data-ttu-id="7746f-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7746f-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7746f-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7746f-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7746f-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7746f-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7746f-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7746f-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7746f-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7746f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7746f-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7746f-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7746f-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7746f-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7746f-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7746f-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7746f-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7746f-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7746f-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7746f-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7746f-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7746f-204">a.</span><span class="sxs-lookup"><span data-stu-id="7746f-204">a.</span></span> <span data-ttu-id="7746f-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7746f-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7746f-206">b.</span><span class="sxs-lookup"><span data-stu-id="7746f-206">b.</span></span> <span data-ttu-id="7746f-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7746f-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7746f-208">c.</span><span class="sxs-lookup"><span data-stu-id="7746f-208">c.</span></span> <span data-ttu-id="7746f-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7746f-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7746f-210">d.</span><span class="sxs-lookup"><span data-stu-id="7746f-210">d.</span></span> <span data-ttu-id="7746f-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7746f-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="7746f-212">Een testgebruiker TeamSeer maken</span><span class="sxs-lookup"><span data-stu-id="7746f-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="7746f-213">Azure AD tooenable gebruikers toolog in tooTeamSeer, ze in tooShiftPlanning moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="7746f-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="7746f-214">In geval van TeamSeer Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="7746f-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="7746f-215">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7746f-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7746f-216">Meld u bij tooyour **TeamSeer** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7746f-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="7746f-217">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="7746f-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR-beheerder")</span><span class="sxs-lookup"><span data-stu-id="7746f-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="7746f-219">a.</span><span class="sxs-lookup"><span data-stu-id="7746f-219">a.</span></span> <span data-ttu-id="7746f-220">Ga te**HR Admin \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7746f-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="7746f-221">b.</span><span class="sxs-lookup"><span data-stu-id="7746f-221">b.</span></span> <span data-ttu-id="7746f-222">Klik op **uitvoeren van de wizard nieuwe gebruiker Hallo**.</span><span class="sxs-lookup"><span data-stu-id="7746f-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="7746f-223">In Hallo **Gebruikersdetails** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7746f-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7746f-224">![Details van gebruiker](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Gebruikersdetails")</span><span class="sxs-lookup"><span data-stu-id="7746f-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="7746f-225">a.</span><span class="sxs-lookup"><span data-stu-id="7746f-225">a.</span></span> <span data-ttu-id="7746f-226">Type Hallo **voornaam**, **achternaam**, **gebruikersnaam (e-mailadres)** van een geldige AAD-account dat u wilt dat tooprovision in toohello gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="7746f-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="7746f-227">b.</span><span class="sxs-lookup"><span data-stu-id="7746f-227">b.</span></span> <span data-ttu-id="7746f-228">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7746f-228">Click **Next**.</span></span>

4. <span data-ttu-id="7746f-229">Volg Hallo op het scherm instructies voor het toevoegen van een nieuwe gebruiker en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7746f-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="7746f-230">U kunt andere TeamSeer gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TeamSeer tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7746f-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7746f-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7746f-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7746f-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTeamSeer toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7746f-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7746f-234">**tooassign Britta Simon tooTeamSeer, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7746f-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="7746f-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7746f-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7746f-237">Selecteer in de lijst met de toepassingen van Hallo **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="7746f-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="7746f-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7746f-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7746f-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7746f-241">Click **Add** button.</span></span> <span data-ttu-id="7746f-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7746f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7746f-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7746f-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7746f-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7746f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7746f-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7746f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7746f-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7746f-247">Testing single sign-on</span></span>

<span data-ttu-id="7746f-248">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="7746f-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="7746f-249">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7746f-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7746f-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7746f-250">Additional resources</span></span>

* [<span data-ttu-id="7746f-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7746f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7746f-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7746f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

