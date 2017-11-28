---
title: 'Zelfstudie: Azure Active Directory-integratie met Procore SSO | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Procore eenmalige aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="1a1a1-103">Zelfstudie: Azure Active Directory-integratie met Procore SSO</span><span class="sxs-lookup"><span data-stu-id="1a1a1-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="1a1a1-104">In deze zelfstudie leert u hoe toointegrate Procore eenmalige aanmelding bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a1a1-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a1a1-105">Procore SSO integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a1a1-106">U kunt beheren in Azure AD wie toegang tot tooProcore eenmalige aanmelding heeft</span><span class="sxs-lookup"><span data-stu-id="1a1a1-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="1a1a1-107">U kunt uw gebruikers tooautomatically get aangemelde tooProcore SSO (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1a1a1-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a1a1-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a1a1-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1a1a1-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a1a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="1a1a1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a1a1-110">Prerequisites</span></span>

<span data-ttu-id="1a1a1-111">tooconfigure Azure AD-integratie met Procore SSO, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="1a1a1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a1a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a1a1-113">Een Procore SSO eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1a1a1-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a1-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a1a1-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a1a1-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1a1a1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a1a1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a1a1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1a1a1-118">Scenario description</span></span>
<span data-ttu-id="1a1a1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a1a1-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a1a1-121">Het toevoegen van Procore SSO van hello galerie</span><span class="sxs-lookup"><span data-stu-id="1a1a1-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="1a1a1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="1a1a1-123">Het toevoegen van Procore SSO van hello galerie</span><span class="sxs-lookup"><span data-stu-id="1a1a1-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="1a1a1-124">tooconfigure hello integratie van Procore SSO in Azure AD, moet u tooadd Procore SSO van hello galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a1a1-125">**tooadd Procore eenmalige aanmelding via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a1a1-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a1a1-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a1a1-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a1a1-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1a1a1-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1a1a1-133">Typ in het zoekvak Hallo **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-133">In hello search box, type **Procore SSO**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="1a1a1-135">Selecteer in het deelvenster resultaten hello, **Procore SSO**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a1a1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a1a1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Procore eenmalige aanmelding op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a1a1-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Procore SSO is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="1a1a1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Procore SSO toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="1a1a1-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Procore eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="1a1a1-142">tooconfigure en eenmalige aanmelding Azure AD-test met Procore SSO, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a1a1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a1a1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a1a1-145">**[Maken van een testgebruiker Procore SSO](#creating-a-procore-sso-test-user)**  -toohave een equivalent van Britta Simon in Procore eenmalige aanmelding die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1a1a1-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a1a1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a1a1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1a1a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a1a1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Procore eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="1a1a1-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Procore SSO Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1a1a1-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a1a1-151">In hello Azure Management portal op Hallo **Procore SSO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1a1a1-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="1a1a1-155">Op Hallo **Procore SSO-domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="1a1a1-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="1a1a1-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a1a1-161">Op Hallo **Procore SSO configuratie** sectie, klikt u op **Procore eenmalige aanmelding configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1a1a1-162">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1a1a1-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="1a1a1-164">tooconfigure eenmalige aanmelding op **Procore SSO** side, aanmelding tooyour procore bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="1a1a1-165">In Hallo werkset vervolgkeuzelijst omlaag, klikt u op **Admin** tooopen Hallo SSO instellingenpagina.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="1a1a1-167">Hallo-waarden in de vakken Hallo als plakken beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="1a1a1-167">Paste hello values in hello boxes as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="1a1a1-169">a.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-169">a.</span></span> <span data-ttu-id="1a1a1-170">In Hallo **eenmalige aanmelding op URL-verlener** vak, plak Hallo SAML entiteit-ID opgehaald uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="1a1a1-171">b.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-171">b.</span></span> <span data-ttu-id="1a1a1-172">In Hallo **SAML aanmelding op de doel-URL** vak, plak Hallo SAML Single Sign-On Service-URL is gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="1a1a1-173">c.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-173">c.</span></span> <span data-ttu-id="1a1a1-174">Open nu Hallo **Metadata XML** gedownloade hierboven van hello Azure-portal en kopiëren Hallo certificaat in het Hallo-tag met de naam **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="1a1a1-175">Plakken Hallo waarde gekopieerd naar Hallo **certificaat voor eenmalige aanmelding x509** vak.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="1a1a1-176">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="1a1a1-177">Na deze instellingen moet u toosend hello **domeinnaam** (bijvoorbeeld **contoso.com**) via die u aan te bij Procore toohello melden [Procore ondersteuningsteam](https://support.procore.com/) en deze zullen activeren van federatieve SSO voor dat domein.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a1a1-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1a1a1-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a1a1-179">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1a1a1-181">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1a1a1-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a1a1-182">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a1a1-184">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a1a1-186">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a1a1-188">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a1a1-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a1a1-190">a.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-190">a.</span></span> <span data-ttu-id="1a1a1-191">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a1a1-192">b.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-192">b.</span></span> <span data-ttu-id="1a1a1-193">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a1a1-194">c.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-194">c.</span></span> <span data-ttu-id="1a1a1-195">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a1a1-196">d.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-196">d.</span></span> <span data-ttu-id="1a1a1-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="1a1a1-198">Maken van een testgebruiker Procore SSO</span><span class="sxs-lookup"><span data-stu-id="1a1a1-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="1a1a1-199">Volg Hallo onderstaande stappen toocreate een Procore testgebruiker op hun kant.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="1a1a1-200">Aanmelding tooyour procore bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="1a1a1-201">In Hallo werkset vervolgkeuzelijst omlaag, klikt u op **Directory** tooopen Hallo bedrijf directory-pagina.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="1a1a1-203">Klik op **toevoegen van een persoon** optie tooopen Hallo formulier en voert u na de opties - uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a1a1-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="1a1a1-205">a.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-205">a.</span></span> <span data-ttu-id="1a1a1-206">In Hallo **voornaam** tekstvak de voornaam van de gebruiker van het type zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="1a1a1-207">b.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-207">b.</span></span> <span data-ttu-id="1a1a1-208">In Hallo **achternaam** tekstvak de achternaam van de gebruiker van het type zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="1a1a1-209">c.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-209">c.</span></span> <span data-ttu-id="1a1a1-210">In Hallo **e-mailadres** textbox e-mailadres van de gebruiker van het type, zoals  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1a1a1-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="1a1a1-211">d.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-211">d.</span></span> <span data-ttu-id="1a1a1-212">Selecteer **machtigingssjabloon** als **machtigingssjabloon Later toepassen**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="1a1a1-213">e.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-213">e.</span></span> <span data-ttu-id="1a1a1-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-214">Click **Create**.</span></span>

4. <span data-ttu-id="1a1a1-215">Controleer de details en bijwerken Hallo voor toegevoegde Neem contact op met de Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-215">Check and update hello details for hello newly added contact.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="1a1a1-217">Klik op **opslaan en verzenden Invitiation** (als een uitnodiging via e-mail vereist is) of **opslaan** (rechtstreeks opslaan) toocomplete Hallo gebruikersregistratie.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a1a1-219">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a1a1-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a1a1-220">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooProcore SSO verlenen.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1a1a1-222">**tooassign Britta Simon tooProcore SSO, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1a1a1-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a1a1-223">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1a1a1-225">Selecteer in de lijst met de toepassingen van Hallo **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="1a1a1-227">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1a1a1-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-229">Click **Add** button.</span></span> <span data-ttu-id="1a1a1-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1a1a1-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a1a1-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a1a1-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a1a1-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1a1-235">Testing single sign-on</span></span>

<span data-ttu-id="1a1a1-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1a1a1-237">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1a1a1-238">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1a1a1-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="1a1a1-239">Als u op Hallo Procore SSO-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Procore SSO-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a1a1-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a1a1-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1a1a1-240">Additional resources</span></span>

* [<span data-ttu-id="1a1a1-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a1a1-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a1a1-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a1a1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

