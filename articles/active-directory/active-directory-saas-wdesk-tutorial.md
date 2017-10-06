---
title: 'Zelfstudie: Azure Active Directory-integratie met Wdesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Wdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="1787a-103">Zelfstudie: Azure Active Directory-integratie met Wdesk</span><span class="sxs-lookup"><span data-stu-id="1787a-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="1787a-104">In deze zelfstudie leert u hoe toointegrate Wdesk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1787a-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1787a-105">Wdesk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1787a-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1787a-106">U kunt beheren in Azure AD die tooWdesk toegang heeft</span><span class="sxs-lookup"><span data-stu-id="1787a-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="1787a-107">U kunt uw gebruikers tooautomatically get aangemelde tooWdesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1787a-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1787a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1787a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1787a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="1787a-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1787a-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1787a-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1787a-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1787a-111">Prerequisites</span></span>

<span data-ttu-id="1787a-112">Azure AD-integratie met Wdesk tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1787a-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="1787a-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1787a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1787a-114">Een Wdesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1787a-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1787a-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1787a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1787a-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1787a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1787a-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1787a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1787a-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1787a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1787a-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1787a-119">Scenario description</span></span>
<span data-ttu-id="1787a-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1787a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1787a-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1787a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1787a-122">Het toevoegen van Wdesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1787a-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="1787a-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1787a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="1787a-124">Het toevoegen van Wdesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1787a-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="1787a-125">tooconfigure hello integratie van Wdesk in Azure AD, moet u tooadd Wdesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1787a-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1787a-126">**tooadd Wdesk via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1787a-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1787a-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1787a-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1787a-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1787a-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1787a-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1787a-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1787a-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1787a-134">Typ in het zoekvak Hallo **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="1787a-134">In hello search box, type **Wdesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="1787a-136">Selecteer in het deelvenster resultaten hello, **Wdesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1787a-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1787a-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1787a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1787a-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Wdesk op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1787a-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1787a-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Wdesk is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1787a-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="1787a-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Wdesk toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1787a-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="1787a-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="1787a-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="1787a-143">tooconfigure en eenmalige aanmelding Azure AD-test met Wdesk, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1787a-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1787a-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1787a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1787a-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1787a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1787a-146">**[Maken van een testgebruiker Wdesk](#creating-a-wdesk-test-user)**  -toohave een equivalent van Britta Simon in Wdesk die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1787a-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1787a-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1787a-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1787a-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1787a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1787a-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1787a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1787a-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Wdesk configureren.</span><span class="sxs-lookup"><span data-stu-id="1787a-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="1787a-151">**Azure AD tooconfigure eenmalige aanmelding met Wdesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1787a-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1787a-152">In de Azure-portal op Hallo Hallo **Wdesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1787a-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1787a-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1787a-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="1787a-156">Op Hallo **Wdesk domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** geïnitieerd modus uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1787a-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="1787a-158">a.</span><span class="sxs-lookup"><span data-stu-id="1787a-158">a.</span></span> <span data-ttu-id="1787a-159">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1787a-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="1787a-160">b.</span><span class="sxs-lookup"><span data-stu-id="1787a-160">b.</span></span> <span data-ttu-id="1787a-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1787a-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="1787a-162">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="1787a-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1787a-163">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus geïnitieerd Hallo stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1787a-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="1787a-165">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1787a-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1787a-166">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1787a-166">These values are not real.</span></span> <span data-ttu-id="1787a-167">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1787a-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1787a-168">U krijgt deze waarden van WDesk portal wanneer u eenmalige aanmelding Hallo configureert.</span><span class="sxs-lookup"><span data-stu-id="1787a-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="1787a-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1787a-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="1787a-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1787a-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1787a-173">In een ander browservenster, aanmelding tooWdesk als een beveiligingsbeheerder.</span><span class="sxs-lookup"><span data-stu-id="1787a-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="1787a-174">Klik in het Hallo linksonder, op **Admin** en kies **accountbeheerder**:</span><span class="sxs-lookup"><span data-stu-id="1787a-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="1787a-176">Navigeer te in Wdesk Admin,**beveiliging**, klikt u vervolgens **SAML** > **SAML instellingen**:</span><span class="sxs-lookup"><span data-stu-id="1787a-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="1787a-178">Onder **algemene instellingen**, Controleer Hallo **SAML eenmalige aanmelding inschakelen**:</span><span class="sxs-lookup"><span data-stu-id="1787a-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="1787a-180">Onder **Details van Service Provider**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="1787a-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="1787a-182">a.</span><span class="sxs-lookup"><span data-stu-id="1787a-182">a.</span></span> <span data-ttu-id="1787a-183">Kopiëren Hallo **aanmeldings-URL** en plak deze in **aanmeldings-Url** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1787a-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1787a-184">b.</span><span class="sxs-lookup"><span data-stu-id="1787a-184">b.</span></span> <span data-ttu-id="1787a-185">Kopiëren Hallo **metagegevens-Url** en plak deze in **id** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1787a-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="1787a-186">c.</span><span class="sxs-lookup"><span data-stu-id="1787a-186">c.</span></span> <span data-ttu-id="1787a-187">Kopiëren Hallo **Consumer url** en plak deze in **antwoord-Url** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1787a-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1787a-188">d.</span><span class="sxs-lookup"><span data-stu-id="1787a-188">d.</span></span> <span data-ttu-id="1787a-189">Klik op **opslaan** op Azure portal toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1787a-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="1787a-190">Klik op **IdP-instellingen configureren** tooopen **IdP-instellingen bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="1787a-191">Klik op **bestand kiezen** toolocate hello **Metadata.xml** opgeslagen vanuit Azure-portal-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="1787a-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="1787a-193">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1787a-193">Click **Save changes**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="1787a-195">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="1787a-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1787a-196">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="1787a-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1787a-197">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1787a-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1787a-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1787a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1787a-199">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1787a-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1787a-201">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1787a-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1787a-202">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1787a-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1787a-204">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1787a-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1787a-206">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1787a-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1787a-208">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1787a-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1787a-210">a.</span><span class="sxs-lookup"><span data-stu-id="1787a-210">a.</span></span> <span data-ttu-id="1787a-211">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1787a-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1787a-212">b.</span><span class="sxs-lookup"><span data-stu-id="1787a-212">b.</span></span> <span data-ttu-id="1787a-213">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1787a-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1787a-214">c.</span><span class="sxs-lookup"><span data-stu-id="1787a-214">c.</span></span> <span data-ttu-id="1787a-215">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1787a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1787a-216">d.</span><span class="sxs-lookup"><span data-stu-id="1787a-216">d.</span></span> <span data-ttu-id="1787a-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1787a-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="1787a-218">Een testgebruiker Wdesk maken</span><span class="sxs-lookup"><span data-stu-id="1787a-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="1787a-219">Azure AD tooenable gebruikers toolog in tooWdesk, ze in Wdesk moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="1787a-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="1787a-220">In Wdesk is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="1787a-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="1787a-221">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1787a-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1787a-222">Meld u bij tooWdesk als een beveiligingsbeheerder.</span><span class="sxs-lookup"><span data-stu-id="1787a-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="1787a-223">Navigeer te**Admin** > **accountbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="1787a-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="1787a-225">Klik op **leden** onder **mensen**.</span><span class="sxs-lookup"><span data-stu-id="1787a-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="1787a-226">Klik nu op **lid toevoegen** tooopen **lid toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="1787a-228">In **gebruiker** tekst hello gebruikersnaam van de gebruiker zoals Voer  **brittasimon@contoso.com**  en klik op **doorgaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1787a-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="1787a-230">Voer Hallo gegevens zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="1787a-230">Enter hello details as shown below:</span></span>
  
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="1787a-232">a.</span><span class="sxs-lookup"><span data-stu-id="1787a-232">a.</span></span> <span data-ttu-id="1787a-233">In **e** tekst hello e-mailadres van gebruikers zoals Voer  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1787a-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="1787a-234">b.</span><span class="sxs-lookup"><span data-stu-id="1787a-234">b.</span></span> <span data-ttu-id="1787a-235">In **voornaam** tekst hello eerste naam van gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1787a-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="1787a-236">c.</span><span class="sxs-lookup"><span data-stu-id="1787a-236">c.</span></span> <span data-ttu-id="1787a-237">In **achternaam** tekst hello laatste naam van gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1787a-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="1787a-238">Klik op **lid opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1787a-238">Click **Save Member** button.</span></span>  

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1787a-240">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1787a-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1787a-241">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWdesk toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="1787a-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1787a-243">**tooassign Britta Simon tooWdesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1787a-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1787a-244">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1787a-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1787a-246">Selecteer in de lijst met de toepassingen van Hallo **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="1787a-246">In hello applications list, select **Wdesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="1787a-248">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1787a-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1787a-250">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1787a-250">Click **Add** button.</span></span> <span data-ttu-id="1787a-251">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1787a-253">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1787a-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1787a-254">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1787a-255">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1787a-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1787a-256">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1787a-256">Testing single sign-on</span></span>

<span data-ttu-id="1787a-257">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1787a-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1787a-258">Als u op Hallo Wdesk tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Wdesk toepassing.</span><span class="sxs-lookup"><span data-stu-id="1787a-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="1787a-259">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1787a-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1787a-260">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1787a-260">Additional resources</span></span>

* [<span data-ttu-id="1787a-261">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1787a-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1787a-262">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1787a-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

