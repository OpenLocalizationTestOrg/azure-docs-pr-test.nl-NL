---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Spark | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory- en Cisco Spark.
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
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="708f7-103">Zelfstudie: Azure Active Directory-integratie met Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="708f7-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="708f7-104">In deze zelfstudie leert u hoe Cisco Spark integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="708f7-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="708f7-105">Cisco Spark integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="708f7-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="708f7-106">U kunt beheren in Azure AD die toegang tot Spark Cisco heeft</span><span class="sxs-lookup"><span data-stu-id="708f7-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="708f7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Cisco Spark (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="708f7-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="708f7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="708f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="708f7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="708f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="708f7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="708f7-110">Prerequisites</span></span>

<span data-ttu-id="708f7-111">Voor het configureren van Azure AD-integratie met Cisco Spark, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="708f7-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="708f7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="708f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="708f7-113">Een Cisco-Spark eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="708f7-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="708f7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="708f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="708f7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="708f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="708f7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="708f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="708f7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="708f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="708f7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="708f7-118">Scenario description</span></span>
<span data-ttu-id="708f7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="708f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="708f7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="708f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="708f7-121">Cisco Spark uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="708f7-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="708f7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="708f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="708f7-123">Cisco Spark uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="708f7-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="708f7-124">Voor het configureren van de integratie van Cisco Spark in Azure AD, moet u Cisco Spark uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="708f7-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="708f7-125">**Als u wilt toevoegen Cisco Spark uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="708f7-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="708f7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="708f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="708f7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="708f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="708f7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="708f7-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="708f7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="708f7-133">Typ in het zoekvak **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="708f7-133">In the search box, type **Cisco Spark**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="708f7-135">Selecteer in het deelvenster resultaten **Cisco Spark**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="708f7-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="708f7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="708f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="708f7-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Cisco Spark op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="708f7-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="708f7-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Cisco Spark in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="708f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="708f7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Cisco Spark tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="708f7-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="708f7-141">Wijs in Cisco Spark, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="708f7-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="708f7-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Cisco Spark, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="708f7-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="708f7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="708f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="708f7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="708f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="708f7-145">**[Maken van een Cisco-Spark testgebruiker](#creating-a-cisco-spark-test-user)**  - Cisco Spark die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="708f7-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="708f7-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="708f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="708f7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="708f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="708f7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="708f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="708f7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="708f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="708f7-150">**Voor het configureren van Azure AD eenmalige aanmelding met Cisco Spark, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="708f7-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="708f7-151">In de Azure-portal op de **Cisco Spark** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="708f7-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="708f7-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="708f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="708f7-155">Op de **Cisco Spark domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="708f7-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="708f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="708f7-157">a.</span></span> <span data-ttu-id="708f7-158">In de **aanmeldings-URL** textbox, typ een URL als:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="708f7-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="708f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="708f7-159">b.</span></span> <span data-ttu-id="708f7-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="708f7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="708f7-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="708f7-161">This value is not real.</span></span> <span data-ttu-id="708f7-162">Deze waarde door de werkelijke ID bijwerken.</span><span class="sxs-lookup"><span data-stu-id="708f7-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="708f7-163">Neem contact op met [Cisco Spark Client ondersteuningsteam](https://support.ciscospark.com/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="708f7-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="708f7-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="708f7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="708f7-166">Cisco Spark toepassing verwacht de SAML-asserties naar specifieke kenmerken bevatten.</span><span class="sxs-lookup"><span data-stu-id="708f7-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="708f7-167">Configureer de volgende kenmerken voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="708f7-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="708f7-168">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="708f7-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="708f7-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="708f7-169">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="708f7-171">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="708f7-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="708f7-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="708f7-172">Attribute Name</span></span>  | <span data-ttu-id="708f7-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="708f7-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="708f7-174">UID</span><span class="sxs-lookup"><span data-stu-id="708f7-174">uid</span></span>    | <span data-ttu-id="708f7-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="708f7-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="708f7-176">a.</span><span class="sxs-lookup"><span data-stu-id="708f7-176">a.</span></span> <span data-ttu-id="708f7-177">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="708f7-180">b.</span><span class="sxs-lookup"><span data-stu-id="708f7-180">b.</span></span> <span data-ttu-id="708f7-181">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="708f7-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="708f7-182">c.</span><span class="sxs-lookup"><span data-stu-id="708f7-182">c.</span></span> <span data-ttu-id="708f7-183">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="708f7-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="708f7-184">d.</span><span class="sxs-lookup"><span data-stu-id="708f7-184">d.</span></span> <span data-ttu-id="708f7-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="708f7-185">Click **Ok**.</span></span>

7. <span data-ttu-id="708f7-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="708f7-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="708f7-188">Aanmelden bij [Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="708f7-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="708f7-189">Selecteer **instellingen** en klikt u onder de **verificatie** sectie, klikt u op **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="708f7-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="708f7-191">Selecteer **een 3rd derden identiteitsprovider integreren. (Geavanceerd)**  en Ga naar het volgende scherm.</span><span class="sxs-lookup"><span data-stu-id="708f7-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="708f7-192">Op de **Idp-metagegevens importeren** pagina beide slepen en neerzetten van het metagegevensbestand van de Azure AD naar de pagina of de optie van de browser bestand gebruiken om te zoeken en upload het metagegevensbestand van de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="708f7-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="708f7-193">Selecteer **certificaat dat is ondertekend door een certificeringsinstantie in de metagegevens (veiliger) vereisen** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="708f7-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="708f7-195">Selecteer **SSO testverbinding**, en wanneer er wordt een nieuw browsertabblad geopend, verifiëren met Azure AD met aanmelden.</span><span class="sxs-lookup"><span data-stu-id="708f7-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="708f7-196">Ga terug naar de **Cisco Cloud samenwerking Management** browsertabblad.</span><span class="sxs-lookup"><span data-stu-id="708f7-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="708f7-197">Als de test geslaagd is, schakelt u **deze test is geslaagd. Schakel de optie eenmalige aanmelding** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="708f7-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="708f7-198">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="708f7-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="708f7-199">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="708f7-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="708f7-200">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="708f7-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="708f7-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="708f7-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="708f7-202">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="708f7-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="708f7-204">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="708f7-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="708f7-205">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="708f7-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="708f7-207">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="708f7-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="708f7-209">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="708f7-211">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="708f7-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="708f7-213">a.</span><span class="sxs-lookup"><span data-stu-id="708f7-213">a.</span></span> <span data-ttu-id="708f7-214">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="708f7-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="708f7-215">b.</span><span class="sxs-lookup"><span data-stu-id="708f7-215">b.</span></span> <span data-ttu-id="708f7-216">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="708f7-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="708f7-217">c.</span><span class="sxs-lookup"><span data-stu-id="708f7-217">c.</span></span> <span data-ttu-id="708f7-218">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="708f7-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="708f7-219">d.</span><span class="sxs-lookup"><span data-stu-id="708f7-219">d.</span></span> <span data-ttu-id="708f7-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="708f7-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="708f7-221">Maken van een Cisco-Spark testgebruiker</span><span class="sxs-lookup"><span data-stu-id="708f7-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="708f7-222">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken.</span><span class="sxs-lookup"><span data-stu-id="708f7-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="708f7-223">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Cisco Spark maken.</span><span class="sxs-lookup"><span data-stu-id="708f7-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="708f7-224">Ga naar de [Cisco Cloud samenwerking Management](https://admin.ciscospark.com/) met uw volledige beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="708f7-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="708f7-225">Klik op **gebruikers** en vervolgens **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="708f7-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="708f7-227">In de **gebruiker beheren** Selecteer **handmatig toevoegen of wijzigen van gebruikers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="708f7-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="708f7-228">Selecteer **namen en e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="708f7-228">Select **Names and Email address**.</span></span> <span data-ttu-id="708f7-229">Vul vervolgens het tekstvak als volgt in:</span><span class="sxs-lookup"><span data-stu-id="708f7-229">Then, fill out the textbox as follows:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="708f7-231">a.</span><span class="sxs-lookup"><span data-stu-id="708f7-231">a.</span></span> <span data-ttu-id="708f7-232">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="708f7-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="708f7-233">b.</span><span class="sxs-lookup"><span data-stu-id="708f7-233">b.</span></span> <span data-ttu-id="708f7-234">In de **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="708f7-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="708f7-235">c.</span><span class="sxs-lookup"><span data-stu-id="708f7-235">c.</span></span> <span data-ttu-id="708f7-236">In de **e-mailadres** textbox type  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="708f7-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="708f7-237">Klik op het plusteken om toe te voegen Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="708f7-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="708f7-238">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="708f7-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="708f7-239">In de **Services toevoegen voor gebruikers** venster, klikt u op **opslaan** en vervolgens **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="708f7-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="708f7-240">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="708f7-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="708f7-241">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="708f7-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="708f7-243">**Als u wilt toewijzen Britta Simon met Cisco Spark, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="708f7-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="708f7-244">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="708f7-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="708f7-246">Selecteer in de lijst met toepassingen **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="708f7-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="708f7-248">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="708f7-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="708f7-250">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="708f7-250">Click **Add** button.</span></span> <span data-ttu-id="708f7-251">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="708f7-253">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="708f7-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="708f7-254">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="708f7-255">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="708f7-256">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="708f7-256">Testing single sign-on</span></span>

<span data-ttu-id="708f7-257">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="708f7-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="708f7-258">Als u op de tegel Cisco Spark in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="708f7-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="708f7-259">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="708f7-259">Additional resources</span></span>

* [<span data-ttu-id="708f7-260">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="708f7-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="708f7-261">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="708f7-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

