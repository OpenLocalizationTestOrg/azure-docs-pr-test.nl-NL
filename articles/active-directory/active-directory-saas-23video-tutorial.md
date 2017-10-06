---
title: 'Zelfstudie: Azure Active Directory-integratie met 23 Video | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 23 Video.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="4e229-103">Zelfstudie: Azure Active Directory-integratie met 23 Video</span><span class="sxs-lookup"><span data-stu-id="4e229-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="4e229-104">In deze zelfstudie leert u hoe toointegrate 23 Video met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e229-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e229-105">Integratie van 23 biedt Video met Azure AD Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4e229-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e229-106">U kunt beheren in Azure AD die toegang heeft too23 Video</span><span class="sxs-lookup"><span data-stu-id="4e229-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="4e229-107">U kunt uw gebruikers in staat om tooautomatically inschakelen aangemelde too23 Video (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="4e229-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e229-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4e229-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4e229-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e229-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e229-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4e229-110">Prerequisites</span></span>

<span data-ttu-id="4e229-111">Azure AD-integratie met 23 Video tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4e229-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="4e229-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4e229-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e229-113">Een 23 Video eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4e229-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e229-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4e229-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e229-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4e229-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e229-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4e229-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e229-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e229-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e229-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4e229-118">Scenario description</span></span>
<span data-ttu-id="4e229-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4e229-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e229-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4e229-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e229-121">Het toevoegen van 23 Video van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4e229-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="4e229-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e229-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="4e229-123">Het toevoegen van 23 Video van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4e229-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="4e229-124">tooconfigure hello integratie van 23 Video in Azure AD, moet u tooadd 23 Video van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4e229-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e229-125">**tooadd 23 Video via Hallo gallery uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="4e229-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e229-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4e229-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e229-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e229-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4e229-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e229-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4e229-133">Typ in het zoekvak Hallo **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="4e229-133">In hello search box, type **23 Video**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="4e229-135">Selecteer in het deelvenster resultaten hello, **23 Video**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e229-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e229-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e229-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e229-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met 23 Video op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4e229-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e229-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 23 Video is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e229-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="4e229-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in 23 moet Video toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4e229-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="4e229-141">In 23 Video Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4e229-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4e229-142">tooconfigure en test eenmalige aanmelding Azure AD met 23 Video, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e229-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e229-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4e229-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e229-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e229-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e229-145">**[Maken van een 23 Video testgebruiker](#creating-a-23-video-test-user)**  -toohave een equivalent van Britta Simon in 23 Video die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4e229-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e229-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e229-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e229-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4e229-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e229-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4e229-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e229-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw 23 Video-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e229-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="4e229-150">**Voer tooconfigure Azure AD eenmalige aanmelding met 23 Video Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e229-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e229-151">In de Azure-portal op Hallo Hallo **23 Video** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4e229-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4e229-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4e229-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="4e229-155">Op Hallo **23 URL's en Video domein** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e229-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="4e229-157">a.</span><span class="sxs-lookup"><span data-stu-id="4e229-157">a.</span></span> <span data-ttu-id="4e229-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="4e229-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="4e229-159">b.</span><span class="sxs-lookup"><span data-stu-id="4e229-159">b.</span></span> <span data-ttu-id="4e229-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="4e229-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e229-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4e229-161">These values are not real.</span></span> <span data-ttu-id="4e229-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="4e229-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4e229-163">Neem contact op met [23 Video Client ondersteuningsteam](mailto:support@23company.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4e229-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4e229-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4e229-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="4e229-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4e229-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e229-168">Op Hallo **23 videoconfiguratie** sectie, klikt u op **configureren 23 Video** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4e229-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4e229-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4e229-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="4e229-171">tooconfigure eenmalige aanmelding op **23 Video** zijde, moet u toosend Hallo gedownload **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL**te[23 Video ondersteuningsteam](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="4e229-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="4e229-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4e229-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e229-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4e229-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e229-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e229-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e229-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4e229-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e229-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4e229-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4e229-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e229-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e229-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4e229-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e229-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4e229-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e229-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4e229-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e229-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e229-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e229-187">a.</span><span class="sxs-lookup"><span data-stu-id="4e229-187">a.</span></span> <span data-ttu-id="4e229-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e229-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e229-189">b.</span><span class="sxs-lookup"><span data-stu-id="4e229-189">b.</span></span> <span data-ttu-id="4e229-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e229-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e229-191">c.</span><span class="sxs-lookup"><span data-stu-id="4e229-191">c.</span></span> <span data-ttu-id="4e229-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4e229-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e229-193">d.</span><span class="sxs-lookup"><span data-stu-id="4e229-193">d.</span></span> <span data-ttu-id="4e229-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4e229-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="4e229-195">Een 23 Video testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4e229-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="4e229-196">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in 23 Video van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4e229-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="4e229-197">**een gebruiker met de naam van Britta Simon in 23 Video toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4e229-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e229-198">Meld u op tooyour 23 Video bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4e229-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="4e229-199">Ga te**instellingen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="4e229-200">In **gebruikers** sectie, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="4e229-200">In **Users** section, click **Configure**.</span></span>
   
    ![Gebruiker toewijzen][400]

4. <span data-ttu-id="4e229-202">Klik op **een nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-202">Click **Add a new user**.</span></span> 
   
    ![Gebruiker toewijzen][401]

5. <span data-ttu-id="4e229-204">In Hallo **iemand uitnodigen toojoin deze site** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4e229-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Gebruiker toewijzen][402]

    <span data-ttu-id="4e229-206">a.</span><span class="sxs-lookup"><span data-stu-id="4e229-206">a.</span></span> <span data-ttu-id="4e229-207">In Hallo **e-mailadressen** textbox Britta Simon van e-mailadres typt in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e229-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="4e229-208">b.</span><span class="sxs-lookup"><span data-stu-id="4e229-208">b.</span></span> <span data-ttu-id="4e229-209">Klik op **Hallo-gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4e229-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e229-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4e229-211">In deze sectie, schakelt u Britta Simon toouse Azure eenmalige aanmelding verleent toegang tot too23 Video.</span><span class="sxs-lookup"><span data-stu-id="4e229-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4e229-213">**tooassign Britta Simon too23 Video Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4e229-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e229-214">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4e229-216">Selecteer in de lijst met de toepassingen van Hallo **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="4e229-216">In hello applications list, select **23 Video**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="4e229-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4e229-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4e229-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4e229-220">Click **Add** button.</span></span> <span data-ttu-id="4e229-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e229-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4e229-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e229-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e229-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e229-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e229-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4e229-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e229-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4e229-226">Testing single sign-on</span></span>

<span data-ttu-id="4e229-227">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4e229-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4e229-228">Als u op Hallo 23 Video-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour 23 Video-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4e229-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4e229-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4e229-229">Additional resources</span></span>

* [<span data-ttu-id="4e229-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e229-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e229-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e229-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
