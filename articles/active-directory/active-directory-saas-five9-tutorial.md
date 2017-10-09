---
title: 'Zelfstudie: Azure Active Directory-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Five9 Plus Adapter (CTI, neem contact op met Center-Agents).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="d1480-103">Zelfstudie: Azure Active Directory-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents)</span><span class="sxs-lookup"><span data-stu-id="d1480-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="d1480-104">In deze zelfstudie leert u hoe toointegrate Five9 Plus Adapter (CTI, neem contact op met Center-Agents) met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1480-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1480-105">Five9 Plus Adapter (CTI, neem contact op met Center-Agents) integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d1480-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d1480-106">U kunt beheren in Azure AD wie heeft toegang tot tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents)</span><span class="sxs-lookup"><span data-stu-id="d1480-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="d1480-107">U kunt uw gebruikers tooautomatically get aangemelde tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents) inschakelen (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="d1480-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1480-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d1480-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d1480-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1480-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1480-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d1480-110">Prerequisites</span></span>

<span data-ttu-id="d1480-111">tooconfigure Azure AD-integratie met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="d1480-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="d1480-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d1480-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1480-113">Een Five9 Plus Adapter (CTI, neem contact op met Center-Agents) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d1480-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1480-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d1480-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1480-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1480-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d1480-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1480-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1480-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1480-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d1480-118">Scenario description</span></span>
<span data-ttu-id="d1480-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d1480-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1480-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d1480-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1480-121">Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1480-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="d1480-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1480-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="d1480-123">Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1480-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="d1480-124">tooconfigure hello integratie van Five9 Plus Adapter (CTI, neem contact op met Center-Agents) in Azure AD, moet u tooadd Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d1480-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d1480-125">**tooadd Five9 Plus Adapter (CTI, neem contact op met Center-Agents) uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d1480-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1480-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d1480-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1480-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1480-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d1480-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1480-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d1480-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1480-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d1480-133">Typ in het zoekvak Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**.</span><span class="sxs-lookup"><span data-stu-id="d1480-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="d1480-135">Selecteer in het deelvenster resultaten hello, **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1480-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1480-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1480-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1480-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Five9 Plus-Adapter (CTI, neem contact op met Center-Agents) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d1480-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1480-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent Five9 Plus adapter (CTI, neem contact op met Center-Agents) is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1480-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="d1480-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo Five9 Plus adapter (CTI, neem contact op met Center-Agents) toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d1480-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="d1480-141">Five9 Plus adapter (CTI, neem contact op met Center-Agents), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d1480-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d1480-142">tooconfigure en test eenmalige aanmelding Azure AD met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d1480-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d1480-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d1480-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1480-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1480-145">**[Maken van een testgebruiker Five9 Plus Adapter (CTI, neem contact op met Center-Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave een equivalent van Britta Simon Five9 Plus adapter (CTI, neem contact op met Center-Agents) die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d1480-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1480-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d1480-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1480-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d1480-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1480-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d1480-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1480-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Five9 Plus Adapter (CTI, neem contact op met Center-Agents).</span><span class="sxs-lookup"><span data-stu-id="d1480-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="d1480-150">**tooconfigure eenmalige aanmelding Azure AD met Five9 Plus Adapter (CTI, neem contact op met Center-Agents), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d1480-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="d1480-151">In de Azure-portal op Hallo Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d1480-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d1480-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d1480-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="d1480-155">Op Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="d1480-157">a.</span><span class="sxs-lookup"><span data-stu-id="d1480-157">a.</span></span> <span data-ttu-id="d1480-158">In Hallo **id** textbox, type patronen u een URL met hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="d1480-159">Omgeving</span><span class="sxs-lookup"><span data-stu-id="d1480-159">Environment</span></span>      |       <span data-ttu-id="d1480-160">URL</span><span class="sxs-lookup"><span data-stu-id="d1480-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="d1480-161">Voor 'Five9 Plus Adapter voor Microsoft Dynamics CRM'</span><span class="sxs-lookup"><span data-stu-id="d1480-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="d1480-162">Voor 'Five9 Plus Adapter voor Zendesk'</span><span class="sxs-lookup"><span data-stu-id="d1480-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="d1480-163">Voor 'Five9 Plus Adapter voor bureaublad Toolkit Agent'</span><span class="sxs-lookup"><span data-stu-id="d1480-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="d1480-164">b.</span><span class="sxs-lookup"><span data-stu-id="d1480-164">b.</span></span> <span data-ttu-id="d1480-165">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="d1480-166">Omgeving</span><span class="sxs-lookup"><span data-stu-id="d1480-166">Environment</span></span>     |      <span data-ttu-id="d1480-167">URL</span><span class="sxs-lookup"><span data-stu-id="d1480-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="d1480-168">Voor 'Five9 Plus Adapter voor Microsoft Dynamics CRM'</span><span class="sxs-lookup"><span data-stu-id="d1480-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="d1480-169">Voor 'Five9 Plus Adapter voor Zendesk'</span><span class="sxs-lookup"><span data-stu-id="d1480-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="d1480-170">Voor 'Five9 Plus Adapter voor bureaublad Toolkit Agent'</span><span class="sxs-lookup"><span data-stu-id="d1480-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="d1480-171">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d1480-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="d1480-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d1480-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1480-175">Op Hallo **Five9 Plus (CTI, neem contact op met Center-Agents) adapterconfiguratie** sectie, klikt u op **configureren Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** tooopen **aanmeldingconfigureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d1480-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d1480-176">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d1480-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="d1480-178">tooconfigure eenmalige aanmelding op **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)** zijde, moet u toosend Hallo gedownload **Certificate(Base64), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Five9 Plus Adapter (CTI, neem contact op met Center-Agents) ondersteuningsteam](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="d1480-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="d1480-179">Ook daarnaast voor het configureren van SSO verdere Volg Hallo onderstaande stappen volgens toohello adapter:</span><span class="sxs-lookup"><span data-stu-id="d1480-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="d1480-180">a.</span><span class="sxs-lookup"><span data-stu-id="d1480-180">a.</span></span> <span data-ttu-id="d1480-181">'Five9 Plus Adapter voor bureaublad Toolkit Agent' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="d1480-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="d1480-182">b.</span><span class="sxs-lookup"><span data-stu-id="d1480-182">b.</span></span> <span data-ttu-id="d1480-183">'Five9 Plus Adapter voor Microsoft Dynamics CRM' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="d1480-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="d1480-184">c.</span><span class="sxs-lookup"><span data-stu-id="d1480-184">c.</span></span> <span data-ttu-id="d1480-185">'Five9 Plus Adapter voor Zendesk' Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="d1480-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="d1480-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d1480-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d1480-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d1480-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d1480-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1480-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1480-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d1480-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1480-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d1480-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d1480-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d1480-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1480-193">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d1480-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1480-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d1480-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1480-197">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d1480-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1480-199">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1480-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1480-201">a.</span><span class="sxs-lookup"><span data-stu-id="d1480-201">a.</span></span> <span data-ttu-id="d1480-202">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1480-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1480-203">b.</span><span class="sxs-lookup"><span data-stu-id="d1480-203">b.</span></span> <span data-ttu-id="d1480-204">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d1480-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1480-205">c.</span><span class="sxs-lookup"><span data-stu-id="d1480-205">c.</span></span> <span data-ttu-id="d1480-206">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d1480-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d1480-207">d.</span><span class="sxs-lookup"><span data-stu-id="d1480-207">d.</span></span> <span data-ttu-id="d1480-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d1480-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="d1480-209">Maken van een testgebruiker Five9 Plus Adapter (CTI, neem contact op met Center-Agents)</span><span class="sxs-lookup"><span data-stu-id="d1480-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="d1480-210">In deze sectie maakt u een gebruiker met de naam van Britta Simon Five9 Plus adapter (CTI, neem contact op met Center-Agents).</span><span class="sxs-lookup"><span data-stu-id="d1480-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="d1480-211">Werken met [Five9 Plus Adapter (CTI, neem contact op met Center-Agents) ondersteuningsteam](https://www.five9.com/about/contact) Hallo gebruikers toevoegen in Hallo Five9 Plus Adapter (CTI, neem contact op met Center-Agents) platform.</span><span class="sxs-lookup"><span data-stu-id="d1480-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="d1480-212">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d1480-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d1480-213">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1480-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d1480-214">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents).</span><span class="sxs-lookup"><span data-stu-id="d1480-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d1480-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, neem contact op met Center-Agents), Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d1480-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="d1480-217">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1480-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d1480-219">Selecteer in de lijst met de toepassingen van Hallo **Five9 Plus Adapter (CTI, neem contact op met Center-Agents)**.</span><span class="sxs-lookup"><span data-stu-id="d1480-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="d1480-221">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d1480-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d1480-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d1480-223">Click **Add** button.</span></span> <span data-ttu-id="d1480-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1480-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d1480-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1480-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d1480-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1480-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1480-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1480-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1480-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1480-229">Testing single sign-on</span></span>

<span data-ttu-id="d1480-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d1480-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d1480-231">Als u op Hallo Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Five9 Plus Adapter (CTI, neem contact op met Center-Agents)-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1480-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="d1480-232">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1480-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1480-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d1480-233">Additional resources</span></span>

* [<span data-ttu-id="d1480-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1480-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1480-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1480-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

