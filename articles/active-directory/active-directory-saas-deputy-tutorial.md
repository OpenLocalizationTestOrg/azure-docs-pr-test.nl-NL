---
title: 'Zelfstudie: Azure Active Directory-integratie met vice | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en vice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="4c55e-103">Zelfstudie: Azure Active Directory-integratie met vice</span><span class="sxs-lookup"><span data-stu-id="4c55e-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="4c55e-104">In deze zelfstudie leert u hoe toointegrate vice met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c55e-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c55e-105">Vice integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c55e-106">U kunt beheren in Azure AD die tooDeputy toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4c55e-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="4c55e-107">U kunt uw gebruikers tooautomatically get aangemelde tooDeputy (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4c55e-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c55e-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4c55e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4c55e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c55e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c55e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4c55e-110">Prerequisites</span></span>

<span data-ttu-id="4c55e-111">Azure AD-integratie met vice tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4c55e-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="4c55e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4c55e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c55e-113">Een vice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4c55e-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c55e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4c55e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c55e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c55e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4c55e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c55e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c55e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c55e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4c55e-118">Scenario description</span></span>
<span data-ttu-id="4c55e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4c55e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c55e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c55e-121">Het toevoegen van vice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4c55e-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="4c55e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c55e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="4c55e-123">Het toevoegen van vice van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4c55e-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="4c55e-124">tooconfigure hello integratie van vice in Azure AD, moet u tooadd vice uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4c55e-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c55e-125">**tooadd vice via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c55e-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c55e-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4c55e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c55e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c55e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4c55e-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4c55e-133">Typ in het zoekvak Hallo **vice**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-133">In hello search box, type **Deputy**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="4c55e-135">Selecteer in het deelvenster resultaten hello, **vice**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c55e-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c55e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c55e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c55e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met vice op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4c55e-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c55e-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in vice is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c55e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="4c55e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in vice toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4c55e-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="4c55e-141">Wijs in vice, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4c55e-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c55e-142">tooconfigure en eenmalige aanmelding Azure AD-test met vice, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c55e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4c55e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c55e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c55e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c55e-145">**[Maken van een testgebruiker vice](#creating-a-deputy-test-user)**  -toohave een equivalent van Britta Simon in vice die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4c55e-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c55e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4c55e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c55e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4c55e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c55e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4c55e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c55e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing vice configureren.</span><span class="sxs-lookup"><span data-stu-id="4c55e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="4c55e-150">**Azure AD tooconfigure eenmalige aanmelding met vice, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c55e-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c55e-151">In de Azure-portal op Hallo Hallo **vice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4c55e-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4c55e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="4c55e-155">Op Hallo **vice domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="4c55e-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="4c55e-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c55e-157">a.</span></span> <span data-ttu-id="4c55e-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="4c55e-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c55e-159">b.</span></span> <span data-ttu-id="4c55e-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="4c55e-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4c55e-162">U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="4c55e-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="4c55e-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="4c55e-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="4c55e-165">Vice regio achtervoegsel is optioneel, of moet een van de volgende gebruiken: Australië | n.v.t. | EU | als | la | af | een | ent Australië | ent na | ent eu | ent-als | ent la | ent af | ent een</span><span class="sxs-lookup"><span data-stu-id="4c55e-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c55e-166">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4c55e-166">These values are not real.</span></span> <span data-ttu-id="4c55e-167">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="4c55e-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4c55e-168">Neem contact op met [vice ondersteuningsteam](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4c55e-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="4c55e-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4c55e-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="4c55e-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4c55e-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4c55e-173">Op Hallo **vice configuratie** sectie, klikt u op **vice configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4c55e-174">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4c55e-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="4c55e-176">Navigeer toohello volgende URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="4c55e-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="4c55e-177">Ga te**beveiligingsinstellingen** en klik op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="4c55e-179">Op deze **beveiligingsinstellingen** pagina, voert u onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="4c55e-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="4c55e-181">a.</span><span class="sxs-lookup"><span data-stu-id="4c55e-181">a.</span></span> <span data-ttu-id="4c55e-182">Schakel **aanmelden bij sociale Media**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="4c55e-183">b.</span><span class="sxs-lookup"><span data-stu-id="4c55e-183">b.</span></span> <span data-ttu-id="4c55e-184">Open uw Base64-gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **OpenSSL certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="4c55e-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="4c55e-185">c.</span><span class="sxs-lookup"><span data-stu-id="4c55e-185">c.</span></span> <span data-ttu-id="4c55e-186">Typ in het tekstvak Hallo SAML-URL voor eenmalige aanmelding`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="4c55e-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="4c55e-187">d.</span><span class="sxs-lookup"><span data-stu-id="4c55e-187">d.</span></span> <span data-ttu-id="4c55e-188">Vervang in Hallo SAML SSO URL textbox `<your subdomain>` met een subdomein.</span><span class="sxs-lookup"><span data-stu-id="4c55e-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="4c55e-189">e.</span><span class="sxs-lookup"><span data-stu-id="4c55e-189">e.</span></span> <span data-ttu-id="4c55e-190">Vervang in Hallo SAML SSO URL textbox `<saml sso url>` Hello **SAML Single Sign-On Service-URL** u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4c55e-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="4c55e-191">f.</span><span class="sxs-lookup"><span data-stu-id="4c55e-191">f.</span></span> <span data-ttu-id="4c55e-192">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="4c55e-193">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4c55e-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c55e-194">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4c55e-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c55e-195">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c55e-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c55e-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4c55e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c55e-197">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4c55e-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4c55e-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c55e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c55e-200">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4c55e-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c55e-202">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c55e-204">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4c55e-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c55e-206">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c55e-208">a.</span><span class="sxs-lookup"><span data-stu-id="4c55e-208">a.</span></span> <span data-ttu-id="4c55e-209">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c55e-210">b.</span><span class="sxs-lookup"><span data-stu-id="4c55e-210">b.</span></span> <span data-ttu-id="4c55e-211">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c55e-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c55e-212">c.</span><span class="sxs-lookup"><span data-stu-id="4c55e-212">c.</span></span> <span data-ttu-id="4c55e-213">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4c55e-214">d.</span><span class="sxs-lookup"><span data-stu-id="4c55e-214">d.</span></span> <span data-ttu-id="4c55e-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="4c55e-216">Een testgebruiker vice maken</span><span class="sxs-lookup"><span data-stu-id="4c55e-216">Creating a Deputy test user</span></span>

<span data-ttu-id="4c55e-217">Azure AD tooenable gebruikers toolog in tooDeputy, ze in vice moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="4c55e-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="4c55e-218">In geval van een vice is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="4c55e-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="4c55e-219">een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c55e-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="4c55e-220">Tooyour vice bedrijf site aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4c55e-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="4c55e-221">Klik op het bovenste navigatievenster Hallo **mensen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="4c55e-222">![Mensen](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="4c55e-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="4c55e-223">Klik op Hallo **mensen toevoegen** en klik op **toevoegen één persoon**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="4c55e-224">![Personen toevoegen](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "personen toevoegen")</span><span class="sxs-lookup"><span data-stu-id="4c55e-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="4c55e-225">Hallo volgende stappen uit te voeren en op **opslaan en uit te nodigen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="4c55e-226">![Nieuwe gebruiker](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="4c55e-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="4c55e-227">a.</span><span class="sxs-lookup"><span data-stu-id="4c55e-227">a.</span></span> <span data-ttu-id="4c55e-228">In Hallo **naam** textbox typenaam van de gebruiker Hallo zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="4c55e-229">b.</span><span class="sxs-lookup"><span data-stu-id="4c55e-229">b.</span></span> <span data-ttu-id="4c55e-230">In Hallo **e** textbox type Hallo e-mailadres van een Azure AD-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4c55e-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="4c55e-231">c.</span><span class="sxs-lookup"><span data-stu-id="4c55e-231">c.</span></span> <span data-ttu-id="4c55e-232">In Hallo **op werkt** textbox typenaam Hallo bedrijven.</span><span class="sxs-lookup"><span data-stu-id="4c55e-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="4c55e-233">d.</span><span class="sxs-lookup"><span data-stu-id="4c55e-233">d.</span></span> <span data-ttu-id="4c55e-234">Klik op **opslaan en uit te nodigen** knop.</span><span class="sxs-lookup"><span data-stu-id="4c55e-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="4c55e-235">Hallo AAD accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="4c55e-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="4c55e-236">U kunt andere vice gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door vice tooprovision AAD gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="4c55e-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4c55e-237">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c55e-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4c55e-238">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDeputy toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="4c55e-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4c55e-240">**tooassign Britta Simon tooDeputy, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4c55e-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c55e-241">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4c55e-243">Selecteer in de lijst met de toepassingen van Hallo **vice**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-243">In hello applications list, select **Deputy**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="4c55e-245">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4c55e-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4c55e-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4c55e-247">Click **Add** button.</span></span> <span data-ttu-id="4c55e-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4c55e-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c55e-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c55e-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c55e-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c55e-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4c55e-253">Testing single sign-on</span></span>

<span data-ttu-id="4c55e-254">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4c55e-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4c55e-255">Als u op Hallo vice-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour vice toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c55e-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c55e-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4c55e-256">Additional resources</span></span>

* [<span data-ttu-id="4c55e-257">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c55e-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c55e-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c55e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

