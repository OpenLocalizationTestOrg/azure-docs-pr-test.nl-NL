---
title: 'Zelfstudie: Azure Active Directory-integratie met ADP eTime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ADP eTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="97b81-103">Zelfstudie: Azure Active Directory-integratie met ADP eTime</span><span class="sxs-lookup"><span data-stu-id="97b81-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="97b81-104">In deze zelfstudie leert u hoe toointegrate ADP eTime met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97b81-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97b81-105">ADP eTime integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="97b81-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="97b81-106">U kunt beheren in Azure AD wie toegang tot tooADP eTime heeft</span><span class="sxs-lookup"><span data-stu-id="97b81-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="97b81-107">U kunt uw gebruikers tooautomatically get aangemelde tooADP eTime (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="97b81-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97b81-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="97b81-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="97b81-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97b81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97b81-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97b81-110">Prerequisites</span></span>

<span data-ttu-id="97b81-111">Azure AD-integratie met ADP eTime tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="97b81-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="97b81-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="97b81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97b81-113">Een ADP eTime eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="97b81-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97b81-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="97b81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97b81-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="97b81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97b81-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="97b81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97b81-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97b81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97b81-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="97b81-118">Scenario description</span></span>
<span data-ttu-id="97b81-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="97b81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97b81-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="97b81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97b81-121">Het toevoegen van ADP eTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="97b81-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="97b81-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="97b81-123">Het toevoegen van ADP eTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="97b81-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="97b81-124">tooconfigure hello integratie van ADP eTime in Azure AD, moet u tooadd ADP eTime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="97b81-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97b81-125">**tooadd ADP eTime via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97b81-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b81-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97b81-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97b81-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b81-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="97b81-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b81-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="97b81-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b81-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="97b81-133">Typ in het zoekvak Hallo **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="97b81-133">In hello search box, type **ADP eTime**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="97b81-135">Selecteer in het deelvenster resultaten hello, **ADP eTime**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="97b81-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97b81-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97b81-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ADP eTime op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="97b81-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97b81-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ADP eTime is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b81-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="97b81-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ADP eTime toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="97b81-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="97b81-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="97b81-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="97b81-142">tooconfigure en eenmalige aanmelding Azure AD-test met ADP eTime, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97b81-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="97b81-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="97b81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="97b81-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97b81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97b81-145">**[Maken van een gebruiker ADP eTime test](#creating-an-adp-etime-test-user)**  -toohave een equivalent van Britta Simon in ADP eTime die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="97b81-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="97b81-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="97b81-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97b81-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="97b81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97b81-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="97b81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97b81-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw ADP eTime-toepassing.</span><span class="sxs-lookup"><span data-stu-id="97b81-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="97b81-150">**Voer tooconfigure Azure AD eenmalige aanmelding met ADP eTime, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97b81-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b81-151">In de Azure-portal op Hallo Hallo **ADP eTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="97b81-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="97b81-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="97b81-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="97b81-155">Op Hallo **ADP eTime domein en URL's** sectie, voert u Hallo stap:</span><span class="sxs-lookup"><span data-stu-id="97b81-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="97b81-157">a.</span><span class="sxs-lookup"><span data-stu-id="97b81-157">a.</span></span> <span data-ttu-id="97b81-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="97b81-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="97b81-159">b.</span><span class="sxs-lookup"><span data-stu-id="97b81-159">b.</span></span> <span data-ttu-id="97b81-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="97b81-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="97b81-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="97b81-161">These values are not hello real.</span></span> <span data-ttu-id="97b81-162">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="97b81-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="97b81-163">Neem contact op met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="97b81-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="97b81-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="97b81-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="97b81-166">Hallo ADP eTime toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="97b81-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="97b81-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="97b81-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="97b81-168">Hallo claimnaam altijd worden **'PersonImmutableID'** en het Hallo-waarde die we tooExtensionAttribute2 waarin hebt toegewezen werknemer-id van gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="97b81-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="97b81-169">Hier Hallo gebruiker toewijzen van Azure AD tooADP eTime op Hallo werknemer-id wordt uitgevoerd, maar kunt u deze tooa van een andere waarde ook op basis van de toepassingsinstellingen van uw toewijzen.</span><span class="sxs-lookup"><span data-stu-id="97b81-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="97b81-170">Dus neem werk met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) eerste toouse Hallo juiste id van een gebruiker en wijs die waarde met de Hallo **'PersonImmutableID'** claim.</span><span class="sxs-lookup"><span data-stu-id="97b81-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="97b81-172">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97b81-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="97b81-173">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="97b81-173">Attribute Name</span></span> | <span data-ttu-id="97b81-174">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="97b81-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="97b81-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="97b81-175">PersonImmutableID</span></span> | <span data-ttu-id="97b81-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="97b81-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="97b81-177">a.</span><span class="sxs-lookup"><span data-stu-id="97b81-177">a.</span></span> <span data-ttu-id="97b81-178">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b81-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="97b81-181">b.</span><span class="sxs-lookup"><span data-stu-id="97b81-181">b.</span></span> <span data-ttu-id="97b81-182">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="97b81-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="97b81-183">c.</span><span class="sxs-lookup"><span data-stu-id="97b81-183">c.</span></span> <span data-ttu-id="97b81-184">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="97b81-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="97b81-185">d.</span><span class="sxs-lookup"><span data-stu-id="97b81-185">d.</span></span> <span data-ttu-id="97b81-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="97b81-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97b81-187">Voordat u de SAML-verklaring Hallo configureren kunt, moet u toocontact uw [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="97b81-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="97b81-188">U moet deze waarde tooconfigure Hallo aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="97b81-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="97b81-189">Op Hallo **ADP eTime configuratie** sectie, klikt u op **ADP configureren eTime** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="97b81-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="97b81-191">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="97b81-191">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="97b81-193">tooconfigure eenmalige aanmelding op **ADP eTime** zijde, moet u toosend Hallo gedownload **Metadata XML** te[ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="97b81-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="97b81-194">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="97b81-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="97b81-195">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="97b81-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="97b81-196">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97b81-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97b81-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="97b81-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="97b81-198">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="97b81-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="97b81-200">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97b81-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b81-201">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97b81-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97b81-203">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="97b81-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97b81-205">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="97b81-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97b81-207">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97b81-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97b81-209">a.</span><span class="sxs-lookup"><span data-stu-id="97b81-209">a.</span></span> <span data-ttu-id="97b81-210">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97b81-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97b81-211">b.</span><span class="sxs-lookup"><span data-stu-id="97b81-211">b.</span></span> <span data-ttu-id="97b81-212">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97b81-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97b81-213">c.</span><span class="sxs-lookup"><span data-stu-id="97b81-213">c.</span></span> <span data-ttu-id="97b81-214">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="97b81-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="97b81-215">d.</span><span class="sxs-lookup"><span data-stu-id="97b81-215">d.</span></span> <span data-ttu-id="97b81-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="97b81-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="97b81-217">Maken van een gebruiker ADP eTime testen</span><span class="sxs-lookup"><span data-stu-id="97b81-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="97b81-218">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in ADP eTime van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="97b81-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="97b81-219">Werken met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) tooadd Hallo gebruikers in Hallo ADP eTime-account.</span><span class="sxs-lookup"><span data-stu-id="97b81-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="97b81-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b81-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="97b81-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="97b81-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="97b81-223">**tooassign Britta Simon tooADP eTime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97b81-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b81-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97b81-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="97b81-226">Selecteer in de lijst met de toepassingen van Hallo **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="97b81-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="97b81-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="97b81-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="97b81-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="97b81-230">Click **Add** button.</span></span> <span data-ttu-id="97b81-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b81-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="97b81-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="97b81-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="97b81-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b81-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97b81-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97b81-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97b81-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97b81-236">Testing single sign-on</span></span>

<span data-ttu-id="97b81-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="97b81-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="97b81-238">Als u op Hallo ADP eTime tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ADP eTime toepassing.</span><span class="sxs-lookup"><span data-stu-id="97b81-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="97b81-239">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97b81-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="97b81-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="97b81-240">Additional resources</span></span>

* [<span data-ttu-id="97b81-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97b81-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97b81-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97b81-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

