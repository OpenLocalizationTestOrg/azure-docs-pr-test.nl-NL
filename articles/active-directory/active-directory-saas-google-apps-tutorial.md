---
title: 'Zelfstudie: Azure Active Directory-integratie met Google Apps in Azure | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Google Apps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="258fe-103">Zelfstudie: Azure Active Directory-integratie met Google Apps</span><span class="sxs-lookup"><span data-stu-id="258fe-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="258fe-104">In deze zelfstudie leert u hoe toointegrate Google Apps met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="258fe-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="258fe-105">Google Apps integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="258fe-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="258fe-106">U kunt beheren in Azure AD wie toegang tot tooGoogle Apps heeft</span><span class="sxs-lookup"><span data-stu-id="258fe-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="258fe-107">U kunt uw gebruikers tooautomatically get aangemelde tooGoogle Apps (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="258fe-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="258fe-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="258fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="258fe-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="258fe-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="258fe-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="258fe-110">Prerequisites</span></span>

<span data-ttu-id="258fe-111">tooconfigure Azure AD-integratie met Google Apps, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="258fe-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="258fe-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="258fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="258fe-113">Een Google Apps eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="258fe-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="258fe-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="258fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="258fe-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="258fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="258fe-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="258fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="258fe-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="258fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="258fe-118">Zelfstudievideo</span><span class="sxs-lookup"><span data-stu-id="258fe-118">Video tutorial</span></span>
<span data-ttu-id="258fe-119">Hoe tooEnable Single Sign-On tooGoogle Apps 2 minuten:</span><span class="sxs-lookup"><span data-stu-id="258fe-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="258fe-120">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="258fe-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="258fe-121">**V: Chromebooks en andere apparaten Chrome compatibel zijn met eenmalige aanmelding Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="258fe-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="258fe-122">A: Ja, zijn de gebruikers kunnen toosign in hun Chromebook apparaten met hun Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="258fe-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="258fe-123">Zie dit [Google Apps ondersteunen artikel](https://support.google.com/chrome/a/answer/6060880) voor informatie over gebruikers mogelijk om wordt gevraagd referenties twee keer.</span><span class="sxs-lookup"><span data-stu-id="258fe-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="258fe-124">**V: als ik eenmalige aanmelding, worden gebruikers kunnen toouse hun toosign Azure AD-referenties in een Google-product, zoals Google leslokaal, GMail, Google Drive, YouTube, enzovoort worden?**</span><span class="sxs-lookup"><span data-stu-id="258fe-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="258fe-125">A: Ja, afhankelijk van [welke Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) u tooenable kiezen of uitschakelt voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="258fe-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="258fe-126">**V: kan ik eenmalige aanmelding voor alleen een subset van mijn gebruikers Google Apps inschakelen?**</span><span class="sxs-lookup"><span data-stu-id="258fe-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="258fe-127">A: niet onmiddellijk bij eenmalige aanmelding inschakelen, moet alle uw Google Apps gebruikers tooauthenticate met hun Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="258fe-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="258fe-128">Omdat Google Apps biedt geen ondersteuning voor meerdere id-providers, Hallo id-provider voor uw Google Apps-omgeving kan Azure AD zijn of Google-- maar niet beide op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="258fe-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="258fe-129">**V: als een gebruiker is aangemeld via Windows, worden dat ze automatisch tooGoogle Apps zonder een wachtwoord wordt gevraagd een verificatie?**</span><span class="sxs-lookup"><span data-stu-id="258fe-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="258fe-130">A: Er zijn twee opties voor het inschakelen van dit scenario.</span><span class="sxs-lookup"><span data-stu-id="258fe-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="258fe-131">Eerst gebruikers kunnen aanmelden bij Windows 10-apparaten via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="258fe-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="258fe-132">U kunt ook gebruikers kunnen aanmelden bij Windows-apparaten die lid zijn van een domein tooan on-premises Active Directory die is ingeschakeld voor eenmalige aanmelding tooAzure AD via een [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) implementatie.</span><span class="sxs-lookup"><span data-stu-id="258fe-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="258fe-133">In beide gevallen moet u tooperform Hallo stappen in de volgende zelfstudie tooenable eenmalige aanmelding tussen Azure AD Hallo en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="258fe-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="258fe-134">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="258fe-134">Scenario description</span></span>
<span data-ttu-id="258fe-135">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="258fe-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="258fe-136">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="258fe-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="258fe-137">Google Apps uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="258fe-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="258fe-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="258fe-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="258fe-139">Google Apps uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="258fe-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="258fe-140">tooconfigure hello integratie van Google Apps in Azure AD, moet u tooadd Google Apps uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="258fe-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="258fe-141">**tooadd Google Apps uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="258fe-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="258fe-142">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="258fe-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="258fe-144">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="258fe-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="258fe-145">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="258fe-145">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="258fe-147">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="258fe-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="258fe-149">Typ in het zoekvak Hallo **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="258fe-149">In hello search box, type **Google Apps**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="258fe-151">Selecteer in het deelvenster resultaten hello, **Google Apps**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="258fe-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="258fe-153">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="258fe-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="258fe-154">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Google Apps op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="258fe-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="258fe-155">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Google Apps is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="258fe-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="258fe-156">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Google Apps toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="258fe-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="258fe-157">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="258fe-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="258fe-158">tooconfigure en eenmalige aanmelding Azure AD-test met Google Apps, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="258fe-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="258fe-159">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="258fe-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="258fe-160">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="258fe-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="258fe-161">**[Maken van een testgebruiker Google Apps](#creating-a-google-apps-test-user)**  -toohave een equivalent van Britta Simon in Google Apps die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="258fe-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="258fe-162">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="258fe-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="258fe-163">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="258fe-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="258fe-164">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="258fe-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="258fe-165">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Google Apps configureren.</span><span class="sxs-lookup"><span data-stu-id="258fe-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="258fe-166">**Voer tooconfigure Azure AD eenmalige aanmelding met Google Apps Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="258fe-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="258fe-167">In de Azure-portal op Hallo Hallo **Google Apps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="258fe-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="258fe-169">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="258fe-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="258fe-171">Op Hallo **Google Apps Domain en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="258fe-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="258fe-173">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="258fe-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="258fe-174">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="258fe-174">This value is not real.</span></span> <span data-ttu-id="258fe-175">Hallo-waarde met de Hallo werkelijke aanmeldings-URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="258fe-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="258fe-176">Neem contact op met de Hallo [Google ondersteuningsteam](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="258fe-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="258fe-177">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla Hallo certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="258fe-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="258fe-179">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="258fe-179">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="258fe-181">Op Hallo **Google Apps-configuratie** sectie, klikt u op **Google Apps configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="258fe-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="258fe-182">Kopiëren Hallo **Sign-Out-URL, SAML Single Sign-On Service-URL en wijzigen wachtwoord URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="258fe-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="258fe-184">Een nieuw tabblad openen in uw browser en meld u aan bij Hallo [Google Apps-beheerconsole](http://admin.google.com/) met uw administrator-account.</span><span class="sxs-lookup"><span data-stu-id="258fe-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="258fe-185">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="258fe-185">Click **Security**.</span></span> <span data-ttu-id="258fe-186">Als er geen Hallo-koppeling, kan het verborgen onder Hallo **meer besturingselementen** menu Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="258fe-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Klik op 'Security' (Beveiliging).][10]

9. <span data-ttu-id="258fe-188">Op Hallo **beveiliging** pagina, klikt u op **instellen van eenmalige aanmelding (SSO).**</span><span class="sxs-lookup"><span data-stu-id="258fe-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Klik op eenmalige aanmelding.][11]

10. <span data-ttu-id="258fe-190">Voer Hallo configuratiewijzigingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="258fe-190">Perform hello following configuration changes:</span></span>
   
    ![Eenmalige aanmelding configureren][12]
   
    <span data-ttu-id="258fe-192">a.</span><span class="sxs-lookup"><span data-stu-id="258fe-192">a.</span></span> <span data-ttu-id="258fe-193">Selecteer **Setup-SSO met derden identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="258fe-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="258fe-194">b.</span><span class="sxs-lookup"><span data-stu-id="258fe-194">b.</span></span> <span data-ttu-id="258fe-195">In de **aanmelden pagina-URL** veld in Google Apps, plak Hallo-waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="258fe-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="258fe-196">c.</span><span class="sxs-lookup"><span data-stu-id="258fe-196">c.</span></span> <span data-ttu-id="258fe-197">In Hallo **afmelden pagina-URL** veld in Google Apps, plak Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="258fe-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="258fe-198">d.</span><span class="sxs-lookup"><span data-stu-id="258fe-198">d.</span></span> <span data-ttu-id="258fe-199">In Hallo **URL voor wachtwoord wijzigen** veld in Google Apps, plak Hallo-waarde van **wijzigen wachtwoord URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="258fe-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="258fe-200">e.</span><span class="sxs-lookup"><span data-stu-id="258fe-200">e.</span></span> <span data-ttu-id="258fe-201">In Google Apps voor Hallo **verificatiecertificaat**, uploaden Hallo certificaat dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="258fe-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="258fe-202">f.</span><span class="sxs-lookup"><span data-stu-id="258fe-202">f.</span></span> <span data-ttu-id="258fe-203">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="258fe-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="258fe-204">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="258fe-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="258fe-205">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="258fe-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="258fe-206">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="258fe-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="258fe-207">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="258fe-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="258fe-208">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="258fe-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="258fe-210">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="258fe-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="258fe-211">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="258fe-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="258fe-213">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="258fe-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="258fe-215">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="258fe-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="258fe-217">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="258fe-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="258fe-219">a.</span><span class="sxs-lookup"><span data-stu-id="258fe-219">a.</span></span> <span data-ttu-id="258fe-220">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="258fe-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="258fe-221">b.</span><span class="sxs-lookup"><span data-stu-id="258fe-221">b.</span></span> <span data-ttu-id="258fe-222">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="258fe-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="258fe-223">c.</span><span class="sxs-lookup"><span data-stu-id="258fe-223">c.</span></span> <span data-ttu-id="258fe-224">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="258fe-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="258fe-225">d.</span><span class="sxs-lookup"><span data-stu-id="258fe-225">d.</span></span> <span data-ttu-id="258fe-226">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="258fe-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="258fe-227">Een testgebruiker Google Apps maken</span><span class="sxs-lookup"><span data-stu-id="258fe-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="258fe-228">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Google Apps Software van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="258fe-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="258fe-229">Google Apps ondersteunt automatische inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="258fe-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="258fe-230">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="258fe-230">There is no action for you in this section.</span></span> <span data-ttu-id="258fe-231">Als een gebruiker in Google Apps Software nog niet bestaat, wordt een nieuwe gemaakt wanneer u tooaccess Google Apps Software probeert.</span><span class="sxs-lookup"><span data-stu-id="258fe-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="258fe-232">Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [Google ondersteuningsteam](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="258fe-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="258fe-233">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="258fe-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="258fe-234">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooGoogle Apps.</span><span class="sxs-lookup"><span data-stu-id="258fe-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="258fe-236">**tooassign Britta Simon tooGoogle Apps, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="258fe-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="258fe-237">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="258fe-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="258fe-239">Selecteer in de lijst met de toepassingen van Hallo **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="258fe-239">In hello applications list, select **Google Apps**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="258fe-241">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="258fe-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="258fe-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="258fe-243">Click **Add** button.</span></span> <span data-ttu-id="258fe-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="258fe-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="258fe-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="258fe-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="258fe-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="258fe-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="258fe-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="258fe-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="258fe-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="258fe-249">Testing single sign-on</span></span>

<span data-ttu-id="258fe-250">In deze sectie tootest uw eenmalige aanmelding-instellingen, open Toegangsvenster op Hallo [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), meldt u zich bij Hallo test-account en klikt u op **Google Apps** -tegel in Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="258fe-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="258fe-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="258fe-251">Additional resources</span></span>

* [<span data-ttu-id="258fe-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="258fe-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="258fe-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="258fe-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="258fe-254">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="258fe-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png