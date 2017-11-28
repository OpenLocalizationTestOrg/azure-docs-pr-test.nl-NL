---
title: 'Zelfstudie: Azure Active Directory-integratie met eKincare | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en eKincare.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="36935-103">Zelfstudie: Azure Active Directory-integratie met eKincare</span><span class="sxs-lookup"><span data-stu-id="36935-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="36935-104">In deze zelfstudie leert u hoe toointegrate eKincare met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36935-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36935-105">EKincare integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="36935-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36935-106">U kunt beheren in Azure AD die tooeKincare toegang heeft</span><span class="sxs-lookup"><span data-stu-id="36935-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="36935-107">U kunt uw gebruikers tooautomatically get aangemelde tooeKincare (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="36935-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36935-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="36935-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36935-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36935-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36935-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="36935-110">Prerequisites</span></span>

<span data-ttu-id="36935-111">Azure AD-integratie met eKincare tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="36935-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="36935-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="36935-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36935-113">Een eKincare eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="36935-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36935-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="36935-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36935-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="36935-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36935-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="36935-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36935-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36935-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36935-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="36935-118">Scenario description</span></span>
<span data-ttu-id="36935-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="36935-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36935-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="36935-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36935-121">Het toevoegen van eKincare van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="36935-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="36935-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="36935-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="36935-123">Het toevoegen van eKincare van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="36935-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="36935-124">tooconfigure hello integratie van eKincare in Azure AD, moet u tooadd eKincare uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="36935-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36935-125">**tooadd eKincare via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="36935-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36935-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="36935-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36935-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="36935-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36935-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="36935-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="36935-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="36935-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="36935-133">Typ in het zoekvak Hallo **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="36935-133">In hello search box, type **eKincare**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="36935-135">Selecteer in het deelvenster resultaten hello, **eKincare**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="36935-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36935-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="36935-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36935-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met eKincare op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="36935-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="36935-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in eKincare is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36935-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="36935-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in eKincare toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="36935-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="36935-141">Wijs in eKincare, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="36935-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36935-142">tooconfigure en eenmalige aanmelding Azure AD-test met eKincare, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36935-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36935-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="36935-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36935-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36935-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36935-145">**[Maken van een testgebruiker eKincare](#creating-a-ekincare-test-user)**  -toohave een equivalent van Britta Simon in eKincare die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="36935-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36935-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="36935-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36935-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="36935-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36935-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="36935-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36935-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing eKincare configureren.</span><span class="sxs-lookup"><span data-stu-id="36935-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="36935-150">**Azure AD tooconfigure eenmalige aanmelding met eKincare, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="36935-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="36935-151">In de Azure-portal op Hallo Hallo **eKincare** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="36935-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="36935-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="36935-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="36935-155">Op Hallo **eKincare domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36935-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="36935-157">a.</span><span class="sxs-lookup"><span data-stu-id="36935-157">a.</span></span> <span data-ttu-id="36935-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="36935-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="36935-159">b.</span><span class="sxs-lookup"><span data-stu-id="36935-159">b.</span></span> <span data-ttu-id="36935-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="36935-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36935-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="36935-161">These values are not real.</span></span> <span data-ttu-id="36935-162">Werk deze waarden met Hallo werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="36935-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="36935-163">Neem contact op met [eKincare ondersteuningsteam](mailto:tech@ekincare.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="36935-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="36935-164">Hallo SAML asserties verwacht eKincare toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="36935-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="36935-165">Configureer Hallo claims voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="36935-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="36935-166">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="36935-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="36935-167">Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="36935-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="36935-168">Hallo claimnaam altijd worden **'werknemer-id'** en Hallo-waarde die we toouser.extensionattribute1 met Hallo werknemer-id van gebruiker Hallo hebt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="36935-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="36935-169">Hallo van de andere twee claims naam eenledige</span><span class="sxs-lookup"><span data-stu-id="36935-169">hello other two claims' name i.e</span></span> <span data-ttu-id="36935-170">**'organizationid'** en **'organisatienaam'** altijd dezelfde en hun waarden Hallo details van de organisatie van de gebruiker Hallo Hallo respectievelijk bevatten.</span><span class="sxs-lookup"><span data-stu-id="36935-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="36935-172">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36935-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="36935-173">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="36935-173">Attribute Name</span></span> | <span data-ttu-id="36935-174">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="36935-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="36935-175">Werknemer-id</span><span class="sxs-lookup"><span data-stu-id="36935-175">employeeid</span></span> | <span data-ttu-id="36935-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="36935-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="36935-177">OrganizationId</span><span class="sxs-lookup"><span data-stu-id="36935-177">organizationid</span></span> | <span data-ttu-id="36935-178">*'uniquevalue'*</span><span class="sxs-lookup"><span data-stu-id="36935-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="36935-179">Organisatienaam</span><span class="sxs-lookup"><span data-stu-id="36935-179">organizationname</span></span> | <span data-ttu-id="36935-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="36935-180">*user.companyname*</span></span> |

    <span data-ttu-id="36935-181">a.</span><span class="sxs-lookup"><span data-stu-id="36935-181">a.</span></span> <span data-ttu-id="36935-182">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="36935-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="36935-185">b.</span><span class="sxs-lookup"><span data-stu-id="36935-185">b.</span></span> <span data-ttu-id="36935-186">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="36935-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="36935-187">c.</span><span class="sxs-lookup"><span data-stu-id="36935-187">c.</span></span> <span data-ttu-id="36935-188">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="36935-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="36935-189">d.</span><span class="sxs-lookup"><span data-stu-id="36935-189">d.</span></span> <span data-ttu-id="36935-190">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="36935-190">Click **Ok**</span></span>

6. <span data-ttu-id="36935-191">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="36935-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="36935-193">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="36935-193">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="36935-195">tooconfigure eenmalige aanmelding op **eKincare** zijde, moet u toosend Hallo gedownload **Metadata XML** te[eKincare ondersteuningsteam](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="36935-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="36935-196">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="36935-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="36935-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="36935-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36935-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="36935-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36935-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36935-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36935-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="36935-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="36935-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="36935-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="36935-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="36935-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36935-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="36935-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36935-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="36935-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36935-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="36935-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36935-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36935-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36935-212">a.</span><span class="sxs-lookup"><span data-stu-id="36935-212">a.</span></span> <span data-ttu-id="36935-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36935-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36935-214">b.</span><span class="sxs-lookup"><span data-stu-id="36935-214">b.</span></span> <span data-ttu-id="36935-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36935-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36935-216">c.</span><span class="sxs-lookup"><span data-stu-id="36935-216">c.</span></span> <span data-ttu-id="36935-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="36935-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36935-218">d.</span><span class="sxs-lookup"><span data-stu-id="36935-218">d.</span></span> <span data-ttu-id="36935-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="36935-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="36935-220">Een testgebruiker eKincare maken</span><span class="sxs-lookup"><span data-stu-id="36935-220">Creating a eKincare test user</span></span>

<span data-ttu-id="36935-221">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="36935-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="36935-222">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="36935-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="36935-223">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooeKincare toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="36935-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="36935-225">**tooassign Britta Simon tooeKincare, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="36935-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="36935-226">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="36935-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="36935-228">Selecteer in de lijst met de toepassingen van Hallo **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="36935-228">In hello applications list, select **eKincare**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="36935-230">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="36935-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="36935-232">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="36935-232">Click **Add** button.</span></span> <span data-ttu-id="36935-233">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="36935-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="36935-235">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="36935-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36935-236">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="36935-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36935-237">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="36935-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36935-238">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="36935-238">Testing single sign-on</span></span>

<span data-ttu-id="36935-239">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="36935-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="36935-240">Als u op Hallo eKincare tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour eKincare toepassing.</span><span class="sxs-lookup"><span data-stu-id="36935-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="36935-241">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangsvenster](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="36935-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36935-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="36935-242">Additional resources</span></span>

* [<span data-ttu-id="36935-243">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36935-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36935-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36935-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

