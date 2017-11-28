---
title: 'Zelfstudie: Azure Active Directory-integratie met kunnen LMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LMS opvangen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="68b0c-103">Zelfstudie: Azure Active Directory-integratie met LMS opnemen</span><span class="sxs-lookup"><span data-stu-id="68b0c-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="68b0c-104">In deze zelfstudie leert u hoe toointegrate Absorb LMS met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68b0c-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68b0c-105">LMS kunnen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68b0c-106">U kunt beheren in Azure AD wie toegang tot tooAbsorb LMS heeft</span><span class="sxs-lookup"><span data-stu-id="68b0c-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="68b0c-107">U kunt uw gebruikers tooautomatically get aangemelde tooAbsorb LMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="68b0c-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68b0c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="68b0c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68b0c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="68b0c-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="68b0c-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68b0c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b0c-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="68b0c-111">Prerequisites</span></span>

<span data-ttu-id="68b0c-112">Azure AD-integratie met LMS kunnen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="68b0c-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="68b0c-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="68b0c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="68b0c-114">Een LMS kunnen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="68b0c-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68b0c-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="68b0c-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68b0c-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68b0c-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="68b0c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68b0c-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68b0c-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68b0c-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="68b0c-119">Scenario description</span></span>
<span data-ttu-id="68b0c-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="68b0c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68b0c-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68b0c-122">Toe te voegen kunnen LMS uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="68b0c-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="68b0c-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="68b0c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="68b0c-124">Toe te voegen kunnen LMS uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="68b0c-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="68b0c-125">tooconfigure hello integratie van LMS opnemen in tooAzure AD, moet u tooadd Absorb LMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="68b0c-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68b0c-126">**tooadd Absorb LMS via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="68b0c-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68b0c-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="68b0c-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="68b0c-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68b0c-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-130">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="68b0c-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="68b0c-134">Typ in het zoekvak Hallo **LMS kunnen**, selecteer **LMS kunnen** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="68b0c-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![LMS opnemen in lijst met resultaten Hallo](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="68b0c-136">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b0c-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="68b0c-137">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met kunnen LMS op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="68b0c-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68b0c-138">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in kunnen LMS is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68b0c-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="68b0c-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in kunnen LMS toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="68b0c-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="68b0c-140">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LMS opvangen.</span><span class="sxs-lookup"><span data-stu-id="68b0c-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="68b0c-141">tooconfigure en eenmalige aanmelding Azure AD-test met LMS opnemen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68b0c-142">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="68b0c-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68b0c-143">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68b0c-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68b0c-144">**[Maken van een testgebruiker kunnen LMS](#create-an-absorb-lms-test-user)**  -toohave een equivalent van Britta Simon in kunnen LMS gekoppelde toohello Azure AD-weergave van de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="68b0c-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68b0c-145">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="68b0c-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68b0c-146">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="68b0c-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="68b0c-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="68b0c-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="68b0c-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LMS kunnen configureren.</span><span class="sxs-lookup"><span data-stu-id="68b0c-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="68b0c-149">**Azure AD tooconfigure eenmalige aanmelding met LMS kunnen uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="68b0c-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="68b0c-150">In Azure-portal op Hallo Hallo **kunnen LMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="68b0c-152">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="68b0c-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="68b0c-154">Op Hallo **kunnen LMS domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![LMS domein en de URL's eenmalige aanmelding informatie opnemen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="68b0c-156">a.</span><span class="sxs-lookup"><span data-stu-id="68b0c-156">a.</span></span> <span data-ttu-id="68b0c-157">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="68b0c-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="68b0c-158">b.</span><span class="sxs-lookup"><span data-stu-id="68b0c-158">b.</span></span> <span data-ttu-id="68b0c-159">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="68b0c-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="68b0c-160">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="68b0c-160">These values are not hello real.</span></span> <span data-ttu-id="68b0c-161">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="68b0c-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="68b0c-162">Neem contact op met [kunnen LMS Client ondersteuningsteam](https://www.absorblms.com/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="68b0c-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="68b0c-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="68b0c-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="68b0c-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="68b0c-165">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="68b0c-167">Op Hallo **LMS configuratie kunnen** sectie, klikt u op **kunnen LMS configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="68b0c-168">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="68b0c-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![LMS configuratie opnemen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="68b0c-170">In een ander browservenster, meld u aan tooyour kunnen LMS bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="68b0c-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="68b0c-171">Klik op Hallo **pictogram** op Hallo-beheerinterface.</span><span class="sxs-lookup"><span data-stu-id="68b0c-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="68b0c-173">Klik op **portalinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-173">Click **Portal Settings**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="68b0c-175">Klik op Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="68b0c-175">Click hello **Users** tab.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="68b0c-177">Volgende stappen tooaccess Hallo Single Sign-On configuratievelden Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="68b0c-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="68b0c-179">a.</span><span class="sxs-lookup"><span data-stu-id="68b0c-179">a.</span></span> <span data-ttu-id="68b0c-180">Selecteer Hallo juiste **modus**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="68b0c-181">b.</span><span class="sxs-lookup"><span data-stu-id="68b0c-181">b.</span></span> <span data-ttu-id="68b0c-182">Open Hallo certificaat dat u hebt gedownload van Azure-portal in Kladblok Hallo Hallo verwijderen **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---** code en plak Hallo resterende inhoud in Hallo **sleutel** textbox.</span><span class="sxs-lookup"><span data-stu-id="68b0c-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="68b0c-183">c.</span><span class="sxs-lookup"><span data-stu-id="68b0c-183">c.</span></span> <span data-ttu-id="68b0c-184">In Hallo **Id-eigenschap**, selecteer Hallo juiste kenmerk dat u hebt geconfigureerd zoals Hallo gebruikers-id in hello Azure AD (bijvoorbeeld als Hallo userprinciplename is ingeschakeld in Azure AD en vervolgens de gebruikersnaam hier zou worden geselecteerd.)</span><span class="sxs-lookup"><span data-stu-id="68b0c-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="68b0c-185">d.</span><span class="sxs-lookup"><span data-stu-id="68b0c-185">d.</span></span> <span data-ttu-id="68b0c-186">In Hallo **aanmeldings-URL**, plak Hallo **'SAML Single Sign-On Service URL'** waarde die u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="68b0c-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="68b0c-187">e.</span><span class="sxs-lookup"><span data-stu-id="68b0c-187">e.</span></span> <span data-ttu-id="68b0c-188">In Hallo **afmelding URL**, Hallo plakken **'Sign-Out URL'** waarde die u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="68b0c-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="68b0c-189">Schakel **'Alleen SSO aanmelden toestaan'**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="68b0c-191">Klik op **'Opgeslagen'.**</span><span class="sxs-lookup"><span data-stu-id="68b0c-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="68b0c-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="68b0c-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68b0c-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="68b0c-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68b0c-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68b0c-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="68b0c-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="68b0c-195">Create an Azure AD test user</span></span>

<span data-ttu-id="68b0c-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="68b0c-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="68b0c-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="68b0c-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68b0c-199">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="68b0c-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68b0c-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68b0c-203">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68b0c-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68b0c-207">a.</span><span class="sxs-lookup"><span data-stu-id="68b0c-207">a.</span></span> <span data-ttu-id="68b0c-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68b0c-209">b.</span><span class="sxs-lookup"><span data-stu-id="68b0c-209">b.</span></span> <span data-ttu-id="68b0c-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68b0c-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68b0c-211">c.</span><span class="sxs-lookup"><span data-stu-id="68b0c-211">c.</span></span> <span data-ttu-id="68b0c-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68b0c-213">d.</span><span class="sxs-lookup"><span data-stu-id="68b0c-213">d.</span></span> <span data-ttu-id="68b0c-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="68b0c-215">Een testgebruiker LMS kunnen maken</span><span class="sxs-lookup"><span data-stu-id="68b0c-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="68b0c-216">Azure AD tooenable gebruikers toolog in tooAbsorb LMS, ze in tooAbsorb LMS moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="68b0c-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="68b0c-217">Inrichting is een handmatige taak voor LMS opvangen.</span><span class="sxs-lookup"><span data-stu-id="68b0c-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="68b0c-218">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="68b0c-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="68b0c-219">Aanmelden tooyour kunnen LMS bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="68b0c-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="68b0c-220">Klik op **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="68b0c-220">Click **Users** tab.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="68b0c-222">Klik op **gebruikers** onder Hallo **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="68b0c-222">Click **Users** under hello **Users** tab.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="68b0c-224">Selecteer **gebruiker** van **nieuwe toevoegen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="68b0c-224">Select **User** from **Add New** drop-down.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="68b0c-226">Op Hallo **gebruiker toevoegen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="68b0c-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="68b0c-228">a.</span><span class="sxs-lookup"><span data-stu-id="68b0c-228">a.</span></span> <span data-ttu-id="68b0c-229">In Hallo **voornaam** textbox type Hallo Voornaam zoals Britta.</span><span class="sxs-lookup"><span data-stu-id="68b0c-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="68b0c-230">b.</span><span class="sxs-lookup"><span data-stu-id="68b0c-230">b.</span></span> <span data-ttu-id="68b0c-231">In Hallo **achternaam** textbox type Hallo achternaam zoals Simon.</span><span class="sxs-lookup"><span data-stu-id="68b0c-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="68b0c-232">c.</span><span class="sxs-lookup"><span data-stu-id="68b0c-232">c.</span></span> <span data-ttu-id="68b0c-233">In Hallo **gebruikersnaam** textbox, typ de gebruikersnaam zoals Britta Simon Hallo.</span><span class="sxs-lookup"><span data-stu-id="68b0c-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="68b0c-234">d.</span><span class="sxs-lookup"><span data-stu-id="68b0c-234">d.</span></span> <span data-ttu-id="68b0c-235">In Hallo **wachtwoord** textbox type wachtwoord op Hallo van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68b0c-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="68b0c-236">e.</span><span class="sxs-lookup"><span data-stu-id="68b0c-236">e.</span></span> <span data-ttu-id="68b0c-237">In Hallo **wachtwoord bevestigen** textbox type Hallo hetzelfde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="68b0c-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="68b0c-238">f.</span><span class="sxs-lookup"><span data-stu-id="68b0c-238">f.</span></span> <span data-ttu-id="68b0c-239">Als u **ACTIVE**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="68b0c-240">Klik op **'Opgeslagen'.**</span><span class="sxs-lookup"><span data-stu-id="68b0c-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="68b0c-241">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b0c-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="68b0c-242">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="68b0c-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="68b0c-244">**tooassign Britta Simon tooAbsorb LMS, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="68b0c-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="68b0c-245">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="68b0c-247">Selecteer in de lijst met de toepassingen van Hallo **kunnen LMS**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![Hallo LMS kunnen koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="68b0c-249">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="68b0c-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. <span data-ttu-id="68b0c-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="68b0c-251">Click **Add** button.</span></span> <span data-ttu-id="68b0c-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="68b0c-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="68b0c-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68b0c-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68b0c-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="68b0c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="68b0c-257">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="68b0c-257">Test single sign-on</span></span>

<span data-ttu-id="68b0c-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="68b0c-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="68b0c-259">Hallo kunnen LMS-tegel in Hallo paneel voor Apptoegang, klikt u op krijgt u automatisch aangemelde tooyour kunnen LMS toepassing.</span><span class="sxs-lookup"><span data-stu-id="68b0c-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="68b0c-260">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="68b0c-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68b0c-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="68b0c-261">Additional resources</span></span>

* [<span data-ttu-id="68b0c-262">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68b0c-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68b0c-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68b0c-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

