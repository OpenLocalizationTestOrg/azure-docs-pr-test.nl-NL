---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceChannel | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ServiceChannel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="a435e-103">Zelfstudie: Azure Active Directory-integratie met ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="a435e-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="a435e-104">In deze zelfstudie leert u hoe toointegrate ServiceChannel met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a435e-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a435e-105">ServiceChannel integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a435e-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a435e-106">U kunt beheren in Azure AD die tooServiceChannel toegang heeft</span><span class="sxs-lookup"><span data-stu-id="a435e-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="a435e-107">U kunt uw gebruikers tooautomatically get aangemelde tooServiceChannel (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a435e-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a435e-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="a435e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="a435e-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a435e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a435e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a435e-110">Prerequisites</span></span>

<span data-ttu-id="a435e-111">Azure AD-integratie met ServiceChannel tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a435e-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="a435e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a435e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a435e-113">Een ServiceChannel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a435e-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a435e-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a435e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a435e-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a435e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a435e-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a435e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a435e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a435e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a435e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a435e-118">Scenario description</span></span>
<span data-ttu-id="a435e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a435e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a435e-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a435e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a435e-121">Het toevoegen van ServiceChannel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a435e-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="a435e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a435e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="a435e-123">Het toevoegen van ServiceChannel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="a435e-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="a435e-124">tooconfigure hello integratie van ServiceChannel in Azure AD, moet u tooadd ServiceChannel uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a435e-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a435e-125">**tooadd ServiceChannel via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a435e-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a435e-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a435e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a435e-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a435e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a435e-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a435e-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a435e-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="a435e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a435e-133">Typ in het zoekvak Hallo **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="a435e-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="a435e-135">Selecteer in het deelvenster resultaten hello, **ServiceChannel**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a435e-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a435e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a435e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a435e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met ServiceChannel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a435e-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a435e-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ServiceChannel is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a435e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="a435e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in ServiceChannel toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="a435e-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="a435e-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="a435e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="a435e-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van ServiceChannel, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a435e-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a435e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="a435e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a435e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a435e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a435e-145">**[Maken van een testgebruiker ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a435e-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="a435e-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a435e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a435e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a435e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a435e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a435e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a435e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing ServiceChannel configureren.</span><span class="sxs-lookup"><span data-stu-id="a435e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="a435e-150">**Azure AD tooconfigure eenmalige aanmelding met ServiceChannel, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a435e-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="a435e-151">In hello Azure Management portal op Hallo **ServiceChannel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a435e-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a435e-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a435e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="a435e-155">Op Hallo **ServiceChannel-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a435e-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="a435e-157">a.</span><span class="sxs-lookup"><span data-stu-id="a435e-157">a.</span></span> <span data-ttu-id="a435e-158">In Hallo **id** textbox Hallo typewaarde als:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="a435e-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="a435e-159">b.</span><span class="sxs-lookup"><span data-stu-id="a435e-159">b.</span></span> <span data-ttu-id="a435e-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="a435e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a435e-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="a435e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="a435e-162">U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate.</span><span class="sxs-lookup"><span data-stu-id="a435e-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a435e-163">We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id.</span><span class="sxs-lookup"><span data-stu-id="a435e-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="a435e-164">Neem contact op met [ServiceChannel ondersteuningsteam](https://servicechannel.zendesk.com/hc/en-us) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a435e-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="a435e-165">Uw toepassing ServiceChannel verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="a435e-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="a435e-166">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="a435e-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="a435e-167">**NameIdentifier (gebruikers-id)** is alleen verplichte claim Hallo en Hallo standaardwaarde is **user.userprincipalname** maar ServiceChannel verwacht deze toegewezen met toobe **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a435e-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="a435e-168">Als u van plan bent tooenable NET In Time gebruikers inrichten, moet u Hallo claims zoals hieronder wordt weergegeven na toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a435e-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="a435e-169">**Rol** claim moet toobe te toegewezen**user.assignedroles** die Hallo-rol van Hallo gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="a435e-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="a435e-170">U kunt verwijzen ServiceChannel handleiding [hier](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) voor meer informatie over claims.</span><span class="sxs-lookup"><span data-stu-id="a435e-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="a435e-172">Klik op de [hier](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow hoe tooconfigure **rol** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="a435e-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="a435e-173">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="a435e-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="a435e-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="a435e-174">Attribute Name</span></span> | <span data-ttu-id="a435e-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="a435e-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="a435e-176">Rol</span><span class="sxs-lookup"><span data-stu-id="a435e-176">Role</span></span>| <span data-ttu-id="a435e-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="a435e-177">user.assignedroles</span></span> |

    <span data-ttu-id="a435e-178">a.</span><span class="sxs-lookup"><span data-stu-id="a435e-178">a.</span></span> <span data-ttu-id="a435e-179">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a435e-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="a435e-182">b.</span><span class="sxs-lookup"><span data-stu-id="a435e-182">b.</span></span> <span data-ttu-id="a435e-183">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="a435e-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a435e-184">c.</span><span class="sxs-lookup"><span data-stu-id="a435e-184">c.</span></span> <span data-ttu-id="a435e-185">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="a435e-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a435e-186">d.</span><span class="sxs-lookup"><span data-stu-id="a435e-186">d.</span></span> <span data-ttu-id="a435e-187">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="a435e-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="a435e-188">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a435e-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="a435e-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a435e-190">Click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a435e-192">Op Hallo **ServiceChannel configuratie** sectie, klikt u op **configureren ServiceChannel** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a435e-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a435e-193">Houd er rekening mee Hallo **SAML Enitity ID** van Hallo **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="a435e-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="a435e-194">tooconfigure eenmalige aanmelding op **ServiceChannel** zijde, moet u toosend Hallo gedownload **certificaat (Base64)** en **SAML entiteit-ID** te[ Het ondersteuningsteam van ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="a435e-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="a435e-195">Ze stelt deze in volgorde toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="a435e-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a435e-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a435e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a435e-197">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a435e-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a435e-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a435e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a435e-200">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a435e-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a435e-202">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a435e-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a435e-204">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a435e-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a435e-206">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a435e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a435e-208">a.</span><span class="sxs-lookup"><span data-stu-id="a435e-208">a.</span></span> <span data-ttu-id="a435e-209">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a435e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a435e-210">b.</span><span class="sxs-lookup"><span data-stu-id="a435e-210">b.</span></span> <span data-ttu-id="a435e-211">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a435e-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a435e-212">c.</span><span class="sxs-lookup"><span data-stu-id="a435e-212">c.</span></span> <span data-ttu-id="a435e-213">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a435e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a435e-214">d.</span><span class="sxs-lookup"><span data-stu-id="a435e-214">d.</span></span> <span data-ttu-id="a435e-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a435e-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="a435e-216">Een testgebruiker ServiceChannel maken</span><span class="sxs-lookup"><span data-stu-id="a435e-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="a435e-217">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a435e-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="a435e-218">Voor volledige gebruikersinrichting, neem contact op met [ondersteuningsteam ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="a435e-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a435e-219">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a435e-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a435e-220">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooServiceChannel toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="a435e-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a435e-222">**tooassign Britta Simon tooServiceChannel, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="a435e-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="a435e-223">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a435e-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a435e-225">Selecteer in de lijst met de toepassingen van Hallo **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="a435e-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="a435e-227">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a435e-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a435e-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a435e-229">Click **Add** button.</span></span> <span data-ttu-id="a435e-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a435e-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a435e-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="a435e-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a435e-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a435e-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a435e-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a435e-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a435e-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a435e-235">Testing single sign-on</span></span>

<span data-ttu-id="a435e-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a435e-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a435e-237">Als u op Hallo ServiceChannel-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ServiceChannel-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a435e-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a435e-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a435e-238">Additional resources</span></span>

* [<span data-ttu-id="a435e-239">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a435e-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a435e-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a435e-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png