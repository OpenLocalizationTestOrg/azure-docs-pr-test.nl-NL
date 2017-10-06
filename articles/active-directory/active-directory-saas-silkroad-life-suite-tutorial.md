---
title: 'Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SilkRoad levensduur Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="3543d-103">Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite</span><span class="sxs-lookup"><span data-stu-id="3543d-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="3543d-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SilkRoad levensduur Suite met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3543d-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="3543d-105">SilkRoad levensduur Suite integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3543d-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="3543d-106">U kunt beheren in Azure AD wie toegang tot tooSilkRoad levensduur Suite heeft</span><span class="sxs-lookup"><span data-stu-id="3543d-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="3543d-107">U kunt uw gebruikers tooautomatically get aangemelde tooSilkRoad Suite levensduur van eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="3543d-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="3543d-108">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3543d-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3543d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3543d-109">Prerequisites</span></span>
<span data-ttu-id="3543d-110">Azure AD-integratie met SilkRoad levensduur Suite tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3543d-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="3543d-111">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3543d-111">An Azure AD subscription</span></span>
* <span data-ttu-id="3543d-112">Een abonnement SilkRoad levensduur Suite SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3543d-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="3543d-113">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3543d-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="3543d-114">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3543d-115">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3543d-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3543d-116">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3543d-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="3543d-117">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3543d-117">Scenario Description</span></span>
<span data-ttu-id="3543d-118">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD-eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3543d-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="3543d-119">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3543d-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3543d-120">Het toevoegen van SilkRoad levensduur Suite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3543d-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="3543d-121">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="3543d-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="3543d-122">SilkRoad levensduur Suite van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3543d-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="3543d-123">tooconfigure hello integratie van SilkRoad levensduur Suite in Azure AD, moet u tooadd SilkRoad levensduur Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3543d-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3543d-124">**tooadd SilkRoad levensduur Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3543d-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3543d-125">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3543d-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="3543d-127">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="3543d-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3543d-128">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="3543d-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="3543d-130">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="3543d-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="3543d-132">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="3543d-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="3543d-134">Typ in het zoekvak Hallo **SilkRoad levensduur Suite**.</span><span class="sxs-lookup"><span data-stu-id="3543d-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="3543d-136">Selecteer in het deelvenster met resultaten Hallo **SilkRoad levensduur Suite**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3543d-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Toepassingen][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3543d-138">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="3543d-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3543d-139">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Azure AD-SSO met SilkRoad levensduur Suite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3543d-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3543d-140">Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SilkRoad leven Suite tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3543d-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="3543d-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SilkRoad leven Suite toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3543d-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="3543d-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SilkRoad leven Suite.</span><span class="sxs-lookup"><span data-stu-id="3543d-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="3543d-143">tooconfigure en test eenmalige aanmelding Azure AD met SilkRoad levensduur Suite, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3543d-144">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3543d-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3543d-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3543d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3543d-146">**[Maken van een testgebruiker SilkRoad levensduur Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave een equivalent van Britta Simon in SilkRoad levensduur-pakket dat is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="3543d-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3543d-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3543d-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3543d-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3543d-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3543d-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3543d-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="3543d-150">Hallo-doel van deze sectie is tooenable Azure AD-eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure SSO in uw toepassing SilkRoad levensduur Suite.</span><span class="sxs-lookup"><span data-stu-id="3543d-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="3543d-151">**tooconfigure eenmalige aanmelding Azure AD met SilkRoad levensduur Suite uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3543d-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3543d-152">Eenmalige aanmelding tooyour SilkRoad bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="3543d-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="3543d-153">tooobtain toegang toohello SilkRoad levensduur Suite verificatie-toepassing voor federatie configureren met Microsoft Azure AD en neem contact op met ondersteuning voor SilkRoad of uw vertegenwoordiger SilkRoad Services.</span><span class="sxs-lookup"><span data-stu-id="3543d-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="3543d-154">Ga te**serviceprovider**, en klik vervolgens op **Federation Details**.</span><span class="sxs-lookup"><span data-stu-id="3543d-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][10] 

3. <span data-ttu-id="3543d-156">Klik op **Federatiemetagegevens downloaden**, en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3543d-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][11] 

4. <span data-ttu-id="3543d-158">In de klassieke Azure-portal op Hallo Hallo **SilkRoad levensduur Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3543d-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 

5. <span data-ttu-id="3543d-160">Op Hallo **wilt u hoe gebruikers toosign op tooSilkRoad levensduur Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][7] 

6. <span data-ttu-id="3543d-162">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD voor eenmalige aanmelding][8]   
 1. <span data-ttu-id="3543d-164">In Hallo **aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign op tooyour SilkRoad levensduur Suite site gebruikt (bijvoorbeeld: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="3543d-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="3543d-165">Open Hallo gedownload **Silkroad** bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="3543d-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="3543d-166">Zoek Hallo **AssertionConsumerService** label en kopiëren Hallo **locatie** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="3543d-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Azure AD voor eenmalige aanmelding][21] 
 4. <span data-ttu-id="3543d-168">Hallo-waarde in Hallo plakken **antwoord-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3543d-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="3543d-169">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-169">Click **Next**.</span></span>

6. <span data-ttu-id="3543d-170">Op Hallo **op SilkRoad levensduur Suite eenmalige aanmelding configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]  
 1. <span data-ttu-id="3543d-172">Klik op downloaden certificaat en sla Hallo-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3543d-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="3543d-173">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-173">Click **Next**.</span></span>

7. <span data-ttu-id="3543d-174">In uw **SilkRoad** toepassing, klikt u op **verificatie bronnen**.</span><span class="sxs-lookup"><span data-stu-id="3543d-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][12] 

8. <span data-ttu-id="3543d-176">Klik op **verificatiebron toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3543d-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][13] 

9. <span data-ttu-id="3543d-178">In Hallo **verificatie-bron toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][14]  
 1. <span data-ttu-id="3543d-180">Onder **optie 2 - bestand met metagegevens**, klikt u op **Bladeren** tooupload Hallo gedownload bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="3543d-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="3543d-181">Klik op **maken id-Provider met behulp van bestandsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="3543d-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="3543d-182">In Hallo **verificatie bronnen** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3543d-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][15] 

11. <span data-ttu-id="3543d-184">Op Hallo **verificatiebron bewerken** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3543d-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][16] 
 1. <span data-ttu-id="3543d-186">Als **ingeschakeld**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="3543d-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="3543d-187">In Hallo **IdP beschrijving** textbox, typ een beschrijving voor uw configuratie (bijvoorbeeld: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="3543d-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="3543d-188">In Hallo **IdP naam** textbox, typ een naam die specifieke tooyour configuratie (bijvoorbeeld: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="3543d-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="3543d-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3543d-189">Click **Save**.</span></span>

12. <span data-ttu-id="3543d-190">Uitschakelen voor alle andere verificatie-bronnen.</span><span class="sxs-lookup"><span data-stu-id="3543d-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD voor eenmalige aanmelding][17]

13. <span data-ttu-id="3543d-192">In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD voor eenmalige aanmelding][18]

14. <span data-ttu-id="3543d-194">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3543d-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD voor eenmalige aanmelding][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3543d-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3543d-196">Create an Azure AD test user</span></span>
<span data-ttu-id="3543d-197">Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3543d-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="3543d-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3543d-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3543d-200">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3543d-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="3543d-202">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="3543d-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3543d-203">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3543d-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3543d-205">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3543d-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3543d-207">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="3543d-209">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3543d-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="3543d-210">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3543d-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="3543d-211">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-211">Click **Next**.</span></span>

6. <span data-ttu-id="3543d-212">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="3543d-214">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3543d-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="3543d-215">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3543d-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="3543d-216">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3543d-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="3543d-217">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="3543d-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="3543d-218">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="3543d-218">Click **Next**.</span></span>

7. <span data-ttu-id="3543d-219">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3543d-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3543d-221">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3543d-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="3543d-223">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3543d-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="3543d-224">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="3543d-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="3543d-225">Maak een testgebruiker SilkRoad levensduur Suite</span><span class="sxs-lookup"><span data-stu-id="3543d-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="3543d-226">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SilkRoad leven Suite van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3543d-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="3543d-227">De Britta moet een SSO-ID hebben (dit wordt soms aangeduid tooas een *AuthParam*) die overeenkomt met de Britta **emailaddress** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3543d-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="3543d-228">**toocreate een gebruiker Britta Simon aangeroepen in SilkRoad leven Suite uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3543d-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="3543d-229">Vraag uw SilkRoad levensduur Suite support team toocreate een gebruiker die als heeft **SSO-ID** kenmerk Hallo dezelfde als Hallo waarde **emailaddress** van Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3543d-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3543d-230">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3543d-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="3543d-231">Hallo doel van deze sectie is tooenable Britta Simon toouse Azure SSO haar toegang tooSilkRoad levensduur Suite verleent.</span><span class="sxs-lookup"><span data-stu-id="3543d-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3543d-233">**tooassign Britta Simon tooSilkRoad levensduur Suite uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3543d-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3543d-234">Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="3543d-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3543d-236">Selecteer in de lijst met de toepassingen van Hallo **SilkRoad levensduur Suite**.</span><span class="sxs-lookup"><span data-stu-id="3543d-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Gebruiker toewijzen][202] 

3. <span data-ttu-id="3543d-238">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3543d-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203] 

4. <span data-ttu-id="3543d-240">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3543d-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3543d-241">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="3543d-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3543d-243">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3543d-243">Test single sign-on</span></span>
<span data-ttu-id="3543d-244">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="3543d-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="3543d-245">Als u op Hallo SilkRoad levensduur Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SilkRoad levensduur Suite-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3543d-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3543d-246">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="3543d-246">Additional Resources</span></span>
* [<span data-ttu-id="3543d-247">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3543d-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3543d-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3543d-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





