---
title: 'Zelfstudie: Azure Active Directory-integratie met ADP Globalview | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ADP Globalview.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="4dd7c-103">Zelfstudie: Azure Active Directory-integratie met ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="4dd7c-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="4dd7c-104">In deze zelfstudie leert u hoe toointegrate ADP Globalview met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4dd7c-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4dd7c-105">ADP Globalview integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4dd7c-106">U kunt beheren in Azure AD wie toegang tot tooADP Globalview heeft</span><span class="sxs-lookup"><span data-stu-id="4dd7c-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="4dd7c-107">U kunt uw gebruikers tooautomatically get aangemelde tooADP Globalview (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4dd7c-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4dd7c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4dd7c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4dd7c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4dd7c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dd7c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4dd7c-110">Prerequisites</span></span>

<span data-ttu-id="4dd7c-111">Azure AD-integratie met ADP Globalview tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="4dd7c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4dd7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4dd7c-113">Een ADP Globalview eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4dd7c-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4dd7c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4dd7c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4dd7c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4dd7c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4dd7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4dd7c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4dd7c-118">Scenario description</span></span>
<span data-ttu-id="4dd7c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4dd7c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4dd7c-121">Het toevoegen van ADP Globalview van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4dd7c-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="4dd7c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4dd7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="4dd7c-123">Het toevoegen van ADP Globalview van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4dd7c-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="4dd7c-124">tooconfigure hello integratie van ADP Globalview in Azure AD, moet u tooadd ADP Globalview uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4dd7c-125">**tooadd ADP Globalview via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4dd7c-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4dd7c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4dd7c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4dd7c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4dd7c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4dd7c-133">Typ in het zoekvak Hallo **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="4dd7c-135">Selecteer in het deelvenster resultaten hello, **ADP Globalview**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4dd7c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4dd7c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4dd7c-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met ADP Globalview op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4dd7c-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4dd7c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ADP Globalview is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="4dd7c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ADP Globalview toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="4dd7c-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="4dd7c-142">tooconfigure en eenmalige aanmelding Azure AD-test met ADP Globalview, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4dd7c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4dd7c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4dd7c-145">**[Maken van een testgebruiker ADP Globalview](#creating-an-adp-globalview-test-user)**  -toohave een equivalent van Britta Simon in ADP Globalview die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4dd7c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4dd7c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4dd7c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4dd7c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4dd7c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ADP Globalview configureren.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="4dd7c-150">**Voer tooconfigure Azure AD eenmalige aanmelding met ADP Globalview, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4dd7c-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="4dd7c-151">In de Azure-portal op Hallo Hallo **ADP Globalview** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4dd7c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="4dd7c-155">Op Hallo **ADP Globalview domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="4dd7c-157">In Hallo **id** textbox, typ een URL met Hallo patroon volgen: `https://<subdomain>.globalview.adp.com/federate` of`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="4dd7c-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd7c-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-158">hello value is not real.</span></span> <span data-ttu-id="4dd7c-159">Hallo-waarde met de Hallo bijwerken werkelijke id.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="4dd7c-160">Neem contact op met [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="4dd7c-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="4dd7c-163">Hallo ADP GlobalView toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="4dd7c-164">Hallo volgende Schermafbeelding toont een voorbeeld voor het.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="4dd7c-165">Hallo claim namen altijd worden **'PersonImmutableID'** en het Hallo-waarde die we tooExtensionAttribute2 waarin hebt toegewezen werknemer-id van gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="4dd7c-166">Hier Hallo gebruiker toewijzen van Azure AD-tooADP GlobalView op Hallo werknemer-id wordt gedaan, maar u tooa andere waarde ook op basis van de instellingen van de toepassing kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="4dd7c-167">U kunt werkt met Hallo ADP GlobalView team eerste toouse Hallo juiste id van een gebruiker en wijs die waarde met de Hallo **'PersonImmutableID'** claim.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="4dd7c-168">U kunt ook Hallo e-mail en UserID claim zoals in afbeelding Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="4dd7c-170">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4dd7c-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="4dd7c-171">Attribute Name</span></span> | <span data-ttu-id="4dd7c-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="4dd7c-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="4dd7c-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="4dd7c-173">personalimmutableid</span></span> | <span data-ttu-id="4dd7c-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="4dd7c-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="4dd7c-175">E-mail</span><span class="sxs-lookup"><span data-stu-id="4dd7c-175">email</span></span>               | <span data-ttu-id="4dd7c-176">User.mail</span><span class="sxs-lookup"><span data-stu-id="4dd7c-176">user.mail</span></span> |
    | <span data-ttu-id="4dd7c-177">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="4dd7c-177">userid</span></span>              | <span data-ttu-id="4dd7c-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="4dd7c-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="4dd7c-179">a.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-179">a.</span></span> <span data-ttu-id="4dd7c-180">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4dd7c-183">b.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-183">b.</span></span> <span data-ttu-id="4dd7c-184">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4dd7c-185">c.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-185">c.</span></span> <span data-ttu-id="4dd7c-186">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4dd7c-187">d.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-187">d.</span></span> <span data-ttu-id="4dd7c-188">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd7c-189">Voordat u de SAML-verklaring Hallo configureren kunt, moet u toocontact uw [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="4dd7c-190">U moet deze waarde tooconfigure Hallo aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="4dd7c-191">Op Hallo **ADP Globalview configuratie** sectie, klikt u op **configureren ADP Globalview** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4dd7c-192">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4dd7c-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="4dd7c-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="4dd7c-196">tooconfigure eenmalige aanmelding op **ADP Globalview** zijde, moet u toosend Hallo gedownload **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dd7c-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="4dd7c-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4dd7c-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4dd7c-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4dd7c-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4dd7c-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4dd7c-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4dd7c-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4dd7c-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4dd7c-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4dd7c-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="4dd7c-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4dd7c-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4dd7c-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4dd7c-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4dd7c-212">a.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-212">a.</span></span> <span data-ttu-id="4dd7c-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4dd7c-214">b.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-214">b.</span></span> <span data-ttu-id="4dd7c-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4dd7c-216">c.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-216">c.</span></span> <span data-ttu-id="4dd7c-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4dd7c-218">d.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-218">d.</span></span> <span data-ttu-id="4dd7c-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="4dd7c-220">Een testgebruiker ADP Globalview maken</span><span class="sxs-lookup"><span data-stu-id="4dd7c-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="4dd7c-221">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in ADP GlobalView van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="4dd7c-222">Werken met [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) tooadd Hallo gebruikers in Hallo ADP GlobalView-account.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4dd7c-223">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4dd7c-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4dd7c-224">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4dd7c-226">**tooassign Britta Simon tooADP Globalview, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4dd7c-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="4dd7c-227">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4dd7c-229">Selecteer in de lijst met de toepassingen van Hallo **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="4dd7c-231">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4dd7c-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-233">Click **Add** button.</span></span> <span data-ttu-id="4dd7c-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4dd7c-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4dd7c-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4dd7c-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4dd7c-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4dd7c-239">Testing single sign-on</span></span>

<span data-ttu-id="4dd7c-240">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4dd7c-241">Als u op Hallo ADP GlobalView-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ADP GlobalView toepassing.</span><span class="sxs-lookup"><span data-stu-id="4dd7c-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4dd7c-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4dd7c-242">Additional resources</span></span>

* [<span data-ttu-id="4dd7c-243">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dd7c-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4dd7c-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4dd7c-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

