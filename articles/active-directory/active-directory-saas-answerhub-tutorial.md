---
title: 'Zelfstudie: Azure Active Directory-integratie met AnswerHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="a011e-103">Zelfstudie: Azure Active Directory-integratie met AnswerHub</span><span class="sxs-lookup"><span data-stu-id="a011e-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="a011e-104">In deze zelfstudie leert u hoe toointegrate AnswerHub met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a011e-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a011e-105">AnswerHub integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a011e-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a011e-106">U kunt beheren in Azure AD die tooAnswerHub toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a011e-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="a011e-107">U kunt uw gebruikers tooautomatically get aangemelde tooAnswerHub (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a011e-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a011e-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a011e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a011e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a011e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a011e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a011e-110">Prerequisites</span></span>

<span data-ttu-id="a011e-111">Azure AD-integratie met AnswerHub tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a011e-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="a011e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a011e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a011e-113">Een AnswerHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a011e-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a011e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a011e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a011e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a011e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a011e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a011e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a011e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a011e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a011e-118">Scenario description</span></span>
<span data-ttu-id="a011e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a011e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a011e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a011e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a011e-121">Het toevoegen van AnswerHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a011e-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="a011e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a011e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="a011e-123">Het toevoegen van AnswerHub van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a011e-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="a011e-124">tooconfigure hello integratie van AnswerHub in Azure AD, moet u tooadd AnswerHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a011e-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a011e-125">**tooadd AnswerHub via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a011e-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a011e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a011e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a011e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a011e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a011e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a011e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a011e-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a011e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a011e-133">Typ in het zoekvak Hallo **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="a011e-133">In hello search box, type **AnswerHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="a011e-135">Selecteer in het deelvenster resultaten hello, **AnswerHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a011e-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a011e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a011e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a011e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met AnswerHub op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a011e-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a011e-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AnswerHub is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a011e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="a011e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AnswerHub toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a011e-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="a011e-141">Wijs in AnswerHub, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="a011e-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a011e-142">tooconfigure en eenmalige aanmelding Azure AD-test met AnswerHub, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a011e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a011e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a011e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a011e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a011e-145">**[Maken van een testgebruiker AnswerHub](#creating-an-answerhub-test-user)**  -toohave een equivalent van Britta Simon in AnswerHub die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a011e-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a011e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a011e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a011e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a011e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a011e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a011e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a011e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AnswerHub configureren.</span><span class="sxs-lookup"><span data-stu-id="a011e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="a011e-150">**Azure AD tooconfigure eenmalige aanmelding met AnswerHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a011e-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="a011e-151">In de Azure-portal op Hallo Hallo **AnswerHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a011e-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a011e-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a011e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="a011e-155">Op Hallo **AnswerHub domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="a011e-157">a.</span><span class="sxs-lookup"><span data-stu-id="a011e-157">a.</span></span> <span data-ttu-id="a011e-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="a011e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="a011e-159">b.</span><span class="sxs-lookup"><span data-stu-id="a011e-159">b.</span></span> <span data-ttu-id="a011e-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="a011e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a011e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a011e-161">These values are not real.</span></span> <span data-ttu-id="a011e-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="a011e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a011e-163">Neem contact op met [AnswerHub Client ondersteuningsteam](mailto:success@answerhub.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a011e-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a011e-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a011e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="a011e-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a011e-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a011e-168">Op Hallo **AnswerHub configuratie** sectie, klikt u op **configureren AnswerHub** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a011e-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a011e-169">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a011e-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="a011e-171">In een ander browservenster, meld u bij uw bedrijf AnswerHub site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a011e-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a011e-172">Als u nodig hebt bij het configureren van AnswerHub, neem dan contact op met [ondersteuningsteam van AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="a011e-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="a011e-173">Ga te**beheer**.</span><span class="sxs-lookup"><span data-stu-id="a011e-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="a011e-174">Klik op Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a011e-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="a011e-175">In het navigatiedeelvenster Hallo op Hallo linkerkant in Hallo **sociale instellingen** sectie, klikt u op **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="a011e-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="a011e-176">Klik op **IDP Config** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a011e-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="a011e-177">Op Hallo **IDP Config** tabblad, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="a011e-178">![Setup van SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="a011e-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="a011e-179">a.</span><span class="sxs-lookup"><span data-stu-id="a011e-179">a.</span></span> <span data-ttu-id="a011e-180">In **IDP aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a011e-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="a011e-181">b.</span><span class="sxs-lookup"><span data-stu-id="a011e-181">b.</span></span> <span data-ttu-id="a011e-182">In **IDP afmelding URL** textbox plakken **Sign-Out URL** waarde die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a011e-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="a011e-183">c.</span><span class="sxs-lookup"><span data-stu-id="a011e-183">c.</span></span> <span data-ttu-id="a011e-184">In **IDP-naamnotatie id** textbox Voer Hallo gebruiker id dezelfde waarde als de geselecteerde in Azure-portal op **gebruikerskenmerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="a011e-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="a011e-185">d.</span><span class="sxs-lookup"><span data-stu-id="a011e-185">d.</span></span> <span data-ttu-id="a011e-186">Klik op **sleutels en certificaten**.</span><span class="sxs-lookup"><span data-stu-id="a011e-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="a011e-187">Voer op Hallo sleutels en certificaten tabblad Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="a011e-188">![Sleutels en certificaten](./media/active-directory-saas-answerhub-tutorial/ic785173.png "sleutels en certificaten")</span><span class="sxs-lookup"><span data-stu-id="a011e-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="a011e-189">a.</span><span class="sxs-lookup"><span data-stu-id="a011e-189">a.</span></span> <span data-ttu-id="a011e-190">Open uw base-64 gecodeerde certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IDP openbare sleutel (x 509-indeling)** textbox.</span><span class="sxs-lookup"><span data-stu-id="a011e-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="a011e-191">b.</span><span class="sxs-lookup"><span data-stu-id="a011e-191">b.</span></span> <span data-ttu-id="a011e-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a011e-192">Click **Save**.</span></span>

14. <span data-ttu-id="a011e-193">Op Hallo **IDP Config** tabblad **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a011e-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a011e-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="a011e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a011e-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="a011e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a011e-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a011e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a011e-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a011e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a011e-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a011e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a011e-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a011e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a011e-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a011e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a011e-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a011e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a011e-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a011e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a011e-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a011e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a011e-209">a.</span><span class="sxs-lookup"><span data-stu-id="a011e-209">a.</span></span> <span data-ttu-id="a011e-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a011e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a011e-211">b.</span><span class="sxs-lookup"><span data-stu-id="a011e-211">b.</span></span> <span data-ttu-id="a011e-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a011e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a011e-213">c.</span><span class="sxs-lookup"><span data-stu-id="a011e-213">c.</span></span> <span data-ttu-id="a011e-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a011e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a011e-215">d.</span><span class="sxs-lookup"><span data-stu-id="a011e-215">d.</span></span> <span data-ttu-id="a011e-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a011e-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="a011e-217">Een testgebruiker AnswerHub maken</span><span class="sxs-lookup"><span data-stu-id="a011e-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="a011e-218">Azure AD tooenable gebruikers toolog in tooAnswerHub, ze in AnswerHub moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="a011e-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="a011e-219">In geval van AnswerHub Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a011e-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="a011e-220">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a011e-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a011e-221">Meld u bij tooyour **AnswerHub** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="a011e-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="a011e-222">Ga te**beheer**.</span><span class="sxs-lookup"><span data-stu-id="a011e-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="a011e-223">Klik op Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a011e-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="a011e-224">In het navigatiedeelvenster Hallo op Hallo linkerkant in Hallo **gebruikers beheren** sectie, klikt u op **maken of importeren gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a011e-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="a011e-225">![Gebruikers en groepen](./media/active-directory-saas-answerhub-tutorial/ic785175.png "gebruikers en groepen")</span><span class="sxs-lookup"><span data-stu-id="a011e-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="a011e-226">Type Hallo **e-mailadres**, **gebruikersnaam** en **wachtwoord** van een geldig Azure Active Directory-account die u wilt dat tooprovision in Hallo tekstvakken gerelateerd en klik vervolgens op  **Sla**.</span><span class="sxs-lookup"><span data-stu-id="a011e-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a011e-227">U kunt andere AnswerHub gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door AnswerHub tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="a011e-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a011e-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a011e-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a011e-229">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAnswerHub toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="a011e-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a011e-231">**tooassign Britta Simon tooAnswerHub, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a011e-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="a011e-232">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a011e-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a011e-234">Selecteer in de lijst met de toepassingen van Hallo **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="a011e-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="a011e-236">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a011e-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a011e-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a011e-238">Click **Add** button.</span></span> <span data-ttu-id="a011e-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a011e-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a011e-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a011e-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a011e-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a011e-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a011e-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a011e-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a011e-244">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a011e-244">Testing single sign-on</span></span>

<span data-ttu-id="a011e-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a011e-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a011e-246">Als u op Hallo AnswerHub tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour AnswerHub toepassing.</span><span class="sxs-lookup"><span data-stu-id="a011e-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="a011e-247">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a011e-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a011e-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a011e-248">Additional resources</span></span>

* [<span data-ttu-id="a011e-249">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a011e-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a011e-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a011e-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

