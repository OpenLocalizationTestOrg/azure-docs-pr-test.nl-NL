---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="17668-103">Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="17668-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="17668-104">In deze zelfstudie leert u hoe toointegrate werkplek door Facebook met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17668-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17668-105">Werkplek door Facebook integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="17668-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17668-106">U kunt beheren in Azure AD wie toegang tot tooWorkplace door Facebook heeft</span><span class="sxs-lookup"><span data-stu-id="17668-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="17668-107">U kunt uw gebruikers tooautomatically get aangemelde tooWorkplace door Facebook (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="17668-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17668-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="17668-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17668-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17668-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17668-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="17668-110">Prerequisites</span></span>

<span data-ttu-id="17668-111">Azure AD-integratie met werkplek door Facebook tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="17668-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="17668-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="17668-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17668-113">Een werkplek met eenmalige aanmelding Facebook abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="17668-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17668-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="17668-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17668-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="17668-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17668-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="17668-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17668-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17668-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17668-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="17668-118">Scenario description</span></span>
<span data-ttu-id="17668-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="17668-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17668-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="17668-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17668-121">Het toevoegen van werkplek door Facebook van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="17668-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="17668-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17668-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="17668-123">Het toevoegen van werkplek door Facebook van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="17668-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="17668-124">tooconfigure hello integratie van werkplek door Facebook in Azure AD, moet u tooadd werkplek door Facebook uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="17668-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17668-125">**tooadd werkplek door Facebook via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17668-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17668-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="17668-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17668-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17668-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17668-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17668-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="17668-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17668-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="17668-133">Typ in het zoekvak Hallo **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="17668-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="17668-135">Selecteer in het deelvenster resultaten hello, **werkplek door Facebook**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="17668-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17668-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17668-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17668-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met werkplek door Facebook op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="17668-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17668-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werkplek door Facebook is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17668-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="17668-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in werkplek door Facebook toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="17668-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="17668-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="17668-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="17668-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van werkplek door Facebook, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17668-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17668-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="17668-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17668-144">**[Configureren van Herauthenticatie frequentie](#configuring-reauthentication-frequency)**  -tooconfigure werkplek tooprompt voor een SAML-controle.</span><span class="sxs-lookup"><span data-stu-id="17668-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="17668-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17668-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="17668-146">**[Maken van een werkplek door Facebook testgebruiker](#creating-a-workplace-by-facebook-test-user)**  -toohave een equivalent van Britta Simon in werkplek door Facebook die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="17668-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="17668-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="17668-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="17668-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="17668-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17668-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="17668-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17668-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.</span><span class="sxs-lookup"><span data-stu-id="17668-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="17668-151">**Azure AD tooconfigure eenmalige aanmelding met werkplek door Facebook, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17668-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="17668-152">In de Azure-portal op Hallo Hallo **werkplek door Facebook** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="17668-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="17668-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="17668-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="17668-156">Op Hallo **werkplek Facebook-domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17668-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="17668-158">a.</span><span class="sxs-lookup"><span data-stu-id="17668-158">a.</span></span> <span data-ttu-id="17668-159">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="17668-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="17668-160">b.</span><span class="sxs-lookup"><span data-stu-id="17668-160">b.</span></span> <span data-ttu-id="17668-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="17668-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17668-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="17668-162">These values are not hello real.</span></span> <span data-ttu-id="17668-163">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="17668-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17668-164">Neem contact op met [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="17668-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="17668-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="17668-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="17668-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="17668-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17668-169">Op Hallo **werkplek door Facebook configuratie** sectie, klikt u op **werkplek configureren door Facebook** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="17668-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17668-170">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="17668-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="17668-172">In een ander browservenster, aanmelding tooyour werkplek door Facebook bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="17668-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="17668-173">Als onderdeel van SAML-verificatieproces hello, kan werkplek gebruikmaken van queryreeksen van up grootte in volgorde toopass parameters tooAzure AD too2.5 kB.</span><span class="sxs-lookup"><span data-stu-id="17668-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="17668-174">In Hallo **bedrijf Dashboard**, gaat u toohello **verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="17668-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="17668-175">Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="17668-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="17668-176">Invoer Hallo-waarden die zijn gekopieerd uit **werkplek door Facebook configuratie** sectie van de Azure-portal in de bijbehorende velden Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="17668-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="17668-177">In **SAML URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17668-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="17668-178">In **URL-verlener SAML textbox**, plak Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17668-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="17668-179">In **SAML afmelding omleiden** (optioneel) plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="17668-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="17668-180">Open uw **base-64 gecodeerde certificaat** in Kladblok gedownload vanuit Azure-portal Hallo inhoud van het kopiëren naar het Klembord en plak deze toothe **SAML certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="17668-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="17668-181">Mogelijk moet u tooenter Hallo doelgroep-URL de URL van de geadresseerde, en URL ACS (Assertion Consumer-Service) die worden vermeld onder Hallo **SAML-configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="17668-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="17668-182">Schuif toohello onder aan de sectie Hallo en klikt u op Hallo **Test SSO** knop.</span><span class="sxs-lookup"><span data-stu-id="17668-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="17668-183">Dit resulteert in een pop-upvenster wordt weergegeven met Azure AD-aanmeldingspagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="17668-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="17668-184">Geef uw referenties in als normale tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="17668-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="17668-185">**Voor probleemoplossing:** Controleer Hallo e-mailadres wordt geretourneerd door Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="17668-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="17668-186">Zodra het Hallo-test is voltooid, schuif toohello onder aan Hallo pagina en klik op Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="17668-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="17668-187">Alle gebruikers met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="17668-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="17668-188">**SAML afmelding omleiden (optioneel)** -</span><span class="sxs-lookup"><span data-stu-id="17668-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="17668-189">U kunt kiezen toooptionally een Url van de afmelding SAML te configureren die de gebruikte toopoint op de pagina voor Azure AD-afmelding kan zijn.</span><span class="sxs-lookup"><span data-stu-id="17668-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="17668-190">Als deze instelling is ingeschakeld en geconfigureerd, langer Hallo gebruiker niet gerichte toohello werkplek afmelding pagina.</span><span class="sxs-lookup"><span data-stu-id="17668-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="17668-191">Hallo-gebruiker worden in plaats daarvan omgeleide toohello-url die is toegevoegd in Hallo SAML afmelding omleiden instelling.</span><span class="sxs-lookup"><span data-stu-id="17668-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="17668-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="17668-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17668-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="17668-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17668-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17668-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="17668-195">Herauthenticatie frequentie configureren</span><span class="sxs-lookup"><span data-stu-id="17668-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="17668-196">U kunt configureren werkplek tooprompt voor een SAML-controle elke dag drie dagen, week, twee weken, maanden of nooit.</span><span class="sxs-lookup"><span data-stu-id="17668-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="17668-197">Hallo minimale waarde voor Hallo SAML-controle voor mobiele toepassingen is ingesteld tooone week.</span><span class="sxs-lookup"><span data-stu-id="17668-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="17668-198">U kunt ook een SAML opnieuw instellen voor alle gebruikers met behulp van de knop Hallo afdwingen: vereisen SAML-verificatie voor alle gebruikers nu.</span><span class="sxs-lookup"><span data-stu-id="17668-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17668-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="17668-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="17668-200">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="17668-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="17668-202">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17668-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17668-203">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="17668-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17668-205">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="17668-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17668-207">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="17668-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17668-209">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="17668-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17668-211">a.</span><span class="sxs-lookup"><span data-stu-id="17668-211">a.</span></span> <span data-ttu-id="17668-212">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17668-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17668-213">b.</span><span class="sxs-lookup"><span data-stu-id="17668-213">b.</span></span> <span data-ttu-id="17668-214">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17668-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17668-215">c.</span><span class="sxs-lookup"><span data-stu-id="17668-215">c.</span></span> <span data-ttu-id="17668-216">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="17668-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17668-217">d.</span><span class="sxs-lookup"><span data-stu-id="17668-217">d.</span></span> <span data-ttu-id="17668-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="17668-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="17668-219">Maken van een werkplek door Facebook testgebruiker</span><span class="sxs-lookup"><span data-stu-id="17668-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="17668-220">In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook.</span><span class="sxs-lookup"><span data-stu-id="17668-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="17668-221">Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="17668-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="17668-222">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="17668-222">There is no action for you in this section.</span></span> <span data-ttu-id="17668-223">Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u tooaccess werkplek probeert met Facebook.</span><span class="sxs-lookup"><span data-stu-id="17668-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="17668-224">Als u een gebruiker handmatig, neem contact op met toocreate moet [werkplek door ondersteuningsteam Facebook-Client](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="17668-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17668-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17668-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17668-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooWorkplace met Facebook.</span><span class="sxs-lookup"><span data-stu-id="17668-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="17668-228">**tooassign Britta Simon tooWorkplace door Facebook, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="17668-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="17668-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="17668-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="17668-231">Selecteer in de lijst met de toepassingen van Hallo **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="17668-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="17668-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="17668-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="17668-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="17668-235">Click **Add** button.</span></span> <span data-ttu-id="17668-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17668-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="17668-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="17668-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17668-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17668-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17668-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="17668-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17668-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="17668-241">Testing single sign-on</span></span>

<span data-ttu-id="17668-242">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="17668-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="17668-243">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17668-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="17668-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="17668-244">Additional resources</span></span>

* [<span data-ttu-id="17668-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17668-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17668-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17668-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="17668-247">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="17668-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

