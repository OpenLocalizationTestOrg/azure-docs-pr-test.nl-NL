---
title: 'Zelfstudie: Azure Active Directory-integratie met Autotask werkplek | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Autotask werkplek.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="2bf93-103">Zelfstudie: Azure Active Directory-integratie met Autotask werkplek</span><span class="sxs-lookup"><span data-stu-id="2bf93-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="2bf93-104">In deze zelfstudie leert u hoe toointegrate Autotask werkplek met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bf93-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bf93-105">Autotask werkplek integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2bf93-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2bf93-106">U kunt beheren in Azure AD wie toegang tot tooAutotask werkplek heeft</span><span class="sxs-lookup"><span data-stu-id="2bf93-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="2bf93-107">U kunt uw gebruikers tooautomatically get aangemelde tooAutotask werkplek (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2bf93-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bf93-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2bf93-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2bf93-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bf93-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bf93-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2bf93-110">Prerequisites</span></span>

<span data-ttu-id="2bf93-111">Azure AD-integratie met Autotask werkplek tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2bf93-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="2bf93-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2bf93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bf93-113">Een Autotask werkplek eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2bf93-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="2bf93-114">U moet een beheerder of super-beheerder in de werkplek.</span><span class="sxs-lookup"><span data-stu-id="2bf93-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="2bf93-115">U moet een administrator-account hebben in hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bf93-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="2bf93-116">Hallo-gebruikers die deze functie maakt gebruik van een account binnen werkplek en hello Azure AD en hun e-mailadressen voor beide moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="2bf93-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf93-117">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bf93-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bf93-118">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2bf93-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bf93-119">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2bf93-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bf93-120">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bf93-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bf93-121">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2bf93-121">Scenario description</span></span>
<span data-ttu-id="2bf93-122">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2bf93-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bf93-123">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2bf93-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bf93-124">Het toevoegen van Autotask werkplek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2bf93-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="2bf93-125">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bf93-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="2bf93-126">Het toevoegen van Autotask werkplek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2bf93-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="2bf93-127">tooconfigure hello integratie van Autotask werkplek in Azure AD, moet u tooadd Autotask werkplek uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2bf93-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2bf93-128">**tooadd Autotask werkplek via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bf93-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bf93-129">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2bf93-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="2bf93-131">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2bf93-132">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-132">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="2bf93-134">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bf93-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="2bf93-136">Typ in het zoekvak Hallo **Autotask werkplek**, selecteer **Autotask werkplek** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bf93-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met zoekresultaten Autotask werkplek in Hallo](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2bf93-138">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bf93-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2bf93-139">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD bij Autotask werkplek op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2bf93-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2bf93-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Autotask werkplek is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bf93-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="2bf93-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Autotask werkplek toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2bf93-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="2bf93-142">Op de werkplek Autotask, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2bf93-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2bf93-143">tooconfigure en test eenmalige aanmelding Azure AD bij Autotask werkplek, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bf93-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2bf93-144">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2bf93-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2bf93-145">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bf93-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bf93-146">**[Maken van een testgebruiker Autotask werkplek](#create-an-autotask-workplace-test-user)**  -toohave een equivalent van Britta Simon in Autotask werkplek die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2bf93-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bf93-147">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2bf93-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bf93-148">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2bf93-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2bf93-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2bf93-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2bf93-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Autotask werkplek.</span><span class="sxs-lookup"><span data-stu-id="2bf93-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="2bf93-151">**Voer tooconfigure Azure AD eenmalige aanmelding bij Autotask werkplek, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bf93-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bf93-152">In de Azure-portal op Hallo Hallo **Autotask werkplek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2bf93-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2bf93-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="2bf93-156">U kunt eventueel tooconfigure Hallo toepassing in **IDP** geïnitieerd modus uitvoeren van de volgende stappen uit op Hallo Hallo **Autotask werkplek domein en de URL's** sectie:</span><span class="sxs-lookup"><span data-stu-id="2bf93-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Autotask werkplek domein en URL's eenmalige aanmelding-informatie voor IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="2bf93-158">a.</span><span class="sxs-lookup"><span data-stu-id="2bf93-158">a.</span></span> <span data-ttu-id="2bf93-159">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="2bf93-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="2bf93-160">b.</span><span class="sxs-lookup"><span data-stu-id="2bf93-160">b.</span></span> <span data-ttu-id="2bf93-161">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2bf93-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="2bf93-162">Indien gewenst tooconfigure Hallo toepassing in **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2bf93-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Autotask werkplek domein en URL's eenmalige aanmelding-informatie voor SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="2bf93-164">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="2bf93-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2bf93-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2bf93-165">These values are not real.</span></span> <span data-ttu-id="2bf93-166">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="2bf93-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2bf93-167">Neem contact op met [Autotask werkplek Client ondersteuningsteam](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2bf93-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="2bf93-168">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2bf93-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="2bf93-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2bf93-170">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2bf93-172">In een ander browservenster Hallo logboek aan tooWorkplace Online met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="2bf93-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="2bf93-173">Wanneer u Hallo IdP configureert, moet een subdomein toobe opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2bf93-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="2bf93-174">tooconfirm hello juist subdomein, aanmelding tooWorkplace Online.</span><span class="sxs-lookup"><span data-stu-id="2bf93-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="2bf93-175">Nadat u bent aangemeld, moet u Opmerking toohello subdomein in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="2bf93-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="2bf93-176">Hallo subdomein hello deel uitmaakt tussen Hallo 'https://' en '.awp.autotask.net/' en moet ons, eu, ca of Australië.</span><span class="sxs-lookup"><span data-stu-id="2bf93-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="2bf93-177">Ga te**configuratie** > **Single Sign-On** en Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2bf93-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Autotask Single Sign-on-configuratie](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="2bf93-179">a.</span><span class="sxs-lookup"><span data-stu-id="2bf93-179">a.</span></span> <span data-ttu-id="2bf93-180">Selecteer Hallo **XML-bestand met metagegevens** optie en vervolgens uploaden Hallo **Metadata XML** gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2bf93-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="2bf93-181">b.</span><span class="sxs-lookup"><span data-stu-id="2bf93-181">b.</span></span> <span data-ttu-id="2bf93-182">Klik op **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-182">Click **Enable SSO**.</span></span>
    
    ![Configuratie goedkeuren Autotask voor eenmalige aanmelding](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="2bf93-184">c.</span><span class="sxs-lookup"><span data-stu-id="2bf93-184">c.</span></span> <span data-ttu-id="2bf93-185">Selecteer Hallo **bevestig ik deze informatie juist is en deze IdP vertrouwde** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2bf93-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="2bf93-186">d.</span><span class="sxs-lookup"><span data-stu-id="2bf93-186">d.</span></span> <span data-ttu-id="2bf93-187">Klik op **goedkeuren**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="2bf93-188">Als u hulp bij het configureren van Autotask werkplek nodig hebt, raadpleegt u [deze pagina](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget hulp bij uw werkplekaccount.</span><span class="sxs-lookup"><span data-stu-id="2bf93-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="2bf93-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2bf93-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2bf93-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2bf93-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2bf93-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bf93-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2bf93-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2bf93-192">Create an Azure AD test user</span></span>

<span data-ttu-id="2bf93-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2bf93-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="2bf93-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bf93-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bf93-196">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="2bf93-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2bf93-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2bf93-200">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bf93-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2bf93-202">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2bf93-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2bf93-204">a.</span><span class="sxs-lookup"><span data-stu-id="2bf93-204">a.</span></span> <span data-ttu-id="2bf93-205">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bf93-206">b.</span><span class="sxs-lookup"><span data-stu-id="2bf93-206">b.</span></span> <span data-ttu-id="2bf93-207">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="2bf93-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2bf93-208">c.</span><span class="sxs-lookup"><span data-stu-id="2bf93-208">c.</span></span> <span data-ttu-id="2bf93-209">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="2bf93-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2bf93-210">d.</span><span class="sxs-lookup"><span data-stu-id="2bf93-210">d.</span></span> <span data-ttu-id="2bf93-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="2bf93-212">Maken van een testgebruiker Autotask werkplek</span><span class="sxs-lookup"><span data-stu-id="2bf93-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="2bf93-213">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Autotask maken.</span><span class="sxs-lookup"><span data-stu-id="2bf93-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="2bf93-214">Neem contact op met [Autotask werkplek ondersteuningsteam](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd Hallo gebruikers in Hallo Autotask werkplek platform.</span><span class="sxs-lookup"><span data-stu-id="2bf93-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2bf93-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bf93-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2bf93-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAutotask werkplek.</span><span class="sxs-lookup"><span data-stu-id="2bf93-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="2bf93-218">**tooassign Britta Simon tooAutotask werkplek, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2bf93-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bf93-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2bf93-221">Selecteer in de lijst met de toepassingen van Hallo **Autotask werkplek**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![Hallo Autotask werkplek koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="2bf93-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2bf93-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="2bf93-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2bf93-225">Click **Add** button.</span></span> <span data-ttu-id="2bf93-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bf93-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="2bf93-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2bf93-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2bf93-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bf93-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bf93-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2bf93-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2bf93-231">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2bf93-231">Test single sign-on</span></span>

<span data-ttu-id="2bf93-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2bf93-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2bf93-233">Als u op Hallo Autotask werkplek-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Autotask werkplek toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bf93-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="2bf93-234">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2bf93-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bf93-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2bf93-235">Additional resources</span></span>

* [<span data-ttu-id="2bf93-236">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bf93-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bf93-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bf93-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

