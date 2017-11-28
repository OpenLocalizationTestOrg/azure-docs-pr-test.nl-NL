---
title: 'Zelfstudie: Azure Active Directory-integratie met suiker CRM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en suiker CRM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="5fdb1-103">Zelfstudie: Azure Active Directory-integratie met suiker CRM</span><span class="sxs-lookup"><span data-stu-id="5fdb1-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="5fdb1-104">In deze zelfstudie leert u hoe toointegrate suiker CRM met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fdb1-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fdb1-105">Suiker CRM integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fdb1-106">U kunt beheren in Azure AD wie toegang tot tooSugar CRM heeft</span><span class="sxs-lookup"><span data-stu-id="5fdb1-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="5fdb1-107">U kunt uw gebruikers tooautomatically get aangemelde tooSugar CRM (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5fdb1-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fdb1-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5fdb1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5fdb1-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fdb1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fdb1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5fdb1-110">Prerequisites</span></span>

<span data-ttu-id="5fdb1-111">Azure AD-integratie met suiker CRM tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="5fdb1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5fdb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fdb1-113">Een CRM suiker eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5fdb1-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fdb1-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fdb1-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fdb1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fdb1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fdb1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fdb1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5fdb1-118">Scenario description</span></span>
<span data-ttu-id="5fdb1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fdb1-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fdb1-121">Het toevoegen van suiker CRM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5fdb1-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="5fdb1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fdb1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="5fdb1-123">Het toevoegen van suiker CRM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="5fdb1-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="5fdb1-124">tooconfigure hello integratie van suiker CRM in Azure AD, moet u tooadd suiker CRM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fdb1-125">**tooadd suiker CRM via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fdb1-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5fdb1-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fdb1-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5fdb1-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5fdb1-133">Typ in het zoekvak Hallo **suiker CRM**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="5fdb1-135">Selecteer in het deelvenster resultaten hello, **suiker CRM**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fdb1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fdb1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fdb1-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met suiker CRM op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fdb1-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in suiker CRM is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="5fdb1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in suiker CRM toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="5fdb1-141">In suiker CRM, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5fdb1-142">tooconfigure en test eenmalige aanmelding Azure AD met suiker CRM, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fdb1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fdb1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fdb1-145">**[Maken van een testgebruiker suiker CRM](#creating-a-sugar-crm-test-user)**  -toohave een equivalent van Britta Simon in suiker CRM die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fdb1-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fdb1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fdb1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5fdb1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fdb1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing suiker CRM.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="5fdb1-150">**Azure AD tooconfigure eenmalige aanmelding met suiker CRM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fdb1-151">In de Azure-portal op Hallo Hallo **suiker CRM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5fdb1-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="5fdb1-155">Op Hallo **suiker CRM-domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="5fdb1-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="5fdb1-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-158">hello value is not real.</span></span> <span data-ttu-id="5fdb1-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5fdb1-160">Neem contact op met [suiker CRM-Client-ondersteuningsteam](https://support.sugarcrm.com/) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="5fdb1-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="5fdb1-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fdb1-165">Op Hallo **suiker CRM configuratie** sectie, klikt u op **configureren suiker CRM** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5fdb1-166">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="5fdb1-168">In een ander browservenster, meld u aan tooyour suiker CRM bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="5fdb1-169">Ga te**Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="5fdb1-170">![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="5fdb1-171">In Hallo **beheer** sectie, klikt u op **wachtwoordbeheer**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="5fdb1-172">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="5fdb1-173">Selecteer **SAML-verificatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="5fdb1-174">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="5fdb1-175">In Hallo **SAML-verificatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5fdb1-176">![SAML-verificatie](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="5fdb1-177">a.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-177">a.</span></span> <span data-ttu-id="5fdb1-178">In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="5fdb1-179">b.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-179">b.</span></span> <span data-ttu-id="5fdb1-180">In Hallo **SLO URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="5fdb1-181">c.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-181">c.</span></span> <span data-ttu-id="5fdb1-182">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="5fdb1-183">d.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-183">d.</span></span> <span data-ttu-id="5fdb1-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5fdb1-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fdb1-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fdb1-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fdb1-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fdb1-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5fdb1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5fdb1-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5fdb1-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fdb1-192">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fdb1-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fdb1-196">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fdb1-198">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fdb1-200">a.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-200">a.</span></span> <span data-ttu-id="5fdb1-201">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fdb1-202">b.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-202">b.</span></span> <span data-ttu-id="5fdb1-203">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fdb1-204">c.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-204">c.</span></span> <span data-ttu-id="5fdb1-205">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5fdb1-206">d.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-206">d.</span></span> <span data-ttu-id="5fdb1-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="5fdb1-208">Een testgebruiker suiker CRM maken</span><span class="sxs-lookup"><span data-stu-id="5fdb1-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="5fdb1-209">In de volgorde tooenable Azure AD gebruikers toolog in tooSugar CRM, moeten ze ingerichte tooSugar CRM zijn.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="5fdb1-210">In geval van suiker CRM Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="5fdb1-211">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fdb1-212">Meld u bij tooyour **suiker CRM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="5fdb1-213">Ga te**Admin**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="5fdb1-214">![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="5fdb1-215">In Hallo **beheer** sectie, klikt u op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="5fdb1-216">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="5fdb1-217">Ga te**gebruikers \> nieuwe gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="5fdb1-218">![Nieuwe gebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "nieuwe gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="5fdb1-219">Op Hallo **gebruikersprofiel** tabblad, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="5fdb1-220">![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="5fdb1-221">a.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-221">a.</span></span> <span data-ttu-id="5fdb1-222">Type Hallo **gebruikersnaam**, **achternaam**, en **e-mailadres** van een geldige Azure Active Directory-gebruiker in Hallo gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="5fdb1-223">Als **Status**, selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="5fdb1-224">Op tabblad hello, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fdb1-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="5fdb1-225">![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="5fdb1-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="5fdb1-226">a.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-226">a.</span></span> <span data-ttu-id="5fdb1-227">Geef het wachtwoord Hallo in Hallo gerelateerd textbox.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="5fdb1-228">b.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-228">b.</span></span> <span data-ttu-id="5fdb1-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="5fdb1-230">U kunt andere suiker CRM gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door suiker CRM tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5fdb1-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fdb1-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5fdb1-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5fdb1-234">**tooassign Britta Simon tooSugar CRM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="5fdb1-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fdb1-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5fdb1-237">Selecteer in de lijst met de toepassingen van Hallo **suiker CRM**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="5fdb1-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5fdb1-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-241">Click **Add** button.</span></span> <span data-ttu-id="5fdb1-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5fdb1-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fdb1-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fdb1-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fdb1-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5fdb1-247">Testing single sign-on</span></span>

<span data-ttu-id="5fdb1-248">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5fdb1-249">Als u op Hallo suiker CRM-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour suiker CRM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fdb1-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fdb1-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5fdb1-250">Additional resources</span></span>

* [<span data-ttu-id="5fdb1-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fdb1-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fdb1-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fdb1-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

