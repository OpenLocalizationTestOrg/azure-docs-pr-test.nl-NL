---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Spark | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory- en Cisco Spark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="778ff-103">Zelfstudie: Azure Active Directory-integratie met Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="778ff-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="778ff-104">In deze zelfstudie leert u hoe toointegrate Cisco Spark met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="778ff-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="778ff-105">Cisco Spark integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="778ff-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="778ff-106">U kunt beheren in Azure AD wie toegang tot tooCisco Spark heeft</span><span class="sxs-lookup"><span data-stu-id="778ff-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="778ff-107">U kunt uw gebruikers tooautomatically get aangemelde tooCisco Spark (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="778ff-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="778ff-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="778ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="778ff-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="778ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="778ff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="778ff-110">Prerequisites</span></span>

<span data-ttu-id="778ff-111">Azure AD-integratie met Cisco Spark tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="778ff-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="778ff-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="778ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="778ff-113">Een Cisco-Spark eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="778ff-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="778ff-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="778ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="778ff-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="778ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="778ff-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="778ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="778ff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="778ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="778ff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="778ff-118">Scenario description</span></span>
<span data-ttu-id="778ff-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="778ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="778ff-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="778ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="778ff-121">Het toevoegen van Cisco Spark van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="778ff-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="778ff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="778ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="778ff-123">Het toevoegen van Cisco Spark van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="778ff-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="778ff-124">tooconfigure hello integratie van Cisco Spark in Azure AD, moet u tooadd Cisco Spark uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="778ff-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="778ff-125">**Cisco Spark via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="778ff-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="778ff-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="778ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="778ff-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="778ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="778ff-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="778ff-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="778ff-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="778ff-133">Typ in het zoekvak Hallo **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="778ff-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="778ff-135">Selecteer in het deelvenster resultaten hello, **Cisco Spark**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="778ff-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="778ff-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="778ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="778ff-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Cisco Spark op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="778ff-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="778ff-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Cisco Spark is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="778ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="778ff-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Cisco Spark toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="778ff-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="778ff-141">In een Cisco-Spark Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="778ff-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="778ff-142">tooconfigure en eenmalige aanmelding Azure AD-test met Cisco Spark, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="778ff-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="778ff-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="778ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="778ff-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="778ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="778ff-145">**[Maken van een Cisco-Spark testgebruiker](#creating-a-cisco-spark-test-user)**  -toohave een equivalent van Britta Simon in Cisco Spark die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="778ff-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="778ff-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="778ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="778ff-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="778ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="778ff-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="778ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="778ff-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="778ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="778ff-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Cisco-Spark Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="778ff-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="778ff-151">In de Azure-portal op Hallo Hallo **Cisco Spark** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="778ff-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="778ff-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="778ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="778ff-155">Op Hallo **Cisco Spark domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="778ff-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="778ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="778ff-157">a.</span></span> <span data-ttu-id="778ff-158">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="778ff-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="778ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="778ff-159">b.</span></span> <span data-ttu-id="778ff-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="778ff-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="778ff-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="778ff-161">This value is not real.</span></span> <span data-ttu-id="778ff-162">Deze waarde bijwerken Hello werkelijke id.</span><span class="sxs-lookup"><span data-stu-id="778ff-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="778ff-163">Neem contact op met [Cisco Spark Client ondersteuningsteam](https://support.ciscospark.com/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="778ff-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="778ff-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="778ff-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="778ff-166">Cisco Spark toepassing verwacht hello SAML asserties toocontain specifieke kenmerken.</span><span class="sxs-lookup"><span data-stu-id="778ff-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="778ff-167">Configureer Hallo kenmerken voor deze toepassing te volgen.</span><span class="sxs-lookup"><span data-stu-id="778ff-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="778ff-168">U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="778ff-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="778ff-169">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="778ff-169">hello following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="778ff-171">In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="778ff-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="778ff-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="778ff-172">Attribute Name</span></span>  | <span data-ttu-id="778ff-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="778ff-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="778ff-174">UID</span><span class="sxs-lookup"><span data-stu-id="778ff-174">uid</span></span>    | <span data-ttu-id="778ff-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="778ff-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="778ff-176">a.</span><span class="sxs-lookup"><span data-stu-id="778ff-176">a.</span></span> <span data-ttu-id="778ff-177">Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="778ff-180">b.</span><span class="sxs-lookup"><span data-stu-id="778ff-180">b.</span></span> <span data-ttu-id="778ff-181">In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="778ff-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="778ff-182">c.</span><span class="sxs-lookup"><span data-stu-id="778ff-182">c.</span></span> <span data-ttu-id="778ff-183">Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="778ff-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="778ff-184">d.</span><span class="sxs-lookup"><span data-stu-id="778ff-184">d.</span></span> <span data-ttu-id="778ff-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="778ff-185">Click **Ok**.</span></span>

7. <span data-ttu-id="778ff-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="778ff-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="778ff-188">Aanmelden te[Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="778ff-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="778ff-189">Selecteer **instellingen** en onder Hallo **verificatie** sectie, klikt u op **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="778ff-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="778ff-191">Selecteer **een 3rd derden identiteitsprovider integreren. (Geavanceerd)**  en ga toohello volgende scherm.</span><span class="sxs-lookup"><span data-stu-id="778ff-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="778ff-192">Op Hallo **Idp-metagegevens importeren** pagina beide slepen hello Azure AD-metagegevensbestand naar Hallo pagina drop of Hallo bestand browser optie toolocate en gebruik hello Azure AD-metagegevensbestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="778ff-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="778ff-193">Selecteer **certificaat dat is ondertekend door een certificeringsinstantie in de metagegevens (veiliger) vereisen** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="778ff-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="778ff-195">Selecteer **SSO testverbinding**, en wanneer er wordt een nieuw browsertabblad geopend, verifiëren met Azure AD met aanmelden.</span><span class="sxs-lookup"><span data-stu-id="778ff-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="778ff-196">Retourneren van toohello **Cisco Cloud samenwerking Management** browsertabblad. Als het Hallo-test is geslaagd, selecteert u **deze test is geslaagd. Schakel de optie eenmalige aanmelding** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="778ff-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="778ff-197">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="778ff-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="778ff-198">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="778ff-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="778ff-199">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="778ff-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="778ff-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="778ff-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="778ff-201">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="778ff-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="778ff-203">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="778ff-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="778ff-204">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="778ff-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="778ff-206">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="778ff-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="778ff-208">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="778ff-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="778ff-210">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="778ff-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="778ff-212">a.</span><span class="sxs-lookup"><span data-stu-id="778ff-212">a.</span></span> <span data-ttu-id="778ff-213">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="778ff-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="778ff-214">b.</span><span class="sxs-lookup"><span data-stu-id="778ff-214">b.</span></span> <span data-ttu-id="778ff-215">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="778ff-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="778ff-216">c.</span><span class="sxs-lookup"><span data-stu-id="778ff-216">c.</span></span> <span data-ttu-id="778ff-217">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="778ff-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="778ff-218">d.</span><span class="sxs-lookup"><span data-stu-id="778ff-218">d.</span></span> <span data-ttu-id="778ff-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="778ff-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="778ff-220">Maken van een Cisco-Spark testgebruiker</span><span class="sxs-lookup"><span data-stu-id="778ff-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="778ff-221">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken.</span><span class="sxs-lookup"><span data-stu-id="778ff-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="778ff-222">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken.</span><span class="sxs-lookup"><span data-stu-id="778ff-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="778ff-223">Ga toohello [Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="778ff-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="778ff-224">Klik op **gebruikers** en vervolgens **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="778ff-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="778ff-226">In Hallo **gebruiker beheren** Selecteer **handmatig toevoegen of wijzigen van gebruikers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="778ff-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="778ff-227">Selecteer **namen en e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="778ff-227">Select **Names and Email address**.</span></span> <span data-ttu-id="778ff-228">Vul vervolgens Hallo textbox als volgt in:</span><span class="sxs-lookup"><span data-stu-id="778ff-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="778ff-230">a.</span><span class="sxs-lookup"><span data-stu-id="778ff-230">a.</span></span> <span data-ttu-id="778ff-231">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="778ff-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="778ff-232">b.</span><span class="sxs-lookup"><span data-stu-id="778ff-232">b.</span></span> <span data-ttu-id="778ff-233">In Hallo **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="778ff-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="778ff-234">c.</span><span class="sxs-lookup"><span data-stu-id="778ff-234">c.</span></span> <span data-ttu-id="778ff-235">In Hallo **e-mailadres** textbox type  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="778ff-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="778ff-236">Klik op Hallo plus tooadd Britta Simon ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="778ff-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="778ff-237">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="778ff-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="778ff-238">In Hallo **Services toevoegen voor gebruikers** venster, klikt u op **opslaan** en vervolgens **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="778ff-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="778ff-239">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="778ff-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="778ff-240">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="778ff-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="778ff-242">**tooassign Britta Simon tooCisco Spark, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="778ff-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="778ff-243">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="778ff-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="778ff-245">Selecteer in de lijst met de toepassingen van Hallo **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="778ff-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="778ff-247">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="778ff-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="778ff-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="778ff-249">Click **Add** button.</span></span> <span data-ttu-id="778ff-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="778ff-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="778ff-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="778ff-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="778ff-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="778ff-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="778ff-255">Testing single sign-on</span></span>

<span data-ttu-id="778ff-256">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="778ff-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="778ff-257">Als u op Hallo Cisco Spark-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Cisco Spark-toepassing.</span><span class="sxs-lookup"><span data-stu-id="778ff-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="778ff-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="778ff-258">Additional resources</span></span>

* [<span data-ttu-id="778ff-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="778ff-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="778ff-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="778ff-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

