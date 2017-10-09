---
title: 'Zelfstudie: Azure Active Directory-integratie met Hackerone | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Hackerone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="3a307-103">Zelfstudie: Azure Active Directory-integratie met HackerOne</span><span class="sxs-lookup"><span data-stu-id="3a307-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="3a307-104">In deze zelfstudie leert u hoe toointegrate HackerOne met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a307-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a307-105">HackerOne integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3a307-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a307-106">U kunt beheren in Azure AD die tooHackerOne toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3a307-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="3a307-107">U kunt uw gebruikers tooautomatically get aangemelde tooHackerOne (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3a307-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a307-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3a307-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a307-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a307-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a307-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a307-110">Prerequisites</span></span>

<span data-ttu-id="3a307-111">Azure AD-integratie met HackerOne tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3a307-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="3a307-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3a307-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a307-113">Een HackerOne eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3a307-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a307-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3a307-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a307-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3a307-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a307-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3a307-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a307-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a307-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a307-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3a307-118">Scenario description</span></span>
<span data-ttu-id="3a307-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3a307-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a307-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3a307-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a307-121">Het toevoegen van HackerOne van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3a307-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="3a307-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a307-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="3a307-123">Het toevoegen van HackerOne van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3a307-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="3a307-124">tooconfigure hello integratie van HackerOne in Azure AD, moet u tooadd HackerOne uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3a307-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a307-125">**tooadd HackerOne via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3a307-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a307-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3a307-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a307-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a307-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a307-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a307-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3a307-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a307-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3a307-133">Typ in het zoekvak Hallo **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="3a307-133">In hello search box, type **HackerOne**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="3a307-135">Selecteer in het deelvenster resultaten hello, **HackerOne**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a307-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a307-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a307-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3a307-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met HackerOne op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3a307-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a307-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in HackerOne is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a307-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="3a307-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HackerOne toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3a307-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="3a307-141">Wijs in HackerOne, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="3a307-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a307-142">tooconfigure en eenmalige aanmelding Azure AD-test met HackerOne, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a307-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a307-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3a307-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a307-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a307-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a307-145">**[Maken van een testgebruiker HackerOne](#creating-a-hackerone-test-user)**  -toohave een equivalent van Britta Simon in HackerOne die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3a307-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a307-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3a307-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a307-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3a307-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a307-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3a307-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a307-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing HackerOne configureren.</span><span class="sxs-lookup"><span data-stu-id="3a307-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="3a307-150">**Azure AD tooconfigure eenmalige aanmelding met HackerOne, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3a307-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a307-151">In de Azure-portal op Hallo Hallo **HackerOne** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3a307-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3a307-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3a307-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="3a307-155">Op Hallo **HackerOne één aanmeldings-URL en id** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a307-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="3a307-157">a.</span><span class="sxs-lookup"><span data-stu-id="3a307-157">a.</span></span> <span data-ttu-id="3a307-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="3a307-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="3a307-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a307-159">b.</span></span> <span data-ttu-id="3a307-160">In Hallo **id** textbox, typ een URL als:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="3a307-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3a307-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="3a307-161">This value is not real.</span></span> <span data-ttu-id="3a307-162">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="3a307-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3a307-163">Neem contact op met [HackerOne ondersteuningsteam](mailto:support@hackerone.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="3a307-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="3a307-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3a307-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="3a307-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3a307-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a307-168">Op Hallo **HackerOne configuratie** sectie, klikt u op **configureren HackerOne** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3a307-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3a307-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3a307-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="3a307-171">Aanmelding tooyour HackerOne tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3a307-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="3a307-172">Klik op Hallo in het menu bovenaan Hallo Hallo '**instellingen**. "</span><span class="sxs-lookup"><span data-stu-id="3a307-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="3a307-174">Navigeer te'**verificatie**'en klik op'**SAML-instellingen toevoegen**. "</span><span class="sxs-lookup"><span data-stu-id="3a307-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="3a307-176">Op Hallo **SAML instellingen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3a307-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="3a307-178">a.</span><span class="sxs-lookup"><span data-stu-id="3a307-178">a.</span></span> <span data-ttu-id="3a307-179">In Hallo **e-maildomein** textbox, typt u een geregistreerde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="3a307-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="3a307-180">b.</span><span class="sxs-lookup"><span data-stu-id="3a307-180">b.</span></span> <span data-ttu-id="3a307-181">In **eenmalige aanmelding op URL** tekstvakken, plak Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3a307-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a307-182">c.</span><span class="sxs-lookup"><span data-stu-id="3a307-182">c.</span></span> <span data-ttu-id="3a307-183">Open uw **certificaatbestand** in Kladblok gedownload vanuit Azure-portal Hallo inhoud van het kopiëren naar het Klembord en plak deze toohello **X509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="3a307-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="3a307-184">d.</span><span class="sxs-lookup"><span data-stu-id="3a307-184">d.</span></span> <span data-ttu-id="3a307-185">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3a307-185">Click **Save**.</span></span>

11. <span data-ttu-id="3a307-186">Voer in het dialoogvenster Hallo verificatie-instellingen, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a307-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="3a307-188">a.</span><span class="sxs-lookup"><span data-stu-id="3a307-188">a.</span></span> <span data-ttu-id="3a307-189">Klik op **test uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="3a307-189">Click **Run test**.</span></span>

    <span data-ttu-id="3a307-190">b.</span><span class="sxs-lookup"><span data-stu-id="3a307-190">b.</span></span> <span data-ttu-id="3a307-191">Als waarde van Hallo Hallo **Status** veld gelijk is aan **status van de laatste test: gemaakt**Neem contact op met uw [HackerOne ondersteuningsteam](mailto:support@hackerone.com) toorequest een overzicht van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="3a307-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="3a307-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="3a307-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a307-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="3a307-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a307-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a307-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a307-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3a307-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a307-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3a307-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3a307-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3a307-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a307-199">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3a307-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a307-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3a307-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a307-203">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3a307-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a307-205">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a307-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a307-207">a.</span><span class="sxs-lookup"><span data-stu-id="3a307-207">a.</span></span> <span data-ttu-id="3a307-208">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a307-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a307-209">b.</span><span class="sxs-lookup"><span data-stu-id="3a307-209">b.</span></span> <span data-ttu-id="3a307-210">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a307-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a307-211">c.</span><span class="sxs-lookup"><span data-stu-id="3a307-211">c.</span></span> <span data-ttu-id="3a307-212">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3a307-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a307-213">d.</span><span class="sxs-lookup"><span data-stu-id="3a307-213">d.</span></span> <span data-ttu-id="3a307-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3a307-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="3a307-215">Een testgebruiker HackerOne maken</span><span class="sxs-lookup"><span data-stu-id="3a307-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="3a307-216">Maak vervolgens een gebruiker Britta Simon in HackerOne genoemd.</span><span class="sxs-lookup"><span data-stu-id="3a307-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="3a307-217">HackerOne ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3a307-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="3a307-218">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3a307-218">There is no action item for you in this section.</span></span> <span data-ttu-id="3a307-219">Wanneer u HackerOne opent, wordt een nieuwe gebruiker gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3a307-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3a307-220">Als u handmatig een gebruiker toocreate nodig, moet u toocontact Hallo certificeren ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="3a307-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3a307-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a307-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3a307-222">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHackerOne toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="3a307-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3a307-224">**tooassign Britta Simon tooHackerOne, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3a307-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a307-225">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a307-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3a307-227">Selecteer in de lijst met de toepassingen van Hallo **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="3a307-227">In hello applications list, select **HackerOne**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="3a307-229">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3a307-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3a307-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3a307-231">Click **Add** button.</span></span> <span data-ttu-id="3a307-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a307-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3a307-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a307-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a307-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a307-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a307-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a307-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a307-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a307-237">Testing single sign-on</span></span>

<span data-ttu-id="3a307-238">Ten slotte kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3a307-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="3a307-239">Als u op Hallo HackerOne tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour HackerOne toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a307-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a307-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3a307-240">Additional resources</span></span>

* [<span data-ttu-id="3a307-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a307-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a307-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a307-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

