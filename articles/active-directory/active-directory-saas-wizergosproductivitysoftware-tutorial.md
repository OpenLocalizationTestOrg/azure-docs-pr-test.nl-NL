---
title: 'Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Wizergos productiviteitssoftware.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="33d71-103">Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware</span><span class="sxs-lookup"><span data-stu-id="33d71-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="33d71-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Wizergos productiviteitssoftware met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33d71-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33d71-105">Wizergos productiviteitssoftware integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="33d71-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="33d71-106">U kunt beheren in Azure AD wie toegang tot tooWizergos productiviteitssoftware heeft</span><span class="sxs-lookup"><span data-stu-id="33d71-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="33d71-107">U kunt uw gebruikers tooautomatically get aangemelde tooWizergos productiviteitssoftware eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="33d71-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="33d71-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="33d71-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="33d71-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33d71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33d71-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="33d71-110">Prerequisites</span></span>
<span data-ttu-id="33d71-111">Azure AD-integratie met Wizergos productiviteitssoftware tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="33d71-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="33d71-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="33d71-112">An Azure AD subscription</span></span>
* <span data-ttu-id="33d71-113">Een abonnement Wizergos productiviteit Software SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="33d71-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="33d71-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="33d71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="33d71-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="33d71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="33d71-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="33d71-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="33d71-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33d71-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33d71-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="33d71-118">Scenario description</span></span>
<span data-ttu-id="33d71-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD-eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="33d71-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="33d71-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="33d71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33d71-121">Het toevoegen van Wizergos productiviteitssoftware van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="33d71-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="33d71-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="33d71-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="33d71-123">Het toevoegen van Wizergos productiviteitssoftware van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="33d71-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="33d71-124">tooconfigure hello integratie van Software voor Wizergos productiviteit in Azure AD, moet u tooadd Wizergos productiviteitssoftware uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="33d71-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="33d71-125">**tooadd Wizergos productiviteitssoftware uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="33d71-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="33d71-126">In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33d71-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="33d71-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="33d71-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="33d71-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d71-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Toepassingen][2]
4. <span data-ttu-id="33d71-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="33d71-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Toepassingen][3]
5. <span data-ttu-id="33d71-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="33d71-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Toepassingen][4]
6. <span data-ttu-id="33d71-135">Typ in het zoekvak Hallo **Wizergos productiviteitssoftware**.</span><span class="sxs-lookup"><span data-stu-id="33d71-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="33d71-137">Selecteer in het deelvenster resultaten hello, **Wizergos productiviteitssoftware**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33d71-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Hallo-app in de galerie Hallo selecteren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="33d71-139">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="33d71-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="33d71-140">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Azure AD-SSO met Wizergos productiviteitssoftware op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="33d71-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33d71-141">Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Wizergos productiviteitssoftware tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33d71-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="33d71-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Wizergos productiviteitssoftware toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="33d71-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="33d71-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Wizergos productiviteitssoftware.</span><span class="sxs-lookup"><span data-stu-id="33d71-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="33d71-144">tooconfigure en eenmalige aanmelding Azure AD-test met BynWizergos productiviteit Softwareder, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="33d71-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="33d71-145">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="33d71-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="33d71-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33d71-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33d71-147">**[Maken van een testgebruiker Wizergos productiviteitssoftware](#creating-a-wizergos-productivity-software-test-user)**  -toohave een equivalent van Britta Simon in Wizergos productiviteitssoftware die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="33d71-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="33d71-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="33d71-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33d71-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="33d71-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="33d71-150">Configuratie van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="33d71-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="33d71-151">In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Wizergos productiviteit.</span><span class="sxs-lookup"><span data-stu-id="33d71-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="33d71-152">**tooconfigure eenmalige aanmelding Azure AD met Wizergos productiviteitssoftware, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="33d71-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="33d71-153">In de klassieke portal Hallo op Hallo **Wizergos productiviteitssoftware** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33d71-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][6] 
2. <span data-ttu-id="33d71-155">Op Hallo **wilt u hoe gebruikers toosign op tooWizergos productiviteitssoftware** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="33d71-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="33d71-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, klikt u op **volgende**:</span><span class="sxs-lookup"><span data-stu-id="33d71-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="33d71-159">Op Hallo **eenmalige aanmelding op Wizergos productiviteitssoftware configureren** pagina, klikt u op **certificaat downloaden**, en sla Hallo-bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="33d71-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="33d71-161">In een ander browservenster, aanmelding tooyour Wizergos productiviteitssoftware tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="33d71-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="33d71-162">Hallo hamburger menu en selecteer **Admin**.</span><span class="sxs-lookup"><span data-stu-id="33d71-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="33d71-164">Selecteer in de beheerpagina linkerkant menu **verificatie** en klik op **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="33d71-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="33d71-166">Uitvoeren van de volgende stappen uit op Hallo **verificatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="33d71-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="33d71-168">Klik op **uploaden** knop tooupload Hallo certificaat gedownload vanuit Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33d71-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="33d71-169">In Hallo **URL-verlener** textbox plaatsen Hallo-waarde van **URL-verlener** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33d71-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="33d71-170">In Hallo **-URL met eenmalige aanmelding** textbox plaatsen Hallo-waarde van **één Service-URL aanmelding** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33d71-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="33d71-171">In Hallo **-URL met eenmalige Sign-Out** textbox plaatsen Hallo-waarde van **Service-URL met eenmalige Sign-out** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33d71-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="33d71-172">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="33d71-172">Click **Save** button.</span></span>
9. <span data-ttu-id="33d71-173">In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="33d71-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]
10. <span data-ttu-id="33d71-175">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="33d71-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="33d71-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="33d71-177">Create an Azure AD test user</span></span>
<span data-ttu-id="33d71-178">Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="33d71-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="33d71-180">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="33d71-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="33d71-181">In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33d71-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="33d71-183">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="33d71-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="33d71-184">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="33d71-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="33d71-186">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="33d71-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="33d71-188">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="33d71-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="33d71-190">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="33d71-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="33d71-191">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33d71-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="33d71-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="33d71-192">Click **Next**.</span></span>
6. <span data-ttu-id="33d71-193">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="33d71-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="33d71-195">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="33d71-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="33d71-196">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="33d71-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="33d71-197">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="33d71-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="33d71-198">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="33d71-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="33d71-199">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="33d71-199">Click **Next**.</span></span>
7. <span data-ttu-id="33d71-200">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="33d71-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="33d71-202">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="33d71-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="33d71-204">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="33d71-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="33d71-205">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="33d71-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="33d71-206">Een testgebruiker Wizergos productiviteitssoftware maken</span><span class="sxs-lookup"><span data-stu-id="33d71-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="33d71-207">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Wizergos productiviteitssoftware maken.</span><span class="sxs-lookup"><span data-stu-id="33d71-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="33d71-208">Neem contact op met het ondersteuningsteam Wizergos productiviteitssoftware via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd Hallo gebruikers in Hallo Wizergos productiviteitssoftware platform.</span><span class="sxs-lookup"><span data-stu-id="33d71-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="33d71-209">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="33d71-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="33d71-210">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure SSO verleent haar toegang tooWizergos productiviteitssoftware.</span><span class="sxs-lookup"><span data-stu-id="33d71-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Gebruiker toewijzen][200]

<span data-ttu-id="33d71-212">**tooassign Britta Simon tooWizergos productiviteitssoftware, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="33d71-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="33d71-213">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="33d71-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Gebruiker toewijzen][201]
2. <span data-ttu-id="33d71-215">Selecteer in de lijst met de toepassingen van Hallo **Wizergos productiviteitssoftware**.</span><span class="sxs-lookup"><span data-stu-id="33d71-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="33d71-217">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="33d71-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Gebruiker toewijzen][203]
4. <span data-ttu-id="33d71-219">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="33d71-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="33d71-220">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="33d71-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="33d71-222">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="33d71-222">Test single sign-on</span></span>
<span data-ttu-id="33d71-223">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="33d71-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="33d71-224">Als u op Hallo Wizergos productiviteitssoftware tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Wizergos productiviteit softwaretoepassing.</span><span class="sxs-lookup"><span data-stu-id="33d71-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33d71-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="33d71-225">Additional resources</span></span>
* [<span data-ttu-id="33d71-226">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33d71-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33d71-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33d71-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
