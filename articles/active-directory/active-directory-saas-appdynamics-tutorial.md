---
title: 'Zelfstudie: Azure Active Directory-integratie met AppDynamics | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AppDynamics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="8f495-103">Zelfstudie: Azure Active Directory-integratie met AppDynamics</span><span class="sxs-lookup"><span data-stu-id="8f495-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="8f495-104">In deze zelfstudie leert u hoe toointegrate AppDynamics met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f495-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f495-105">AppDynamics integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8f495-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f495-106">U kunt beheren in Azure AD die tooAppDynamics toegang heeft</span><span class="sxs-lookup"><span data-stu-id="8f495-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="8f495-107">U kunt uw gebruikers tooautomatically get aangemelde tooAppDynamics (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8f495-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f495-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8f495-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f495-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f495-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f495-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8f495-110">Prerequisites</span></span>

<span data-ttu-id="8f495-111">Azure AD-integratie met AppDynamics tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8f495-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="8f495-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8f495-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f495-113">Een AppDynamics eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8f495-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f495-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8f495-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f495-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f495-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8f495-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f495-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f495-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f495-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8f495-118">Scenario description</span></span>
<span data-ttu-id="8f495-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8f495-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f495-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8f495-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f495-121">Het toevoegen van AppDynamics van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8f495-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="8f495-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8f495-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="8f495-123">Het toevoegen van AppDynamics van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8f495-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="8f495-124">tooconfigure hello integratie van AppDynamics in Azure AD, moet u tooadd AppDynamics uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8f495-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f495-125">**tooadd AppDynamics via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f495-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f495-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8f495-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f495-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f495-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f495-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f495-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8f495-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8f495-133">Typ in het zoekvak Hallo **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="8f495-133">In hello search box, type **AppDynamics**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="8f495-135">Selecteer in het deelvenster resultaten hello, **AppDynamics**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8f495-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f495-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8f495-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f495-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AppDynamics op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8f495-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f495-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AppDynamics is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f495-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="8f495-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AppDynamics toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8f495-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="8f495-141">Wijs in AppDynamics, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="8f495-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f495-142">tooconfigure en eenmalige aanmelding Azure AD-test met AppDynamics, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f495-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8f495-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f495-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f495-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f495-145">**[Maken van een testgebruiker AppDynamics](#creating-an-appdynamics-test-user)**  -toohave een equivalent van Britta Simon in AppDynamics die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8f495-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f495-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8f495-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f495-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8f495-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f495-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8f495-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f495-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AppDynamics configureren.</span><span class="sxs-lookup"><span data-stu-id="8f495-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="8f495-150">**Azure AD tooconfigure eenmalige aanmelding met AppDynamics, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f495-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f495-151">In de Azure-portal op Hallo Hallo **AppDynamics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8f495-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8f495-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8f495-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="8f495-155">Op Hallo **AppDynamics domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="8f495-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f495-157">a.</span></span> <span data-ttu-id="8f495-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="8f495-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="8f495-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f495-159">b.</span></span> <span data-ttu-id="8f495-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="8f495-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f495-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8f495-161">These values are not real.</span></span> <span data-ttu-id="8f495-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="8f495-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8f495-163">Neem contact op met [AppDynamics Client ondersteuningsteam](https://www.appdynamics.com/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8f495-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8f495-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8f495-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="8f495-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8f495-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8f495-168">Op Hallo **AppDynamics configuratie** sectie, klikt u op **configureren AppDynamics** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8f495-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8f495-169">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8f495-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="8f495-171">In een ander browservenster, meld u aan tooyour AppDynamics bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="8f495-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="8f495-172">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**, en klik vervolgens op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="8f495-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="8f495-173">![Beheer](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="8f495-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="8f495-174">Klik op Hallo **verificatieprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="8f495-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="8f495-175">![Verificatieprovider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "verificatieprovider")</span><span class="sxs-lookup"><span data-stu-id="8f495-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="8f495-176">In Hallo **verificatieprovider** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8f495-177">![De SAML-configuratie](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="8f495-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="8f495-178">a.</span><span class="sxs-lookup"><span data-stu-id="8f495-178">a.</span></span> <span data-ttu-id="8f495-179">Als **verificatieprovider**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8f495-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="8f495-180">b.</span><span class="sxs-lookup"><span data-stu-id="8f495-180">b.</span></span> <span data-ttu-id="8f495-181">In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8f495-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8f495-182">c.</span><span class="sxs-lookup"><span data-stu-id="8f495-182">c.</span></span> <span data-ttu-id="8f495-183">In Hallo **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8f495-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="8f495-184">d.</span><span class="sxs-lookup"><span data-stu-id="8f495-184">d.</span></span> <span data-ttu-id="8f495-185">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="8f495-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="8f495-186">e.</span><span class="sxs-lookup"><span data-stu-id="8f495-186">e.</span></span> <span data-ttu-id="8f495-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8f495-187">Click **Save**.</span></span>

     <span data-ttu-id="8f495-188">![Sla](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="8f495-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="8f495-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="8f495-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f495-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="8f495-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f495-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f495-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f495-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8f495-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f495-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8f495-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8f495-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f495-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f495-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8f495-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f495-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8f495-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f495-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8f495-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f495-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f495-204">a.</span><span class="sxs-lookup"><span data-stu-id="8f495-204">a.</span></span> <span data-ttu-id="8f495-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f495-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f495-206">b.</span><span class="sxs-lookup"><span data-stu-id="8f495-206">b.</span></span> <span data-ttu-id="8f495-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f495-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f495-208">c.</span><span class="sxs-lookup"><span data-stu-id="8f495-208">c.</span></span> <span data-ttu-id="8f495-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8f495-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f495-210">d.</span><span class="sxs-lookup"><span data-stu-id="8f495-210">d.</span></span> <span data-ttu-id="8f495-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f495-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="8f495-212">Een testgebruiker AppDynamics maken</span><span class="sxs-lookup"><span data-stu-id="8f495-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="8f495-213">Azure AD tooenable gebruikers toolog in tooAppDynamics, ze in AppDynamics moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="8f495-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="8f495-214">In geval van AppDynamics Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="8f495-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="8f495-215">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f495-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f495-216">Aanmelden tooyour AppDynamics bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8f495-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="8f495-217">Ga te**gebruikers**, en klik vervolgens op  **+**  tooopen hello **gebruiker maken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="8f495-218">![Gebruikers](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="8f495-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="8f495-219">In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f495-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8f495-220">![Gebruiker maken](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="8f495-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="8f495-221">a.</span><span class="sxs-lookup"><span data-stu-id="8f495-221">a.</span></span> <span data-ttu-id="8f495-222">Type Hallo **gebruikersnaam**, **naam**, **e**, **nieuw wachtwoord**, **nieuw wachtwoord herhalen** van een geldige AAD gewenste tooprovision in Hallo account gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="8f495-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="8f495-223">b.</span><span class="sxs-lookup"><span data-stu-id="8f495-223">b.</span></span> <span data-ttu-id="8f495-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8f495-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8f495-225">U kunt andere AppDynamics gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door AppDynamics tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="8f495-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8f495-226">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f495-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8f495-227">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAppDynamics toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8f495-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8f495-229">**tooassign Britta Simon tooAppDynamics, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8f495-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f495-230">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8f495-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8f495-232">Selecteer in de lijst met de toepassingen van Hallo **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="8f495-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="8f495-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8f495-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8f495-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8f495-236">Click **Add** button.</span></span> <span data-ttu-id="8f495-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8f495-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f495-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f495-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f495-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f495-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8f495-242">Testing single sign-on</span></span>

<span data-ttu-id="8f495-243">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="8f495-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f495-244">Als u op Hallo AppDynamics-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour AppDynamics toepassing.</span><span class="sxs-lookup"><span data-stu-id="8f495-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f495-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8f495-245">Additional resources</span></span>

* [<span data-ttu-id="8f495-246">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f495-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f495-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f495-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

