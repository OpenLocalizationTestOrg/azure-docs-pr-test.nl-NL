---
title: 'Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Qlik zin Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="2aff0-103">Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise</span><span class="sxs-lookup"><span data-stu-id="2aff0-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="2aff0-104">In deze zelfstudie leert u hoe toointegrate Qlik zin Enterprise met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2aff0-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2aff0-105">Qlik zin Enterprise integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2aff0-106">U kunt beheren in Azure AD die toegang tooQlik Enterprise zin heeft.</span><span class="sxs-lookup"><span data-stu-id="2aff0-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="2aff0-107">U kunt uw gebruikers tooautomatically get aangemelde tooQlik zin Enterprise (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="2aff0-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2aff0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="2aff0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2aff0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2aff0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aff0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2aff0-110">Prerequisites</span></span>

<span data-ttu-id="2aff0-111">Azure AD-integratie met Qlik zin Enterprise tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2aff0-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="2aff0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2aff0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2aff0-113">Een Qlik zin Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2aff0-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2aff0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2aff0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2aff0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2aff0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2aff0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2aff0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2aff0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2aff0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2aff0-118">Scenario description</span></span>
<span data-ttu-id="2aff0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2aff0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2aff0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2aff0-121">Het toevoegen van Qlik zin Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2aff0-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="2aff0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2aff0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="2aff0-123">Het toevoegen van Qlik zin Enterprise van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2aff0-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="2aff0-124">tooconfigure hello integratie van Qlik zin Enterprise in Azure AD, moet u tooadd Qlik zin Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2aff0-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2aff0-125">**tooadd Qlik zin Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2aff0-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2aff0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2aff0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="2aff0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2aff0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="2aff0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2aff0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="2aff0-133">Typ in het zoekvak Hallo **Qlik zin Enterprise**, selecteer **Qlik zin Enterprise** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2aff0-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Qlik zin Enterprise in de lijst met resultaten Hallo](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2aff0-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aff0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2aff0-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Qlik zin Enterprise op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2aff0-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2aff0-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Qlik zin onderneming is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aff0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="2aff0-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Qlik zin onderneming toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2aff0-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="2aff0-139">Wijs in Qlik zin Enterprise, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2aff0-140">tooconfigure en test eenmalige aanmelding Azure AD met Qlik zin voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2aff0-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2aff0-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2aff0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2aff0-143">**[Maak een testgebruiker Qlik zin Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave een equivalent van Britta Simon in Qlik zin onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2aff0-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2aff0-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2aff0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2aff0-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2aff0-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2aff0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2aff0-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Qlik zin Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2aff0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="2aff0-148">**tooconfigure eenmalige aanmelding Azure AD bij Qlik zin Enterprise, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2aff0-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="2aff0-149">In de Azure-portal op Hallo Hallo **Qlik zin Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2aff0-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2aff0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="2aff0-153">Op Hallo **Qlik zin Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en Qlik zin Enterprise domein eenmalige aanmelding informatie](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="2aff0-155">a.</span><span class="sxs-lookup"><span data-stu-id="2aff0-155">a.</span></span> <span data-ttu-id="2aff0-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="2aff0-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2aff0-157">Houd er rekening mee hallo afsluitende slash aan Hallo einde van deze URI.</span><span class="sxs-lookup"><span data-stu-id="2aff0-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="2aff0-158">Dit is vereist.</span><span class="sxs-lookup"><span data-stu-id="2aff0-158">It is required.</span></span>
    
    <span data-ttu-id="2aff0-159">b.</span><span class="sxs-lookup"><span data-stu-id="2aff0-159">b.</span></span> <span data-ttu-id="2aff0-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="2aff0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-161">These values are not real.</span></span> <span data-ttu-id="2aff0-162">Deze waarden met Hallo werkelijke aanmeldings-URL en id, die worden beschreven verderop in deze zelfstudie of neem contact op met update [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2aff0-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="2aff0-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2aff0-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="2aff0-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-165">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2aff0-167">Voorbereiden Hallo federatieve metagegevens-XML-bestand, zodat u die tooQlik zin-server uploaden kunt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2aff0-168">Voordat u uploadt Hallo IdP metagegevens toohello Qlik zin server, moet de Hallo bestand bewerkt toobe tooremove informatie tooensure werking tussen Azure AD en Qlik zin-server.</span><span class="sxs-lookup"><span data-stu-id="2aff0-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="2aff0-170">a.</span><span class="sxs-lookup"><span data-stu-id="2aff0-170">a.</span></span> <span data-ttu-id="2aff0-171">Hallo FederationMetaData.xml bestand, dat u hebt gedownload vanuit Azure-portal in een teksteditor openen.</span><span class="sxs-lookup"><span data-stu-id="2aff0-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="2aff0-172">b.</span><span class="sxs-lookup"><span data-stu-id="2aff0-172">b.</span></span> <span data-ttu-id="2aff0-173">Zoeken naar Hallo waarde **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="2aff0-174">Er zijn vier gegevens (twee paren openen en sluiten elementlabels).</span><span class="sxs-lookup"><span data-stu-id="2aff0-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="2aff0-175">c.</span><span class="sxs-lookup"><span data-stu-id="2aff0-175">c.</span></span> <span data-ttu-id="2aff0-176">Hallo RoleDescriptor tags en alle informatie daartussen in Hallo bestand verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2aff0-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="2aff0-177">d.</span><span class="sxs-lookup"><span data-stu-id="2aff0-177">d.</span></span> <span data-ttu-id="2aff0-178">Hallo-bestand opslaan en deze in de buurt te houden voor gebruik verderop in dit document.</span><span class="sxs-lookup"><span data-stu-id="2aff0-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="2aff0-179">Navigeer toohello Qlik zin Qlik Management Console (QMC) als een gebruiker die virtuele proxyconfiguraties kunt maken.</span><span class="sxs-lookup"><span data-stu-id="2aff0-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="2aff0-180">Hallo QMC, klik op Hallo **virtuele proxy's** menu-item.</span><span class="sxs-lookup"><span data-stu-id="2aff0-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="2aff0-182">Klik onder Hallo van welkomstscherm op Hallo **nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="2aff0-184">welkomstscherm virtuele proxy bewerken wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="2aff0-185">Op Hallo is rechts van welkomstscherm een menu voor het zichtbaar maken van configuratie-opties.</span><span class="sxs-lookup"><span data-stu-id="2aff0-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="2aff0-187">Hallo identificatie menu-optie is ingeschakeld, Voer Hallo identificatiegegevens voor hello Azure virtuele proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="2aff0-189">a.</span><span class="sxs-lookup"><span data-stu-id="2aff0-189">a.</span></span> <span data-ttu-id="2aff0-190">Hallo **beschrijving** veld is een beschrijvende naam voor de virtuele proxyconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2aff0-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="2aff0-191">Voer een waarde voor een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="2aff0-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="2aff0-192">b.</span><span class="sxs-lookup"><span data-stu-id="2aff0-192">b.</span></span> <span data-ttu-id="2aff0-193">Hallo **voorvoegsel** veld identificeert Hallo virtuele proxy eindpunt voor het verbinden van tooQlik zin met Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2aff0-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="2aff0-194">Voer een naam uniek voorvoegsel voor deze virtuele proxy.</span><span class="sxs-lookup"><span data-stu-id="2aff0-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="2aff0-195">c.</span><span class="sxs-lookup"><span data-stu-id="2aff0-195">c.</span></span> <span data-ttu-id="2aff0-196">**Time-out voor inactiviteit sessie (minuten)** Hallo time-out voor verbindingen via deze virtuele proxy is.</span><span class="sxs-lookup"><span data-stu-id="2aff0-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="2aff0-197">d.</span><span class="sxs-lookup"><span data-stu-id="2aff0-197">d.</span></span> <span data-ttu-id="2aff0-198">Hallo **cookie-kop sessienaam** is Hallo cookie naam opslaan Hallo sessie-id voor Hallo Qlik zin sessie een gebruiker na een geslaagde authenticatie ontvangt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="2aff0-199">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="2aff0-199">This name must be unique.</span></span>

12. <span data-ttu-id="2aff0-200">Klik op Hallo verificatie menu optie toomake zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="2aff0-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="2aff0-201">Hallo verificatie scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="2aff0-203">a.</span><span class="sxs-lookup"><span data-stu-id="2aff0-203">a.</span></span> <span data-ttu-id="2aff0-204">Hallo **anonieme toegangsmodus** vervolgkeuzelijst bepaalt als anonieme gebruikers toegang Qlik zin via virtuele Hallo-proxy tot mogelijk.</span><span class="sxs-lookup"><span data-stu-id="2aff0-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="2aff0-205">Hallo standaardoptie is geen anonieme gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2aff0-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="2aff0-206">b.</span><span class="sxs-lookup"><span data-stu-id="2aff0-206">b.</span></span> <span data-ttu-id="2aff0-207">Hallo **verificatiemethode** vervolgkeuzelijst bepaalt Hallo verificatie schema Hallo virtuele proxy wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="2aff0-208">Selecteer SAML in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="2aff0-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="2aff0-209">Meer opties als gevolg hiervan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="2aff0-210">c.</span><span class="sxs-lookup"><span data-stu-id="2aff0-210">c.</span></span> <span data-ttu-id="2aff0-211">In Hallo **SAML host URI veld**, invoer Hallo hostnaam gebruikers invoeren tooaccess Qlik zin via deze virtuele SAML-proxy.</span><span class="sxs-lookup"><span data-stu-id="2aff0-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="2aff0-212">Hallo-hostnaam is Hallo-uri van Hallo Qlik zin-server.</span><span class="sxs-lookup"><span data-stu-id="2aff0-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="2aff0-213">d.</span><span class="sxs-lookup"><span data-stu-id="2aff0-213">d.</span></span> <span data-ttu-id="2aff0-214">In Hallo **SAML entiteit-ID**, Voer Hallo dezelfde waarde die is opgegeven voor veld URI Hallo SAML-host.</span><span class="sxs-lookup"><span data-stu-id="2aff0-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="2aff0-215">e.</span><span class="sxs-lookup"><span data-stu-id="2aff0-215">e.</span></span> <span data-ttu-id="2aff0-216">Hallo **SAML IdP metagegevens** Hallo bestand bewerkt eerder in Hallo **Federatiemetagegevens van Azure AD-configuratie bewerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="2aff0-217">**Voordat u uploadt Hallo IdP metagegevens, Hallo bestand bewerkt toobe moet** tooensure goede werking van tooremove informatie tussen Azure AD en Qlik zin-server.</span><span class="sxs-lookup"><span data-stu-id="2aff0-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="2aff0-218">**Raadpleeg de bovenstaande instructies voor toohello als Hallo bestand heeft nog toobe bewerkt.**</span><span class="sxs-lookup"><span data-stu-id="2aff0-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="2aff0-219">Als Hallo-bestand is bewerkt klikt u op de knop Bladeren Hallo en selecteer Hallo bewerkte metagegevens bestand tooupload het toohello virtuele proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="2aff0-220">f.</span><span class="sxs-lookup"><span data-stu-id="2aff0-220">f.</span></span> <span data-ttu-id="2aff0-221">Hallo naam of het schema kenmerkverwijzing voor Hallo SAML-kenmerk dat vertegenwoordigt Hallo invoeren **UserID** Azure AD toohello Qlik zin server verzendt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="2aff0-222">Schema referentie-informatie is beschikbaar in hello Azure app schermen post-configuratie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="2aff0-223">toouse hello naamkenmerk, voer `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="2aff0-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="2aff0-224">g.</span><span class="sxs-lookup"><span data-stu-id="2aff0-224">g.</span></span> <span data-ttu-id="2aff0-225">Voer Hallo-waarde voor Hallo **gebruikerslijst** die zijn aangesloten toousers tijdens de verificatie tooQlik zin server via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aff0-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="2aff0-226">Hardcoded waarden moeten worden omgeven door **vierkante haakjes []**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="2aff0-227">een kenmerk in hello Azure AD SAML-verklaring verzonden toouse Geef Hallo-naam van Hallo kenmerk in dit tekstvak **zonder** vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="2aff0-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="2aff0-228">h.</span><span class="sxs-lookup"><span data-stu-id="2aff0-228">h.</span></span> <span data-ttu-id="2aff0-229">Hallo **SAML-ondertekeningsalgoritme** sets Hallo serviceprovider (in dit geval Qlik zin server) voor Certificaatondertekening voor Hallo virtuele proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="2aff0-230">Als Qlik zin server gebruikmaakt van een vertrouwd certificaat gegenereerd met behulp van de Microsoft Enhanced RSA and AES Cryptographic Provider, Hallo SAML-ondertekeningsalgoritme ook wijzigen**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="2aff0-231">ik.</span><span class="sxs-lookup"><span data-stu-id="2aff0-231">i.</span></span> <span data-ttu-id="2aff0-232">Hallo SAML kenmerk toewijzing sectie kunt u extra kenmerken zoals groepen toobe verzonden tooQlik zin voor gebruik in regels.</span><span class="sxs-lookup"><span data-stu-id="2aff0-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="2aff0-233">Klik op Hallo **LOAD BALANCING** menu optie toomake deze zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="2aff0-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="2aff0-234">Hallo Load Balancing scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="2aff0-236">Klik op Hallo **toevoegen nieuwe serverknooppunt** knop, selecteer engine knooppunt of knooppunten Qlik zin wordt sessies toofor taakverdeling doeleinden verzenden en klikt u op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="2aff0-238">Klik op Hallo menu Geavanceerd optie toomake zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="2aff0-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="2aff0-239">Hallo geavanceerde scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="2aff0-241">Hallo Host witte lijst identificeert hostnamen die worden geaccepteerd wanneer toohello Qlik zin server verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="2aff0-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="2aff0-242">**Voer Hallo-hostnaam gebruikers opgeven wanneer tooQlik zin server verbinding kunnen maken.**</span><span class="sxs-lookup"><span data-stu-id="2aff0-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="2aff0-243">Hallo-hostnaam is Hallo dezelfde waarde als Hallo SAML host uri zonder Hallo https://.</span><span class="sxs-lookup"><span data-stu-id="2aff0-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="2aff0-244">Klik op Hallo **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="2aff0-246">Klik op OK tooaccept Hallo waarschuwingsbericht weergegeven waarin wordt vermeld proxy's gekoppelde toohello virtuele proxy wordt opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="2aff0-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="2aff0-248">Aan de rechterkant Hallo van welkomstscherm, Hallo gekoppelde items menu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="2aff0-249">Klik op Hallo **proxy's** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="2aff0-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="2aff0-251">Hallo proxy scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-251">hello proxy screen appears.</span></span>  <span data-ttu-id="2aff0-252">Klik op Hallo **koppeling** knop Hallo onder toolink proxy toohello virtuele proxy.</span><span class="sxs-lookup"><span data-stu-id="2aff0-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="2aff0-254">Selecteer Hallo proxyknooppunt dat ondersteuning biedt voor deze virtuele proxyverbinding en klikt u op Hallo **koppeling** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="2aff0-255">Na het koppelen, wordt Hallo proxy vermeld onder de bijbehorende proxy's.</span><span class="sxs-lookup"><span data-stu-id="2aff0-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="2aff0-258">Nadat het over vijf tooten seconden Hallo vernieuwen QMC bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2aff0-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="2aff0-259">Klik op Hallo **QMC vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="2aff0-261">Wanneer Hallo QMC is vernieuwd, klikt u op Hallo **virtuele proxy's** menu-item.</span><span class="sxs-lookup"><span data-stu-id="2aff0-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="2aff0-262">Hallo nieuwe SAML virtuele proxy vermelding wordt vermeld in de tabel Hallo op het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="2aff0-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="2aff0-263">Één klik op Hallo virtuele proxy vermelding.</span><span class="sxs-lookup"><span data-stu-id="2aff0-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="2aff0-265">Hallo onderaan welkomstscherm in wordt Hallo downloaden SP metagegevens knop geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2aff0-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="2aff0-266">Klik op Hallo **downloaden SP metagegevens** knop toosave hello tooa bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="2aff0-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="2aff0-268">Open Hallo sp metagegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="2aff0-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="2aff0-269">Houd rekening met Hallo **id van de entiteit** post en Hallo **AssertionConsumerService** vermelding.</span><span class="sxs-lookup"><span data-stu-id="2aff0-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="2aff0-270">Deze waarden zijn equivalent toohello **id** en Hallo **aanmelden URL** in de configuratie van de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aff0-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="2aff0-271">Plak deze waarden in Hallo **Qlik zin Enterprise domein en de URL's** sectie in de toepassingsconfiguratie hello Azure AD als ze niet overeen komen en vervolgens moet u ze in Azure AD-App-configuratiewizard Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="2aff0-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="2aff0-273">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2aff0-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2aff0-274">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2aff0-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2aff0-275">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2aff0-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2aff0-276">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2aff0-276">Create an Azure AD test user</span></span>
<span data-ttu-id="2aff0-277">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2aff0-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="2aff0-279">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2aff0-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2aff0-280">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![Hello Azure Active Directory-knop](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2aff0-282">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2aff0-284">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2aff0-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![knop voor Hallo toevoegen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2aff0-286">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2aff0-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="2aff0-288">a.</span><span class="sxs-lookup"><span data-stu-id="2aff0-288">a.</span></span> <span data-ttu-id="2aff0-289">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="2aff0-290">b.</span><span class="sxs-lookup"><span data-stu-id="2aff0-290">b.</span></span> <span data-ttu-id="2aff0-291">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="2aff0-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="2aff0-292">c.</span><span class="sxs-lookup"><span data-stu-id="2aff0-292">c.</span></span> <span data-ttu-id="2aff0-293">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="2aff0-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="2aff0-294">d.</span><span class="sxs-lookup"><span data-stu-id="2aff0-294">d.</span></span> <span data-ttu-id="2aff0-295">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="2aff0-296">Maak een testgebruiker Qlik zin Enterprise</span><span class="sxs-lookup"><span data-stu-id="2aff0-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="2aff0-297">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Qlik zin onderneming maken.</span><span class="sxs-lookup"><span data-stu-id="2aff0-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="2aff0-298">Werken met [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) Hallo gebruikers toevoegen in Hallo Qlik zin Enterprise-platform.</span><span class="sxs-lookup"><span data-stu-id="2aff0-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="2aff0-299">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2aff0-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2aff0-300">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aff0-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2aff0-301">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooQlik zin Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2aff0-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="2aff0-303">**tooassign Britta Simon tooQlik zin Enterprise, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2aff0-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="2aff0-304">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2aff0-306">Selecteer in de lijst met de toepassingen van Hallo **Qlik zin Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Hallo Qlik zin Enterprise koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="2aff0-308">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2aff0-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="2aff0-310">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2aff0-310">Click **Add** button.</span></span> <span data-ttu-id="2aff0-311">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2aff0-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="2aff0-313">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2aff0-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2aff0-314">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2aff0-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2aff0-315">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2aff0-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2aff0-316">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2aff0-316">Test single sign-on</span></span>

<span data-ttu-id="2aff0-317">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2aff0-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2aff0-318">Als u op Hallo Qlik zin Enterprise-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Qlik zin bedrijfstoepassing.</span><span class="sxs-lookup"><span data-stu-id="2aff0-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2aff0-319">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2aff0-319">Additional resources</span></span>

* [<span data-ttu-id="2aff0-320">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2aff0-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2aff0-321">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2aff0-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

