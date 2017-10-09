---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Business Object Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Business Object Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="a6fdd-103">Zelfstudie: Azure Active Directory-integratie met SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="a6fdd-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="a6fdd-104">In deze zelfstudie leert u hoe toointegrate SAP Business Object Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6fdd-105">U de volgende voordelen wanneer u een SAP Business Object Cloud met Azure AD integreert Hallo krijgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="a6fdd-106">In Azure AD, kunt u bepalen wie toegang tooSAP Business Object Cloud heeft.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="a6fdd-107">U kunt uw gebruikers tooSAP Business Object Cloud automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="a6fdd-108">U kunt uw accounts op één centrale locatie hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="a6fdd-109">Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6fdd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a6fdd-110">Prerequisites</span></span>

<span data-ttu-id="a6fdd-111">tooset van Azure AD-integratie met SAP Business Object Cloud, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="a6fdd-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a6fdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6fdd-113">Een SAP Business Object Cloud met eenmalige aanmelding ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="a6fdd-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="a6fdd-114">Als u Hallo stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="a6fdd-115">Aanbevelingen voor het testen van Hallo stappen in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="a6fdd-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="a6fdd-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6fdd-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a6fdd-118">Scenario description</span></span>
<span data-ttu-id="a6fdd-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="a6fdd-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6fdd-121">SAP Business Object Cloud uit de galerie Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="a6fdd-122">Instellen en testen van eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="a6fdd-123">SAP Business Object Cloud van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a6fdd-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="a6fdd-124">tooset van integratie van SAP Business Object Cloud met Azure AD in de galerie Hallo Hallo SAP Business Object Cloud tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6fdd-125">tooadd SAP Business Object Cloud uit de galerie Hallo:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="a6fdd-126">In Hallo [Azure-portal](https://portal.azure.com), Hallo linkermenu in, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="a6fdd-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![pagina met toepassingen Hallo Enterprise][2]
    
3. <span data-ttu-id="a6fdd-130">Selecteer een nieuwe toepassing tooadd **nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-130">tooadd a new application, select **New application**.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="a6fdd-132">Voer in het zoekvak Hallo **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![Hallo zoekvak](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="a6fdd-134">Selecteer in het deelvenster resultaten hello, **SAP Business Object Cloud**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud in de lijst met resultaten Hallo](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a6fdd-136">Instellen en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6fdd-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="a6fdd-137">In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met SAP Business Object Cloud op basis van een testgebruiker met de naam *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="a6fdd-138">Voor één aanmelding toowork moet Azure AD tooknow hello Azure AD-equivalent gebruiker in de Cloud voor SAP Business-Object.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="a6fdd-139">Een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in een SAP Business Object Cloud moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="a6fdd-140">Hallo tooestablish relatie in SAP Business Object Cloud koppelen voor **gebruikersnaam**, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="a6fdd-141">tooconfigure en eenmalige aanmelding Azure AD-test met SAP Business Object Cloud, volledige Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="a6fdd-142">[Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="a6fdd-143">Een gebruiker toouse ingesteld met deze functie.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="a6fdd-144">[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="a6fdd-145">Azure AD tests eenmalige aanmelding met Hallo gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="a6fdd-146">[Maken van een SAP Business Object Cloud testgebruiker](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="a6fdd-147">Maakt een equivalent van Britta Simon in SAP Business Object Cloud die is gekoppeld toohello Azure AD-weergave van Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="a6fdd-148">[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="a6fdd-149">Stelt Britta Simon toouse eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6fdd-150">[Test eenmalige aanmelding](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="a6fdd-151">Controleert of dat die Hallo configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="a6fdd-152">Instellen van eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6fdd-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="a6fdd-153">In deze sectie maakt inschakelen u Azure AD één aanmelding in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="a6fdd-154">Vervolgens instellen u eenmalige aanmelding in uw toepassing SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="a6fdd-155">tooset van Azure AD eenmalige aanmelding met SAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="a6fdd-156">In de Azure-portal op Hallo Hallo **SAP Business Object Cloud** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Schakel eenmalige aanmelding][4]

2. <span data-ttu-id="a6fdd-158">Op Hallo **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Selecteer op basis van SAML eenmalige aanmelding](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="a6fdd-160">Onder **SAP Business Object Cloud-domein en URL's**, volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="a6fdd-161">In Hallo **aanmeldings-URL** Voer een URL Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="a6fdd-162">In Hallo **id** Voer een URL Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL's en SAP Business Object Cloud-domein-URL 's](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="a6fdd-164">Hallo-waarden in deze URL's zijn voor alleen demonstratie.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="a6fdd-165">Hallo-waarden bijwerken met de werkelijke Hallo aanmelding URL en de id-URL.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="a6fdd-166">tooget hello aanmeldings-URL, neem contact op met Hallo [SAP Business Object Cloud Client ondersteuningsteam](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="a6fdd-167">U kunt Hallo identificatie-URL ophalen door Hallo SAP Business Object cloudmetagegevens downloaden vanuit Hallo-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="a6fdd-168">Dit wordt verderop in de zelfstudie Hallo uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="a6fdd-169">Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="a6fdd-170">Sla het metagegevensbestand Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-170">Then, save hello metadata file on your computer.</span></span>

    ![Selecteer de metagegevens-XML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="a6fdd-172">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-172">Select **Save**.</span></span>

    ![Opslaan selecteren](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6fdd-174">Meld u tooyour SAP Business Object Cloud bedrijf site als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="a6fdd-175">Selecteer **Menu** > **System** > **beheer**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Selecteer vervolgens Menu, systeem en beheer](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="a6fdd-177">Op Hallo **beveiliging** tabblad, selecteer Hallo **bewerken** pictogram (pen).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Selecteer op het tabblad Beveiliging Hallo bewerkingspictogram Hallo](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="a6fdd-179">Voor **verificatiemethode**, selecteer **SAML eenmalige aanmelding (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Eenmalige aanmelding SAML voor Hallo verificatiemethode selecteren](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="a6fdd-181">toodownload hello serviceprovider metagegevens (stap 1), selecteer **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="a6fdd-182">In het metagegevensbestand hello, vindt en kopieert Hallo **id van de entiteit** waarde.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="a6fdd-183">In hello Azure portal onder **SAP Business Object Cloud-domein en URL's**, Hallo waarde plakken in Hallo **id** vak.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Kopieer en plak Hallo id van de entiteit waarde](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="a6fdd-185">tooupload hello serviceprovider metagegevens (stap 2) in Hallo-bestand dat u hebt gedownload van Azure-portal onder Hallo **identiteitsprovider uploaden metagegevens**, selecteer **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Selecteer onder de metagegevens van de identiteitsprovider uploaden, uploaden](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="a6fdd-187">In Hallo **gebruikerskenmerk** wilt weergeven, selecteer Hallo-gebruikerskenmerk (stap 3) wilt u toouse voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="a6fdd-188">Dit gebruikerskenmerk maps toohello id-provider.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="a6fdd-189">een aangepast kenmerk op Hallo van de gebruiker pagina gebruik Hallo tooenter **aangepaste SAML-toewijzing** optie.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="a6fdd-190">Of u kunt een selecteren **e** of **gebruikers-ID** als Hallo gebruikerskenmerk.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="a6fdd-191">In ons voorbeeld we geselecteerd **e** omdat we Hallo Gebruikersclaim id Hello toegewezen **userprincipalname** kenmerk in Hallo **gebruikerskenmerken** sectie in Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="a6fdd-192">Dit biedt een unieke gebruikers e-mailadres waarmee toohello cloudtoepassing SAP Business-Object in elke geslaagde SAML-reactie wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Selecteer de gebruiker-kenmerk](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="a6fdd-194">tooverify Hallo-account met Hallo id-provider (stap 4), in Hallo **aanmelding referentie (E-mail)** Voer het e-mailadres van de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="a6fdd-195">Selecteer **Account controleren**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="a6fdd-196">Hallo-systeem voegt aanmeldingsreferenties toohello gebruikersaccount toe.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Voer e-mailadres en selecteer Account controleren](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="a6fdd-198">Selecteer Hallo **opslaan** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-198">Select hello **Save** icon.</span></span>

    ![Pictogram opslaan](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="a6fdd-200">U kunt een beknopte versie van deze instructies in Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u uw app instelt!</span><span class="sxs-lookup"><span data-stu-id="a6fdd-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="a6fdd-201">Nadat u Hallo app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer Hallo **Single Sign-On** tabblad. U hebt toegang tot documentatie in Hallo Hallo ingesloten **configuratie** sectie Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="a6fdd-202">Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a6fdd-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a6fdd-203">Create an Azure AD test user</span></span>
<span data-ttu-id="a6fdd-204">In deze sectie maakt u een testgebruiker met de naam Britta Simon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="a6fdd-205">toocreate een testgebruiker in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="a6fdd-206">Selecteer in de Azure-portal in het linkermenu Hallo Hallo **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6fdd-208">toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6fdd-210">Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6fdd-212">In Hallo **gebruiker** dialoogvenster, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="a6fdd-213">In Hallo **naam** Voer **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="a6fdd-214">In Hallo **gebruikersnaam** Voer Hallo e-mailadres van de gebruiker Hallo Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="a6fdd-215">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="a6fdd-216">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-216">Select **Create**.</span></span>

        ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD-gebruiker maken][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="a6fdd-219">Een SAP Business Object Cloud testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a6fdd-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="a6fdd-220">Azure AD-gebruikers moeten worden ingericht in SAP Business Object Cloud voordat ze tooSAP Business Object Cloud kunnen aanmelden.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="a6fdd-221">In een SAP Business Object Cloud is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="a6fdd-222">tooprovision een gebruikersaccount:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="a6fdd-223">Meld u tooyour SAP Business Object Cloud bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="a6fdd-224">Selecteer **Menu** > **beveiliging** > **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="a6fdd-226">Op Hallo **gebruikers** pagina tooadd nieuwe Gebruikersdetails, selecteer  **+** .</span><span class="sxs-lookup"><span data-stu-id="a6fdd-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Gebruikers toevoegen](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="a6fdd-228">Voltooi Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="a6fdd-229">In Hallo **gebruikers-ID** Voer Hallo gebruikers-ID van gebruiker hello, zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="a6fdd-230">In Hallo **VOORNAAM** Voer Hallo voornaam van de gebruiker hello, zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="a6fdd-231">In Hallo **ACHTERNAAM** achternaam op Hallo van Hallo gebruiker, zoals Voer **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="a6fdd-232">In Hallo **WEERGAVENAAM** Voer Hallo volledige naam van de gebruiker hello, zoals **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="a6fdd-233">In Hallo **e** Voer Hallo e-mailadres van de gebruiker hello, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a6fdd-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="a6fdd-234">Op Hallo **rollen selecteren** pagina, selecteer de juiste rol Hallo voor Hallo gebruiker en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Rol selecteren](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="a6fdd-236">Selecteer Hallo **opslaan** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a6fdd-237">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6fdd-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a6fdd-238">In deze sectie maakt toestaan u Hallo gebruiker Britta Simon eenmalige aanmelding toouse Azure AD Hallo gebruiker account toegang tooSAP Business Object Cloud verleent.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="a6fdd-239">tooassign Britta Simon tooSAP Business Object Cloud:</span><span class="sxs-lookup"><span data-stu-id="a6fdd-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="a6fdd-240">Hallo toepassingen weergave opent in hello Azure-portal, en gaat u toohello directory weergeven.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="a6fdd-241">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a6fdd-243">Selecteer in de lijst met de toepassingen van Hallo **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="a6fdd-245">Selecteer in het linkermenu Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-245">In hello left menu, select **Users and groups**.</span></span>

    ![Gebruikers en groepen selecteren][202] 

4. <span data-ttu-id="a6fdd-247">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-247">Select **Add**.</span></span> <span data-ttu-id="a6fdd-248">Klik vervolgens op Hallo **toevoegen toewijzing** pagina **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Hallo toevoegen toewijzing pagina][203]

5. <span data-ttu-id="a6fdd-250">Op Hallo **gebruikers en groepen** pagina in de lijst Hallo van gebruikers, selecteer **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="a6fdd-251">Op Hallo **gebruikers en groepen** pagina **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="a6fdd-252">Op Hallo **toevoegen toewijzing** pagina **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a6fdd-254">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a6fdd-254">Test single sign-on</span></span>

<span data-ttu-id="a6fdd-255">In deze sectie kunt u uw configuratie Azure AD eenmalige aanmelding met behulp van het toegangsvenster Hallo testen.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="a6fdd-256">Wanneer u Hallo SAP Business Object Cloud-tegel in het toegangsvenster Hallo selecteert, moet u tooyour SAP Business Object Cloud-toepassing automatisch worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="a6fdd-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="a6fdd-257">Zie voor meer informatie over het toegangsvenster Hallo [inleiding toohello toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6fdd-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6fdd-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a6fdd-258">Additional resources</span></span>

* [<span data-ttu-id="a6fdd-259">Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6fdd-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6fdd-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6fdd-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

