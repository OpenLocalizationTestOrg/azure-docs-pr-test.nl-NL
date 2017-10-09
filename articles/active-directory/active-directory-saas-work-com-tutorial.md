---
title: 'Zelfstudie: Azure Active Directory-integratie met Work.com | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="4952b-103">Zelfstudie: Azure Active Directory-integratie met Work.com</span><span class="sxs-lookup"><span data-stu-id="4952b-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="4952b-104">In deze zelfstudie leert u hoe toointegrate Work.com met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4952b-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4952b-105">Work.com integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4952b-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4952b-106">U kunt beheren in Azure AD die tooWork.com toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4952b-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="4952b-107">U kunt uw gebruikers tooautomatically get aangemelde tooWork.com (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4952b-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4952b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4952b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4952b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4952b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4952b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4952b-110">Prerequisites</span></span>

<span data-ttu-id="4952b-111">Azure AD-integratie met Work.com tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4952b-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="4952b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4952b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4952b-113">Een Work.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4952b-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4952b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4952b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4952b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4952b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4952b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4952b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4952b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4952b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4952b-118">Scenario description</span></span>
<span data-ttu-id="4952b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4952b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4952b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4952b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4952b-121">Work.com van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4952b-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="4952b-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="4952b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="4952b-123">Work.com van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4952b-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="4952b-124">tooconfigure hello integratie van Work.com in Azure AD, moet u tooadd Work.com uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4952b-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4952b-125">**tooadd Work.com via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4952b-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4952b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4952b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4952b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4952b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4952b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4952b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4952b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4952b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4952b-133">Typ in het zoekvak hello, **Work.com**, selecteer **Work.com** Klik vanuit het deelvenster resultaten **toevoegen** knop tooadd Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="4952b-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Uit de galerie toevoegen](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4952b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="4952b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4952b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Work.com op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4952b-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4952b-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Work.com is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4952b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="4952b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Work.com toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4952b-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="4952b-139">Wijs in Work.com, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4952b-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4952b-140">tooconfigure en eenmalige aanmelding Azure AD-test met Work.com, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4952b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4952b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4952b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4952b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4952b-143">**[Maak een testgebruiker Work.com](#create-a-workcom-test-user)**  -toohave een equivalent van Britta Simon in Work.com die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4952b-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4952b-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4952b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4952b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4952b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4952b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4952b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4952b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Work.com configureren.</span><span class="sxs-lookup"><span data-stu-id="4952b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="4952b-148">tooconfigure eenmalige aanmelding, moet u een aangepaste domeinnaam van Work.com toosetup nog.</span><span class="sxs-lookup"><span data-stu-id="4952b-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="4952b-149">U moet ten minste een domein toodefine naam, uw domeinnaam testen en implementeren van de hele organisatie tooyour.</span><span class="sxs-lookup"><span data-stu-id="4952b-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="4952b-150">**Azure AD tooconfigure eenmalige aanmelding met Work.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4952b-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4952b-151">In de Azure-portal op Hallo Hallo **Work.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4952b-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4952b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4952b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="4952b-155">Op Hallo **Work.com domein en de URL's** sectie, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4952b-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Sectie Work.com domein en URL 's](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="4952b-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4952b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4952b-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="4952b-158">This value is not real.</span></span> <span data-ttu-id="4952b-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="4952b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4952b-160">Neem contact op met [Work.com Client ondersteuningsteam](https://help.salesforce.com/articleView?id=000159855&type=3) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="4952b-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="4952b-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4952b-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="4952b-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4952b-163">Click **Save** button.</span></span>

    ![De knop Opslaan](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4952b-165">Op Hallo **Work.com configuratie** sectie, klikt u op **configureren Work.com** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4952b-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4952b-166">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4952b-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![De configuratiesectie Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="4952b-168">Aanmelden tooyour Work.com tenant als administrator.</span><span class="sxs-lookup"><span data-stu-id="4952b-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="4952b-169">Ga te**Setup**.</span><span class="sxs-lookup"><span data-stu-id="4952b-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="4952b-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="4952b-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="4952b-171">Op Hallo navigatiedeelvenster links in Hallo **beheren** sectie, klikt u op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello  **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="4952b-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="4952b-172">![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="4952b-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="4952b-173">tooverify die uw domein is correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd tooUsers**' en bekijk uw '**mijn domeininstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="4952b-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="4952b-174">![Domein geïmplementeerd tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser domein geïmplementeerd")</span><span class="sxs-lookup"><span data-stu-id="4952b-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="4952b-175">Meld u bij tooyour Work.com tenant.</span><span class="sxs-lookup"><span data-stu-id="4952b-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="4952b-176">Ga te**Setup**.</span><span class="sxs-lookup"><span data-stu-id="4952b-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="4952b-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="4952b-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="4952b-178">Vouw Hallo **beveiligingsmechanismen** menu en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4952b-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="4952b-179">![Eenmalige aanmelding instellingen](./media/active-directory-saas-work-com-tutorial/ic794113.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="4952b-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="4952b-180">Op Hallo **instellingen voor eenmalige aanmelding** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="4952b-181">![SAML ingeschakeld](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML ingeschakeld")</span><span class="sxs-lookup"><span data-stu-id="4952b-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="4952b-182">a.</span><span class="sxs-lookup"><span data-stu-id="4952b-182">a.</span></span> <span data-ttu-id="4952b-183">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="4952b-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="4952b-184">b.</span><span class="sxs-lookup"><span data-stu-id="4952b-184">b.</span></span> <span data-ttu-id="4952b-185">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="4952b-185">Click **New**.</span></span>

15. <span data-ttu-id="4952b-186">In Hallo **SAML Single Sign-On-instellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="4952b-187">![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On-instelling")</span><span class="sxs-lookup"><span data-stu-id="4952b-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="4952b-188">a.</span><span class="sxs-lookup"><span data-stu-id="4952b-188">a.</span></span> <span data-ttu-id="4952b-189">In Hallo **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="4952b-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="4952b-190">Om een waarde voor **naam** Hallo automatisch invullen **API-naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="4952b-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="4952b-191">b.</span><span class="sxs-lookup"><span data-stu-id="4952b-191">b.</span></span> <span data-ttu-id="4952b-192">In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4952b-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4952b-193">c.</span><span class="sxs-lookup"><span data-stu-id="4952b-193">c.</span></span> <span data-ttu-id="4952b-194">certificaat van de tooupload Hallo gedownload vanuit Azure-portal klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="4952b-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="4952b-195">d.</span><span class="sxs-lookup"><span data-stu-id="4952b-195">d.</span></span> <span data-ttu-id="4952b-196">In Hallo **entiteit-Id** textbox type `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="4952b-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="4952b-197">e.</span><span class="sxs-lookup"><span data-stu-id="4952b-197">e.</span></span> <span data-ttu-id="4952b-198">Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.</span><span class="sxs-lookup"><span data-stu-id="4952b-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="4952b-199">f.</span><span class="sxs-lookup"><span data-stu-id="4952b-199">f.</span></span> <span data-ttu-id="4952b-200">Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentfier element van Hallo onderwerp instructie**.</span><span class="sxs-lookup"><span data-stu-id="4952b-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="4952b-201">g.</span><span class="sxs-lookup"><span data-stu-id="4952b-201">g.</span></span> <span data-ttu-id="4952b-202">In **identiteit Provider aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4952b-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4952b-203">h.</span><span class="sxs-lookup"><span data-stu-id="4952b-203">h.</span></span> <span data-ttu-id="4952b-204">In **identiteit Provider afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4952b-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4952b-205">ik.</span><span class="sxs-lookup"><span data-stu-id="4952b-205">i.</span></span> <span data-ttu-id="4952b-206">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="4952b-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="4952b-207">j.</span><span class="sxs-lookup"><span data-stu-id="4952b-207">j.</span></span> <span data-ttu-id="4952b-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4952b-208">Click **Save**.</span></span>

16. <span data-ttu-id="4952b-209">Klik in de klassieke portal van Work.com op Hallo navigatiedeelvenster links op **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein** tooopen hello **mijn domein**pagina.</span><span class="sxs-lookup"><span data-stu-id="4952b-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="4952b-210">![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic794115.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="4952b-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="4952b-211">Op Hallo **mijn domein** pagina in Hallo **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="4952b-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="4952b-212">![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic767826.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="4952b-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="4952b-213">Op Hallo **aanmelding pagina huisstijl** pagina in Hallo **verificatieservice** sectie, Hallo-naam van uw **SAML SSO instellingen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4952b-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="4952b-214">Selecteer deze en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4952b-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="4952b-215">![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic784366.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="4952b-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="4952b-216">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4952b-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4952b-217">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4952b-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4952b-218">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4952b-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4952b-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4952b-219">Create an Azure AD test user</span></span>
<span data-ttu-id="4952b-220">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4952b-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4952b-222">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4952b-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4952b-223">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4952b-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4952b-225">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4952b-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4952b-227">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4952b-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Toevoegen](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4952b-229">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4952b-231">a.</span><span class="sxs-lookup"><span data-stu-id="4952b-231">a.</span></span> <span data-ttu-id="4952b-232">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4952b-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4952b-233">b.</span><span class="sxs-lookup"><span data-stu-id="4952b-233">b.</span></span> <span data-ttu-id="4952b-234">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4952b-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4952b-235">c.</span><span class="sxs-lookup"><span data-stu-id="4952b-235">c.</span></span> <span data-ttu-id="4952b-236">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4952b-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4952b-237">d.</span><span class="sxs-lookup"><span data-stu-id="4952b-237">d.</span></span> <span data-ttu-id="4952b-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4952b-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="4952b-239">Een testgebruiker Work.com maken</span><span class="sxs-lookup"><span data-stu-id="4952b-239">Create a Work.com test user</span></span>
<span data-ttu-id="4952b-240">Voor Azure Active Directory gebruikers toobe kunnen toosign in, moeten ze ingerichte tooWork.com zijn. In geval van Work.com Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="4952b-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="4952b-241">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4952b-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="4952b-242">Meld u op tooyour Work.com bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="4952b-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="4952b-243">Ga te**Setup**.</span><span class="sxs-lookup"><span data-stu-id="4952b-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="4952b-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="4952b-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="4952b-245">Ga te**gebruikers beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4952b-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="4952b-246">![Gebruikers beheren](./media/active-directory-saas-work-com-tutorial/IC784369.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="4952b-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="4952b-247">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="4952b-247">Click **New User**.</span></span>
   
    <span data-ttu-id="4952b-248">![Alle gebruikers](./media/active-directory-saas-work-com-tutorial/IC794117.png "alle gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4952b-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="4952b-249">In Hallo sectie gebruiker bewerken, uitvoeren Hallo stappen hebt uitgevoerd, in de kenmerken van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo:</span><span class="sxs-lookup"><span data-stu-id="4952b-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="4952b-250">![Gebruiker bewerken](./media/active-directory-saas-work-com-tutorial/ic794118.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="4952b-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="4952b-251">a.</span><span class="sxs-lookup"><span data-stu-id="4952b-251">a.</span></span> <span data-ttu-id="4952b-252">In Hallo **voornaam** textbox type Hallo **voornaam** van Hallo gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4952b-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="4952b-253">b.</span><span class="sxs-lookup"><span data-stu-id="4952b-253">b.</span></span> <span data-ttu-id="4952b-254">In Hallo **achternaam** textbox type Hallo **achternaam** van Hallo gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4952b-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="4952b-255">c.</span><span class="sxs-lookup"><span data-stu-id="4952b-255">c.</span></span> <span data-ttu-id="4952b-256">In Hallo **Alias** textbox type Hallo **naam** van Hallo gebruiker **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="4952b-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="4952b-257">d.</span><span class="sxs-lookup"><span data-stu-id="4952b-257">d.</span></span> <span data-ttu-id="4952b-258">In Hallo **e** textbox type Hallo **e-mailadres** van gebruiker  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4952b-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="4952b-259">e.</span><span class="sxs-lookup"><span data-stu-id="4952b-259">e.</span></span> <span data-ttu-id="4952b-260">In Hallo **gebruikersnaam** textbox, typ een naam van gebruiker, zoals  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4952b-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="4952b-261">f.</span><span class="sxs-lookup"><span data-stu-id="4952b-261">f.</span></span> <span data-ttu-id="4952b-262">In Hallo **bijnaam** textbox, typ een **bijnaam** van gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4952b-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="4952b-263">g.</span><span class="sxs-lookup"><span data-stu-id="4952b-263">g.</span></span> <span data-ttu-id="4952b-264">Selecteer **rol**, **gebruikerslicentie**, en **profiel**.</span><span class="sxs-lookup"><span data-stu-id="4952b-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="4952b-265">h.</span><span class="sxs-lookup"><span data-stu-id="4952b-265">h.</span></span> <span data-ttu-id="4952b-266">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4952b-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="4952b-267">Hello Azure AD-accounthouder krijgt een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="4952b-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4952b-268">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4952b-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4952b-269">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooWork.com toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="4952b-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4952b-271">**tooassign Britta Simon tooWork.com, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4952b-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4952b-272">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4952b-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4952b-274">Selecteer in de lijst met de toepassingen van Hallo **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="4952b-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com in de lijst van app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="4952b-276">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4952b-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4952b-278">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4952b-278">Click **Add** button.</span></span> <span data-ttu-id="4952b-279">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4952b-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4952b-281">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4952b-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4952b-282">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4952b-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4952b-283">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4952b-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4952b-284">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4952b-284">Test single sign-on</span></span>

<span data-ttu-id="4952b-285">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4952b-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4952b-286">Als u op Hallo Work.com tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Work.com toepassing.</span><span class="sxs-lookup"><span data-stu-id="4952b-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="4952b-287">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4952b-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4952b-288">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4952b-288">Additional resources</span></span>

* [<span data-ttu-id="4952b-289">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4952b-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4952b-290">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4952b-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

